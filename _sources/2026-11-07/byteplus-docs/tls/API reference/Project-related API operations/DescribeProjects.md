---
title: "DescribeProjects"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-describeprojects"
---

Call the DescribeProjects interface to view all project information in the current region.

<span id="usage-notes"></span>
## Usage notes


* This interface is used to list all project information of the current user in the current region. It supports page query, offset query, and fuzzy query by project name or ID.

* The call frequency limit for this interface is 20 times/s, and exceeding the frequency limit will result in an ExceedQPSLimit error.


<span id="request-syntax"></span>
## Request syntax


* Request Method: **GET**

* Request URL: **https://tls\-{Region}.bytepluses.com/DescribeProjects**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="query"></span>
### Query


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|PageNumber |Integer |False |`10` |The page number when paging the query. The default is 1, that is, the return starts from the first page of data. |
|PageSize |Integer |False |`20` |The page size. The default is 20, with a maximum of 100. |
|ProjectName |String |False |`test` |The name of the project, supports fuzzy matching. |
|ProjectId |String |False |`1e2fd27e` |The ID of the project, supports fuzzy matching. |
|IsFullName |Boolean |False |`true` |Whether to perform an exact match when filtering by project name.<br><br><br>* true: Exact match.<br><br>* false: (Default) Fuzzy query. |
|IamProjectName |String |False |`default` |Filter according to the IAM project. Exact match. |
|Tags |String |False |`[{\ "key\":\ "key2\",\ "Value\":\ "value1\"}]` |Filter according to the topic tags. |


<span id="responses"></span>
## Responses

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).


|Name |Type |Example |Description |
|---|---|---|---|
|Projects |Array of [ProjectInfo](https://docs.byteplus.com/en/docs/38/16746#projectinfo) |`/` |The projects information. |
|Total |Integer |`1` |The total number of the projects. |


<span id="projectinfo"></span>
### ProjectInfo


|Name |Type |Example |Description |
|---|---|---|---|
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/38/16746#tag) |`[{"Key":"key1","Value":"value1"}]` |The topic tag information.<br><br>&nbsp;<br><br>Tags are used for the identification and classification of cloud resources. You can classify projects and topics through tags, which facilitates resource search and resource aggregation. |
|ProjectId |String |`f**********` |The ID of the project. |
|CreateTime |String |`2021-08-19 11:41:29` |The creation time of the project. |
|TopicCount |Integer |`5` |The number of the topics under the current project. |
|Description |String |`This is a test project.` |The description information of the project. |
|ProjectName |String |`test-project` |The name of the project. |
|IamProjectName |String |`default` |The IAM project to which the project belongs. |
|InnerNetDomain |String |`tls-cn-beijing.ibytepluses.com` |The private network connection domain name. |


<span id="tag"></span>
### Tag


|Name |Type |Example |Description |
|---|---|---|---|
|Key |String |`owner` |The key of the tag. For setting rules, please refer to [Tag Setting Rules](https://docs.byteplus.com/docs/tls/Add_tags#rules-for-setting-tags). |
|Value |String |`zhangsan` |The value of the tag. For setting rules, please refer to [Tag Setting Rules](https://docs.byteplus.com/docs/tls/Add_tags#rules-for-setting-tags). |


<span id="sample-request"></span>
## Sample Request

```json
GET https://tls-{Region}.bytepluses.com/DescribeProjects?ProjectName=test&PageNumber=1&PageSize=20&IsFullName=false&IamProjectName=default&Tags=[{"Key":"key1","Value":"value1"}]HTTP/1.1
```


<span id="sample-response"></span>
## Sample Response

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
    "Projects": [
        {
            "ProjectId": "a1*******",
            "ProjectName": "test1",
            "Description": "test1",
            "CreateTime": "2022-03-14 20:59:21",
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
    ],
    "Total": 1
}
```


<span id="error-code"></span>
## Error code

The following table lists the error codes related to the interface and business logic. For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |Invalid request parameter. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
