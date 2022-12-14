---
title: "Get longRunningOperation"
description: "Get the status of a long-running operation, represented by a longRunningOperation object."
author: "mlafleur"
ms.localizationpriority: medium
ms.prod: "industrydata"
doc_type: apiPageType
---

# Get longRunningOperation

Namespace: microsoft.graph

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

Get the status of a long-running operation, represented by a [longRunningOperation](../resources/longrunningoperation.md) object.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

| Permission type                        | Permissions (from least to most privileged) |
| :------------------------------------- | :------------------------------------------ |
| Delegated (work or school account)     | **TODO: Provide applicable permissions.**   |
| Delegated (personal Microsoft account) | **TODO: Provide applicable permissions.**   |
| Application                            | **TODO: Provide applicable permissions.**   |

## HTTP request

<!-- {
  "blockType": "ignored"
}
-->

```http
GET /longRunningOperation
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

If successful, this method returns a `200 OK` response code and a [longRunningOperation](../resources/longrunningoperation.md) object in the response body.

## Examples

### Request

The following is an example of a request.

<!-- {
  "blockType": "request",
  "name": "get_longrunningoperation"
}
-->

```http
GET https://graph.microsoft.com/beta/longRunningOperation
```

### Response

The following is an example of the response.

> **Note:** The response object shown here might be shortened for readability.

<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.longRunningOperation"
}
-->

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "value": {
    "@odata.type": "#microsoft.graph.longRunningOperation",
    "createdDateTime": "String (timestamp)",
    "id": "5c5670d6-a2c0-a394-ef42-882954856de5",
    "lastActionDateTime": "String (timestamp)",
    "resourceLocation": "String",
    "status": "String",
    "statusDetail": "String"
  }
}
```
