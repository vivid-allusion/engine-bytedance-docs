---
title: "ListSkills - Batch queries details of multiple Skills"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/ListSkills_-_Batch_queries_details_of_multiple_Skills"
---

Query details of multiple Skills using custom filter conditions.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|JifTYi">必选</span> `Sample value: ListSkills`

The action that you want to perform. Value: ListSkills.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|umTzs4">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**PageNumber ** <span data-label="purple">integer </span>`Optional Sample value: 1`

The current page number.


* Starting value: 1.

* Default value: 1



**PageSize**<span data-label="purple"> integer </span>`Optional Sample value: 10`

The number of entries returned on each page in a pagination query.


* Value range: 1–100.

* Default value: 10.



**Filter ** <span data-label="purple">object </span>`Optional` `Sample value: --`

The filter conditions for Skill. If this parameter is not specified, all Skills that meet the conditions are returned by default.


**Status ** <span data-label="purple">string[] </span>`Optional` `Sample value: creating`

The Skill status. The status of Skill is determined by the status of its versions. Valid values:


* creating: Creating. This indicates that the Skill has only one version, and that version is being created.

* failed: Unavailable. This indicates that all versions of the Skill are unavailable.

* updating: Updating. This indicates that the Skill has more than one version, and at least one version is being created.

* running: Running. This indicates that the versions of the Skill are in a state other than those described above.



**Name ** <span data-label="purple">string </span>`Optional` `Sample value: algorithmic-art`

The Skill name.



**Id ** <span data-label="purple">string </span>`Optional` `Sample value: s-yed19lc8ow54****`

The Skill ID.




**TagFilters ** <span data-label="purple">object[] </span>`Optional` `Sample value: --`

The associated tags.


**Key ** <span data-label="purple">string </span><span data-api-tag="require|o0dDpS">必选</span> `Sample value: key01`

The tag key.



**Values ** <span data-label="purple">string[] </span><span data-api-tag="require|xiXTru">必选</span> `Sample value: value01`

The tag value. Separate multiple values with commas (,). Filtering is performed based on the OR logical relationship.




**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: default`

Name of the associated project.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TotalCount ** <span data-label="purple">integer </span>`Sample value: 1`

The total number of Skills that meet the conditions.



**Items ** <span data-label="purple">object[] </span>`Sample value: --`

The Skill details.


**Id ** <span data-label="purple">string </span>`Sample value: s-yed19lc8ow54****`

The Skill ID.



**Name ** <span data-label="purple">string </span>`Sample value: name1`

The Skill name.



**Status ** <span data-label="purple">string </span>`Sample value: creating`

The Skill status.



**Description ** <span data-label="purple">string </span>`Sample value: description1`

The description of the Skill.



**CreateTimeStamp ** <span data-label="purple">string </span>`Sample value: 1767528835`

The creation time of the Skill (Unix timestamp format).



**UpdateTimeStamp ** <span data-label="purple">string </span>`Sample value: 1767528835`

The update time of the Skill (Unix timestamp format).



**Versions ** <span data-label="purple">string[] </span>`Sample value: v1`

The Skill version number.



**ProjectName ** <span data-label="purple">string </span>`Sample value: default`

The name of the project associated with the Skill.



**Tags ** <span data-label="purple">object[] </span>`Sample value: --`

The tags associated with the Skill.


**Key ** <span data-label="purple">string </span>`Sample value: key01`

The tag key.



**Value ** <span data-label="purple">string </span>`Sample value: value01`

The tag value.





&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=ListSkills&Version=2025-10-30 HTTP/1.1
{
  "PageNumber": 1,
  "PageSize": 10,
  "Filter": {
    "Status": [
      "creating"
    ],
    "Name": "algorithmic-art",
    "Id": "s-yed19lc8ow54****"
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
    "RequestId": "2026012015343322510****",
    "Action": "ListSkills",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "TotalCount": 1,
    "Items": [
      {
        "Id": "s-yed19lc8ow54****",
        "Name": "name1",
        "Status": "creating",
        "Description": "description1",
        "CreateTimeStamp": "1767528835",
        "UpdateTimeStamp": "1767528835",
        "Versions": [
          "v1"
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
