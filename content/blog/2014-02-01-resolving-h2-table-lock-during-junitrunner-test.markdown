---
layout: post
title: "Resolving H2 table lock during JUnitRunner test"
date: 2014-02-01
type: posts
---
After adding a new test to a project that uses Play Framework 1.2.X and thus leverages H2 for Junit functional testing, I began encountering a table lock during setup() when the framework was attempting to delete the contents of an entity table.

I initially blamed the lock on bad model design and wasted a significant amount of time tweaking JPA entity relationships and corresponding CRUD operations in an attempt to resolve it. I ultimately resolved the issue after realizing it was in fact caused by a badly designed test.

I was directly modifying entities within the transaction that wrapped my functional test and then emulating API calls that relied upon the state of those same entities. Long story short, my test was attempting something similar to this:

	class FunctionalTest { //Runs entire test in the same transaction

		setup(){
			//reset H2 datastore in an distinct transaction
		}

		atest(){
			User u = User.findById(1);
			u.address = new Address();
			u.save();

			//test continues
		}

		btest(){
			Request req = GET("/user/1");

		}
	}


In my contrived example above, after Junit runs atest() and just before running btest() - it will call setup() and attempt to reset the database in a separate transaction. But, atest() claimed a lock for insert on User and in H2 that locks the entire table by default thus setup() will be unable to reset the User table and will fail with a lock timeout.

To resolve this - you'll either need to redesign your test to avoid manipulating entities directly in the testcase or run each test in a distinct transaction.
