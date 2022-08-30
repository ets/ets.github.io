---
title: Explaining SDF to suits
date: 2016-04-06
type: posts
tags:
- Signed Distance Fields
---

I posted the following on an internal blog at Social Tables in an attempt to explain a bit about what our Software Engineering group was up to at the time.

---
We've got a special subject this issue to take the edge off that geek-withdrawal : "Drawing Text with Signed Distance Fields" or using SDF text rendering for those in the know.

## What's SDF?
Signed distance field (SDF) is a technique for rendering bitmap fonts without jagged edges even at high magnifications. It was first introduced in 2007 with [this bit of light reading by Valve](http://www.valvesoftware.com/publications/2007/SIGGRAPH2007_AlphaTestedMagnification.pdf) and couples the use of a bitmap and glyphs with a GLSL shader that can sample and sharpen said glyphs.

## What's SDF ... in English (preferably with pictures)?
So...you know what sounds easy but is really really hard? Drawing legible letters in Venue Mapper. Wait - what? Why's that hard you ask?

Here's a screenshot of "Social Tables" rendered in 12pt font by Microsoft Word:

![SDF](/images/sdf-1.png)

Completely legible. But here's that exact same image after I zoom in a few times:

![SDF](/images/sdf-2.png)

Not so great. Possibly legible but if we rendered text like this as users zoom in and out in Venue Mapper we'd have to bundle subscriptions with aspirin.

SDF is a technique we've just begun using to more efficiently render text in Venue Mapper 3 - it performs better (app is faster) and looks prettier than the techniques we've used previously.

Here's a [movie of SDF in action in VM3 courtesy of our own Van Drunen](https://youtu.be/8yt7kSftNU4).
