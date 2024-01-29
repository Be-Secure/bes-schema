---
layout: page
title: Environment
permalink: /environment/
nav_order: 7
---

# BeS Environment Info & Status

**Version 0.1.0 (Jan 25, 2024)**

Original authors:
- Vinod Panicker (@panickervinod)
- Harimohan Rajamohanan (@harimohanr)
- Arun Suresh (@asa1997 )

# Purpose

This document defines the data interchange format for environments for any given organisation. An organization powered by BeSLab shall publish their environments to its peers as well the community dashboard BeSLighthouse. The data in this scehma can be used by other tools under the organization.
This format is stable, but further backwards compatible changes may still be made.
Feedback from maintainers of other vulnerability databases and security response teams
is most welcome. Please feel free to create an [issue in this repo](https://github.com/Be-Secure/bes-schema/issues/new).

# Format Overview

The format is a JSON-based encoding format, using the following informal schema.
The exact details of each field are elaborated in the next section. All 'STRING's
contain UTF-8 text.

<!-- A JSON Schema for validation is also available
[here](https://github.com/Be-Secure/bes-schema/blob/main/validation/assessment-report-schema-validator.json). -->

<!-- A sample json for your understanding is available
[here](https://be-secure.github.io/bes-schema/example/projects-of-interest-schema-sample.json). -->

```json
{
  "schema_version": "STRING",
  "environments":[
    {
        "name": "STRING",
        "version": "STRING",
        "type": "STRING",
        "owner": {
            "name": "STRING",
            "type": "STRING"
        },
        "date_of_creation": "STRING",
        "last_update_date": "STRING",
        "last_execution": {
            "name": "STRING",
            "type": "STRING",
            "status": "STRING",
            "timestamp": "STRING"
        }
    }
  ]
}
```
