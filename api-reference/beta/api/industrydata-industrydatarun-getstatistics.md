---
title: "industryDataRun: getStatistics"
description: "Calculate statistics for a run group."
author: "mlafleur"
ms.localizationpriority: medium
ms.prod: "industrydata"
doc_type: apiPageType
---

# industryDataRun: getStatistics

Namespace: microsoft.graph.industryData

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

Calculate statistics for a run group.

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
GET /external/industryData/runs/{industryDataRunId}/getStatistics
```

## Request headers

| Name          | Description               |
| :------------ | :------------------------ |
| Authorization | Bearer {token}. Required. |

## Request body

Do not supply a request body for this method.

## Response

If successful, this function returns a `200 OK` response code and an [industryDataRunStatistics](../resources/industrydata-industrydatarunstatistics.md) in the response body.

## Examples

### Request

The following is an example of a request.

<!-- {
  "blockType": "request",
  "name": "industrydatarunthis.getstatistics"
}
-->

```http
GET https://graph.microsoft.com/beta/external/industryData/runs/918d4a8f-599b-4f6a-b409-e892855db534/getStatistics
```

### Response

The following is an example of the response.

> **Note:** The response object shown here might be shortened for readability.

<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.industryData.industryDataRunStatistics"
}
-->

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "@odata.type": "#microsoft.graph.industryData.industryDataRunStatistics",
  "activityStatistics": [
    {
      "count": "154390",
      "role": "student"
    },
    {
      "count": "59820",
      "role": "teacher"
    }
  ],
  "inboundTotals": {
    "errors": "0",
    "groups": "565987",
    "matchedPeopleByRole": [
      {
        "count": "154390",
        "role": "student"
      },
      {
        "count": "59820",
        "role": "teacher"
      }
    ],
    "memberships": "1235120",
    "organizations": "16",
    "people": "278473",
    "unmatchedPeopleByRole": [],
    "warnings": "0"
  },
  "runId": "918d4a8f-599b-4f6a-b409-e892855db534",
  "status": "completed"
}
```
