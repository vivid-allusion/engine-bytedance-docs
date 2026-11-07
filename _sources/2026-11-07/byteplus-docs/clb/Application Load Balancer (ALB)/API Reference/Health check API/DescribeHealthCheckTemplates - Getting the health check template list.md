---
title: "DescribeHealthCheckTemplates - Getting the health check template list"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeHealthCheckTemplates"
---

Call the DescribeHealthCheckTemplates API to query the list of health check templates.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* The maximum number of templates that can be queried by ID in a single request is 20.

* Submit up to 40 API requests per second.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeHealthCheckTemplates&groupName=%E5%81%A5%E5%BA%B7%E6%A3%80%E6%9F%A5%E6%A8%A1%E6%9D%BF&serviceCode=alb&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|fykp9L">必选</span> `Example: DescribeHealthCheckTemplates`

Action to execute. Set the value to DescribeHealthCheckTemplates.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|F3IowU">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**TagFilters.N.Key ** <span data-label="purple">string[] </span>`optional` `Example: TagFilters.1.Key=k1&TagFilters.2.Key=k2`

The tag key.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. Multiple tag keys have a logical AND relationship. The query returns health check templates tagged with all the specified keys.

* Duplicate values are not allowed.



**TagFilters.N.Values.N ** <span data-label="purple">string[] </span>`optional` `Example: TagFilters.1.Value.1=v1&TagFilters.1.Value.2=v2&TagFilters.2.Value.1=v3`

The tag value.


* The first N specifies the serial number of a tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns health check templates that have any of the specified tag values for that key.

