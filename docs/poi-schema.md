---
layout: page
title: Projects Of Interest
permalink: /projects-of-interest/
nav_order: 2
---


# Open Source Software Projects of Interest (OSSPoI)

**Version 0.1.0 (Jan 23, 2024)**

Original authors:
- Arun Suresh 

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
[here](https://github.com/Be-Secure/bes-schema/blob/main/validation/assessment-report-schema-validator.json). -->

A sample json for your understanding is available
[here](../example/projects-of-interest-schema-sample.json).

```json
{
  "schema_version": "0.1.0",
  "items": [
    {
      "bes_tracking_id": "NUMBER",
      "issue_url": "STRING",
      "name": "STRING",
      "description": "STRING",
      "bes_technology_stack": "STRING",
      "created_at": "STRING",
      "updated_at": "STRING",
      "html_url": "STRING",
      "homepage": "STRING",
      "owner": {
        "login": "STRING",
        "type": "STRING"
      },
      "parent": "STRING",
      "license": "STRING",
      "language": { "STRING": "NUMBER" },
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

The data for this schema can be fetched from the api for the repository.

## items.bes_tracking_id

```json
{
  "bes_tracking_id": "STRING"
}
```

The issue ID of the TAVOSS track request for the project raised under Be-Secure.

## items.issue_url

```json
{
  "issue_url": "STRING"
}
```

URL to the TAVOSS track request under Be-Secure.

## items.name

```json
{
  "name": "STRING"
}
```

Name of the OSS.

## items.description

```json
{
  "description": "STRING"
}
```

A small description about the project.

## items.bes_technology_stack

```json
{
  "bes_technology_stack": "STRING"
}
```
The category under which the project belong.

## items.created_at

```json
{
  "created_at": "STRING"
}
```
Date and time at which the project repo was created.

## items.updated_at

```json
{
  "updated_at": "STRING"
}
```

Date and time of the last update.

## items.html_url

```json
{
  "html_url": "STRING"
}
```

The url to the repository.

## items.homepage

```json
{
  "homepage": "STRING"
}
```
URL to the webpage of the project.

## items.owner

```json
{
  "owner": {
        "login": "STRING",
        "type": "STRING"
      }
}
```

Details of the owner of the repo.

<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>login</code></td>
      <td>
       Name of the owner of the repo
      </td>
    </tr>
    <tr>
      <td><code>type</code></td>
      <td>
        Organization/User
      </td>
    </tr>
  </tbody>
</table>

## items.parent

```json
{
  "parent": "STRING"
}
```

URL to the parent repo of the project.

## items.license

```json
{
  "license": "STRING"
}
```

This field contains the license of the project.

## item.language

```json
{
  "language": {"STRING": "NUMBER"}
}
```

A dictionary containing the list of the languages used inside the project and their respective size.

## item.tags

```json
{
  "tags": ["STRING"]
}
```

A list containing different tags assigned to the project. Mainly used for filtering in the UI.