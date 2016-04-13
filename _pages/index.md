---
permalink: /
title: Introduction
---

This guide describes how 18F builds and operates secure, resilient,
maintainable distributed systems in the cloud.

The DevOps movement emerged from internet companies that had to solve a
wicked problem: how to build reliable, secure distributed systems at
an unprecedented scale, while enabling a rate of change to those
systems that was orders of magnitude faster than the industry had ever
achieved. Over the last few years, ideas from the DevOps movement have been adopted across many different
industries, including highly regulated domains such as financial
services and government.

In this guide we will present a variant on
DevOps known as _Rugged DevOps_, which incorporates the principles of
the [Rugged Manifesto](https://www.ruggedsoftware.org/). We chose to
focus on Rugged DevOps because in government we have a public duty to build systems
that are resilient to attacks, and which must survive and evolve over
long periods of time.

### Overview of this guide

We begin by introducing the principles of DevOps, and the software
delivery lifecycle, known as _Continuous Delivery_ that enables us to
implement these principles. We then discuss how to build quality and
security into applications throughout their lifecycle. Moving to the
operations side, we cover how to build and evolve secure, resilient
operational environments, and the implications for developers of
building services that can run in these environments.
