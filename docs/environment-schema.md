---
layout: page
title: Environment
permalink: /environment/
nav_order: 7
---

# BeS Environment Info & Status

**Version 0.1.0 (Jan 25, 2024)**

Original authors:

- Vinod Panicker ([@panickervinod](https://github.com/panickervinod))
- Harimohan Rajamohanan ([@harimohanr](https://github.com/harimohanr))
- Arun Suresh ([@asa1997](https://github.com/asa1997))
- Sudhir Verma([@sudhirverma](https://github.com/sudhirverma))

# Purpose

This document outlines a standardized data interchange format for open source software environments of interest (OSSEoI) within organizations. The environments are used to set up an environment for OSSPoI which would contain all the necessary tools and utilities for a security analyst to start working on it. The OSSEoI encompasses essential project environment details such as environment **name**, **version** specifics, **author** information, **date_of_creation**, **last_update_date**, **last_execution** details as well as details of **compatible playbooks**. These details facilitate seamless sharing among peers within the organization and publication to the BeSLighthouse community dashboard. Open Source project environments can be onbaorded into BeSLab by BLIman utility. These environments can be installed using a utility called BeSman.

This standardized data interchange format not only streamlines the sharing and publication process of open source software project environments within organizations but also significantly reduces the time required for BeSLabs to set up the projects. By providing a structured framework for exchanging essential project details, BeSLabs can expedite their assessment procedures and evaluation of open source projects.

This format is stable, but further backwards compatible changes may still be made. Please feel free to create an [issue in this repo](https://github.com/Be-Secure/bes-schema/issues/new).

# Example playbook

```json
{
  "schema_version": "0.0.1",
  "environments":[
    {
        "name": "fastjson-RT-env",
        "version": {
          "tag": "0.0.1",
          "release_date": "2024-05-27T09:27:34"
        },
        "author": {
            "name": "BeSLab",
            "type": "Lab"
        },
        "date_of_creation": "2024-05-25T09:27:34",
        "last_update_date": "2024-05-25T09:27:34",
        "last_execution": {
            "name": "BeSLab",
            "type": "Lab",
            "status": "Success",
            "timestamp": "2024-05-25T09:27:34"
        },
        "compatible_playbooks": [
          {
            "name": "scorecard",
            "version": ["0.0.1"]
          },
          {
            "name": "criticality_score",
            "version": ["0.0.1"]
          },
        ]
    }
  ]
}
```


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
        "version": {
          "tag": "STRING",
          "release_date": "STRING"
        },
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
        "compatible_playbooks": [
          {
            "name": "STRING",
            "version": ["STRING"]
          }
        ]
    }
  ]
}
```

## schema_version

```json
{
	"schema_version": "STRING"
}
```

The `schema_version` field is used to indicate which version of the schema
for the env details was exported with. This can help consumer applications
decide how to import the data for their own systems and offer some protection
against future breaking changes. The value should be a string matching the 
schema version, which follows the [SemVer 2.0.0](https://semver.org) format, with
no leading "v" prefix. If no value is specified, it should be assumed to be `1.0.0`,
matching version 1.0 of the schema. Clients can assume that new minor and patch
versions of the schema only add new fields, without changing the meaning of old
fields, so that a client that knows how to read version 1.2.0 can process data
identifying as schema version 1.3.0 by ignoring any unexpected fields. 

## environments

The `environments` is a json array which list all the environments and its details.

### environments.name

```json
{
  "name": "STRING"
}
```

The `name` field gives you the name of the environment script. It is a string of the format `besman-<project>-<type>-env`. The `<project>` refers to the oss project. Keep in mind that the hyphens(-) in the project name should be underscored(_). The `type` refers to whether the env script is `RT` or `BT`.

### environments.version

```json
{
  "version": {
      "tag": "STRING",
      "release_date": "STRING"
  }
}
```

The `version` field is a dictionary with two properties, 
- `tag`: Gives you the tag of the release.
- `release_date`: Gives you the date of the releae of the env script.

### environments.author

```json
{
  "author": {
      "name": "STRING",
      "type": "STRING"
  }
}
```

The `author` field is a dictionary which gives you the author of the env script.
- The `name` property gives you the name of the entity.
- The `type` property gives you whether the entity is a `user` or `organization` or `lab`.


### environments.date_of_creation and environments.last_update_date

```json
{
  "date_of_creation": "STRING",
  "last_update_date": "STRING"
}
```

The `date_of_creation` field gives you the date of creation of the environment script and the `last_update_date` gives you the date at which the env script was last modified.

### environments.last_execution

```json
{
  "last_execution": {
    "name": "STRING",
    "type": "STRING",
    "status": "STRING",
    "timestamp": "STRING"
  }
}
```

The `last_execution` field gives you the details of the last execution of the environment script.

- The `name` property gives you the name of the entity that executed the env script.
- The `type` property gives you whether the entity is a `lab` or `user` or `organization`
- The `status` property gives you the status of the execution. It accepts the following values - `success` or `failed`.
- The `timestamp` property gives you the time of last execution as an RFC3339-formatted timestamp. 

### environments.compatible_playbooks

```json
"compatible_playbooks": [
  {
    "name": "STRING",
    "version": ["STRING"]
  }
]

The `compatible_playbooks` field gives you the list of playbooks than can be executed inside this environment.

- The `name` property gives you the name of the playbook.
- The `version` is a list of compatible versions of the playbook.

```