---
layout: page
title: Vulnerabilities Of Interest
permalink: /vulnerabilities-of-interest/
nav_order: 3
---

# Open Source Software Vulnerabilities of Interest ( OSSVoI )

**Version 0.1.0 (Jan 30, 2024)**

Original authors:
- Vinod Panicker (@panickervinod)
- Harimohan Rajamohanan (@harimohanr)
- Arun Suresh (@asa1997 )

# Purpose

This document defines the data interchange format for open source vulnerabilities of interest (VOI) for any given organisation . An organization powered by BeSLab shall publish their OSSVoI to its peers as well the community dashboard BeSLighthouse.
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
  "vulnerabilities": [
    {
      "id": "STRING",
      "summary": "STRING",
      "description": "STRING",
      "aliases": [
        "STRING"
      ],
      "cwe": "STRING",
      "published_date": "STRING",
      "modified_date": "STRING",
      "fix_available": "STRING",
      "severity": {
        "type": "STRING",
        "score": "NUMBER"
      },
      "exploitable": "STRING",
      "affected_projects": [
        {
          "id": "NUMBER",
          "name": "STRING",
          "range": {
            "introduced": "STRING",
            "fixed": "STRING"
          },
          "versions": [
            "STRING"
          ]
        }
      ],
      "references": [
        {
          "type": "STRING",
          "url": "STRING"
        }
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

## vulnerabilities

A list which contains the details of the vulnerabilities of interest for an organization/lab.

### vulnerabilities.id

```json
{
  "id": "STRING"
}
```
The id field is a unique identifier for the vulnerability entry. It is a string of the format `<DB>-<ENTRYID>`, where `DB` names the database and `ENTRYID` is in the format used by the database. For example: “OSV-2020-111”, “CVE-2021-3114”, or “GHSA-vp9c-fpxx-744v”.

### vulnerabilities.summary

```json
{
  "summary": "STRING"
}
```

The summary field gives a one-line, English textual summary of the vulnerability. It is recommended that this field be kept short, on the order of no more than 120 characters.

### vulnerabilities.description

```json
{
  "description": "STRING"
}
```

The detailed description of the vulnerability. 

### vulnerabilities.aliases

```json
{
    "aliases": [
        "STRING"
    ]
}
```

The `aliases` field gives a list of IDs of the same vulnerability in other databases, in the form of the `id` field. This allows one database to claim that its own entry describes the same vulnerability as one or more entries in other databases.

Two vulnerabilities can be described as aliases if a potential patch that addresses one of the vulnerabilities (and no other vulnerabilities) will also address the other vulnerability, and vice versa. Aliases may be used for vulnerabilities affecting different packages or ecosystems as long as they follow this definition.

Aliases should be considered symmetric (if A is an alias of B, then B is an alias of A) and transitive (If A aliases B and B aliases C, then A aliases C).

Aliases should not be used in records that bundle many different vulnerabilities in one patch of a distribution of a package. Listing multiple vulnerabilities as aliases would mean that they are all identical (due to the symmetry/transitivity of aliases), not that one release fixes multiple (distinct) vulnerabilities.

### vulnerabilities.cwe

```json
{
  "cwe": "STRING"
}
```

The `cwe` field indicates the CWE id that corresponds to the vulnerability’s category. It follows the format `CWE-<number>` as a string.

### vulnerabilities.published_date

```json
{
  "published_date": "STRING"
}
```

The `published_date` field gives the time the entry should be considered to have been published, as an RFC3339-formatted time stamp.

### vulnerabilities.modified_date

```json
{
  "modified_date": "STRING"
}
```

The `modified_date` field gives the time the entry was last modified, as an RFC3339-formatted timestamp.


### vulnerabilities.fix_available

```json
{
  "fix_available": "STRING"
}
```
The field `fix_available` gives you whether this vulnerability as been fixed or not. It takes the following values - `Available` or `Not Available`.

### vulnerabilities.severity

```json
{
    "severity": [
        {
            "type": "STRING",
            "score": "STRING"
        }
    ]
}
```

The `severity` field is a JSON array that allows generating systems to describe the severity of a vulnerability using one or more quantitative scoring methods. Each severity item is a JSON object specifying a `type` and `score` property, described below.

The `type` property must be one of the types defined below, which describes the quantitative method used to calculate the associated `score`.

<table>
  <thead>
    <tr>
      <th>Severity Type</th>
      <th>Score Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>CVSS_V2</code></td>
      <td>A CVSS vector string representing the unique characteristics and severity of the vulnerability using a version of the <a href="https://www.first.org/cvss/v2/">Common Vulnerability Scoring System</a> notation that is == 2.0 (e.g."AV:L/AC:M/Au:N/C:N/I:P/A:C").</td>
    </tr>
    <tr>
        <td><code>CVSS_V3</code></td>
        <td>A CVSS vector string representing the unique characteristics and severity of the vulnerability using a version of the <a href="https://www.first.org/cvss/">Common Vulnerability Scoring System</a> notation that is >= 3.0 and < 4.0 (e.g."CVSS:3.1/AV:N/AC:H/PR:N/UI:N/S:C/C:H/I:N/A:N").</td>
    </tr>
    <tr>
        <td><code>CVSS_V4</code></td>
        <td>A CVSS vector string representing the unique characterictics and severity of the vulnerability using a version on the <a href="https://www.first.org/cvss/v2/">Common Vulnerability Scoring System</a> notation that is >= 4.0 and < 5.0 (e.g. "CVSS:4.0/AV:N/AC:L/AT:N/PR:H/UI:N/VC:L/VI:L/VA:N/SC:N/SI:N/SA:N").</td>
    </tr>
  </tbody>
</table>

The `score` property is a string representing the severity score based on the selected `Sverity Type`, as described above.

### vulnerabilities.exploitable

```json
{
  "exploitable": "STRING"
}
```

The field `exploitable` field tells you whether this vulnerability can be exploited. It takes the following values - `yes` or `no`.


### vulnerabilities.affected_projects

```json
{
  "affected_projects": [
          {
            "id": "NUMBER",
            "name": "STRING",
            "range": {
              "introduced": "STRING",
              "fixed": "STRING"
            },
            "versions": [
              "STRING"
            ]
          }
    ]
}
```

The `affected_projects` field gives you the projects under [Projects of Interest (PoI)](https://be-secure.github.io/BeSLighthouse/Project-Of-Interest) list that are affected by this vulnerability.


- The `id` field gives you the project's tracking id under BeS.
- The `name` field gives you the name of the project.
- THe `range` gives you the range of version affected by the vulnerability for this project.
  - The `introduced` field gives you the version of the project where the vulnerability was started.
  - The `fixed` field gives you the version of the project where the vulnerability is fixed.
- The `version` field is a json array that lists all the affected versions of the project.
  
### vulnerabilities.references

```json
{
  "references": [
    {
      "type": "STRING",
      "url": "STRING"
    }
  ]
}
```

The `references` field contains a list of JSON objects describing references. Each object has a string field `type` specifying the type of reference, and a string field `url`. The `url` is the fully-qualified URL (including the scheme, typically “https://”) linking to additional information, advisories, issue tracker entries, and so on about the vulnerability itself. The type specifies what kind of reference the URL is.

The known reference type values are:

- `ADVISORY`: A published security advisory for the vulnerability.
- `ARTICLE`: An article or blog post describing the vulnerability.
- `DETECTION`: A tool, script, scanner, or other mechanism that allows for detection of the vulnerability in production environments. e.g. YARA rules, hashes, virus signature, or other scanners.
- `DISCUSSION`: A social media discussion regarding the vulnerability, e.g. a Twitter, Mastodon, Hacker News, or Reddit thread.
- `REPORT`: A report, typically on a bug or issue tracker, of the vulnerability.
- `FIX`: A source code browser link to the fix (e.g., a GitHub commit) Note that the fix type is meant for viewing by people using web browsers. Programs interested in analyzing the exact commit range would do better to use the GIT-typed affected[].ranges entries (described above).
- `INTRODUCED`: A source code browser link to the introduction of the vulnerability (e.g., a GitHub commit) Note that the introduced type is meant for viewing by people using web browsers. Programs interested in analyzing the exact commit range would do better to use the GIT-typed affected[].ranges entries (described above).
- `PACKAGE`: A home web page for the package.
- `EVIDENCE`: A demonstration of the validity of a vulnerability claim, e.g. app.any.run replaying the exploitation of the vulnerability.
- `WEB`: A web page of some unspecified kind.


