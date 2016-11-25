Readiness endpoint
==================


Path
----

`/__/ready`

Purpose
-------
Lets the caller (probably k8s or a load balancer or similar) know the application is in a state where is it able to serve requests.

Behaviour
---------
Returns `200` if ready with a body of `ready\n` if the application is ready

Returns `503` with no response body otherwise.

SHOULD not be cacheable.


SHOULD expect to be called often (i.e., needs to be fast.)
