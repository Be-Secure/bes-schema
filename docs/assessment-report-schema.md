---
layout: page
title: Assessment Report
permalink: /assessment-report/
nav_order: 5
---

# Open Source Assessment Report Schema (OSAR)

**Version 0.1.0 (Jan 18, 2024)**

Original authors:
- Vinod Panicker ([@panickervinod](https://github.com/panickervinod))
- Harimohan Rajamohanan ([@harimohanr](https://github.com/harimohanr))

# Purpose

This document defines a standard interchange format for describing
vulnerability assessment reports for open source assets.

We hope to define a simple format that all BeS Labs can export,
to make it easier for users, security researchers, and any other efforts to
consume all available databases. Use of this format would also make it easier
for the databases themselves to share or cross-check information. Ultimately,
this format aims to enable automated, accurate, and distributed management
of vulnerability assessments of open source assets such as projects and ML models.

This format is stable, but further backwards compatible changes may still be made.
Feedback from maintainers of other vulnerability databases and security response teams
is most welcome. Please feel free to create an
[issue in this repo](https://github.com/Be-Secure/bes-schema/issues/new).

# Format Overview

The format is a JSON-based encoding format, using the following informal schema.
The exact details of each field are elaborated in the next section. All strings
contain UTF-8 text.

A JSON Schema for validation is also available
[here](https://github.com/Be-Secure/bes-schema/blob/main/validation/assessment-report-schema.json).

```json
{
    "schema_version": string,
    "asset": {
        "type": string,
        "name": string,
        "url": string
    },
    "assessments": [
        {
            "tool": {
                "name": string,
                "type": string,
                "version": string,
                "playbook": string
            },
            "execution": {
                "type": string,
                "id": string,
                "status": string,
                "timestamp": timestamp,
                "url": string
            },
            "result": [
                {
                    "type": string,
                    "attribute": string,
                    "value": string
                }
            ]
        }
    ]
}
```

Overall, the approach of this schema is to define only the fields that
absolutely must be shared between labs, leaving customizations to the
"ecosystem_specific" and "database_specific" blocks (see below)

# Field Details

## schema_version field

```json
{
	"schema_version": string
}
```

The `schema_version` field is used to indicate which version of the schema
a particular vulnerability assessment was exported with. This can help consumer applications
decide how to import the data for their own systems and offer some protection
against future breaking changes. The value should be a string matching the 
schema version, which follows the [SemVer 2.0.0](https://semver.org) format, with
no leading "v" prefix. If no value is specified, it should be assumed to be `1.0.0`,
matching version 1.0 of the schema. Clients can assume that new minor and patch
versions of the schema only add new fields, without changing the meaning of old
fields, so that a client that knows how to read version 1.2.0 can process data
identifying as schema version 1.3.0 by ignoring any unexpected fields.

## open source asset attributes

```json
"asset": {
    "type": string,
    "name": string,
    "url": string
}
```

Description goes here


## assessment tool attributes

```json
"tool": {
    "name": string,
    "type": string,
    "version": string,
    "playbook": string
}
```

Description goes here

## Assessment playbook execution attributes

```json
"execution": {
    "type": string,
    "id": string,
    "status": string,
    "timestamp": timestamp,
    "url": string
}
```

Description goes here

## Assessment playbook execution attributes

```json
"result": [
    {
        "type": string,
        "attribute": string,
        "value": string
    }
]
```

<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>A</code></td>
      <td>
        Description goes here
      </td>
    </tr>
    <tr>
      <td><code>A</code></td>
      <td>
        Description goes here
      </td>
    </tr>
  </tbody>
</table>

Description goes here