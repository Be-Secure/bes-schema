---
layout: page
title: Models Of Interest
permalink: /models-of-interest/
nav_order: 4
---


# Open Source Models of Interest (OSMoI)

**Version 0.1.0 (Jan 25, 2024)**

Original authors:

- Vinod Panicker ([@panickervinod](https://github.com/panickervinod))
- Harimohan Rajamohanan ([@harimohanr](https://github.com/harimohanr))
- Arun Suresh ([@asa1997](https://github.com/asa1997))
- Sudhir Verma([@sudhirverma](https://github.com/sudhirverma))

# Purpose

This document outlines a standardized data interchange format for open source software models of interest (OSSMoI) within organizations. The OSSMoI encompasses essential model details such as model **id**, model **name**, model **type**, **owner** information, **parent** information, **modality** information, **size** information. These details facilitate seamless sharing among peers within the organization and publication to the BeSLighthouse community dashboard. Open Source models can be onbaorded into BeSLab by BLIman utility.

This standardized data interchange format not only streamlines the sharing and publication process of open source software models within organizations but also significantly reduces the time required for BeSLabs to assess models of interest. By providing a structured framework for exchanging essential model details, BeSLabs can expedite their assessment procedures and evaluation of open source models.

This format is stable, but further backwards compatible changes may still be made. Please feel free to create an [issue in this repo](https://github.com/Be-Secure/bes-schema/issues/new).

# Format Overview

The format is a JSON-based encoding format, using the following informal schema.
The exact details of each field are elaborated in the next section. All 'STRING's
contain UTF-8 text.

A sample json for your understanding is available
[here](../example/moi-report-schema-sample.json).

```json
{
    "schema_version": "0.1.0",
    "models": [
        {
            "id": "NUMBER",
            "issue_url": "STRING",
            "type": "STRING",
            "name": "STRING",
            "description": "STRING",
            "created_date": "STRING",
            "model_url": "STRING",
            "dataset_url": "STRING",
            "label_url": "STRING",
            "parent": {
              "name": "STRING",
              "type": "STRING",
              "url": "STRING"
            },
            "owner": {
              "name": "STRING",
              "type": "STRING"
            },
            "modality": {
                "input_type": "STRING",
                "output_type": "STRING"
            },
            "size": "STRING",
            "dependencies": ["STRING"],
            "license": "STRING",
        }
    ]
}
```

# Field Details

## models.id

```json
{
    "id": "STRING"
}
```

The field contains the tracking id of the model under BeS.

## models.issue_url

```json
{
    "issue_url": "STRING"
}
```

The url to the track reequest raised.

## models.type

```json
{
    "type": "STRING"
}
```

The type of the model - Classic or LLM.

## models.name

```json
{
    "name": "STRING"
}
```

Name of the model.

## models.description

```json
{
    "description": "STRING"
}
```

Description of the model.

## models.created_date

```json
{
    "created_date": "STRING"
}
```

The date at which the model was added to moi.

## models.model_url

```json
{
    "model_url": "STRING"
}
```

The url to the model binary.

## models.dataset_url

```json
{
    "dataset_url": "STRING"
}
```

The url to the dataset that is used to train the model.

## models.label_url

```json
{
    "label_url": "STRING"
}
```

The url to the labels of the dataset used for training.

## models.parent

```json
{
  "parent": {
            "name": "STRING",
            "type": "STRING",
        }
}
```

The details of the parent organization of the model are given here.

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
       Name of the parent of the model
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

## models.owner

```json
{
  "owner": {
        "name": "STRING",
        "type": "STRING"
      }
}
```

Details of the current owner of the model.

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
       Name of the owner of the model
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

## models.modality

```json
{
    "modality": {
        "input_type": "STRING",
        "output_type": "STRING"
    }
}
```

The field contains the type of the model input and type of the model output.

## models.size

```json
{
    "size": "STRING"
}
```

The size of the trainable weights.

## models.dependencies

```json
{
    "dependencies": ["STRING"]
}
```
The list of dependencies of the model.

## license

```json
{
    "license": "STRING"
}
```

License of the model.