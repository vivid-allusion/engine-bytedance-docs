---
title: "DescribeUserData - Queries instance custom data"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeUserData"
---

Call the DescribeUserData operation to query the custom data of an ECS instance.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes


* The returned custom data of the instance is in Base64\-encoded format.

* If no custom data is specified for the instance, an empty value is returned.

* For information about how to configure custom data for an instance, see [Configuring custom data](https://docs.byteplus.com/en/docs/ecs/Configuring-custom-data).


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeUserData&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|hl9xM6">必选</span> `Sample value: DescribeUserData`

The operation that you want to perform. Valid value: DescribeUserData.



**Version**<span data-label="purple"> string</span><span data-api-tag="require|PgkkBw">必选</span>  `Sample value: 2020-04-01`

The API version. Value: 2020\-04\-01.



**ScheduledInstanceId ** <span data-label="purple">string </span>`Optional` `Sample value: esi-ycvye5a380l8j1ld****`

ESI order ID.



**InstanceId ** <span data-label="purple">string </span><span data-api-tag="require|b1gp6T">必选</span> `Sample value: i-l8j0j2jynelea7nu****`

The ID of the instance that you want to query.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InstanceId ** <span data-label="purple">string </span>`Sample value: i-l8j0j2jynelea7nu****`

The instance ID.



**ScheduledInstanceId ** <span data-label="purple">string </span>`Sample value: esi-ycvye5a380l8j1ld****`

ESI order ID.



**UserData ** <span data-label="purple">string </span>`Sample value: IyEvYmluL2Jhc2gKdG91Y2ggL3RtcC91c2VyZG******`

The custom data of the instance.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeUserData&Version=2020-04-01&InstanceId=i-l8j0j2jynelea7nu**** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2021110417394001022514606307D7****",
        "Action": "DescribeUserData",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result":{
        "InstanceId":"i-l8j0j2jynelea7nu****",
        "UserData":"IyEvYmluL2Jhc2gKdG91Y2ggL3RtcC91c2VyZG******"
      }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.InstanceId |The required parameter InstanceId is not supplied. |The instance ID cannot be left empty. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified instance does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
