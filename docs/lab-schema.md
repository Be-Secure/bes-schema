---
layout: page
title: Lab Info
permalink: /lab-info/
nav_order: 9
---

# Bes Lab Info & Status

**Version 0.1.0 (Jan 25, 2024)**

Original authors:
- Vinod Panicker (@panickervinod)
- Harimohan Rajamohanan (@harimohanr)
- Arun Suresh (@asa1997 )

# Purpose

This document gives you information on open source security lab dedicated to fortifying open source projects against potential vulnerabilities for any given organisation.
This format is stable, but further backwards compatible changes may still be made.
Feedback from maintainers of other vulnerability databases and security response teams
is most welcome. Please feel free to create an [issue in this repo](https://github.com/Be-Secure/bes-schema/issues/new).

# Format Overview

The format is a JSON-based encoding format, using the following informal schema.
The exact details of each field are elaborated in the next section. All 'STRING's
contain UTF-8 text.

```json
{
  "schema_version": "STRING",
  "name": "STRING",
  "version": {
    "tag": "STRING",
    "release_date": "STRING"
  },
  "description": "STRING",
  "owner":{
    "name": "STRING",
    "type": "STRING"
  },
  "date_of_creation": "STRING",
  "modified_date": "STRING",
  "size": "STRING",
  "instances": [
    {
        "id": "STRING",
        "name": "STRING",
        "type": "STRING",
        "description": "STRING"
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
the data was exported with. This can help consumer applications
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

The `name` field gives you the name of the lab.

## version

```json
{
  "version": {
      "tag": "STRING",
      "release_date": "STRING"
  }
}
```

The `version` field is a dictionary which gives you the details of version of the lab. The `tag` field is a string which gives you the release tag. The `release_date` field gives you the date of the release.

## description

```json
{
  "description": "STRING"
}
```

The `description` field contains the detailed description of what the lab is about.

## owner

```json
{
  "owner": {
      "name": "STRING",
      "type": "STRING"
  }
}
```

The `owner` field is a dictionary which gives you the details of the entity that owns the lab.

- The `name` field gives you the name of the entity that owns the lab.
- The `type` field gives you the type of entity. It can take the following values - `user` or `organization`.


## date_of_creation

```json
{
  "date_of_creation": "STRING"
}
```

The `date_of_creation` field gives the time the entry should be considered to have been published, as an RFC3339-formatted time stamp.


## modified_date

```json
{
  "modified_date": "STRING"
}
```

The `modified_date` field gives the time the entry was last modified, as an RFC3339-formatted timestamp.

## size

```json
{
  "size": "STRING"
}
```

The `size` field gives you the total size of the lab in standarad metrics (KB, MB, ...).

## instances

```json
{
  "instances": [
    {
        "id": "STRING",
        "name": "STRING",
        "type": "STRING",
        "description": "STRING"
    }
  ]
}
```

The `instances` field is a json array which gives you the details of the instances of the lab. Each entry contains,

- `id`: The id of the instance.
- `name`: The name of the instance.
- `type`: Type of the instance. Eg:- `virtual machine` or `container`.
- `description`: Description about the instance.





