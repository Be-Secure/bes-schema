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
- Arun Suresh (@asa1997)
- Sudhir Verma(@sudhirverma)

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
        "version": {
          "tag": "STRING",
          "release_date": "STRING"
        },
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

### environments.owner

```json
{
  "owner": {
      "name": "STRING",
      "type": "STRING"
  }
}
```

The `owner` field is a dictionary which gives you the owner of the env script.
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
