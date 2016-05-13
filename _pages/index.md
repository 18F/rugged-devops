---
permalink: /
title: Introduction
---

This guide describes how 18F builds and operates secure, resilient,
maintainable distributed systems in the cloud. We do this by applying
principles, patterns and practices taken from the Rugged DevOps movement.

The DevOps movement emerged from internet companies that had to solve a
wicked problem: how to build reliable, secure distributed systems at
an unprecedented scale, while enabling a rate of change to those
systems that was orders of magnitude faster than the industry had ever
achieved. Over the last few years, ideas from the DevOps movement have
been adopted across many different industries, including highly
regulated domains such as financial services and government.

In this guide we will present a variant on DevOps known as _Rugged
DevOps_, which incorporates the principles of the
[Rugged Manifesto](https://www.ruggedsoftware.org/). We chose to focus
on Rugged DevOps because in government we have a public duty to build
systems that are resilient to attacks, and which must survive and
evolve over long periods of time. We also operate in a highly
regulated, low-trust environment that makes the Rugged variant of
DevOps particularly appropriate. Finally, the majority of 18F's staff
are on two year fixed-term contracts---as time passes, we will
increasingly need to operate and evolve systems whose original
delivery team members no longer working here.

This guide describes our current best thinking on how to ensure we can
meet our responsibilities towards the public while continuing to
innovate, and in particular how to ensure that the burden of operating
ever more services remains more or less constant.

### Overview of this guide

We begin by introducing the principles of DevOps, along with the software
delivery lifecycle, known as that enables us to implement these
principles, known as Continuous Delivery. We then discuss how to build
quality and security into applications throughout their
lifecycle. Moving to the operations side, we then cover how to build and
evolve secure, resilient operational environments, and the
implications for developers of building services that can run in these
environments.
