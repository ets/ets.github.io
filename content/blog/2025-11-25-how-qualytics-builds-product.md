---
title: How Qualytics Builds Product
date: 2025-11-25
type: posts
tags:
- qualytics
- startups
- product
- engineering
---

It's been four years since our first product demo at [Qualytics](https://www.qualytics.ai) and as we've developed our eponymous product into an enterprise offering, we've refined our process in lockstep.  I didn't build our team around a manifesto but around a shared mission. We started with customer problems and pushed to deliver robust solutions quickly without breaking things (too badly).

Along the way a few things have crystallized as principles:

### The Method: Directness, Flow, and Alignment

We didn't invent our product development philosophy in a vacuum. It was inspired, in part, by external observation and the search for tools that mirrored our own values. Specifically, we've found deep resonance in the principles outlined in [Lenny Rachitsky](https://www.linkedin.com/in/lennyrachitsky/)'s interview of [Karri Saarinen speaking to "How Linear Builds Product"](https://www.lennysnewsletter.com/p/how-linear-builds-product). In fact, our tightly-knit product development team tried a few ticketing systems before landing on Linear and falling in love.

The Linear Method's Core Philosophy of Directness and the way it's embodied with a "get stuff done" attitude tracks perfectly with our internal culture. It's no surprise that we ultimately chose a ticketing system built by creators who share our approach to building product. It's an interesting spin on Conway's Law where our chosen tools reflect and reinforce our desired organizational communication structure.

As just one example of how Linear's product embodies their approach, it includes a feature that automatically cancels tickets after X days of inactivity. This prioritizes a clean backlog and helps maintain momentum, which is exactly how we want to work. In pay-it-forward fashion, Qualytics now includes a feature that automatically marks inactive data quality anomalies as "ignored."

### Start with the Pain

About 90% of the features we shipped in 2025 trace back to a real conversation with a real customer experiencing real frustration. Not a persona. Not a market segment analysis. An actual human who said something like "I spent three hours tracking down why this dashboard was wrong and it turned out to be a null in a field that should never be null."  The features that make it to our roadmap are the ones where multiple customers have independently described variations of the same problem.

### The Empathy-Driven Loop

Qualytics is built for enterprise customers. Our product teams bring truckloads of empathy when solving problems on their behalf, but our internal environment is decidedly un-enterprisey. Large enterprise pain - the scale, the bureaucracy, the complex permissioning - can be hard to feel when you're a small, agile team.

To combat this, we invest a lot of time and effort in deliberate attempts to dogfood the Qualytics platform. We actively use our own product to manage internal data challenges in support of our demo environments and regression testing artifacts, even when Qualytics is overkill for the task.

We've found that product team members with prior stints in services working directly with enterprise (or prior stints in a position within Qualytics' ICP) have proven very helpful establishing fit within our org and on our team. Hiring for this type of fit is a way to bootstrap the deep contextual understanding that's necessary to build B2B software that matters.

### Cross-Functional by Default

We don't have a wall between engineering and product. Engineers talk directly to customers. Product managers can read code. Customer success feeds directly into development plans.

When an engineer hears a customer describe their workflow, they catch implementation details that would never survive translation through multiple meetings. When product understands the technical constraints, they propose solutions that are actually buildable.

This approach puts more people in more conversations. We work hard to keep them tight.  The upside is feature-market fit.

### Say No More Than Yes

The hardest part of building product isn't deciding what to build. It's deciding what not to build. Every feature has ongoing cost: maintenance, documentation, cognitive load for users, constraints on future architecture.

Steve Jobs, as he often did when talking about product, said it well - "People think focus means saying yes to the thing you’ve got to focus on. But that’s not what it means at all. It means saying no to the hundred other good ideas that there are. You have to pick carefully. I’m actually as proud of the things we haven’t done as the things I have done. Innovation is saying no to 1,000 things.”

We've gotten better at saying no. It is still hard and it feels harsh in the moment. But our product is coherent because we've been willing to disappoint some potential customers to delight the ones we're actually built for.

### Build for the Workflow, Not the Feature

The biggest shift in our thinking has been moving from feature-centric to workflow-centric development. A feature is a capability. A workflow is the entire context in which that capability gets used.

When a data steward needs to investigate an anomaly, they don't just need to see the anomaly. They need to see the history, the related data, the likely cause, and the path to resolution. Building the "view anomaly" feature without building the investigation workflow is building half a bridge.

This is harder. It requires understanding not just what users want to accomplish but how they think about their work. But it's the difference between software that gets used and software that gets loved. We're actively investing in enhancements of common workflows and we're excited about leveraging generative AI in this area.

### The Compound Effect

There's nothing new under the sun here. Learn from users. Stay close to customer pain. You've heard it before. It's not about your product strategy.  It's about execution and the team doing the executing. Culture eats strategy for breakfast.

At the start, we were guessing and following my personal intuition. Now we're informed guessing with more real-world data driving our work. Quality data. Trusted data. That trust drives our confidence in what we deliver, which is a platform to help users build trust in their data, which brings us full circle.


Onward & Upward!