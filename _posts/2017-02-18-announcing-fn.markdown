---
layout: post
title:  "Announcing fn, a serverless framework"
date:   2017-02-05 12:00:00 +0000
categories: serverless software fn
---

For the last couple of months I've been working on
[fn](http://github.com/andrewmccall/fn) (pronounced fun), a serverless
framework. It's been slow going, but hopefully I'll get some more time to spend
on it over the coming months.

Serverless frameworks like AWS Lambda look really good, the problem is they're
tightly tied to the cloud environment they're running in and provide links
primarily to that providers services.

fn builds an abstraction layer on top of the underlying resource scheduler, the
first iteration will be a YARN based scheduler but I intend to follow it up
with Mesos in the near future.

Over the coming weeks I'll try to document some of the thinking around the
design and document some of the development.

fn is Apache 2 licensed and is available to fork on github at (http://github.com/andrewmccall/fn).
