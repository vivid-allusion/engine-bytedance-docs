---
title: "CreateHpcCluster - Creates HPC clusters"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/CreateHpcCluster"
---

Call the CreateHpcCluster operation to create an HPC cluster. You can use the HPC cluster feature to logically isolate HPC\-optimized instances. [Learn more](https://docs.byteplus.com/en/docs/gpu/HPC-cluster-overview).

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=CreateHpcCluster&groupName=%E9%AB%98%E6%80%A7%E8%83%BD%E8%AE%A1%E7%AE%97%E9%9B%86%E7%BE%A4&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|u6lxpP">必选</span> `Sample value: CreateHpcCluster`

The action that you want to perform. Value: CreateHpcCluster.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|m0OvM8">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**ClientToken** <span data-label="purple">string</span> `Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. The client can automatically generate a token, but you need to ensure that it is unique across requests. This prevents duplicate operations caused by multiple retries when the API request times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**Description** <span data-label="purple">string</span> `Optional` `Sample value: HPC cluster for testing.`

The HPC cluster description. Default value: empty string.


* Start with a letter or a Chinese character only.

* Only Chinese, letters, numbers, underscores and hyphens are allowed.

* The length limit is 0 to 255 characters.



**Name** <span data-label="purple">string</span> <span data-api-tag="require|GXKaDL">必选</span> `Sample value: hpcCluster-01`

The name of the HPC cluster.


* Start with a letter or a Chinese character only.

* Only Chinese, letters, numbers, underscores and hyphens are allowed.

* The length limit is 1 to 128 characters.



**ProjectName** <span data-label="purple">string</span> `Optional` `Sample value: project_a`

The project to which the resource belongs. A resource can only belong to one project.


* Only letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* The length is limited to 64 characters.



**Tags.N.Key** <span data-label="purple">string[]</span> <span data-api-tag="require|8PPNvO">必选</span> `Sample value: Tags.1.Key=k1&Tags.2.Key=k2`

The tag key of the user tag.


* Argument \- N: specifies the serial number of the tag key. Valid range: 1–20.

* Separate multiple keys with ampersands (&).

   Naming rules:

* It cannot start with `volc:` or `sys:` in any case form.

* It can contain only language characters, digits, spaces, and English symbols of " _", ".", ":", "/", "=", "+", "\-", and "@".

* It must be 1 to 128 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Keys of the same resource must be unique.</div>




**Tags.N.Value** <span data-label="purple">string[]</span> `Optional` `Sample value: Tags.1.Value=v1&Tags.2.Value=v2`

The tag value of the user tag.


* Argument \- N: specifies the serial number of the tag value. Valid range: 1–20.

* Separate multiple tag values with ampersands (&).

   Naming rules:

* Only language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@" are allowed.

* It must be 0 to 256 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in <code>Tags.N.Key</code> first.</div>




**ZoneId** <span data-label="purple">string</span> <span data-api-tag="require|suAIGF">必选</span> `Sample value: cn-beijing-a`

The ID of the availability zone where the HPC cluster is deployed.

You can call the [DescribeZones](https://docs.byteplus.com/en/docs/ecs/DescribeZones) operation to query the availability zones in the same region.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**HpcClusterId** <span data-label="purple">string</span> `Sample value: hpcCluster-ybowdcxqb1f80nqm****`

The HPC cluster ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=CreateHpcCluster&Version=2020-04-01&ZoneId=cn-beijing-a&Name=hpcCluster-01 HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20220518172504010212035216204B****",
        "Action": "CreateHpcCluster",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "HpcClusterId": "hpcCluster-ybowdcxqb1f80nqm****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidHpcClusterDescription.Malformed |The specified HpcClusterDescription is malformed. |The specified HPC cluster description is invalid. |
|400 |InvalidHpcClusterName.Malformed |The specified HpcClusterName is malformed. |The specified HPC cluster name is invalid. |
|400 |MissingParameter.HpcClusterName |The required parameter HpcClusterName is not supplied. |The name of the HPC cluster cannot be empty. |
|400 |MissingParameter.HpcClusterZoneId |The required parameter HpcClusterZoneId is not supplied. |The ID of the availability zone where the HPC cluster is deployed cannot be empty. |
|404 |InvalidZone.NotFound |The specified zone does not exist. |The specified availability zone does not exist. |
