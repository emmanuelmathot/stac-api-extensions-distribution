# STAC API - Distribution Extension Specification


- [STAC API - Distribution Extension Specification](#stac-api---distribution-extension-specification)
  - [Overview](#overview)
  - [Link Relations](#link-relations)
  - [Endpoints](#endpoints)
  - [Example](#example)

## Overview

- **Title:** Distribution
- **OpenAPI specification:** [openapi.yaml](openapi.yaml)
- **Conformance Classes:**
  - <https://api.stacspec.org/v1.0.0/distribution>
- **Scope:** STAC API - Core
- **[Extension Maturity Classification](https://github.com/radiantearth/stac-api-spec/tree/v1.0.0/README.md#maturity-classification):** Proposal
- **Dependencies**:
  - [STAC API - Core](https://github.com/radiantearth/stac-api-spec/tree/v1.0.0/core)
- **Owner**: @emmanuelmathot

A STAC API Landing Page (a Catalog) can return information about the Catalog and Collection child objects
it contains using the link relation `distribution` to an endpoint `/distrib`.

The purpose of this endpoint is to present information about the distribution of the software serving the STAC API.

## Link Relations

This conformance class also requires implementation of the link relations in the
[STAC API - Core](https://github.com/radiantearth/stac-api-spec/tree/v1.0.0/core) conformance class.

The following Link relations must exist in the Landing Page (root).

| **rel**        | **href**   | **From**                | **Description**                                            |
| -------------- | ---------- | ----------------------- | ---------------------------------------------------------- |
| `distribution` | `/distrib` | STAC API - Distribution | STAC API Software Distribution information of this catalog |

The following Link relations must exist in the `/distrib` endpoint response.

| **rel** | **href**   | **From**                | **Description** |
| ------- | ---------- | ----------------------- | --------------- |
| `root`  | `/`        | STAC Core               | The root URI    |
| `self`  | `/distrib` | STAC API - Distribution | Self reference  |

## Endpoints

This conformance class also requires for the endpoints in the
[STAC API - Core](https://github.com/radiantearth/stac-api-spec/tree/v1.0.0/core) conformance class to be implemented.

| Endpoint   | Returns | Description                                                |
| ---------- | ------- | ---------------------------------------------------------- |
| `/distrib` | JSON    | STAC API Software Distribution information of this catalog |

STAC APIs implementing the *STAC API - Distribution* conformance class must support HTTP GET operation at
`/distrib`, with the return JSON document consisting of a root object `distribution` with
the folowing fields:

| Field Name  | Type   | Description                                                              |
| ----------- | ------ | ------------------------------------------------------------------------ |
| id          | string | **REQUIRED** A unique identifier for this STAC API software distribution |
| name        | string | A human-readable title for this STAC API software distribution           |
| description | string | A description of this STAC API software distribution                     |
| version     | string | The version of the STAC API software distribution                        |
| license     | string | The license of the STAC API software distribution                        |
| links       | array  | **REQUIRED** An array of links to other resources                        |

more fields can be added to the response object, such as an inline change log, or a list of contributors.

## Example

Below is a minimal example, but captures the essence.

The `/distrib` endpoint response object should look as follows:

```json
{
  "id": "super-stac-api-server-1.0",
  "name": "Super STAC API Server 1.0",
  "description": "A super STAC API server that implements the STAC API specification",
  "version": "1.0.0",
  "license": "Apache-2.0",
  "links": [
    {
      "rel": "root",
      "type": "application/json",
      "href": "https://stac-api.example.com"
    },
    {
      "rel": "self",
      "type": "application/json",
      "href": "https://stac-api.example.com/distrib"
    }
  ]
}
```
