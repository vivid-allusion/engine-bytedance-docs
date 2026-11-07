---
title: "ModifyProject"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-modifyproject"
---

Call the ModifyProject interface to modify the project.

<span id="usage-notes"></span>
## Usage notes


* This interface is used to modify the name and description of the project, but does not support modifying the project ID.

* The call frequency limit is 20 times/s, and exceeding the frequency limit will result in the ExceedQPSLimit error.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The project name needs to be unique in the same region under the same account.</div>


<span id="request-syntax"></span>
## Request syntax


* Request Method: **PUT**

* Request URL: **https://tls\-{Region}.bytepluses.com/ModifyProject**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|ProjectId |String |True |`f3e901c3-b17f-42fd-aa8c-dc91a6c7****` |The ID of the project. |
|ProjectName |String |False |`test-project` |The name of the project. Please refer to the [Resource Naming limit](https://docs.byteplus.com/en/docs/tls/Limits#2c1ff6c3) for naming rules. The project name needs to be unique in the same region under the same account. |
|Description |String |False |`This is a test project` |The description information of the project.<br><br><br>* Does not support `<`, `'`, `\`, `\\` and all emoji symbols.<br><br>* The length is 0 to 64 characters. |


<span id="responses"></span>
## Responses

There are no unique return parameters for this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

<span id="sample-request"></span>
## Sample Request

```json
PUT https://tls-{Region}.bytepluses.com/ModifyProject HTTP/1.1
Content-Type: application/json
{
    "ProjectName": "test2",
    "Description": "test",
    "ProjectId": "89**************"
}
```


<span id="sample-response"></span>
## Sample Response

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{}
```


<span id="error-code"></span>
## Error code

The following table lists the error codes related to the interface and business logic. For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |The parameter is invalid. |
|404 |ErrProjectNotExists |Project does not exist. |The project does not exist. |
|409 |ErrProjectAlreadyExists |Project already exist. |The project already exists in this region. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
