---
layout: page
title: Playbook
permalink: /playbook/
nav_order: 8
---

# BeS Playbook Info & Status

**Version 0.1.0 (Jan 30, 2024)**

Original authors:

- Vinod Panicker ([@panickervinod](https://github.com/panickervinod))
- Harimohan Rajamohanan ([@harimohanr](https://github.com/harimohanr))
- Arun Suresh ([@asa1997](https://github.com/asa1997))
- Sudhir Verma([@sudhirverma](https://github.com/sudhirverma))

# Purpose

<!-- This document outlines a standardized data interchange format for open source software playbooks of interest (OSSPloI) within organizations. The OSSPloI encompasses essential playbook details such as playbook **name**, **version** specifics,**type** information, **author** information, **last_execution** details, **detailed report path** and a list of **compatible environments**. These details facilitate seamless sharing among peers within the organization and publication to the BeSLighthouse community dashboard. Open Source playbooks can be onbaorded into BeSLab by BLIman utility.

This standardized data interchange format not only streamlines the sharing and publication process of open source software playbooks within organizations but also significantly reduces the time required for BeSLabs to assess projects of interest. These playbooks help in automating the steps required for assessment activities as well as expediting the time required for it. -->

This document introduces a standardized data interchange format specifically designed for open source software playbooks within organizations. The OSSPloI captures crucial details related to these playbooks, including:

- Playbook Name
- Version Specifics
- Type Information
- Author Details
- Last Execution Information
- Detailed Report Path
- List of Compatible Environments

These comprehensive details facilitate seamless sharing among peers within the organization and enable publication to the BeSLighthouse community dashboard. By leveraging the BLIman utility, organizations can effortlessly onboard their Open Source playbooks into BeSLab.

The adoption of this standardized format not only streamlines the sharing and publication process of open source software playbooks but also significantly reduces the time required for BeSLabs to assess projects of interest. These playbooks play a pivotal role in automating assessment activities and expediting the overall assessment timeline.

This format is stable, but further backwards compatible changes may still be made. Please feel free to create an [issue in this repo](https://github.com/Be-Secure/bes-schema/issues/new).


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
    "playbooks":[
      {
      "name": "STRING",
      "version": "STRING",
      "type": "STRING",
      "author": {
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
  ]
}
```

# Field Details

## playbooks.schema_version

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

## playbooks.name

```json
{
    "name": "STRING"
}
```

The name of the playbook.

## playbooks.version

```json
{
    "version": "STRING"
}
```

Version of the playbook.

## playbooks.type

```json
{
  "type": "STRING"
}
```

The type of the playbook - `assessment` or `exploit`.

## playbooks.author

```json
"author": {
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

## playbooks.date_of_creation

```json
{
  "date_of_creation": "STRING"
}
```

The date of the creation of playbook.

## playbooks.last_updated_date

```json
{
  "last_updated_date": "STRING"
}
```

The date of last updation of the playbook.

## playbooks.last_execution

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

## playbooks.detailed_report_path

```json
{
  "detailed_report_path": "STRING"
}
```

The path to the detailed report of the tools execution is given here.

## playbooks.compatible_envs

```json
"compatible_envs": [
  "STRING"
]
```

A list of compatible BeSman environments.