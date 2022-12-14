---
title: "Update industryDataConnector"
description: "Update the properties of an industryDataConnector object."
author: "mlafleur"
ms.localizationpriority: medium
ms.prod: "industrydata"
doc_type: apiPageType
---

# Update industryDataConnector

Namespace: microsoft.graph.industryData

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

Update the properties of an [industryDataConnector](../resources/industrydata-industrydataconnector.md) object.

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
PATCH /external/industryData/dataConnectors/{industryDataConnectorId}
PATCH /external/industryData/inboundFlows/{inboundFlowId}/dataConnector
```

## Request headers

| Name          | Description                 |
| :------------ | :-------------------------- |
| Authorization | Bearer {token}. Required.   |
| Content-Type  | application/json. Required. |

## Request body

[!INCLUDE [table-intro](../../includes/update-property-table-intro.md)]

| Property    | Type   | Description                               |
| :---------- | :----- | :---------------------------------------- |
| displayName | String | The name of the data connector. Required. |

## Response

If successful, this method returns a `200 OK` response code and an updated [industryDataConnector](../resources/industrydata-industrydataconnector.md) object in the response body.

## Examples

### Request

The following is an example of a request.

<!-- {
  "blockType": "request",
  "name": "update_industrydataconnector"
}
-->

```http
PATCH https://graph.microsoft.com/beta/external/industryData/dataConnectors/{industryDataConnectorId}
Content-Type: application/json
Content-length: 104

{
  "@odata.type": "#microsoft.graph.industryData.industryDataConnector",
  "displayName": "String"
}
```

### Response

The following is an example of the response.

> **Note:** The response object shown here might be shortened for readability.

<!-- {
  "blockType": "response",
  "truncated": true
}
-->

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "@odata.type": "#microsoft.graph.industryData.industryDataConnector",
  "displayName": "String"
}
```
