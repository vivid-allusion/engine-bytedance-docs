---
title: "DescribeSpotAdvice - Queries the average release rate of spot instances over the past 30 days"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeSpotAdvice"
---

Call the DescribeSpotAdvice operation to query information such as the average release rate and average discount rate of spot instances over the past 30 days.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes


* For data on instance type, vCPU count, memory, and other metrics, see [Instance types](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).

* For the operation process, precautions, and operation instructions of spot instances, see [Overview of spot instance](https://docs.byteplus.com/en/docs/ecs/Spot_instances_overview).


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeSpotAdvice&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the request parameters specific to this operation and some common parameters. For more information, please refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|B77TCj">必选</span> `Sample value: DescribeSpotAdvice`

The operation that you want to perform. Valid value: DescribeSpotAdvice.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|oPMMHJ">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**Cpus** <span data-label="purple">integer</span> `Optional` `Sample value: 2`

The number of vCPUs for the instance type.

If you configure both `Cpus` and `MinCpus`, `Cpus` takes effect.



**Gpu.Count** <span data-label="purple">integer</span> `Optional` `Sample value: 2`

The number of GPUs for each GPU instance. For valid values, see [GPU instance types](https://docs.byteplus.com/en/docs/gpu/Instances).



**Gpu.ProductName** <span data-label="purple">string</span> `Optional` `Sample value: Tesla A100`

The type of the GPU computing card.


* Valid values: For detailed information on GPU computing cards of each instance, see [GPU instance types](https://docs.byteplus.com/en/docs/gpu/Instances).

* Default value: None (that is, all types will be queried).

* When a non\-existent GPU computing card type is passed in, the return value is empty.



**InstanceTypeFamily** <span data-label="purple">string</span> `Optional` `Sample value: ecs.g2i`

The instance type family.



**InstanceTypeIds.N** <span data-label="purple">string[]</span> `Optional` `Sample value: InstanceTypeIds.1=ecs.r2a.xlarge&InstanceTypeIds.2=ecs.g2a.xlarge`

Instance type.


* Parameter \- N: This specifies the serial number of the instance type. Valid value: 1–10.

* Multiple instance types are separated by &.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you configure both <code>InstanceTypeFamily</code> and <code>InstanceTypeIds.N</code>, <code>InstanceTypeIds.N</code> takes effect.</div>




**MaxResults** <span data-label="purple">integer</span> `Optional` `Sample value: 100`

The number of entries returned on each page in a pagination query.


* Maximum value: 1000

* Minimum value: 1

* Default value: 100



**MemorySize** <span data-label="purple">integer</span> `Optional` `Sample value: 32768`

The memory size of the instance type. Unit: MiB.

If you configure both `MemorySize` and `MinMemorySize`, `MemorySize` takes effect.



**MinCpus** <span data-label="purple">integer</span> `Optional` `Sample value: 2`

The minimum number of vCPUs for the instance type.


* You can configure this parameter to perform a fuzzy query. For example, if you set `MinCpus` to 2, spot instances with two or more vCPUs in this availability zone are queried.

* If you configure both `Cpus` and `MinCpus`, `Cpus` takes effect.



**MinMemorySize** <span data-label="purple">integer</span> `Optional` `Sample value: 32768`

The minimum memory size of the instance type. Unit: MiB.


* You can configure this parameter to perform a fuzzy query. For example, if you set `MinMemorySize` to 8, spot instances with memory capacity greater than or equal to 8 MiB in this availability zone are queried.

* If you configure both `MemorySize` and `MinMemorySize`, `MemorySize` takes effect.



**NextToken** <span data-label="purple">string</span> `Optional` `Sample value: --`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the `NextToken` parameter to the value returned by the previous API call.



**ZoneId** <span data-label="purple">string</span> `Optional` `Sample value: cn-beijing-a`

The availability zone ID of the instance type.

You can call the [DescribeZones](https://docs.byteplus.com/en/docs/ecs/DescribeZones) operation to query the availability zones in the same region.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The table below lists only the response parameters specific to this operation. For more information, refer to [esponse structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)[esponse structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**AvailableSpotResources** <span data-label="purple">object[]</span> `Sample value: --`

The array consisting of information such as the release rate and discount rate of spot instances over the past 30 days.


**AverageSpotDiscount** <span data-label="purple">integer</span> `Sample value: 20`

The discount rate of the average price of spot instances in the past 30 days compared to the price of pay\-as\-you\-go instances. Unit: %


* Possible values: 1–100

* You can calculate the average price of spot instances based on this value. For example, if the price of a pay\-as\-you\-go instance is 1 and the return value is 40 (that is, 40%), then the average price of spot instances over the past 30 days is 0.4.



**InstanceType** <span data-label="purple">string</span> `Sample value: ecs.g2i.large`

Instance type



**InterruptionRate** <span data-label="purple">integer</span> `Sample value: 0`

The average release rate of spot instances over the past 30 days. Unit: %



**InterruptionRateRange** <span data-label="purple">string</span> `Sample value: 0-3%`

The range of the average release rate of spot instances over the past 30 days, corresponding to the return value of `InterruptionRate`. Possible values:


* 0\-3%

* 3\-5%

* 5\-10%

* 10\-100%



**ZoneId** <span data-label="purple">string</span> `Sample value: cn-beijing-a`

The ID of the availability zone where the instance is located.




**NextToken** <span data-label="purple">string</span> `Sample value: bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******`

The query credentials value returned by this call. If null is returned, this page is the last page.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeSpotAdvice&Version=2020-04-01&ZoneId=cn-beijing-a&InstanceTypeIds.1=ecs.r2a.xlarge HTTP/1.1
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
        "Action": "DescribeSpotAdvice",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing-a"
    },
    "Result": {
        "AvailableSpotResources": [
            {
                "AverageSpotDiscount": 40,
                "InstanceType": "ecs.r2a.xlarge",
                "InterruptionRateRange": "0-3%",
                "InterruptionRate": 0,
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
|400 |LimitExceeded.MaximumInstanceTypeIds |You've reached the limit on the number of InstanceTypeIds that you can set. |The specified number of InstanceTypeIds exceeds the maximum limit. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
