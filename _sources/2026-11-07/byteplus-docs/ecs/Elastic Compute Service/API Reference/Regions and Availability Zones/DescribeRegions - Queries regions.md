---
title: "DescribeRegions - Queries regions"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeRegions"
---

Call the DescribeRegions operation to query region information.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeRegions&groupName=%E5%9C%B0%E5%9F%9F&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|7i14YS">必选</span> `Sample value: DescribeRegions`

The action that you want to perform. Value: DescribeRegions.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|ZOVJLg">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**MaxResults** <span data-label="purple">integer</span> `Optional` `Sample value: 10`

The number of entries returned on each page in a pagination query.


* Maximum value: 20

* Minimum value: 1

* Default value: 10



**NextToken** <span data-label="purple">string</span> `Optional` `Sample value: --`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the `NextToken` parameter to the value returned by the previous API call.



**RegionIds.N** <span data-label="purple">string[]</span> `Optional` `Sample value: RegionIds.1=cn-beijing`

The region ID. Up to 20 region IDs are supported.


* Argument \- N: specifies the serial number of the region ID.

* Separate multiple region IDs with &.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**NextToken** <span data-label="purple">string</span> `Sample value: bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******`

The query credentials value returned by this call. If null is returned, this page is the last page.



**Regions** <span data-label="purple">object[]</span> `Sample value: --`

The information about the regions that meet the conditions.


**RegionId** <span data-label="purple">string</span> `Sample value: cn-beijing`

The region ID.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeRegions&Version=2020-04-01 HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202106111445100102252431000052****",
        "Action": "DescribeRegions",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "NextToken": "eWJwMHd3MzE2dmVwMjkyMnk******",
        "Regions": [
            {
                "RegionId": "cn-beijing"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |LimitExceeded.MaximumRegionIds |The number of specified RegionIds exceeds the maximum limit. |The number of specified region IDs exceeds the upper limit. |
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|429 |FlowLimitExceeded |You've reached the limit on request rate of resources. |Request rate of resources exceeds the limit. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
