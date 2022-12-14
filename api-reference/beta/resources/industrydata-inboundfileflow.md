---
title: "inboundFileFlow resource type"
description: "Represents a flow to import data via a set of files into the canonical store."
author: "mlafleur"
ms.localizationpriority: medium
ms.prod: "industrydata"
doc_type: resourcePageType
---

# inboundFileFlow resource type

Namespace: microsoft.graph.industryData

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

Represents a flow to import data via a set of files into the canonical store.

Inherits from [inboundFlow](industrydata-inboundflow.md).

## Methods

| Method                                                                          | Return type                                                                                | Description                                                                                            |
| :------------------------------------------------------------------------------ | :----------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------- |
| [Create inboundFlow](../api/industrydata-industrydataroot-post-inboundflows.md) | [microsoft.graph.industryData.inboundFlow](industrydata-inboundflow.md)                    | Create a new **inboundFlow** object.                                                                   |
| [List inboundFileFlows](../api/industrydata-inboundfileflow-list.md)            | [microsoft.graph.industryData.inboundFileFlow](industrydata-inboundfileflow.md) collection | Get a list of the [inboundFileFlow](industrydata-inboundfileflow.md) objects and their properties.     |
| [Get inboundFileFlow](../api/industrydata-inboundfileflow-get.md)               | [microsoft.graph.industryData.inboundFileFlow](industrydata-inboundfileflow.md)            | Read the properties and relationships of an [inboundFileFlow](industrydata-inboundfileflow.md) object. |
| [Update inboundFileFlow](../api/industrydata-inboundfileflow-update.md)         | [microsoft.graph.industryData.inboundFileFlow](industrydata-inboundfileflow.md)            | Update the properties of an [inboundFileFlow](industrydata-inboundfileflow.md) object.                 |
| [Delete inboundFileFlow](../api/industrydata-inboundfileflow-delete.md)         | None                                                                                       | Delete an [inboundFileFlow](industrydata-inboundfileflow.md) object.                                   |

## Properties

| Property           | Type            | Description                                                                                                                                                                                                                                                                                           |
| :----------------- | :-------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| dataDomain         | inboundDomain   | The broad category of data that is being imported by this flow. Inherited from [inboundFlow](industrydata-inboundflow.md). The possible values are: `educationRostering`, `unknownFutureValue`.                                                                                                       |
| displayName        | String          | The name of the activity. Inherited from [industryDataActivity](industrydata-industrydataactivity.md).                                                                                                                                                                                                |
| effectiveDateTime  | DateTimeOffset  | The start of the time window when the flow is allowed to run. The Timestamp type represents date and time information using ISO 8601 format and is always in UTC time. For example, midnight UTC on Jan 1, 2014 is `2014-01-01T00:00:00Z`. Inherited from [inboundFlow](industrydata-inboundflow.md). |
| expirationDateTime | DateTimeOffset  | The end of the time window when the flow is allowed to run. The Timestamp type represents date and time information using ISO 8601 format and is always in UTC time. For example, midnight UTC on Jan 1, 2014 is `2014-01-01T00:00:00Z`. Inherited from [inboundFlow](industrydata-inboundflow.md).   |
| readinessStatus    | readinessStatus | The state of the activity from creation through to ready to do work. Inherited from [industryDataActivity](industrydata-industrydataactivity.md). The possible values are: `notReady`, `ready`, `failed`, `disabled`, `expired`, `unknownFutureValue`.                                                |

## Relationships

| Relationship  | Type                                                                 | Description                                                                                                                                             |
| :------------ | :------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------ |
| dataConnector | [industryDataConnector](industrydata-industrydataconnector.md)       | The data connector in the context of which this flow will pull in data from a source system. Inherited from [inboundFlow](industrydata-inboundflow.md). |
| year          | [yearTimePeriodDefinition](industrydata-yeartimeperioddefinition.md) | The year that the data being brought in via this flow applies to. Inherited from [inboundFlow](industrydata-inboundflow.md).                            |

## JSON representation

The following is a JSON representation of the resource.

<!-- {
  "blockType": "resource",
  "keyProperty": "id",
  "@odata.type": "microsoft.graph.industryData.inboundFileFlow",
  "baseType": "microsoft.graph.industryData.inboundFlow",
  "openType": false
}
-->

```json
{
  "@odata.type": "#microsoft.graph.industryData.inboundFileFlow",
  "dataDomain": "String",
  "displayName": "String",
  "effectiveDateTime": "String (timestamp)",
  "expirationDateTime": "String (timestamp)",
  "readinessStatus": "String"
}
```
