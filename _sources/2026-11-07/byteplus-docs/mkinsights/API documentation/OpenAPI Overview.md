---
title: "OpenAPI Overview"
product: "Market Insights"
product_code: "mkinsights"
source: "https://docs.byteplus.com/en/docs/mkinsights/openapi-overview"
---

This page provides an overview of the OpenAPI endpoints currently available for BytePlus Market Insights Agent.

<span id="lvgiR1oA"></span>
## Prerequisites

Before calling a Market Insights OpenAPI endpoint:


1. Obtain an Access Key ID and Secret Access Key (AK/SK) for a BytePlus user under your tenant.

2. Make sure that the user has permission to access Market Insights.


<span id="rUhNVvbB"></span>
### API signature


|**Prerequisite** |**Description** |**Reference** |
|---|---|---|
|Access Key ID and Secret Access Key (AK/SK) |The AK/SK pair is associated with your BytePlus tenant ID and is used to call OpenAPI endpoints.<br><br>Sign in to the BytePlus console, select your profile picture in the upper\-right corner, and go to API Access Key.<br><br>For a sub\-account, also go to the IAM user permissions page and add the MktInsightFullAccess permission. |[Overview of BytePlus OpenAPI](https://docs.byteplus.com/en/docs/byteplus-platform/reference-overview-1)<br><br>[How To Calculate A Signature](https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature) |


> Before publication, confirm that MktInsightFullAccess is the correct IAM policy name, including capitalization.


**API call instructions**


1. Use the following request domain: [mkt-insight.byteplusapi.com](http://mkt-insight.byteplusapi.com/)

2. All endpoints follow the BytePlus OpenAPI specifications. Before sending a request, see [How To Calculate A Signature](https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature) to sign the request.

3. Each API page lists only endpoint\-specific parameters and selected common parameters. For complete definitions, see [Common parameters of BytePlus OpenAPI](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters) and [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


<span id="alVXjXUm"></span>
## Common conventions

Send requests using POST with Content\-Type set to application/json. Use [https://mkt-insight.byteplusapi.com/](https://mkt-insight.byteplusapi.com/) as the domain. Include Action and Version in the URL query parameters and business parameters in the JSON request body.

A successful response contains Result and ResponseMetadata. The client must check both the HTTP status and ResponseMetadata.Error, and retain RequestId for troubleshooting.


|**Common response field** |**Type** |**Description** |
|---|---|---|
|`ResponseMetadata.RequestId` |String |Unique identifier of the API request. This value is not a `ClientToken`. Retain it for troubleshooting. |
|`ResponseMetadata.Action` |String |The API action used in the request. |
|`ResponseMetadata.Version` |String |The API version used in the request. |
|`ResponseMetadata.Service` |String |The service identifier returned by the API gateway. |
|`ResponseMetadata.Region` |String |The region returned by the API gateway. |
|`ResponseMetadata.Error` |Object |Contains Code and Message when the request fails. No error information is included when the request succeeds. |


The error codes listed on each API page are service\-specific errors. For gateway errors related to signatures, authorization, or rate limiting, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes). Example task IDs are provided only to demonstrate the protocol. Replace them with an actual task ID for the current account when calling an API.

<span id="19jLat5m"></span>
## Monitoring task APIs


|**API** |**Description** |
|---|---|
|[CreateMonitorTask](https://docs.byteplus.com/en/docs/mkinsights/CreateMonitorTask) |Creates a monitoring task. The task initially retrieves content based on the configured keywords and sources and can optionally apply relevance evaluation. |
|[UpdateMonitorTask](https://docs.byteplus.com/en/docs/mkinsights/UpdateMonitorTask) |Updates the configuration of an existing monitoring task without changing its task ID or enabled status. This endpoint uses full\-configuration replacement semantics. |
|[GetMonitorTask](https://docs.byteplus.com/en/docs/mkinsights/GetMonitorTask) |Retrieves the configuration, enabled status, creation time, and last update time of a specified monitoring task. |
|[UpdateSubsStatus](https://docs.byteplus.com/en/docs/mkinsights/UpdateSubsStatus) |Enables or pauses a specified monitoring task. Pausing a task does not delete it. |
|[DisableSubsTask](https://docs.byteplus.com/en/docs/mkinsights/DisableSubsTask) |Permanently deletes a specified monitoring task. This operation is different from pausing a task and cannot be undone. |


<span id="HGxtPCGr"></span>
## Content retrieval APIs


|**API** |**Description** |
|---|---|
|[PullPosts](https://docs.byteplus.com/en/docs/mkinsights/PullPosts) |Call the PullPosts API to retrieve posts associated with the current task by page, with optional filters for publish time, ingestion time, and relevance. |
|[Hotspot API](https://docs.byteplus.com/en/docs/mkinsights/HotspotAPIReference) |Call the Social Media Hotspot Report OpenAPI through the BytePlus TOP gateway. |
