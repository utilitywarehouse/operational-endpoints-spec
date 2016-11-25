Health endpoint
===============

Path
----
`/__/health`

Purpose
-------
Lets the caller (monitoring application / tester / developer) know information about the current health of the application. (For example, health might be degraded because only 1 out of 3 database replicas can be reached, might be failing because of an authentication issue, etc)

We may use this to populate operational dashboards etc, and to quickly point the team at the issue that needs fixing.


Behaviour
---------
Where implemented this endpoint:

MUST return `Content-Type: application/json`

MUST return JSON in the form of the following example
```
{
  "name": "uw-foo",
  "description": "Performs the foo bar baz functions",
  "health": "unhealthy",
  "checks": [
    {
      "name": "Database connectivity",
      "health": "healthy",
      "output": "connection to db1234.uw.systems is ok"
    },
    {
      "name": "Message queue connection",
      "health": "degraded",
      "output": "Connected OK to broker01.uw.systems ok\nFailed to connect to broker02.uw.systems",
      "action": "Check that the message queue on broker02.uw.systems is running and check network connectivity"
    },
    {
      "name": "SMTP server connectivity",
      "health": "unhealthy",
      "output": "failed to connect to smtp123.uw.systems on port 25 : Connection refused",
      "action": "Check the SMTP server on smtp123.uw.system is running and check network connectivity",
      "impact": "Users will not receive email notifications whenever a foo bar action is completed"
    }
  ]
}
```

The JSON payload:

MUST include:

* name
* description
* health
* checks
* checks[0]

MAY include other properties not included in this specification if and only if their name begins with `_`

SHOULD include appropriate cache headers


The "health" property MUST be one of the following values:

* healthy - meaning the application is fully healthy and can function properly
* degraded - meaning the application not not fully healthy but can function properly
* unhealthy - meaning the application can not function properly

Consumers of this endpoint MUST tolerate undefined values of `"health"` and SHOULD treat them as `"degraded"`

The top-level “health” property is a MUST reflects the most severe of the individual `check` entries.

Each `check` entry MUST have the following properties:

* name
* health (with the same possible values as the top-level "health" property described above
* output

When a `check` entry is not `healthy` it MUST have an `action` property to guide an operational response.

When a `check` entry is `unhealthy` is MUST have an `impact` property to give a description of how this failure will impact consumers (where appropriate in business friendly terms)



