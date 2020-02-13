---
title: "The Single Source of Truth - Really?"
author: Robert Stiff
layout: post
tags: ["programming", "distributed systems"]
date: 2019-08-26
---

In software engineering, there's often talk of the Source of Truth. Which database is source of truth? Yours or mine? When things get complicated, does it still make sense to think about databases or single systems as the source of truth?

<!--more-->

These conversations have all made the assumption that they can decide who has authority over reality. Unfortunately a database is never a source of truth. The word "source" means the point of origin. When thinking about the source of truth we need to think about where the data originates. Let's look at a few examples.

## An eCommerce Website

The website has an Orders database in the website, and you have a call centre platform with it's own database. It seems like the source of truth would be  the website's Orders database, and the call centre should accept that. But what happens when the call centre wants to take orders too. Does it have to send them through the website so the website can remain the source of truth? That's obviously coupling and creating the website as a single point of failure. 

## Stock Management

Your business starts with 1 warehouse. You get stock levels from the warehouse database and import them in to your purchasing database (for admin staff) and sales database (for your customers). Clearly that warehouse is the source of truth.

Now you expand and add another warehouse. The first warehouse cannot be the source of truth any more because it does not know about stock in the new warehouse, so you create a new stock levels database to hold a view of stock across multiple locations. Is THIS database the source of truth? If it becomes out of sync with the warehouse, it can't be said to be truthful anymore. Saying any of these systems is the source of truth is clearly lieing to yourself.

## The Reality

The reality? None of these systems is the source of truth. To really find the source of truth we have to expand our idea of a 'system' to include 3rd parties, software and importantly people, who make decisions and measure reality. 

For your eCommerce business, the customer is the source of truth for orders. They make the decision. Your website, mobile app or call centre is just the channel by which they place their order. 

For the stock management system, the source of truth is the staff in the warehouse, actually counting stock and recording it on their tablets. Both warehouse databases are equally the source of their respective truths.

So the phrase Source of Truth doesn't refer to which database I have built, it refers to the decision maker and the path by which data about that decision arrives with me.

## Thinking Differently

If we stop to think about databases as an authority we can open ourselves up to other opportunities. Instead of deciding where data should live, we can start thinking about how it should get there. This means we can think in terms of integration and extension. 

Now, a more useful toolset to use is that of event streams. The events may come from multiple places or go to multiple places, but the stream is where you can find that truth.

Databases become storage utilities, and the event stream becomes the centre of your system. Databases can be populated by reading the stream; notifications and other side effects can be triggered by things happening on the stream.

## What does that mean for our examples?

Well, the eCommerce website and the call centre are both sources of orders. Your fulfilment centres, your business intelligence, even your accounts are all reacting to these orders when they happen.

In your stock management system, you might still have a database that shows a view of stock in both warehouses, but it is nothing special. It is merely a projection of the stock keeping events which happened in your warehouses. And any side effects, sending notifications to your purchasing systems or updating business intelligence are triggered not by reading a single central database, bit by the stream.

## So what, I hear you say

Changing the way we think is challenging, and there is always more to it than can be written in a single blog post. 

But thinking about the events that happened in our businesses, and how data about then flows allows us to build software that model our businesses, not make our business adhere to the software.

Things are more extendable, more decoupled and easier to explain to non-technical colleagues.

So next time you are thinking "where is the source of truth?", try asking yourself "How does the truth get here?", "Who cares about it?" and importantly, what event has occurred in your business that we care about?"

You might just find a simpler way to build your software that better represents the reality you are working with.
