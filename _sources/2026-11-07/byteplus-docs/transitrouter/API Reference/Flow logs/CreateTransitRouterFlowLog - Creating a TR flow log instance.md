---
title: "CreateTransitRouterFlowLog - Creating a TR flow log instance"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterFlowLog"
---

Call the CreateTransitRouterFlowLog API to create a Transit Router (TR) flow log.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

In a request parameter such as Tags.N.a, the "N" represents the sequence number of a tag entry. It must be assigned a value in strict numerical order, starting from 1 up to 50. Separate multiple tags with ampersands (&). Each tag key pairs with one tag value.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Exceeding quotas for log projects and log topics in Torch Log Service (TLS) may cause inability to create TR flow logs. For quota details, see [Apply for resource quota](https://docs.byteplus.com/en/docs/tls/Apply_for_resource_quota).

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateTransitRouterFlowLog&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|8R12I8">必选</span> `Example: CreateTransitRouterFlowLog`

The interface name. The current API name is `CreateTransitRouterFlowLog`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|DhZqOF">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterFlowLogName ** <span data-label="purple"> String </span>`optional` `Example: tr-fl-name`

Name of the flow log.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters in length.

* If you do not provide this parameter or leave it unset, it defaults to the ID of the flow log.



**ResourceType ** <span data-label="purple"> String </span><span data-api-tag="require|uBfM75">必选</span> `Example: PeerAttachment`

Type of the resource associated with the flow log


* PeerAttachment: Inter\-region attachment.



**ResourceId ** <span data-label="purple">String </span><span data-api-tag="require|aahce5">必选</span>`Example: tr-attach-aa1etq182fdt****`

ID of the resource associated with the flow log



**Description ** <span data-label="purple"> String </span>`optional` `Example: test`

Description of the flow log.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas ( ， ), and Chinese periods ( 。 ).

* Must be 0 to 255 characters.

* If you do not provide this parameter or leave it unset, it defaults to an empty string.



**LogFormatString ** <span data-label="purple"> String  </span>`optional` `Example: ${srcaddr}${dstaddr}${srcport}${dstport}${protocol}${bytes}`

Log fields recorded by the flow log. Default: ${srcaddr}${dstaddr}${srcport}${dstport}${protocol}${bytes}${tr\-id}${src\-region\-id}${dst\-region\-id}${attachment\-id}${packets}${start}${end}${packets\-lost\-no\-route}${packets\-lost\-blackhole}${direction}.

Among them, ${srcaddr}${dstaddr}${srcport}${dstport}${protocol}${bytes} are 6 required fields, which must be included when customizing log fields.



**TlsProjectName ** <span data-label="purple"> String  </span><span data-api-tag="require|LFoRo8">必选</span> `Example: tls-project`

Name of the flow log project.


* Must be 3 to 64 characters.

* May include Chinese characters, lowercase letters, numbers, underscores (_) and hyphens (\-).

* Must not start or end with an underscore (_) or hyphen (\-).

* Must not start with reserved fields, such as `tls_`, `tos_`, `tls-`, or `volc_`.



**TlsTopicName ** <span data-label="purple"> String </span><span data-api-tag="require|ZkathH">必选</span> `Example: tls-topic`

Name of the flow log topic.


* Must be 3 to 64 characters.

* May include Chinese characters, lowercase letters, numbers, underscores (_) and hyphens (\-).

* Must not start or end with an underscore (_) or hyphen (\-).

* Must not start with reserved fields, such as `tls_`, `tos_`, `tls-`, or `volc_`.



**AggregationInterval ** <span data-label="purple"> Integer </span>`optional` `Example: 1`

The collection period of flow logs. It is also the cycle at which TR aggregates log data and reports data to TLS. Allows 1 and 10 (default), measured in minutes.



**ClientToken ** <span data-label="purple"> String </span>`optional` `Example: test-123`

Client Token is used to ensure the request idempotency.


* This parameter value is auto\-generated by the client. Ensure uniqueness across requests, preventing duplicate actions caused by multiple client retries during API timeouts or server internal errors.

* Must not exceed 64 ASCII characters.

* If you do not set this parameter, idempotency check is not performed.



**Tags.N.Key ** <span data-label="purple"> String </span>`optional` `Example: k1`

The key of the custom tag.


* Must be 1 to 128 characters.

* Case\-sensitive. Must not start with `volc:` or `sys:` in any case form.

* Must not start or end with a space.

* May include letters, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), and at signs (@).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Duplicate tag keys are not allowed for the same resource.</div>


* <div data-tips="true" data-tips-type="default">If you do not provide this parameter or leave it unset, it defaults to empty.</div>




**Tags.N.Value ** <span data-label="purple"> String </span>`optional` `Example: v1`

The value of the custom tag.


* Must be 0 to 255 characters.

* Case\-sensitive. Must not start or end with a space.

* May include letters, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), minus signs (\-) and at signs (@).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To provide this parameter, provide Tags.N.Key first.</div>




**TransitRouterId ** <span data-label="purple"> String  </span><span data-api-tag="require|wuXLiX">必选</span> `Example: tr-7qthudw0ll6jmc****`

