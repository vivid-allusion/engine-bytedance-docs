---
title: "Common parameters"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/common-parameters-v2"
---

This article describes the request and return parameters that each interface needs to use.

<span id="fa44cb12"></span>
## Request URL parameter


|**parameter** |**type** |**Is it required?**  |**meaning** |
|---|---|---|---|
|Action |String |Required |Operations to perform, such as calling DescribeInstances to query the created message queue Kafka Edition instance. |
|Version |String |Required |The version of the API to use, the version number of the message queue Kafka version V2 API is `2022-05-01`. |
|X\-Expires |Integer |Optional |The valid time of the signature, in seconds, the default value is 900. |


<span id="2236bcc5"></span>
## Request header parameter


|**parameter** |**type** |**Is it required?**  |**meaning** |
|---|---|---|---|
|Content\-Type |String |Required |The structured format of the request message body is specified, and the Content\-Type of the message queue Kafka version is fixed as `application/json`. |
|Host |String |Required |As a service address endpoint. The service address of the message queue Kafka version is fixed to `open.ap-southeast-1.byteplusapi.com`.<br><br>When accessing, the message queue Kafka version defaults to nearby visits according to the user's location. At the same time, you can also `Authorization` To access the specified region in. |
|X\-Date |String |Required |This is the date and time you made the request. Specifying a date in the request helps prevent third parties from intercepting your request and resubmitting it later. The date is in ISO8601 Basic format and is specified in YYYYMMDD T'HHMMSS'Z 'format via the X\-Date header. |
|Authorization |String |Required |HTTP standard authentication header field.<br><br>The format is `HMAC-SHA256 Credential={AccessKeyId}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}`. |


The Authorization field is described below.


|**parameter** |**type** |**Is it required?**  |**meaning** |
|---|---|---|---|
|AccessKeyId |String |Required |The key ID used by the access service, which is the Access Key ID. |
|ShortDate |String |Required |The short time in UTC when the service is requested, accurate to the day. format is `YYYYMMDD`, for example `20240201`. |
|Region |String |Required |The Region where the request is to be called. For example, ap\-southeast\-1. |
|Service |String |Required |The name of the service accessed, the name of the message queue Kafka version service is `kafka`. |
|SignedHeaders |String |Required |Headers participating in the signature, separated by semicolons. E.g `x-date`. |
|Signature |String |Required |The calculated signature result string. For how to calculate the signature, please refer to [Signature method](https://docs.byteplus.com/en/docs/kafka/signature-method-v2). |
