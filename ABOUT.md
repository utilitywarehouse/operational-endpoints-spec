About endpoint
==============

Path
----
`/__/about`

Purpose
-------
Lets the caller (documentation aggregator app / tester / developer) know information about the application such as:

* Who is the owner of the service
* What the service does
* Links to source control etc

Behaviour
---------
Where implemented this endpoint:

MUST return `Content-Type: application/json` 

MUST return JSON in the form of the following example
```
{
    "name": "service-name-goes-here",
    "description": "Simple service description goes here (business friendly where possible)",
    "owners": [
        {
            "name": "Team XYZ",
            "slack": "#xyz_team"
        }
    ],
    "links": [
        {
            "url": "https://circleci.com/gh/utilitywarehouse/service-repo/288",
            "description": "Circle CI build"
        },
        {
            "url": "https://github.com/utilitywarehouse/service-repo/README.md",
            "description": "readme"
        }
    ],
    "build-info" : {
    	"revision": "e7d46e130e3b4fa5e959abcb9b5f50fd25bc8c65"
    }
}
```

The JSON payload:

MUST include:

* name
* description
* owners
* owners[0]

SHOULD include:

* build-info

MAY include:

* links

MAY include other properties not included in this specification if and only if their name begins with `_`

SHOULD include appropriate cache headers

