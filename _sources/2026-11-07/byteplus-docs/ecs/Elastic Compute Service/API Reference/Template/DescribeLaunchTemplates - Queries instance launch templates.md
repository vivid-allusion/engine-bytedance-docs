---
title: "DescribeLaunchTemplates - Queries instance launch templates"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeLaunchTemplates"
---

Call the DescribeLaunchTemplates operation to query instance launch templates.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeLaunchTemplates&groupName=%E5%90%AF%E5%8A%A8%E6%A8%A1%E7%89%88&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|2VdwzY">必选</span> `Sample value: DescribeLaunchTemplates`

The action that you want to perform. Value: DescribeLaunchTemplates.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|AbD6eS">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**NextToken** <span data-label="purple">string</span> `Optional` `Sample value: --`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the NextToken parameter to the value returned by the previous API call.



**MaxResults** <span data-label="purple">integer</span> `Optional` `Sample value: 10`

The number of entries per page.


* Maximum value: 100

* Default value: 10



**TagFilters.N.Key** <span data-label="purple">string[]</span> `Optional` `Sample value: TagFilters.1.Key=k1&TagFilters.2.Key=k2`

The tag key of the instance launch template.



**TagFilters.N.Value.N** <span data-label="purple">string[]</span> `Optional` `Sample value: TagFilters.1.Value.1=v1&TagFilters.2.Value.1=v2`

The tag value of the instance launch template.



**LaunchTemplateNames.N** <span data-label="purple">string[]</span> `Optional` `Sample value: LaunchTemplateNames.1=testLaunchTemplateName`

The name of the instance launch template. Up to 10 names are supported.


* Argument \- N: specifies the serial number of the instance launch template.

* Separate multiple names with &.



**LaunchTemplateProjectName** <span data-label="purple">string</span> `Optional` `Sample value: default`

The project to which the instance launch template belongs.



**LaunchTemplateIds.N** <span data-label="purple">string[]</span> `Optional` `Sample value: LaunchTemplateIds.1=lt-3ti78x9h8t4bw****&LaunchTemplateIds.2=lt-ysxc16auaugh9zfy****`

The ID of the instance launch template. Up to 10 IDs are supported.


* Argument \- N: specifies the serial number of the instance launch template.

* Separate multiple IDs with ampersands (&).



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**NextToken** <span data-label="purple">string</span> `Sample value:`

The pagination token returned by this call. If this value is empty, the current page is the last page.



**LaunchTemplates** <span data-label="purple">object[]</span> `Sample value:`

The information of the instance launch template that meets the condition.


**LaunchTemplateId** <span data-label="purple">string</span> `Sample value: lt-ysxc16auaugh9zfy****`

The ID of the instance launch template.



**LaunchTemplateName** <span data-label="purple">string</span> `Sample value: testLaunchTemplateName`

The name of the instance launch template.



**DefaultVersionNumber** <span data-label="purple">integer</span> `Sample value: 1`

The number of the default version of the instance launch template.



**LatestVersionNumber** <span data-label="purple">integer</span> `Sample value: 1`

The number of the latest version of the instance launch template.



**CreatedAt** <span data-label="purple">string</span> `Sample value: 2022-04-10T18:29:38+08:00`

The creation time of the instance launch template.



**UpdatedAt** <span data-label="purple">string</span> `Sample value: 2022-04-14T18:29:38+08:00`

The update time of the instance launch template.



**LaunchTemplateProjectName** <span data-label="purple">string</span> `Sample value: default`

The project to which the instance launch template belongs.



**LaunchTemplateTags** <span data-label="purple">object[]</span>

The tag information of the instance launch template.


**Key** <span data-label="purple">string</span> `Sample value: k1`

The tag key of the instance launch template.



**Value** <span data-label="purple">string</span> `Sample value: v1`

The tag value of the instance launch template.





&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeLaunchTemplates&Version=2020-04-01&LaunchTemplateIds.1=lt-ysxc16auaugh9zfy**** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20220419160338010225133143077B****",
        "Action": "DescribeLaunchTemplates",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "NextToken": "",
        "LaunchTemplates": [
            {
                "LaunchTemplateId": "lt-ysxc16auaugh9zfy****",
                "LaunchTemplateName": "test",
                "DefaultVersionNumber": 1,
                "LatestVersionNumber": 1,
                "CreatedAt": "2022-06-09T10:38:20+08:00",
                "UpdatedAt": "2022-06-09T10:38:20+08:00"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

To learn more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).
