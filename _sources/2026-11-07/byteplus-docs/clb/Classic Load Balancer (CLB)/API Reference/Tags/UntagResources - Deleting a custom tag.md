---
title: "UntagResources - Deleting a custom tag"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/UntagResources"
---

Call the UntagResources API to delete custom tags from a resource

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=UntagResources&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|UpKOna">必选</span> `Example: UntagResources`

Action to execute. Set the value to **UntagResources**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|wJyxY9">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**ResourceType ** <span data-label="purple">String </span><span data-api-tag="require|eSeaV1">必选</span> `Example: clb`

The resource type. Values:


* clb: CLB instance.

* listener

* servergroup: Backend server group.

* acl: Access control.

* certificate



**ResourceIds.N ** <span data-label="purple">String </span><span data-api-tag="require|vqRgud">必选</span> `Example: clb-273sdsdsxxxxxp8u2j****`

The resource ID.


* Parameter \- N: Represents the serial number of a resource ID. A maximum of 50 IDs can be specified per single API call.

* Separate multiple resource IDs with ampersands (&).

* You can call the following API to obtain the resource ID:

   * [DescribeLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancers)

   * [DescribeListeners](https://docs.byteplus.com/en/docs/clb/DescribeListeners)

   * [DescribeServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeServerGroups)

   * [DescribeAcls](https://docs.byteplus.com/en/docs/clb/DescribeAcls)

   * [DescribeCertificates](https://docs.byteplus.com/en/docs/clb/DescribeCertificates)



**TagKeys.N ** <span data-label="purple">String </span><span data-api-tag="require|uZPLRt">必选</span> `Example: k1`

The key of the custom tag to be deleted. Must not start or end with a space.


* Parameter \- N: Represents the serial number of a tag key. A maximum of 50 IDs can be specified per single API call.

* Separate multiple tag keys with ampersands (&).

> If the specified `TagKeys.N` does not exist or are already unbound, the operation returns success by default without reporting an error.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2021062415303301022514515207C4****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=UntagResources&Version=2020-04-01&ResourceType=clb&ResourceIds.1=clb-273sdsdsxxxxxp8u2j****&TagKeys.1=k1
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UntagResources",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidResourceType.Malformed |The specified ResourceType is malformed. |The specified ResourceType format is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey parameter format is invalid. |
|400 |LimitExceeded.Resource |You've reached the limit on the number of resources that you can operate at a time. |You have reached the maximum number of tags that can be processed in a single request. |
|400 |LimitExceeded.TagOperation |You've reached the limit on the number of tags that you can operate at a time. |You have reached the maximum number of tag entries that can be operated on in a single request. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ResourceType'. |This request is missing a required parameter. Please ensure your request includes all required parameters, such as ResourceType. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ResourceIds'. |This request is missing a required parameter. Please ensure your request includes all required parameters, such as ResourceIds. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'TagKeys'. |This request is missing a required parameter. Please ensure your request includes all required parameters, such as TagKeys. |
|403 |InvalidResourceType.ServcieManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
