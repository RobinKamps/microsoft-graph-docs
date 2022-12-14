---
title: "Overview"
description: "Overview of industryData API."
author: "mlafleur"
ms.localizationpriority: medium
ms.prod: "industrydata"
doc_type: conceptual
---

# Working with IndustryData APIs in Microsoft Graph

Namespace: microsoft.graph.industryData

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

IndustryData APIs power [Microsoft School Data Sync](https://sds.microsoft.com) (SDS) platform to help automate the process of importing and synchronizing organizations, users and users associations, and groups with Azure AD and Office 365 from Student Information Systems (SIS) / Student Management Systems (SMS).

Additionally IndustryData provides resources that you can use to retrieve statistics, after data is processed, and assist with monitoring and troubleshooting.

## Overview

The system is an ETL (Extract-Transform-Load) engine. It can be visualized as a bow-tie represented by multiple incoming and outgoing flows. A single transformation process will combine and normalize the imported data to land in the tenants Data Lake.

![industryData overview](../../../concepts/images/industryData-overview-1.png)

First, you'll need to connect to your institution's data. You'll define an Inbound flow: Create **sourceSystemDefinition**, **dataConnector**, and **yearTimePeriodDefinition**. By default, your inbound flow will activate twice (2x) daily (called a Run).

When the Run starts, it will connect to the Inbound flow's **sourceSystemDefinition**, **dataConnector** and perform basic validation. Basic validation ensures that the connection is correct, for OneRoster API as a source, or the filenames and headers are correct for CSV as a source.

Next, the system will transform the data for import in preparation for advanced validation. As part of the data transformation, the data is associated based on the configured **yearTimePeriodDefinition**.

Additionally, the system will also store an updated copy of the tenant's Azure AD into the Data Lake. The copy of Azure AD assists with user matching between the **sourceSystemDefinition** and Azure AD user object. At this stage, the match link is written only to the Data Lake.

Next, the Inbound flow will perform advanced validation to determine  data health. Validation focuses on identifying errors and/or warnings. Validation follows the concept of bringing in good data and keeping out bad data.

- Errors mean that a record didn't pass validation and was removed from further processing.
- Warnings mean that the value on an optional field of a record didn't pass. The value was removed from the record, however, the record was included for further processing.

Errors and warnings will be used to help you better understand data health.

For the data that passed validation, the process uses the configured **yearTimePeriodDefinition** to determine its association for longitudinal storage.

- When the data is stored in our internal representation in the tenants Data Lake, it will identify when it was first seen by _industryData_.
- For data linked with user org, role association, and group association, it's also identified as active in session based on the **yearTimePeriodDefinition**.
- In future runs, for the same Inbound flow, **sourceSystemDefinition**, and **yearTimePeriodDefinition**, _industryData_ will identify if the record is still seen.
- Based on the presence or absence of record, the record will be kept active or be marked as no longer active in session for the configured **yearTimePeriodDefinition**. This process determines the historical and longitudinal nature of the data between days, months and years.

At the end of each Run, **industryDataRunStatistics** are available to determine data health.

- Error and warnings **industryDataRunStatistics** will be produced to help provide an initial understanding of data health.
 <!-- - When investigating data health, _industryData_ provides ability to download a log file that contains information based on the errors and warnings found to begin the data investigation process to correct the data in the source system.

After investigating and addressing any data errors and/or warnings, or are comfortable with the current state of the data health, then you can enable the scenarios with the data that is now in the Education data lake. When enabling a scenario to use this data, the scenario will create an outbound flow. Outbound flows are defined by Microsoft 365 provisioning, Insights & Analytics.

Microsoft 365 Provisioning outbound flows help with simplifying management of users and classes. Only active and matched users are included in the data that will be used to write the link to the AAD user object between the SIS/ SMS and their sections for groups and Teams classrooms.

Insights & Analytics help provide analysis for student progress and activity within their classes. Guided by this data, educators have the information they need to ensure that their students' emotional, social, and academic needs are being met. -->

For more information, see [Microsoft School Data Sync, pre-requisites, and core concepts](/schooldatasync/school-data-sync-overview.md) on the platform and architecture.

## Registration, Permissions, and Authorization

IndustryData APIs can be integrated with 3rd party apps. To enable this integration, we recommend taking time to review the following articles.

- [Explore the basics documentation](/graph/auth/auth-concepts.md)
- [Learn how to add and register an application](/graph/auth-register-app-v2.md)
- [Read and write resources on behalf of a user](/graph/auth-v2-user.md)
- [Permissions via a consent process](/graph/permissions-reference.md)
- [Steps to resolve common errors](/graph/resolve-auth-errors.md)

_We'll be expanding out scopes that are specific to IndustryData, however until then IndustryData APIs support the existing Graph permissions noted below._

| Permissions                     | Type            | Description                                                                         |
| ------------------------------- | --------------- | ----------------------------------------------------------------------------------- |
| EduAdministration.Read          | **Delegated**   | Allows the app to read education app settings on behalf of the user.                |
| EduAdministration.ReadWrite     | **Delegated**   | Allows the app to manage education app settings on behalf of the user.              |
| EduAdministration.Read.All      | **Application** | Read the state and settings of all Microsoft education apps on behalf of the user   |
| EduAdministration.ReadWrite.All | **Application** | Manage the state and settings of all Microsoft education apps on behalf of the user |

## Concepts

IndustryData APIs powers School Data Sync which is a data transformation engine. It imports data sets in from external sources (SIS / SMS), transforms the data into a common data model, and then writes the transformed data to various external services, like users and groups to Azure AD, and ability to create a team based group.

The following articles are to help with some basics that are specific to IndustryData APIs.

### Data Domain

The `dataDomain` property defines the type of data being imported and determines the common data model format it will be stored in. Today the only supported `dataDomain` is _educationRostering_.

### Reference Definitions

**referenceDefinition** represents an enumerated value. Each supported industry domain receives a distinct collection of default and customers can further customize them by overriding default values or adding new values to the tenant.
**referenceDefinition** are used extensively throughout the system, both for configuration and validating data during transformation.

Each **referenceDefinition** uses a composite identifier of `{referenceType}-{code}`. The approach provides a more natural developer experience as most code values are defined by a standards body, and will be recognizable to developers in that industry domain.

[Retrieving referenceDefinition](resources/industrydata-referencedefinition.md)

### Reference Values

When the API requires the developer to provide a **referenceDefinition**, it uses a type derived from **industryDataReferenceValue**.

The **industryDataReferenceValue** is designed to simplify selecting **[referenceDefinition](resources/industrydata-referencedefinition.md)** and to reduce developer configuration by only requiring the `code` value. The type of reference value is defined by the **industryDataReferenceValue** type, eliminating potential confusing as to which **referenceDefinition** a given property is expecting.

#### Example Usage

The `userMatchingSettings.sourceIdentifier` property takes a `industryDataIdentifierTypeReferenceValue` type. This is a `industryDataReferenceValue` type bound to a `RefIdentifierType` reference definition.

Selecting the desired `RefIdentifierType` can be done either by providing a `code` value

```json
"sourceIdentifier": {
    "code": "username"
},
```

or binding the `industryDataReferenceDefinition` entity directly.

```json
"sourceIdentifier": {
    "value@odata.bind": "external/industryData/referenceDefinitions/RefIdentifierType-username"
},
```

### Role Groups

Transformation of the data is often shaped by each individual user's role within an organization. These roles are defined as Reference Definitions. Given the number of potential roles, binding each role individual would result in a tedious user experience. [Role Groups](resources/industrydata-rolegroup.md) are simply a collection of Role values used to provide a convenient way to reference multiple reference definitions. The default role groups are _Students_ and _Staff_.

#### Get the Staff role group

```json
{
  "@odata.type": "#microsoft.graph.industryDataRoleGroup",
  "id": "37a9781b-db61-4a3c-a3c1-8cba92c9998e",
  "displayName": "Staff",
  "roles": [
    { "code": "adjunct" },
    { "code": "administrator" },
    { "code": "advisor" },
    { "code": "affiliate" },
    { "code": "aide" },
    { "code": "alumni" },
    { "code": "assistant" }
  ]
}
```

## Scenarios

### Most Common

The two most common scenarios are _Upload and Validate CSV Data_ and _Run Health and Monitoring_.

- **[Upload and Validate CSV Data](resources/industrydata-azuredatalakeconnector.md)**
- **[Run Health and Monitoring](resources/industrydata-industrydatarun.md)**

### Other Scenarios

- **[Create Inbound Flow](resources/industrydata-inboundflow.md)**
- **[Edit Inbound Flow](resources/industrydata-inboundflow.md)**
