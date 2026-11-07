---
title: "CreateDirectConnectHealthCheck - Creating a health check for Direct Connect"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectHealthCheck"
---

Call the CreateDirectConnectHealthCheck API to create a health check instance.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Each health check instance supports specifying only one subnet as the monitoring source. The source IP is randomly allocated within the specified subnet and cannot be specified manually. For more about quota limits, see [Limits](https://docs.byteplus.com/en/docs/directconnect/Limits#.6YWN6aKd6ZmQ5Yi2).

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDirectConnectHealthCheck&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|ayxY6b">必选</span> `Example: CreateDirectConnectHealthCheck`

The interface name. The current API name is `CreateDirectConnectHealthCheck`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|mIFcyh">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectHealthCheckName ** <span data-label="purple">String </span>`optional` `Example: dchc-01`

The name of the health check instance.


* Must be 1 to 128 characters.

* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-). Must not start with http:// or https://.

* If you do not provide this parameter or leave it empty, it defaults to the health check instance ID.



**Description ** <span data-label="purple">String </span>`optional` `Example: This is a healthcheck`

The description of the health check instance.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If you do not provide this parameter or leave it unset, it defaults to an empty string.



**Region ** <span data-label="purple">String </span><span data-api-tag="require|tlnvtr">必选</span> `Example: ap-southeast-1`

The region where the health check is located. Provide the region of the probe source. It must be the same as the region of the Virtual Private Cloud (VPC).



**VpcId ** <span data-label="purple">String </span><span data-api-tag="require|zy62tk">必选</span> `Example: vpc-01`

The VPC where the health check instance is located. Provide the VPC where the target monitoring source IP is located.



**SubnetId ** <span data-label="purple">String </span><span data-api-tag="require|PUR4iH">必选</span> `Example: subnet-01`

The subnet where the target monitoring source IP is located.



**ClientToken ** <span data-label="purple">String </span>`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.


* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**DirectConnectHealthCheckId ** <span data-label="purple">String </span>`Example: dhc-2752hz4tek****`

The ID of the health check instance.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=CreateDirectConnectHealthCheck&Version=2020-04-01&Region=ap-southeast-1&VpcId=vpc-01&SubnetId=subnet-01 HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "CreateDirectConnectHealthCheck",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****",
        "DirectConnectHealthCheckId": "dhc-2752hz4tek****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDirectConnectHealthCheck.SubnetAZNotSupported |The specified subnet does not support direct connect health check. |The specified subnet does not support health checks. |
|400 |InvalidDirectConnectHealthCheck.ClusterUnavailable |No available health check cluster. |No available health check clusters exist. |
|400 |InvalidDirectConnectHealthCheck.SubnetConflictWithVpc |The specified subnet does not belong to the specified VPC. |The specified subnet does not belong to the specified VPC. |
|400 |InvalidDirectConnectHealthCheck.SubnetNoAvailableIp |The specified subnet does not have available IP addresses. |The specified subnet contains no available IP addresses. |
|400 |InvalidDirectConnectHealthCheck.VpcConflictWithAccount |The specified VPC does not belong to the specified account. |The specified VPC does not belong to the specified account. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|400 |QuotaExceeded.DirectConnectHealthCheck |You've reached the limit on the number of direct connect health check that you can create. |The maximum health checks that you can create have been reached. |
|404 |InvalidDirectConnectHealthCheck.SecurityGroupNotFound |The specified security group does not exist. |The specified security group does not exist. |
|404 |InvalidDirectConnectHealthCheck.SubnetNotFound |The specified subnet does not exist. |The specified subnet does not exist. |
|404 |InvalidDirectConnectHealthCheck.VpcNotFound |The specified VPC does not exist. |The specified Virtual Private Cloud (VPC) does not exist. |
|404 |InvalidDirectConnectHealthCheckCluster.NotFound |The specified direct connect direct connect health check cluster does not exist. |The specified health check cluster does not exist. |
