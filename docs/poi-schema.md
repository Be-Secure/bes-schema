---
layout: page
title: Projects Of Interest
permalink: /projects-of-interest/
nav_order: 2
---


# Open Source Software Projects of Interest (OSSPoI)

**Version 0.1.0 (Jan 23, 2024)**



# Purpose

This document defines a standard way of describing the essential information of each project under a Project of Interest(POI).
This format is stable, but further backwards compatible changes may still be made.
Feedback from maintainers of other vulnerability databases and security response teams
is most welcome. Please feel free to create an
[issue in this repo](https://github.com/Be-Secure/bes-schema/issues/new).

# Format Overview

The format is a JSON-based encoding format, using the following informal schema.
The exact details of each field are elaborated in the next section. All 'STRING's
contain UTF-8 text.

<!-- A JSON Schema for validation is also available
[here](https://github.com/Be-Secure/bes-schema/blob/main/validation/assessment-report-schema-validator.json).

A sample json for your understanding is available
[here](https://github.com/Be-Secure/bes-schema/blob/main/example/assessment-report-schema-sample.json). -->

```json
{
  "schema_version": "0.1.0",
  "items": [
    {
      "bes_tracking_id": "NUMBER",
      "issue_url": "STRING",
      "name": "STRING",
      "full_name": "STRING",
      "description": "STRING",
      "bes_technology_stack": "STRING",
      "created_at": "STRING",
      "updated_at": "STRING",
      "pushed_at": "STRING",
      "html_url": "STRING",
      "homepage": "STRING",
      "owner": {
        "login": "STRING",
        "id": "NUMBER",
        "type": "STRING"
      },
      "project_repos": {
        "main_github_url": "STRING",
        "main_bes_url": "STRING",
        "all_projects": [
          {
            "id": "NUMBER",
            "name": "STRING",
            "url": "STRING"
          }
        ],
        "all_bes_repos": [
          {
            "id": "NUMBER",
            "name": "STRING",
            "url": "STRING"
          }
        ]
      },
      "license": {
        "key": "STRING",
        "name": "STRING",
        "spdx_id": "STRING"
      },
      "language": {
        "Go": "NUMBER",
        "MDX": "NUMBER",
        "HCL": "NUMBER",
        "Shell": "NUMBER",
        "Makefile": "NUMBER",
        "PowerShell": "NUMBER",
        "JavaScript": "NUMBER",
        "Dockerfile": "NUMBER"
      },
      "tags": [
        "STRING"
      ]
    }
  ]
}

```

# Field Details

## schema_version field

```json
{
	"schema_version": "STRING"
}
```

The `schema_version` field is used to indicate which version of the schema
a particular poi list was exported with. This can help consumer applications
decide how to import the data for their own systems and offer some protection
against future breaking changes. The value should be a string matching the 
schema version, which follows the [SemVer 2.0.0](https://semver.org) format, with
no leading "v" prefix. If no value is specified, it should be assumed to be `1.0.0`,
matching version 1.0 of the schema. Clients can assume that new minor and patch
versions of the schema only add new fields, without changing the meaning of old
fields, so that a client that knows how to read version 1.2.0 can process data
identifying as schema version 1.3.0 by ignoring any unexpected fields. 