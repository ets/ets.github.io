---
title: Explaining SDF to suits
date: 2016-04-06 19:18:04
tags:
- Signed Distance Fields
---

I posted the following on an internal blog at Social Tables in an attempt to explain a bit about what our Software Engineering group was up to at the time.

---
We've got a special subject this issue to take the edge off that geek-withdrawal : "Drawing Text with Signed Distance Fields" or using SDF text rendering for those in the know.

## What's SDF?
Signed distance field (SDF) is a technique for rendering bitmap fonts without jagged edges even at high magnifications. It was first introduced in 2007 with this bit of light reading by Valve and couples the use of a bitmap and glyphs with a GLSL shader that can sample and sharpen said glyphs.

## What's SDF ... in English (preferably with pictures)?
So...you know what sounds easy but is really really hard? Drawing legible letters in Venue Mapper. Wait - what? Why's that hard you ask?

Here's a screenshot of "Social Tables" rendered in 12pt font by Microsoft Word:

<img src="https://mail.google.com/mail/u/0/?ui=2&ik=4be6722e5b&view=fimg&th=1543543d1cce453f&attid=0.1&disp=emb&realattid=ii_153ecb6a29e16a81&attbid=ANGjdJ-f2oYILbnL19O-tmZ6EsDcXaYiAGDJ07nPhJijtx2YgYZYDdawK_Id8ieoYWzSoC9o9XuaAXj04eAmGE0JO-I1Ja5kyFDZI1S0zrK3pYGxhm4ZtAZD6BYOOfk&sz=w156-h40&ats=1494809715654&rm=1543543d1cce453f&zw&atsh=1">

Completely legible. But here's that exact same image after I zoom in a few times:

<img src="https://mail.google.com/mail/u/0/?ui=2&ik=4be6722e5b&view=fimg&th=1543543d1cce453f&attid=0.2&disp=emb&realattid=ii_153ecb76b4f32354&attbid=ANGjdJ-hYMp9cspdZYnXIyGJYRtgDsU2-rmyfbcYCd7kW0yJBqfT9F95-sewd_2rD4h2PGheyjmi9AhD0EKG5KT7s4H7WZW92yaYuB-j4Aub_o7Qw0F_TPFZ2Rl19fg&sz=w958-h224&ats=1494809715654&rm=1543543d1cce453f&zw&atsh=1">

Not so great. Possibly legible but if we rendered text like this as users zoom in and out in Venue Mapper we'd have to bundle subscriptions with aspirin.

SDF is a technique we've just begun using to more efficiently render text in Venue Mapper 3 - it performs better (app is faster) and looks prettier than the techniques we've used previously.

Here's a [movie of SDF in action in VM3 courtesy of our own Van Drunen](https://youtu.be/8yt7kSftNU4).
