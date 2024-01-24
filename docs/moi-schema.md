---
layout: page
title: Models Of Interest
permalink: /models-of-interest/
nav_order: 4
---


# Open Source Models of Interest (OSMoI)

**Version 0.2.0 (Jan 24, 2024)**

Original authors:
- Arun Suresh

This document defines a standard way of describing the essential information of each model under the Models of Interest(MOI).
This format is stable, but further backwards compatible changes may still be made.
Feedback from maintainers of other vulnerability databases and security response teams
is most welcome. Please feel free to create an [issue in this repo](https://github.com/Be-Secure/bes-schema/issues/new).

# Format Overview

The format is a JSON-based encoding format, using the following informal schema.
The exact details of each field are elaborated in the next section. All 'STRING's
contain UTF-8 text.

```json
{
    "schema_version": "0.2.0",
    "models": [
        {
            "id": "NUMBER",
            "issue_url": "STRING",
            "type": "STRING",
            "name": "STRING",
            "organization": "STRING",
            "description": "STRING",
            "created_date": "STRING",
            "model_url": "STRING",
            "data_url": "STRING",
            "label_url": "STRING",
            "modality": "STRING; STRING",
            "size": "STRING",
            "dependencies": ["STRING"],
            "training_time": "STRING",
            "quality_control": ["STRING"],
            "access": "STRING",
            "license": "STRING",
        }
    ]
}
```

# Field Details

## id

```json
{
    "id": "STRING"
}
```

The field contains the tracking id of the model under BeS.

## issue_url

```json
{
    "issue_url": "STRING"
}
```

The url to the track reequest raised.

## type

```json
{
    "type": "STRING"
}
```

The type of the model - Classic or LLM.

## name

```json
{
    "name": "STRING"
}
```

Name of the model.

## organization

```json
{
    "organization": "STRING"
}
```

The name of the organisation that developed and published the model.

## description

```json
{
    "description": "STRING"
}
```

Description of the model.

## created_date

```json
{
    "created_date": "STRING"
}
```

The date at which the model was created.

## model_url

```json
{
    "model_url": "STRING"
}
```

The url to the model binary.

## data_url

```json
{
    "data_url": "STRING"
}
```

The url to the data that is used to train the model.

## label_url

```json
{
    "label_url": "STRING"
}
```

The url to the labels of the dataset used for training.

## modality

```json
{
    "modality": "STRING"
}
```

The field contains the type of the model input and type of the model output.

## size

```json
{
    "size": "STRING"
}
```

The size of the trainable weights.

## dependencies

```json
{
    "dependencies": ["STRING"]
}
```
The list of dependencies of the model.

## training_time

```json
{
    "training_time": "STRING"
}
```

The time it took for the model to complete training.

## quality_control

```json
{
    "quality_control": ["STRING"]
}
```

List of quality controls done on the model - assessments/fuzz test.

## access

```json
{
    "access": "STRING"
}
```

Whether the model accessibility is open/close.

## license

```json
{
    "license": "STRING"
}
```

License of the model.