* Separate multiple tag values with an ampersand (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If this parameter is passed in, TagFilters.N.Key must be passed in first.</div>


* <div data-tips="true" data-tips-type="tip">Passing an empty string queries for health check templates with an empty tag value.</div>




**HealthCheckTemplateIds.N ** <span data-label="purple">string[] </span>`optional` `Example: HealthCheckTemplateIds.1=hctpl-123****765&HealthCheckTemplateIds.2=hctpl-123****123`

ID of the health check template.


* Parameter \- N: Represents the serial number of the health check template, with a value range of 1 to 20.

* Separate multiple health check templates with ampersands ( & ).



**HealthCheckTemplateName ** <span data-label="purple">string </span>`optional` `Example: test`

Name of the health check template.



**PageNumber ** <span data-label="purple">integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.



**PageSize ** <span data-label="purple">integer </span>`optional` `Example: 20`

Number of rows per page for paginated queries. Valid range: 1 to 100. Default value: 10.



**ProjectName ** <span data-label="purple">string </span>`optional` `Example: default`

The name of the project to which the health check template belongs.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageSize ** <span data-label="purple">integer </span>`Example: 20`

The number of rows on the current page.



**PageNumber ** <span data-label="purple">integer </span>`Example: 1`

Current page number.



**TotalCount ** <span data-label="purple">integer </span>`Example: 50`

Total number of health check templates that meet the criteria.



**HealthCheckTemplates ** <span data-label="purple">object[] </span>`Example: --`

Details of the qualified health check templates.


**HealthCheckTemplateId ** <span data-label="purple">string </span>`Example: hctpl-123*******765`

Health check template ID.



**HealthCheckTemplateName ** <span data-label="purple">string </span>`Example: test`

Name of the health check template.



**HealthCheckInterval ** <span data-label="purple">integer </span>`Example: 2`

The interval for performing health checks. Default: is 2. Value range 1\-300.



**HealthCheckTimeout ** <span data-label="purple">integer </span>`Example: 2`

Response timeout for health checks: default is 2 seconds, value range 1\-60.



**HealthyThreshold ** <span data-label="purple">integer </span>`Example: 3`

Healthy threshold for health checks: default is 3, value range 2\-10.



**UnhealthyThreshold ** <span data-label="purple">integer </span>`Example: 3`

Unhealthy threshold for health checks, default: 3, value range: 2–10.



**HealthCheckMethod ** <span data-label="purple">string </span>`Example: GET`

The method for health checks; this parameter exists only when HealthCheckProtocol is set to HTTP.


* GET

* HEAD



**HealthCheckDomain ** <span data-label="purple">string </span>`Example: a.com`

Health check domain name. This parameter exists only when HealthCheckProtocol is set to HTTP.



**HealthCheckURI ** <span data-label="purple">string </span>`Example: /`

The path for health checks; this parameter exists only when HealthCheckProtocol is set to HTTP. Default: /.



**HealthCheckHttpCode ** <span data-label="purple">string </span>`Example: http_2xx`

The HTTP status codes indicating a successful health check; this parameter exists only when HealthCheckProtocol is set to HTTP. The default values are http_2xx and http_3xx, separated by commas.



**HealthCheckProtocol ** <span data-label="purple">string </span>`Example: HTTP`

Health check protocol.


* HTTP

* TCP



**HealthCheckHttpVersion ** <span data-label="purple">string </span>`Example: HTTP1.0`

The HTTP protocol version for health checks; this parameter exists only when HealthCheckProtocol is set to HTTP.


* HTTP1.0

* HTTP1.1



**Description ** <span data-label="purple">string </span>`Example: test`

Health check description.



**HealthCheckPort ** <span data-label="purple">integer </span>`Example: 80`

Health check port. When the parameter value is 0, it indicates that the backend server port is used for health checks.



**Tags ** <span data-label="purple">object[] </span>`Example: -`

Tags associated with the health check template.


**Key ** <span data-label="purple">string </span>`Example: key`

The tag key of the custom tag.



**Value ** <span data-label="purple">string </span>`Example: value`

The tag value of the custom tag.




**CreateTime ** <span data-label="purple">string </span>`Example: 2024-12-29T16:37:37Z`

Creation time of the health check template.



**UpdateTime ** <span data-label="purple">string </span>`Example: 2024-12-29T16:37:37Z`

Last operation time of the health check template.



**ProjectName ** <span data-label="purple">string </span>`Example: default`

The name of the project to which the health check template belongs.




**RequestId ** <span data-label="purple">string </span>`Example: 20210816110638****2514606306AF947C`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DescribeHealthCheckTemplates&Version=2020-04-01&PageSize=20&PageNumber=1&HealthCheckTemplateIds.1=hctpl-123****765&HealthCheckTemplateIds.2=hctpl-123****123 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "20210816110638****2514606306AF947C",
        "Action": "DescribeHealthCheckTemplates",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210814160835****2514606300FFE0F3",
        "PageNumber": 1,
        "PageSize": 20,
        "TotalCount": 1,
        "HealthCheckTemplates": [
            {
                "HealthCheckTemplateId": "hctpl-123*******765",
                "HealthCheckTemplateName": "test",
                "HealthCheckInterval": 2,
                "HealthCheckTimeout": 2,
                "HealthyThreshold": 3,
                "UnhealthyThreshold": 3,
                "HealthCheckMethod": "GET",
                "HealthCheckDomain": "a.com",
                "HealthCheckURI": "/",
                "HealthCheckHttpCode": "http_2xx",
                "HealthCheckProtocol": "HTTP",
                "Description": "test"
            },
            {
                "HealthCheckTemplateId": "hctpl-123*******765",
                "HealthCheckTemplateName": "test",
                "HealthCheckInterval": 2,
                "HealthCheckTimeout": 2,
                "HealthyThreshold": 3,
                "UnhealthyThreshold": 3,
                "HealthCheckMethod": "HEAD",
                "HealthCheckDomain": "a.com",
                "HealthCheckURI": "/",
                "HealthCheckHttpCode": "http_2xx",
                "HealthCheckProtocol": "HTTP",
                "Description": "test"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request does not contain required parameters. Please ensure the request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |LimitExceed.HealthCheckTemplate |You've reached the limit on the number of health check templates that you can operate at a time. |The maximum number of health check templates that can be operated on in a single operation has been reached. |
|400 |InvalidHealthCheckTemplateName.Malformed |The specified HealthCheckTemplateName is malformed. |The specified HealthCheckTemplateName parameter format is invalid. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|400 |LimitExceed.TagFilters.Values |You've reached the limit on the number of tag filter values that you can operate at a time. |You have reached the maximum number of tag values that can be operated on in a single request. |
|400 |InvalidTagFilters.Key.Malformed |The specified TagFilters.Key is malformed. |The specified TagFilters.Key parameter format is invalid. |
|400 |InvalidTagFilters.Value.Malformed |The specified TagFilters.Value is malformed. |The specified TagFilters.Value parameter format is invalid. |
|400 |InvalidTagFilters.Key.Duplicated |The specified TagFilters.Key is duplicated. |The specified TagFilters.Key is duplicated. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
