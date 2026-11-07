---
title: "DescribeProject"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-describeproject"
---

Call the DescribeProject interface to query the information of the specified project.

<span id="usage-notes"></span>
## Usage notes

The call frequency limit for this interface is 20 times/s, and exceeding the frequency limit will result in an ExceedQPSLimit error.

<span id="request-syntax"></span>
## Request syntax


* Request Method: **GET**

* Request URL:**https://tls\-{Region}.bytepluses.com/DescribeProject**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="query"></span>
### Query


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|ProjectId |String |True |`f3e901c3-b17f-42fd-aa8c-dc91a6c7****` |The ID of the project. |


<span id="responses"></span>
## Responses

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).


|Name |Type |Example |Description |
|---|---|---|---|
|ProjectName |String |`test-project` |The name of the project. |
|ProjectId |String |`F ********` |The ID of the project. |
|Description |String |`This is a test project.` |The descriptive information of the project. |
|CreateTime |String |`2021-08-19 11:41:29` |The creation time of the project. |
|InnerNetDomain |String |`tls-ap-southeast-1.ibytepluses.com` |The private network connection domain name. |
|TopicCount |Integer |`5` |The number of the topics under the project. |
|IamProjectName |String |`Default` |The IAM project to which the project belongs. |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/38/16745#tag) |`[{"Key": "key1", "Value": "value1"}]` |The topic tag information. |


<span id="tag"></span>
### Tag


|Name |Type |Example |Description |
|---|---|---|---|
|Key |String |`owner` |The key of the tag. For setting rules, please refer to [Tag Setting Rules](https://docs.byteplus.com/docs/tls/Add_tags#rules-for-setting-tags). |
|Value |String |`zhangsan` |The value of the tag. For setting rules, please refer to [Tag Setting Rules](https://docs.byteplus.com/docs/tls/Add_tags#rules-for-setting-tags). |


<span id="sample-request"></span>
## Sample Request

```json
GET https://tls-{Region}.bytepluses.com/DescribeProject?ProjectId=f3********* HTTP/1.1
```


<span id="sample-response"></span>
## Sample Response

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
    "ProjectId": "f3************",
    "ProjectName": "test1",
    "Description": "test1",
    "CreateTime": "2022-02-14 20:59:21",
    "TopicCount": 0,
    "InnerNetDomain": "tls-ap-southeast-1.ibytepluses.com",
    "IamProjectName": "default",
    "Tags": [
        {
            "Key": "key1",
            "Value": "value1"
        }
    ]
}
```


<span id="error-code"></span>
## Error code

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |Invalid request parameter. |
|404 |ErrProjectNotExists |Project does not exist. |The project does not exist. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
