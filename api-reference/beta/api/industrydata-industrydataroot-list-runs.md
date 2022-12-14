---
title: "List industryDataRuns"
description: "Get a list of the industryDataRun objects and their properties."
author: "mlafleur"
ms.localizationpriority: medium
ms.prod: "industrydata"
doc_type: apiPageType
---

# List industryDataRuns

Namespace: microsoft.graph.industryData

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

Get a list of the [industryDataRun](../resources/industrydata-industrydatarun.md) objects and their properties.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

| Permission type                        | Permissions (from least to most privileged)                 |
| :------------------------------------- | :---------------------------------------------------------- |
| Delegated (work or school account)     | EduAdministration.Read, EduAdministration.ReadWrite         |
| Delegated (personal Microsoft account) | Not supported.                                              |
| Application                            | EduAdministration.Read.All, EduAdministration.ReadWrite.All |

## HTTP request

<!-- {
  "blockType": "ignored"
}
-->

```http
GET /external/industryData/runs
```

## Optional query parameters

This method supports some of the OData query parameters to help customize the response. For general information, see [OData query parameters](/graph/query-parameters).

## Request headers

| Name          | Description               |
| :------------ | :------------------------ |
| Authorization | Bearer {token}. Required. |

## Request body

Do not supply a request body for this method.

## Response

If successful, this method returns a `200 OK` response code and a collection of [industryDataRun](../resources/industrydata-industrydatarun.md) objects in the response body.

## Examples

### Request

The following is an example of a request.

<!-- {
  "blockType": "request",
  "name": "list_industrydatarun"
}
-->

```http
GET https://graph.microsoft.com/beta/external/industryData/runs
```

### Response

The following is an example of the response.

> **Note:** The response object shown here might be shortened for readability.

<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "Collection(microsoft.graph.industryData.industryDataRun)"
}
-->

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "value": [
    {
      "@odata.type": "#microsoft.graph.industryData.industryDataRun",
      "id": "918d4a8f-599b-4f6a-b409-e892855db534",
      "displayName": "Run 2023-11-01 11:10 UTC",
      "endDateTime": null,
      "startDateTime": "2023-11-01T11:10:46.924769Z",
      "status": "running"
    },
    {
      "@odata.type": "#microsoft.graph.industryData.industryDataRun",
      "id": "c7625e5d-5765-4f64-a286-5f5b845b38e1",
      "displayName": "Run 2023-10-01 21:10 UTC",
      "endDateTime": "2023-10-01T23:00:26.012Z",
      "startDateTime": "2023-10-01T21:10:46.924769Z",
      "status": "completed"
    }
  ]
}
```
