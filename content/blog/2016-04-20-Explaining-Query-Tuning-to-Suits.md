---
title: Explaining Query Tuning to suits
date: 2016-04-20
type: posts
tags:
- query tuning
---

I posted the following on an internal blog at Social Tables in an attempt to explain a bit about what our Software Engineering group was up to at the time.

---
Today we're going to talk briefly about query tuning - a black art in the craft of software engineering that [predates the Internet](http://dl.acm.org/citation.cfm?doid=582095.582099) but is still incredibly relevant. I don't mean relevant in the "you should really pay attention to national politics" sense.  I mean relevant as in "this can (when done poorly) wreck your whole day."

## What's query tuning?

A query is a request for information from a database. It can be as simple as "find the email address of the Social Tables user named Inigo Montoya", or more complex like "find the ASP of all Social Tables opportunities closed on Fridays that followed a Thursday evening Happy Hour."

Since database structures are complex, in most cases, and especially for not-very-simple queries, the needed data for a query can be collected from a database by accessing it in different ways, through different data-structures, and in different orders. Each different way typically requires different processing time. Processing times of the same query may have large variance, from a fraction of a second to hours, depending on the way selected. The purpose of query tuning, is to find the way to process a given query in minimum time.

## What's query tuning ... in English (preferably with pictures) and how can it wreck my whole day?

Query tuning is an effort to minimize the work performed while answering a query. If done poorly, database queries execute slowly and your application responds slowly. When your application responds slowly bad things happen - like Mary posting a screenshot to #devops (aka your whole day is wrecked).

Last week, Michael Dumont spent some time tuning several queries in our platform and his visuals of that effort are worth > 1,000 words:

Orange = a measure of platform activity
Blue = a measure of how hard the database is working
![Query Tuning](/images/query-tuning-1.png)

Note: unlike Social Tables' Engineers, our database refuses to work harder than 100% ... so those blue peaks are signs of unhappy Social Tables users.

Here are the same measurements after tuning:
![Query Tuning2](/images/query-tuning-2.png)

Happier database === Happier users
