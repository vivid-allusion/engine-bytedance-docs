---
title: "QPS limits on API calls"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-qps-limits-on-api-calls"
---

To prevent service disruptions from API throttling, you must adhere to the queries per second (QPS) limits for your account. This document lists the specific QPS limits for each BytePlus VOD API operation, helping you manage your API call frequency effectively and ensure application stability.

The QPS limit per account for an API operation indicates the maximum number of times that a BytePlus account and its associated IAM users can invoke the API operation per second. For example, the QPS limit per account for the `ApplyUploadInfo` operation is set at 150. If you have a BytePlus account with five IAM users linked to it, and all six entities attempt to simultaneously call the `ApplyUploadInfo` operation, the total number of calls per second must not exceed 150.

> **注意**

* > Not all API operations are subject to QPS limits. The tables below list the API operations that do have QPS limits.

* > Pay attention to the units specified in the tables. The default unit is times per second, with other units like times per minute explicitly mentioned if used.

* > The QPS limits outlined in this article may fluctuate based on the region, actual call volume, and concurrent calls. The actual QPS limit enforced by the service takes precedence.

|API |QPS limit per account |
|---|---|
|[ApplyUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/applyuploadinfo) |150 |
|[CommitUploadInfo](https://docs.byteplus.com/byteplus-vod/reference/commituploadinfo) |150 |
|[UploadMediaByUrl](https://docs.byteplus.com/byteplus-vod/reference/uploadmediabyurl) |100 |
|[QueryUploadTaskInfo](https://docs.byteplus.com/byteplus-vod/reference/queryuploadtaskinfo) |200 |
|[GetMediaInfos](https://docs.byteplus.com/en/byteplus-vod/reference/getmediainfos) |200 |
|[UpdateMediaInfo](https://docs.byteplus.com/en/byteplus-vod/reference/updatemediainfo) |30 |
|[UpdateMediaPublishStatus](https://docs.byteplus.com/en/byteplus-vod/reference/updatemediapublishstatus) |50 |
|[GetPlayInfo](https://docs.byteplus.com/en/byteplus-vod/reference/getplayinfo) |1500 |
|[StartExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution) |50 |
|[GetExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-getexecution) |50 |
