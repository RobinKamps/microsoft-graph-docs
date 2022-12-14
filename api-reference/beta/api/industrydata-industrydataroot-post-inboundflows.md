---
title: "Create inboundFlow"
description: "Create a new inboundFlow object."
author: "mlafleur"
ms.localizationpriority: medium
ms.prod: "industrydata"
doc_type: apiPageType
---

# Create inboundFlow

Namespace: microsoft.graph.industryData

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

Create a new [inboundFlow](../resources/industrydata-inboundflow.md) object.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

| Permission type                        | Permissions (from least to most privileged)                               |
| :------------------------------------- | :------------------------------------------------------------------------ |
| Delegated (work or school account)     | IndustryData-InboundFlow.Read.All, IndustryData-InboundFlow.ReadWrite.All |
| Delegated (personal Microsoft account) | Not supported.                                                            |
| Application                            | IndustryData-InboundFlow.Read.All, IndustryData-InboundFlow.ReadWrite.All |

## HTTP request

<!-- {
  "blockType": "ignored"
}
-->

```http
POST /external/industryData/inboundFlows
```

## Request headers

| Name          | Description                 |
| :------------ | :-------------------------- |
| Authorization | Bearer {token}. Required.   |
| Content-Type  | application/json. Required. |

## Request body

In the request body, supply a JSON representation of the [inboundFlow](../resources/industrydata-inboundflow.md) object.

You can specify the following properties when you create an **inboundFlow**.

| Property           | Type           | Description                                                                                                                                                                                                                                          |
| :----------------- | :------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| dataDomain         | inboundDomain  | The broad category of data that is being imported by this flow. The possible values are: `educationRostering`, `unknownFutureValue`. Required.                                                                                                       |
| displayName        | String         | The name of the process. Inherited from [industryDataActivity](../resources/industrydata-industrydataactivity.md). Required.                                                                                                                         |
| effectiveDateTime  | DateTimeOffset | The start of the time window when the flow is allowed to run. The Timestamp type represents date and time information using ISO 8601 format and is always in UTC time. For example, midnight UTC on Jan 1, 2014 is `2014-01-01T00:00:00Z`. Required. |
| expirationDateTime | DateTimeOffset | The end of the time window when the flow is allowed to run. The Timestamp type represents date and time information using ISO 8601 format and is always in UTC time. For example, midnight UTC on Jan 1, 2014 is `2014-01-01T00:00:00Z`. Optional.   |

## Response

If successful, this method returns a `201 Created` response code and an [inboundFlow](../resources/industrydata-inboundflow.md) object in the response body.

## Examples

### Request

The following is an example of a request.

<!-- {
  "blockType": "request",
  "name": "create_inboundflow_from_"
}
-->

```http
POST https://graph.microsoft.com/beta/external/industryData/inboundFlows
Content-Type: application/json
Content-length: 246

{
  "@odata.type": "#microsoft.graph.industryData.inboundFileFlow",
  "dataDomain": "educationRostering",
  "displayName": "Inbound rostering flow",
  "effectiveDateTime": "2023-03-12T16:40:46.924769+05:30",
  "expirationDateTime": "2023-03-13T16:40:46.924769+05:30",
  "year@odata.bind": "https://graph.microsoft.com/beta/external/industryData/years/ebf18762-ab92-487e-21d1-08daddab28bb",
  "dataConnector@odata.bind": "https://graph.microsoft.com/beta/external/industryData/dataConnectors/51dca0a0-85f6-4478-f526-08daddab2271"
}
```

### Response

The following is an example of the response.

> **Note:** The response object shown here might be shortened for readability.

<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.industryData.inboundFlow"
}
-->

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
    "@odata.type": "#microsoft.graph.industryData.inboundFileFlow",
    "id": "7bd62d17-8c37-4494-f68d-08daddab2911",
    "displayName": "Inbound rostering fow",
    "readinessStatus": "ready",
    "dataDomain": "educationRostering",
    "effectiveDateTime": "2023-03-12T11:10:46.924769Z",
    "expirationDateTime": "2023-03-13T11:10:46.924769Z"
}
```
