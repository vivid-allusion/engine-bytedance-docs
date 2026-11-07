---
title: "DeleteProject"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-deleteproject"
---

Call the DeleteProject interface to delete a project.

<span id="usage-notes"></span>
## Usage notes


* The call frequency limit for this interface is 20 times/s, and exceeding the frequency limit will result in an ExceedQPSLimit error.

* When there are undeleted topics under the project, the project cannot be deleted. Please delete all topics of the project before deleting the project.

* Once the project is deleted, it cannot be recovered. Please operate with caution.


<span id="request-syntax"></span>
## Request syntax


* Request Method: **DELETE**

* Request URL: **https://tls\-{Region}.bytepluses.com/DeleteProject**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|ProjectId |String |True |`f3*****` |The ID of the project. |


<span id="responses"></span>
## Responses

There are no unique return parameters for this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

<span id="sample-request"></span>
## Sample Request

```json
DELETE https://tls-{Region}.bytepluses.com/DeleteProject HTTP/1.1
Content-Type: application/json
{
    "ProjectId": "f3************"
}
```


<span id="sample-response"></span>
## Sample Response

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```


<span id="error-code"></span>
## Error code

The following table lists the error codes related to the interface and business logic. For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |Invalid parameter. |
|400 |ProjectDeletedHasTopic |Project to be deleted has topics, please delete all topics before you delete the project |There are topics in the project, and it cannot be deleted. |
|404 |ProjectNotExists |Project does not exist. |Project does not exist. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal error. |


&nbsp;
