operational-endpoints-spec
==========================

Specifications and examples for common operational endpoints

Introduction
------------

Many of our applications need to expose common information to other systems such as load balancers, monitoring systems, deployment mechanisms etc.  The concepts for these are common across most applications.  These specifications whoe how to do this in a consistent form and at predictable endpoint locations.

We don't propose that all applications must expose this information, just that when they do, it should be done consistently.

All operational endpoints live under `/__/` to make grouping of the handlers/controllers together when implementing.

[Readiness](READY.md)

[About](ABOUT.md)
