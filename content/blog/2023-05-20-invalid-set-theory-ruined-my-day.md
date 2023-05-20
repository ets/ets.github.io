---
title: Invalid set theory ruined my day
date: 2023-05-20
type: posts
tags:
- scala
- spark
- dataset
---
So why was the union of two Datasets formed from the same case class failing?  Not failing with an exception mind you....but failing mathematically!
```
import scala.collection.mutable.ArrayBuffer
import spark.implicits._

// Simple case class
case class Person(name: String, age: Int)

val datasets = ArrayBuffer[Dataset[Person]]()

// Assuming you populate your ArrayBuffer with Datasets...
datasets += Seq(Person("John", 30)).toDS()
datasets += Seq(Person("Jane", 25)).toDS()
datasets += Seq(Person("Mike", 35)).toDS()

// Then reduce (union all) the Datasets ....
val combinedDataset = datasets.reduce(_ union _)

// But combinedDataset did NOT produce the union and this assertion fails!
assert combinedDataset.where(col("name") === "John").count = 1
```

My real world code was far more complicated, but this was exactly what I was observing in the midst of a deep debugging session.  As I fell down the rabbit hole, I painfully determined that there was one problematic dataset.  If that dataset wasn't included in the union, the union worked as expected.  The problematic dataset was formed like this:
```
  val problemSet = df.select(
    $"a_name",
    ageValue
  )
  .as[Person]
```
Nothing looks wrong there.  The dataset is explicitly typed with the case class...so what would cause a union to fail? Further down the rabbit hole we go... In prior logic, the `df` was generating the value of `a_name` using a UDF like this:
```
  val df = anotherDf.select(nameGenerator().as("a_name"), $"*").persist(MEMORY_AND_DISK),
```
A little odd, but nothing alarming there. the UDF returns a string and was defined like this:
```
  val nameGenerator: UserDefinedFunction = udf(() => randomChars().toString)
```
Satisfied that all my datasets were strongly and correctly typed to the same schema (explicitly typed as Person), I unhappily chased red herrings for several more hours before recogniziing a new clue.  The problematic dataset's schema differed from the other dataset in one important way. Here was the schema for the other datasets:
```
 StructField(name,StringType,false)
 StructField(age,IntegerType,false)
```
and now the one created using the logic above:
```
 StructField(name,StringType,true)
 StructField(age,IntegerType,false)
```
Okay!  So there's my root cause.  Spark is refusing to union the differing dataset and it simply excludes it from the combined results. But why?

Turns out that Spark is setting the column populated by the UDF as nullable and the explicit cast to Person with a non optional String typing does NOT change that!  Guh.

The fix was incredibly easy and honestly I was a little surprised it worked given the depth of this "unexpected behavior".  I simply added a predicate when forming the dataset like so:
```
  val noLongerAProblemSet = df.select(
    $"a_name",
    ageValue
  ).where(
    $"a_name_".isNotNull
  ) // ensure the resulting dataset marks name as non nullable
  .as[Person]
```
Set math logic was restored and the universe once again in balance.


