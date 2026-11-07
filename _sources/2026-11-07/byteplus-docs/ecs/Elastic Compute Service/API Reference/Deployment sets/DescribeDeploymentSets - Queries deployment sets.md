---
title: "DescribeDeploymentSets - Queries deployment sets"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeDeploymentSets"
---

Call the DescribeDeploymentSets operation to query deployment set attributes.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeDeploymentSets&groupName=%E9%83%A8%E7%BD%B2%E9%9B%86&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|25CmUH">必选</span> `Sample value: DescribeDeploymentSets`

The action that you want to perform. Value: DescribeDeploymentSets.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|ogUnJK">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**DeploymentSetIds.N** <span data-label="purple">string[]</span> `Optional` `Sample value: DeploymentSetIds.1=dps-yc1o9aahks5m57nk****&DeploymentSetIds.2=dps-ybr1vulgy87grbt6****`

The ID of the deployment set.

You can call [DescribeDeploymentSets](https://docs.byteplus.com/en/docs/ecs/DescribeDeploymentSets) to query deployment set IDs.


* Argument \- N: specifies the serial number of the deployment set. Valid range: 1\-100.

* Separate multiple deployment set IDs with &.



**DeploymentSetName** <span data-label="purple">string</span> `Optional` `Sample value: testDeploymentSet`

The name of the deployment set.


* Cannot start with a number, a hyphen (\-), or an underscore (_).

* Only Chinese, letters, numbers, underscores and hyphens are allowed.

* The length limit is 1 to 128 characters.



**Granularity** <span data-label="purple">string</span> `Optional` `Sample value: host`

The deployment granularity. Valid values:


* host: physical machine

* rack: rack

* switch: switch



**MaxResults** <span data-label="purple">integer</span> `Optional` `Sample value: 10`

The number of entries returned on each page in a pagination query.


* Maximum value: 100

* Default value: 10



**NextToken** <span data-label="purple">string</span> `Optional` `Sample value: --`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the `NextToken` parameter to the value returned by the previous API call.



**Strategy** <span data-label="purple">string</span> `Optional` `Sample value: Availability`

The deployment policy. Valid values:


* Availability: Availability policy.

* AvailabilityGroup: Availability Group policy.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**DeploymentSets** <span data-label="purple">object[]</span> `Sample value: --`

The details of the deployment set.


**Capacities** <span data-label="purple">object[]</span> `Sample value: --`

The capacity information of the deployment set at the availability zone dimension. This parameter is returned only when one or more ECS instances are deployed within the deployment set.


**AvailableCount** <span data-label="purple">integer</span> `Sample value: 3`

The number of ECS instances in the availability zone that can be deployed within the deployment set.



**UsedCount** <span data-label="purple">integer</span> `Sample value: 2`

The number of ECS instances in the deployment set that belong to the availability zone.



**ZoneId** <span data-label="purple">string</span> `Sample value: cn-beijing-a`

Availability zone ID. Only the ID of the availability zone of an ECS instance deployed within the deployment set is returned.




**CreatedAt** <span data-label="purple">string</span> `Sample value: 2021-06-28T18:29:38+08:00`

The creation time of the deployment set.



**DeploymentSetDescription** <span data-label="purple">string</span> `Sample value: Deployment set for disaster recovery`

The description of the deployment set.



**DeploymentSetId** <span data-label="purple">string</span> `Sample value: dps-yc34mry3yifvojpmz3s3`

The ID of the deployment set.



**DeploymentSetName** <span data-label="purple">string</span> `Sample value: testDeploymentSetName`

The name of the deployment set.



**Granularity** <span data-label="purple">string</span> `Sample value: host`

The deployment granularity.



**GroupCount** <span data-label="purple">integer</span> `Sample value: 3`

The number of deployment set groups.

This parameter is returned only when the value of `Strategy` is `AvailabilityGroup`.



**InstanceAmount** <span data-label="purple">integer</span> `Sample value: 1`

The number of ECS instances in the deployment set.



**InstanceIds** <span data-label="purple">string[]</span> `Sample value: ["i-3tigy72q3u3vj0x2****","i-3tigy72q3u3vj0x2****"]`

The ID list of ECS instances in the deployment set.



**Strategy** <span data-label="purple">string</span> `Sample value: Availability`

The deployment policy.




**NextToken** <span data-label="purple">string</span> `Sample value: bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******`

The pagination token returned by this call. If this value is empty, the current page is the last page.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeDeploymentSets&Version=2020-04-01&DeploymentSetIds.1=dps-yc1o9aahks5m57nk**** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2021110417394001022514606307*****",
        "Action": "DescribeDeploymentSets",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "DeploymentSets": [
            {
                "CreatedAt": "2021-11-25T15:12:58+08:00",
                "DeploymentSetDescription": "",
                "DeploymentSetId": "dps-yc1o9aahks5m57nk****",
                "DeploymentSetName": "testDeploymentSet",
                "Strategy": "Availability",
                "Granularity": "host",
                "InstanceAmount": 1,
                "InstanceIds": [
                i-3tigy72q3u3vj0x2****
                ],
                "Capacities": [
                    {
                        "ZoneId": "cn-beijing-a",
                        "UsedCount": 1,
                        "AvailableCount": 4
                    }
                ]
            }
        ],
        "NextToken":"bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|400 |LimitExceeded.MaximumDeploymentSetIds |You've reached the limit on the number of DeploymentSetIds that you can set. |The number of specified deployment sets exceeds the upper limit. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
