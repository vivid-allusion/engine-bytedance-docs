---
title: "DeleteHpcCluster - Deletes HPC clusters"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DeleteHpcCluster"
---

Call the DeleteHpcCluster operation to delete an HPC cluster. HPC clusters within which ECS instances are deployed cannot be deleted.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteHpcCluster&groupName=%E9%AB%98%E6%80%A7%E8%83%BD%E8%AE%A1%E7%AE%97%E9%9B%86%E7%BE%A4&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|xw8oYT">必选</span> `Sample value: DeleteHpcCluster`

The action that you want to perform. Value: DeleteHpcCluster.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|YoJgJZ">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**ClientToken** <span data-label="purple">string</span> `Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents duplicate operations caused by multiple retries when the API request times out or an internal server error occurs. Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**HpcClusterId** <span data-label="purple">string</span> <span data-api-tag="require|0QEObO">必选</span> `Sample value: hpcCluster-ybowdcxqb1f80nqm****`

The HPC cluster ID. You can call [DescribeHpcClusters](https://docs.byteplus.com/en/docs/ecs/DescribeHpcClusters) to query the HPC cluster ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DeleteHpcCluster&Version=2020-04-01&HpcClusterId=hpcCluster-ybowdcxqb1f80nqm**** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202205181726250102121620311E4C****",
        "Action": "DeleteHpcCluster",
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


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |The request uses the same client token as a previous, but non\-identical request. Do not reuse a client token with different requests, unless the requests are identical. |The idempotent parameters are inconsistent. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken is invalid. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still being processed. Please try again later. |
