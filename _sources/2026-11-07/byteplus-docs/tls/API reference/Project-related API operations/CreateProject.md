---
title: "CreateProject"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-createproject"
---

Call the CreateProject interface to create a project.

<span id="usage-notes"></span>
## Usage notes


* The project is the basic unit of resource management in Torch Log Service, used for log resource isolation and access control among multiple users or projects.

* The call frequency limit for this interface is 20 times/s, and exceeding the frequency limit will result in an ExceedQPSLimit error.


<span id="request-syntax"></span>
## Request syntax


* Request Method: **POST**

* Request URL: **https://tls\-{Region}.bytepluses.com/CreateProject**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|ProjectName |String |True |`test-project` |The name of the project. Please refer to the [Resource Naming limit](https://docs.byteplus.com/en/docs/tls/Limits#2c1ff6c3) for naming rules. The project name needs to be unique in the same region under the same account. |
|Region |String |True |`cn-beijing` |The region ID. For a list of supported regions, please refer to the [Service Address](https://docs.byteplus.com/docs/tls/endpoint). |
|Description |String |False |`This is a test project` |The description information of the project.<br><br><br>* Does not support `<`, `'`, `\`, `\\` and all emoji symbols.<br><br>* The length is 0 to 64 characters. |
|IamProjectName |String |False |`default` |The IAM project to which the currently created project belongs. When this parameter is not specified, Torch Log Service will add the project to an IAM project named `default`. |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/38/16743#tag) |False |```Plain Text```<br>```[{"Key": "key1",```<br>```"Value": "value1"}]```<br> |The tags of the project.<br><br>Tags are used for the identification and classification of cloud resources. You can classify projects and topics through tags, which facilitates resource search and resource aggregation. |


<span id="tag"></span>
### Tag


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Key |String |False |`owner` |The key of the tag. For setting rules, please refer to [Tag Setting Rules](https://docs.byteplus.com/docs/tls/Add_tags#rules-for-setting-tags). |
|Value |String |False |`zhangsan` |The value of the tag. For setting rules, please refer to [Tag Setting Rules](https://docs.byteplus.com/docs/tls/Add_tags#rules-for-setting-tags). |


<span id="responses"></span>
## Responses

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).


|Name |Type |Example |Description |
|---|---|---|---|
|ProjectId |String |`fc69****` |The unique ID of the project. |


<span id="sample-request"></span>
## Sample Request

```json
POST https://tls-{Region}.bytepluses.com/CreateProject HTTP/1.1
Content-Type: application/json
{
    "ProjectName": "test1",
    "Description": "test1",
    "Region": "cn-beijing",
    "IamProjectName": "default",
    "Tags": [
        {
            "Key": "key1",
            "Value": "value1"
        }
    ]
}
```


<span id="sample-response"></span>
## Sample Response

```json
HTTP/1.1 200 OK
Content-Type:application/json; charset=utf-8
{
    "ProjectId": "f***********"
}
```


<span id="error-code"></span>
## Error code

The following table lists the error codes related to the interface and business logic. For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |The request contains illegal parameters. |
|409 |ProjectAlreadyExists |Project already exist |The project already exists. |
|400 |ProjectQuotaExceed |Exceeded project quota |Exceeding project number limits. |
|500 |ErrInternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
