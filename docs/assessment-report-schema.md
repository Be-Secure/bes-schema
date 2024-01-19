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
[here](https://github.com/Be-Secure/bes-schema/blob/main/validation/assessment-report-schema-validator.json).

```json
{
    "schema_version": string,
    "asset": {
        "type": string,
        "name": string,
        "url": string,
        "environment": string
    },
    "assessments": [
        {
            "tool": {
                "name": string,
                "type": string,
                "version": string,
                "playbook": string,
                "detailedReport": string
            },
            "execution": {
                "type": string,
                "id": string,
                "status": string,
                "timestamp": timestamp,
                "timeTaken": string
            },
            "results": [
                {
                    "feature": string,
                    "aspect": string,
                    "attribute": string,
                    "value": number
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

## asset field

```json
"asset": {
    "type": string,
    "name": string,
    "url": string
}
```

Details about the open source asset that was assessed.

<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>type</code></td>
      <td>
        Project / Model
      </td>
    </tr>
    <tr>
      <td><code>name</code></td>
      <td>
        Name of the project or model that was assessed
      </td>
    </tr>
        <tr>
      <td><code>url</code></td>
      <td>
        Project source code URL or the ML model card URL
      </td>
    </tr>
  </tbody>
</table>

## assessments.tool field

```json
"tool": {
    "name": string,
    "type": string,
    "version": string,
    "playbook": string,
    "detailedReport": string
}
```

Details about the tool used for assessment. "assessments" is an array and it should contain all the assessments done on a particular asset. For instance, a typical open source assessment in Be-Secure comprises of SAST, Fuzzing, SCA, OpenSSF Criticality Score & ScoreCard and License compliance checks. All the assessments metadata should be contained in this array.

<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>name</code></td>
      <td>
        Name of the tool used for this assessment. For SAST type assessment CodeQL is an example tool name 
      </td>
    </tr>
    <tr>
      <td><code>type</code></td>
      <td>
        SAST / Fuzzing / License Compliance / Criticality Score / SBOM
      </td>
    </tr>
    <tr>
      <td><code>version</code></td>
      <td>
        Tool version
      </td>
    </tr>
    <tr>
      <td><code>playbook</code></td>
      <td>
        Assessment tool playbook name
      </td>
    </tr>
  </tbody>
</table>

## assessments.execution field

```json
"execution": {
    "type": string,
    "id": string,
    "status": string,
    "timestamp": timestamp,
    "timeTaken": string
}
```

Assessment tool execution metadata. 

<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>type</code></td>
      <td>
        Is this assessment tool execution done by an Organization / Individual
      </td>
    </tr>
    <tr>
      <td><code>id</code></td>
      <td>
        Organization Id or the Individual's id (It could be a GitHub id of the individual). An example for organization is Be-Secure
      </td>
    </tr>
    <tr>
      <td><code>status</code></td>
      <td>
        Success / Failure
      </td>
    </tr>
    <tr>
      <td><code>timestamp</code></td>
      <td>
        Date and time of assessment tool execution
      </td>
    </tr>
    <tr>
      <td><code>timeTaken</code></td>
      <td>
        Total time taken in seconds to complete the assessment tool execution
      </td>
    </tr>
  </tbody>
</table>

## assessments.results array

```json
"results": [
    {
        "feature": string,
        "aspect": string,
        "attribute": string,
        "value": number
    }
]
```
Summary of assessment tool execution results. Individual tool execution results should be translated to this format to accomodate the summary of result. 

<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>feature</code></td>
      <td>
        Vulnerability / Code Smell / Criticality Score / ScoreCard / License Compliance / Dependency
      </td>
    </tr>
    <tr>
      <td><code>aspect</code></td>
      <td>
        Severity / Count / Score
      </td>
    </tr>
    <tr>
      <td><code>attribute</code></td>
      <td>
        Depends on the tool feature and the aspect. For instance, in SAST the aspect may be "Severity"and the attribute will be "Critical"
      </td>
    </tr>
    <tr>
      <td><code>value</code></td>
      <td>
        The summary count or value
      </td>
    </tr>
  </tbody>
</table>

For instance, a SAST tool execution result may give 10 vulnerability information and 50 code smells of various severity along with the file name and the exact line numbers. For this schema, the result summary should be abstracted as below.

```json
"results": [
    {
        "feature": "Vulnerability",
        "aspect": "Severity",
        "attribute": "Critical",
        "value": 6
    },
    {
        "feature": "Vulnerability",
        "aspect": "Severity",
        "attribute": "Medium",
        "value": 4
    },
    {
        "feature": "Code Smell",
        "aspect": "Severity",
        "attribute": "Low",
        "value": 50
    }
]
```

