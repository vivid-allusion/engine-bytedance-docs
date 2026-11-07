---
title: "DeleteHealthCheckTemplates - Deleting the health check template"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DeleteHealthCheckTemplates"
---

Call the DeleteHealthCheckTemplates API to delete the health check template.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteHealthCheckTemplates&groupName=%E5%81%A5%E5%BA%B7%E6%A3%80%E6%9F%A5%E6%A8%A1%E6%9D%BF&serviceCode=alb&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|cFXFIa">必选</span> `Example: DeleteHealthCheckTemplates`

Action to execute. Set the value to DeleteHealthCheckTemplates.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|LH7yAC">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**HealthCheckTemplateIds.N ** <span data-label="purple">string[] </span><span data-api-tag="require|0hAk4t">必选</span> `Example: HealthCheckTemplateIds.1=hctpl-123****432 & HealthCheckTemplateIds.2=hctpl-123*****432`

ID of the health check template to be deleted.


* Parameter \- N: Represents the serial number of the health check template, with a value range of 1 to 5.

* Separate multiple health check templates with ampersands ( & ).



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 20210816110638****2514606306AF947C`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DeleteHealthCheckTemplates&Version=2020-04-01&HealthCheckTemplateIds.1=hctpl-3ciw6t6efwef46c6rrtdhxu36 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20210816110638****2514606306AF947C",
        "Action": "DeleteHealthCheckTemplates",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202108161106****22514606306AF947C"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request is missing a required parameter. Ensure that your request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |LimitExceed.HealthCheckTemplate |You've reached the limit on the number of health check templates that you can operate at a time. |The maximum number of health check templates that can be operated on in a single operation has been reached. |
|400 |InvalidIndexOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidHealthCheckTemplateIds.Duplicated |The specified HealthCheckTemplateIds is duplicated. |The specified HealthCheckTemplateIds is duplicated. |
|404 |InvalidHealthCheckTemplate.NotFound |The specified HealthCheckTemplate does not exist. |The specified health check template does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
