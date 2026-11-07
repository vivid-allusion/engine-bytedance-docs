---
title: "Common parameters"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Common_parameters"
---

This section describes the request parameters and response parameters required for each interface.

<span id="e930eff9"></span>
## Request URL parameters


|**Parameters** |**Type** |**Required** |**Description** |
|---|---|---|---|
|Action |String |Yes |Actions to execute, such as calling DescribeInstances to query created Message Queue for RabbitMQ instances. |
|Version |String |Yes |The API version to use; the version for Message Queue for RabbitMQ V2 API is 2022\-01\-01. |
|X\-Expires |Integer |No |Signature valid time in seconds, default is 900. |


<span id="db6ee461"></span>
## Request header parameters


|**Parameters** |**Type** |**Required** |**Description** |
|---|---|---|---|
|Content\-Type |String |Yes |Specifies the structured format of the request body. The Content\-Type for Message Queue for RabbitMQ is fixed as `application/json`. |
|Host |String |Yes |That is, the service address endpoint. The service address for Message Queue for RabbitMQ is fixed as `rabbitmq.xxxapi.com`. When connecting, Message Queue for RabbitMQ defaults to accessing the nearest region based on the user's location. You can also specify the region for access in `Authorization`. |
|X\-Date |String |Yes |This is the date and time you sent the request. Specifying the date in the request helps prevent third parties from intercepting and resubmitting your request later. The date uses ISO8601 Basic format and is specified in the X\-Date header as YYYYMMDD'T'HHMMSS'Z'. |
|Authorization |String |Yes |HTTP standard authentication header field. Format: `HMAC-SHA256 Credential={AccessKeyId}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}`. |


The Authorization field description is as follows.


|**Parameters** |**type** |**Required** |**Description** |
|---|---|---|---|
|AccessKeyId |String |Yes |The key ID used to access the service, called Access Key ID. |
|ShortDate |String |Yes |UTC short time for the request service, accurate to the day. Format: `YYYYMMDD`, e.g., `20180201`. |
|Region |String |Yes |Service region ID for access, for example `cn-beijing`. For the list of regions supported by Message Queue for RabbitMQ, see [service address copy](https://docs.byteplus.com/en/docs/rabbitmq/Service_address). |
|Service |String |Yes |the name of the accessed service; the service name for Message Queue for RabbitMQ is `rabbitmq`. |
|SignedHeaders |String |Yes |Headers involved in the signature, separated by semicolons. For example, `x-date`. |
|Signature |String |Yes |The calculated signature result string. For how to calculate the signature, see [signature mechanism copy](https://docs.byteplus.com/en/docs/rabbitmq/Signature_method). |