The ID of the Transit Router (TR) instance. You can call [DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) to obtain the ID of the TR instance.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TransitRouterFlowLogId ** <span data-label="purple"> String  </span>`Example: tr-fl-12agba4521****`

ID of the flow log instance.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=CreateTransitRouterFlowLog&Version=2020-04-01&ResourceType=PeerAttachment&ResourceId=tr-attach-aa1etq182fdt****&TlsProjectName=tls-project&TlsTopicName=tls-topic&TransitRouterId=tr-7qthudw0ll6jmc**** HTTP/1.1 
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250731T093343Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250731/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
  "ResponseMetadata": {
    "RequestId": "20250731173345117221159091A8EA51",
    "Action": "CreateTransitRouterFlowLog",
    "Version": "2020-04-01",
    "Service": "transitrouter",
    "Region": "cn-beijing"
  },
  "Result": {
    "TransitRouterFlowLogId": "tr-fl-12agba4521****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format specified for the description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.TooLong |The specified description is malformed. Ensure the maximum length of description is 255. |The format specified for the description is invalid. A description must not exceed 255 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the length should be 3 to 64. |The format of the specified name is invalid. A name must be 3 to 63 characters in length. |
|400 |InvalidName.TooLong |The specified name is malformed. Ensure the maximum length of name is 128. |The format specified for the name is invalid. A name must not exceed 128 characters in length. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format specified for the CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidResourceType.Malformed |The specified parameter resource type is invalid. |The resource type is invalid. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format of the specified tag is invalid |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |InvalidTransitRouter.InterRegionFlowLogNotSupported |The specified Transit Router does not support the inter region flow log feature. |The specified TR instance does not support cross\-region flow logs. |
|400 |InvalidTransitRouter.InvalidStatus |The specified Transit Router is not in the correct status for the request. |The specified Transit Router (TR) is in a status that cannot respond to the request. |
|400 |InvalidTransitRouterAttachment.InvalidStatus |The specified Transit Router Attachment is not in the correct status for the request. |The specified network instance attachment is in a status that cannot respond to the request. |
|400 |InvalidTransitRouterFlowLog.AggregationIntervalMalformed |The specified aggregation interval is malformed. |The specified flow log collection period is invalid. |
|400 |InvalidTransitRouterFlowLog.LogFieldNotSupport |There are log filed strings that are not supported. |The field specified in the log format is not supported. |
|400 |InvalidTransitRouterFlowLog.LogFormatMalformed |The specified log format is malformed, and its format is ${field1}${field2}${fieldn} |The format of the specified log string format is invalid. A valid format must be ${field1}${field2}${fieldn}. |
|400 |InvalidTransitRouterFlowLog.RequiredFieldMissing |The required log field string is missing. |The log format does not contain required fields. |
|400 |InvalidTransitRouterFlowLog.ServicePolicyNotAuthorized |The service policy for Transit Router Access TLS has not been authorized. |The TR in the current account is not authorized to access TLS. |
|400 |InvalidTransitRouterFlowLog.TLSNotSupport |TLS service in this region is not supported for this account. |TLS is not supported for the current account in this region. |
|400 |InvalidTransitRouterFlowLog.TLSProjectExists |The specified TLS project name already exists. |The specified log project name exists and cannot be created. |
|400 |InvalidTransitRouterFlowLog.TLSProjectInUse |The specified TLS project already has been used by another service. |The specified log project is already used by another service. |
|400 |InvalidTransitRouterFlowLog.TLSTopicExists |The specified TLS topic name already exists. |The specified log topic name exists and cannot be created. |
|400 |InvalidTransitRouterFlowLog.TLSTopicInUse |The specified TLS topic already has been used by another service. |The specified log topic is already used by another service. |
|400 |InvalidTransitRouterFlowLog.TransitRouterMismatch |The specified peer attachment does not belong to specified Transit Router. |The specified inter\-region attachment does not belong to the specified TR. |
|400 |LimitExceeded.TLSProject |You've reached the limit on the number of TLS projects per region that you can create. |You have reached the maximum TLS log projects that you can create in a single region under the current account. |
|400 |LimitExceeded.TLSTopic |You've reached the limit on the number of TLS topics per project that you can create. |You have reached the maximum number of topics that you can create under a single TLS log project for the current account. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at a time. |You have reached the maximum of tags that can be processed in a single request. |
|403 |Forbidden.CreateTransitRouterFlowLog |You are not authorized to create Transit Router flow log. |No permission to create any flow logs. |
|403 |InvalidTransitRouterFlowLog.TLSAccessDenied |TLS service has not been enabled for this account. |The current account has not activated the TLS. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidTransitRouter.NotFound |The specified Transit Router does not exist. |The specified Transit Router (TR) does not exist. |
|404 |InvalidTransitRouterAttachment.NotFound |The specified Transit Router attachment does not exist. |The specified network instance attachment does not exist. |
|409 |InvalidTransitRouterFlowLog.ResourceDuplicateConfigured |The specified resource has already been configured with a flow log. |The specified network instance is configured with a flow log instance. Duplicate configuration is not permitted. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
