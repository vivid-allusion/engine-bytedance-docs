---
title: "DescribeSpotPriceHistory - Queries historical prices of spot instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeSpotPriceHistory"
---

Call the DescribeSpotPriceHistory operation to query the historical prices of spot instances within the past 30 days.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

For the operation process, precautions, and operation instructions of spot instances, see [Spot instance overview](https://docs.byteplus.com/en/docs/ecs/Spot_instances_overview?lang=en).

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeSpotPriceHistory&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the request parameters specific to this operation and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|Uv4vrR">必选</span> `Sample value: DescribeSpotPriceHistory`

The operation that you want to perform. Valid value: DescribeSpotPriceHistory.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|Z1NFlC">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**InstanceTypeId** <span data-label="purple">string</span> <span data-api-tag="require|R0lzHu">必选</span> `Sample value: ecs.g1ie.xlarge`

The instance type.

You can call [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) to query the instance type.



**MaxResults** <span data-label="purple">integer</span> `Optional` `Sample value: 20`

The number of entries returned on each page in a pagination query.


* Maximum value: 1000

* Minimum value: 1

* Default value: 100



**NextToken** <span data-label="purple">string</span> `Optional` `Sample value: --`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the `NextToken` parameter to the value returned by the previous API call.



**TimestampEnd** <span data-label="purple">string</span> `Optional` `Sample value: 2021-06-28T18:29:38+08:00`

The end time for querying the historical prices of spot instances. This time cannot be later than the current time, nor can it be 30 days ago or earlier.


* The default value is empty, which specifies the current time.

* Time format: `YYYY-mm-ddTHH:MM:SSZ` or `YYYY-mm-ddTHH:MM:SS+ZZ:ZZ`.



**TimestampStart** <span data-label="purple">string</span> `Optional` `Sample value: 2021-06-28T18:29:38+08:00`

The start time for querying the historical prices of spot instances. When the specified time is 30 days ago, the default start time is 30 days ago.


* The default value is empty, which specifies 3 hours before the end time.

* Time format: `YYYY-mm-ddTHH:MM:SSZ` or `YYYY-mm-ddTHH:MM:SS+ZZ:ZZ`.



**ZoneId** <span data-label="purple">string</span> `Optional` `Sample value: cn-beijing-a`

The ID of the availability zone where the instance type is located.

You can call the [DescribeZones](https://docs.byteplus.com/en/docs/ecs/DescribeZones) operation to query the availability zones in the same region.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**NextToken** <span data-label="purple">string</span> `Sample value: bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******`

The query credential returned by this call. If null is returned, this page is the last page.



**SpotPrices** <span data-label="purple">object[]</span> `Sample value: --`

The price details of spot instances.


**InstanceTypeId** <span data-label="purple">string</span> `Sample value: ecs.g1ie.xlarge`

The type of spot instances.



**SpotPrice** <span data-label="purple">float</span> `Sample value: 0.036`

The price of spot instances. Unit: USD.



**Timestamp** <span data-label="purple">string</span> `Sample value: 2021-06-28T18:29:38+08:00`

The time during which spot instances are at this price.



**ZoneId** <span data-label="purple">string</span> `Sample value: cn-beijing-a`

The availability zone ID of spot instances.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeSpotPriceHistory&Version=2020-04-01&ZoneId=cn-beijing-a&InstanceTypeId=ecs.g1ie.xlarge HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230426113431A57961174C490267****",
        "Action": "DescribeSpotPriceHistory",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing-a"
    },
    "Result": {
        "SpotPrices": [
            {
                "InstanceType": "ecs.g1ie.xlarge",
                "SpotPrice": 0.036,
                "Timestamp": "2021-06-28T18:29:38+08:00",
                "ZoneId": "cn-beijing-a"
            }
        ],
        "NextToken": "bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|400 |InvalidTimestampEnd.Malformed |The specified TimestampEnd is malformed. |The specified end time is invalid. |
|400 |InvalidTimestampStart.Malformed |The specified TimestampStart is malformed. |The specified start time is invalid. |
|400 |MissingParameter.InstanceTypeId |The required parameter InstanceTypeId is not supplied. |The ID of the instance type cannot be empty. |
|412 |InvalidTimestampStartTimestampEnd.Mismatch |The specified TimestampStart does not match TimestampEnd. |The specified StartTime and EndTime do not match. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
