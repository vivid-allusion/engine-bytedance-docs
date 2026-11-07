---
title: "ListSkillSpaces - Batch queries Skills space details"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/ListSkillSpaces_-_Batch_queries_Skills_space_details"
---

Query details of multiple Skills spaces using custom filter conditions.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|EAKsiE">必选</span> `Sample value: ListSkillSpaces`

The action that you want to perform. Value: ListSkillSpaces.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|dJw9hp">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**PageNumber ** <span data-label="purple">integer </span>`Optional` `Sample value: 10`

The number of entries returned on each page in a pagination query.


* Value range: 1–100.

* Default value: 10.



**PageSize ** <span data-label="purple">integer </span>`Optional` `Sample value: 1`

The current page number.


* Starting value: 1.

* Default value: 1



**Filter ** <span data-label="purple">object </span>`Optional` `Sample value: --`

The conditions for filtering Skills spaces. If this parameter is not specified, all Skills spaces that meet the conditions are returned by default.


**Status ** <span data-label="purple">string[] </span>`Optional` `Sample value: creating`

The status of the Skills space. Value:


* creating: Being created.

* running: Running.



**Name ** <span data-label="purple">string </span>`Optional` `Sample value: name1`

The name of the Skills space.



**Id ** <span data-label="purple">string </span>`Optional` `Sample value: ss-yed0d8u1ogo2****`

ID of the Skills space.




**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: default`

The name of the project associated with the Skills space.



**TagFilters ** <span data-label="purple">object[] </span>`Optional` `Sample value: --`

The tags associated with the Skills space.


**Key ** <span data-label="purple">string </span><span data-api-tag="require|7DHsCa">必选</span> `Sample value: key01`

The tag key.



**Values ** <span data-label="purple">string[] </span><span data-api-tag="require|8kv5Kd">必选</span> `Sample value: value01`

The tag value. Separate multiple values with commas (,). Filtering is performed based on the OR logical relationship.




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TotalCount ** <span data-label="purple">integer </span>`Sample value: 1`

The total number of Skills spaces that meet the conditions.



**Items ** <span data-label="purple">object[] </span>`Sample value: --`

Details of the Skills space.


**Id ** <span data-label="purple">string </span>`Sample value: ss-yed0d8u1ogo2****`

ID of the Skills space.



**Name ** <span data-label="purple">string </span>`Sample value: name1`

The name of the Skills space.



**Status ** <span data-label="purple">string </span>`Sample value: creating`

The status of the Skills space.



**Description ** <span data-label="purple">string </span>`Sample value: description`

The description of the Skills space.



**CreateTimeStamp ** <span data-label="purple">string </span>`Sample value: 1767528835`

The creation time of the Skills space (in Unix timestamp format).



**UpdateTimeStamp ** <span data-label="purple">string </span>`Sample value: 1767528835`

The update time of the Skills space (in Unix timestamp format).



**Relations ** <span data-label="purple">object[] </span>`Sample value: --`

The details of Skill added to the Skill space.


**SkillSpaceId ** <span data-label="purple">string </span>`Sample value: ss-yed0d8u1ogo2****`

The ID of the Skills space to which the Skill is added.



**SkillId ** <span data-label="purple">string </span>`Sample value: s-yed19lc8ow54****`

The Skill ID.



**SkillName ** <span data-label="purple">string </span>`Sample value: name1`

The Skill name.



**SkillDescription ** <span data-label="purple">string </span>`Sample value: description`

The Skill description.



**SkillStatus ** <span data-label="purple">string </span>`Sample value: running`

The version status of the Skill. Value:


* creating: Being created.

* running: Running.

* failed: Unavailable. This indicates a version creation failure.



**Version ** <span data-label="purple">string </span>`Sample value: v1`

The Skill version number.




**ProjectName ** <span data-label="purple">string </span>`Sample value: default`

The name of the project associated with the Skills space.



**Tags ** <span data-label="purple">object[] </span>`Sample value: --`

The tags associated with the Skills space.


**Key ** <span data-label="purple">string </span>`Sample value: key01`

The tag key.



**Value ** <span data-label="purple">string </span>`Sample value: value01`

The tag value.





&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=ListSkillSpaces&Version=2025-10-30 HTTP/1.1
{
  "PageNumber": 10,
  "PageSize": 1,
  "Filter": {
    "Status": [
      "creating"
    ],
    "Name": "name1",
    "Id": "ss-yed0d8u1ogo2****"
  },
 "TagFilters": [
    {
      "Key": "key01",
      "Values": "value01"
    }
  ],
  "ProjectName": "default"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20260106185205099181230****",
    "Action": "ListSkillSpaces",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "TotalCount": 1,
    "Items": [
      {
        "Id": "ss-yed0d8u1ogo2****",
        "Name": "name1",
        "Status": "creating",
        "Description": "description",
        "CreateTimeStamp": "1767528835",
        "UpdateTimeStamp": "1767528835",
        "Relations": [
          {
            "SkillDescription": "description"
            "SkillId": "s-yed19lc8ow54****",
            "SkillName": "name1",
            "SkillSpaceId": "ss-yed0d8u1ogo2****",
            "SkillStatus": "running",
            "Version": "v1",
          }
        ],
        "ProjectName": "default",
        "Tags": [
            {
              "Key": "key01",
              "Value": "value01"
            }
        ]
      }
    ]
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

To learn more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).
