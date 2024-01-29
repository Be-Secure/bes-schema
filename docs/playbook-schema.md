---
layout: page
title: Playbook
permalink: /playbook/
nav_order: 8
---

# BeS Playbook Info & Status

**Version 0.1.0 (Jan 25, 2024)**

Original authors:
- Vinod Panicker (@panickervinod)
- Harimohan Rajamohanan (@harimohanr)
- Arun Suresh (@asa1997 )

# Purpose

This document defines the data interchange format for playbooks for any given organisation. An organization powered by BeSLab shall publish their playbooks to its peers as well the community dashboard BeSLighthouse. The data in this scehma can be used by other tools under the organization.
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
    },
    "detailed_report_path": "STRING",
    "compatible_envs": ["STRING"]
}
```

# Field Details

## schema_version

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

## name

```json
{
    "name": "STRING"
}
```

The name of the playbook.

## version

```json
{
    "version": "STRING"
}
```

Version of the playbook.

## type

```json
{
  "type": "STRING"
}
```

The type of the playbook - `assessment` or `exploit`.

## owner

```json
"owner": {
  "type": "STRING",
  "name": "STRING"
}
```

The details of the author of the playbook goes here.

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
      <td>User / Organization / Lab</td>
    </tr>
    <tr>
        <td><code>name</code></td>
        <td>Name of the author</td>
    </tr>
  </tbody>
</table>

## date_of_creation

```json
{
  "date_of_creation": "STRING"
}
```

The date of the creation of playbook.

## last_updated_date

```json
{
  "last_updated_date": "STRING"
}
```

The date of last updation of the playbook.

## last_execution

```json
"last_execution": {
    "type": "STRING",
    "name": "STRING",
    "status": "STRING",
    "timestamp": "STRING"
}
```

Details of the last playbook execution is given here.

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
      <td>User / Organization / Lab</td>
    </tr>
    <tr>
        <td><code>name</code></td>
        <td>Name of the entity who ran the playbook</td>
    </tr>
    <tr>
        <td><code>status</code></td>
        <td>success / failure</td>
    </tr>
    <tr>
        <td><code>timestamp</code></td>
        <td>Date and time of last execution</td>
    </tr>
  </tbody>
</table>

## detailed_report_path

```json
{
  "detailed_report_path": "STRING"
}
```

The path to the detailed report of the tools execution is given here.

## compatible_envs

```json
"compatible_envs": [
  "STRING"
]
```

A list of compatible BeSman environments.