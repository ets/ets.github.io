---
title: Explaining Query Tuning to suits
date: 2016-04-20 19:18:04
tags:
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
<img src="https://mail.google.com/mail/u/0/?ui=2&ik=4be6722e5b&view=fimg&th=1543543588cd7db8&attid=0.1&disp=emb&realattid=ii_154352436974512a&attbid=ANGjdJ_8dUL3vkw5EmPb00yEY5WrUywqx_yu5mzd7WXNnUezIR178a1eOiLvkBKVrtIO22Eenqc35sta6KV7b3DIsgetemRL_s9ewy7McKioOclVTD8AOGQbg796l14&sz=w1088-h506&ats=1494795285989&rm=1543543588cd7db8&zw&atsh=1">
Note: unlike Social Tables' Engineers, our database refuses to work harder than 100% ... so those blue peaks are signs of unhappy Social Tables users.

Here are the same measurements after tuning:
<img src="https://mail.google.com/mail/u/0/?ui=2&ik=4be6722e5b&view=fimg&th=1543543588cd7db8&attid=0.2&disp=emb&realattid=ii_1543524f5f5251a7&attbid=ANGjdJ9P9-aDB8by1WaHgUgiJJgzZpyFbE0NrlwLmQgfwbY7eBv6r2LzEr-QdHLlmRhkE_mOS9T6E2d7mrhGYn41D6Q-Q1ZCxp3UXVkgAuk_cYp3ZhJjDrRJ9mf_51s&sz=w1088-h500&ats=1494795285990&rm=1543543588cd7db8&zw&atsh=1">
Happier database === Happier users
