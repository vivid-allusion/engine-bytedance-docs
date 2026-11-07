---
title: "GetSkillSpace - Queries details of a Skills space"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/GetSkillSpace_-_Queries_details_of_a_Skills_space"
---

Query Skills space details.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|5B6ncF">必选</span> `Sample value: GetSkillSpace`

The action that you want to perform. Value: GetSkillSpace.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|HRF20i">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**Id ** <span data-label="purple">string </span><span data-api-tag="require|20vJ0D">必选</span> `Sample value: ss-yed0d8u1ogo2****`

ID of the Skills space.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Id ** <span data-label="purple">string </span>`Sample value: ss-yed0d8u1ogo2****`

ID of the Skills space.



**Name ** <span data-label="purple">string </span>`Sample value: name1`

The name of the Skills space.



**Status ** <span data-label="purple">string </span>`Sample value: creating`

The status of the Skills space. Value:


* creating: Being created.

* running: Running.



**Description ** <span data-label="purple">string </span>`Sample value: description`

The description of the Skills space.



**CreateTimeStamp ** <span data-label="purple">string </span>`Sample value: 1767528835`

The creation time of the Skills space (in Unix timestamp format).



**UpdateTimeStamp ** <span data-label="purple">string </span>`Sample value: 1767528835`

The update time of the Skills space (in Unix timestamp format).



**ProjectName ** <span data-label="purple">string </span>`Sample value: default`

The name of the project associated with the Skills space.



**Tags ** <span data-label="purple">object[] </span>`Sample value: --`

The tags of the Skills space.


**Key ** <span data-label="purple">string </span>`Sample value: key01`

The tag key.



**Value ** <span data-label="purple">string </span>`Sample value: value01`

The tag value.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=GetSkillSpace&Version=2025-10-30 HTTP/1.1
{
  "Id": "ss-yed0d8u1ogo2****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202601061854012171602180****",
    "Action": "GetSkillSpace",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Id": "ss-yed0d8u1ogo2****",
    "Name": "name1",
    "Status": "creating",
    "Description": "description",
    "CreateTimeStamp": "1767528835",
    "UpdateTimeStamp": "1767528835",
    "ProjectName": "default",
    "Tags": [
      {
        "Key": "key01",
        "Value": "value01"
      }
    ]
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

To learn more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).
