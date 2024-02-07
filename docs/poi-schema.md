---
layout: page
title: Projects Of Interest
permalink: /projects-of-interest/
nav_order: 2
---


# Open Source Software Projects of Interest (OSSPoI)

**Version 0.1.0 (Jan 25, 2024)**

Original authors:
- Vinod Panicker (@panickervinod)
- Harimohan Rajamohanan (@harimohanr)
- Arun Suresh (@asa1997)
- Sudhir Verma(@sudhirverma)

# Purpose

This document outlines a standardized data interchange format for open source software projects of interest (OSSPoI) within organizations. The OSSPoI encompasses essential project details such as project **id**, project **name**, **version** specifics, **owner** information, **onboarded_date**, and **last_update_date**. These details facilitate seamless sharing among peers within the organization and publication to the BeSLighthouse community dashboard. Open Source projects can be onbaorded into BeSLab by BLIman utility.

This standardized data interchange format not only streamlines the sharing and publication process of open source software projects within organizations but also significantly reduces the time required for BeSLabs to assess projects of interest. By providing a structured framework for exchanging essential project details, BeSLabs can expedite their assessment procedures and evaluation of open source projects.

This format is stable, but further backwards compatible changes may still be made. Please feel free to create an [issue in this repo](https://github.com/Be-Secure/bes-schema/issues/new).

# Format Overview

The format is a JSON-based encoding format, using the following informal schema.
The exact details of each field are elaborated in the next section. All 'STRING's
contain UTF-8 text.

The data for this schema can be fetched from the api for the repository.

<!-- A JSON Schema for validation is also available
[here](https://github.com/Be-Secure/bes-schema/blob/main/validation/assessment-report-schema-validator.json). -->

A sample json for your understanding is available
[here](https://be-secure.github.io/bes-schema/example/projects-of-interest-schema-sample.json).

```json
{
  "schema_version": "0.1.0",
  "projects": [
      {
          "id": "NUMBER",
          "name": "STRING",
          "version": [
              {
                  "tag": "STRING",
                  "release_date": "STRING"
              }
          ],
          "issue_url": "STRING",
          "description": "STRING",
          "bes_technology_stack": "STRING",
          "onboarded_date": "STRING",
          "last_update_date": "STRING",
          "forked_repo_url": "STRING",
          "tavoss_repo_url": "STRING",
          "homepage_url": "STRING",
          "parent": {
              "name": "STRING",
              "type": "STRING",
              "url": "STRING"
          },
          "owner": {
              "name": "STRING",
              "type": "STRING"
          },
          "sub_projects": [
              {
                  "id": "STRING",
                  "name": "STRING"
              }
          ],
          "license": "STRING",
          "languages": {
              "STRING": "NUMBER"
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


## projects.id

```json
{
  "id": "STRING"
}
```

The issue ID of the TAVOSS track request for the project raised under Be-Secure.

## projects.name

```json
{
  "name": "STRING"
}
```

Name of the OSS.

## projects.version

```json

{
  "version": [
    {
        "tag": "STRING",
        "release_date": "STRING"
    }
  ]
}

```

Contains the details of the tracked version.

<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>tag</code></td>
      <td>
       Version tag of the tracked project
      </td>
    </tr>
    <tr>
      <td><code>release_date</code></td>
      <td>
        The date of release of the tracked version.
      </td>
    </tr>
  </tbody>
</table>

## projects.issue_url

```json
{
  "issue_url": "STRING"
}
```

URL to the TAVOSS track request under Be-Secure.


## projects.description

```json
{
  "description": "STRING"
}
```

A small description about the project.

## projects.bes_technology_stack

```json
{
  "bes_technology_stack": "STRING"
}
```
The category under which the project belong.

## projects.onboarded_date

```json
{
  "onboarded_date": "STRING"
}
```
Date and time at which the project was onboarded.

## projects.last_update_date

```json
{
  "last_update_date": "STRING"
}
```

Date and time of the last update.

## projects.forked_repo_url

```json
{
  "forked_repo_url": "STRING"
}
```

The url to the repository.

## projects.tavoss_repo_url

```json

{
  "tavoss_repo_url": "STRING",
}
```

URL to the TAVOSS version of the project.

## projects.homepage_url

```json
{
  "homepage_url": "STRING"
}
```
URL to the webpage of the project.

## projects.parent

```json
{
  "parent": {
            "name": "STRING",
            "type": "STRING",
        }
}
```

The details of the parent organization of the repo are given here.

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
       Name of the parent of the repo
      </td>
    </tr>
    <tr>
      <td><code>type</code></td>
      <td>
        Organization/User/Lab
      </td>
    </tr>
  </tbody>
</table>

## projects.owner

```json
{
  "owner": {
        "name": "STRING",
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
      <td><code>name</code></td>
      <td>
       Name of the owner of the repo
      </td>
    </tr>
    <tr>
      <td><code>type</code></td>
      <td>
        Organization/User/Lab
      </td>
    </tr>
  </tbody>
</table>

## projects.sub_projects

```json
"sub_projects": [
    {
        "id": "STRING",
        "name": "STRING",
        "url": "STRING"
    }
]
```

Contains the details of the tracked components of the project of interest.

<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>id</code></td>
      <td>
       Tracking id
      </td>
    </tr>
    <tr>
      <td><code>name</code></td>
      <td>
        Name of the sub project
      </td>
    </tr>
    <tr>
      <td><code>url</code></td>
      <td>
        URL to the repo
      </td>
    </tr>
  </tbody>
</table>

## projects.license

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
