---
title: "ModifyInstanceMetadataOptions - Modifies the access mode of instance metadata"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ModifyInstanceMetadataOptions"
---

Call the ModifyInstanceMetadataOptions operation to modify the access mode of instance metadata.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

When you call this operation, if you do not pass in optional parameters, the original configuration is retained.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|zw57US">必选</span> `Sample value: ModifyInstanceMetadataOptions`

The action that you want to perform. Value: ModifyInstanceMetadataOptions.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|DsEkDq">必选</span>` Sample value:2020-04-01`

The API version. Value: 2020\-04\-01.



**HttpTokens ** string <span data-label="purple"></span>`Optional` `Sample value: optional`

The access mode of instance metadata. You can set whether to enable the security hardening mode. Value:


* optional: Not mandatory (Normal Mode and Security Hardening Mode). This allows instance metadata access either directly through the standard method or via the token\-based authentication method.

* required: Mandatory (Security Hardening Mode). This only allows accessing instance metadata through a token\-based authentication method.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For information on how to view metadata and the available metadata items, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Viewing-instance-metadata">Viewing instance metadata</a>.</div>


* <div data-tips="true" data-tips-type="tip">Security Hardening Mode is currently in Beta. If you need a trial, please contact your account manager to apply.</div>




**InstanceId ** <span data-label="purple">string </span><span data-api-tag="require|PVQnNd">必选</span> `Sample value: i-3tigy72q3u3vj0x2****`

The specified instance ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=ModifyInstanceMetadataOptions&Version=2020-04-01&InstanceId=i-3tigy72q3u3vj0x2****&HttpTokens=optional HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
        "ResponseMetadata": {
                "RequestId": "20211104180426010194099035220C****",
                "Action": "ModifyInstanceMetadataOptions",
                "Version": "2020-04-01",
                "Service": "ecs",
                "Region": "cn-beijing"
        },
        "Result": {}
}

```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidHttpTokens.Malformed |The specified HttpTokens is malformed, you can use optional(default) or required. |The specified value for HttpTokens is invalid. Please use optional (default) or required. |
|400 |InvalidInstanceId.Malformed |The specified InstanceId is malformed. |The specified instance ID is invalid. |
|400 |InvalidModifyInstanceMetadataOptions.Unsupported |Modify instance metadata option is not supported. |This feature has not been enabled for your account. Please contact your account manager to apply for allowlist access. |
|400 |MissingParameter.InstanceId |The required parameter InstanceId is not supplied. |The parameter InstanceIds cannot be left empty. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified instance does not exist. |
