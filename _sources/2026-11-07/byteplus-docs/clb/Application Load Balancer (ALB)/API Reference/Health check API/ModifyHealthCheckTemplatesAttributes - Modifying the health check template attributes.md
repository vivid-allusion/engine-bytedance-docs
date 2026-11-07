---
title: "ModifyHealthCheckTemplatesAttributes - Modifying the health check template attributes"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ModifyHealthCheckTemplatesAttributes"
---

Call the ModifyHealthCheckTemplatesAttributes API to modify the health check template attributes.

## Instructions

* The maximum number of templates that can be modified in a single batch is 5.

* Submit up to 10 API requests per second.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyHealthCheckTemplatesAttributes&groupName=%E5%81%A5%E5%BA%B7%E6%A3%80%E6%9F%A5%E6%A8%A1%E6%9D%BF&serviceCode=alb&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: ModifyHealthCheckTemplatesAttributes`

Action to execute. Set the value to ModifyHealthCheckTemplatesAttributes.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**HealthCheckTemplates.N.HealthCheckTemplateId ** string[]必选 `Example: HealthCheckTemplates.1.HealthCheckTemplateId=hctpl-123****765&HealthCheckTemplates.2.HealthCheckTemplateId=hctpl-iuytrfv`

Health check template ID.

**HealthCheckTemplates.N.HealthCheckPort ** integer[]`optional` `Example: HealthCheckTemplates.1.HealthCheckPort=80&HealthCheckTemplates.2.HealthCheckPort=81`

Health check port. Valid values:

* 0: The port of the backend server is used for health checks.

* 1\-65535: Use the port you specify for health checks.

**HealthCheckTemplates.N.Description ** string[]`optional` `Example: HealthCheckTemplates.1.Description=test1&HealthCheckTemplates.2.Description=test2`

Health check description.

* Cannot start with http:// or https://.

* Must start with a letter or Chinese character and may include numbers, half\-width commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

* Must be 1 to 255 characters.

* If left blank, this parameter defaults to an empty string.

**HealthCheckTemplates.N.HealthCheckDomain ** string[]`optional` `Example: HealthCheckTemplates.1.HealthCheckDomain=a.com&HealthCheckTemplates.2.HealthCheckDomain=b.com`

Health check domain name.

* This parameter takes effect only when HealthCheckProtocol is set to HTTP.

* Requirements:

   * Must contain at least one '.' but must not start or end with '.'.

   * A single string consists of letters, numbers, '\-', and '.' characters. '\-' cannot appear at the beginning or end of the string.

   * Length limit is 1 to 128 characters.

   * If not specified, this parameter is empty. By default, CLB uses the private IP address of each backend server for health checks.

**HealthCheckTemplates.N.HealthCheckHttpCode ** string[]`optional` `Example: HealthCheckTemplates.1.HealthCheckHttpCode=http_2xx&HealthCheckTemplates.2.HealthCheckHttpCode=http_3xx,http_4xx`

The HTTP status code indicates a successful health check.

* Separate multiple status codes with commas. This parameter takes effect only when HealthCheckProtocol is set to HTTP.

* Valid values:

   * http_2xx

   * http_3xx

   * http_4xx

   * http_5xx

**HealthCheckTemplates.N.HealthCheckHttpVersion ** string[]`optional` `Example: HealthCheckTemplates.1.HealthCheckHttpVersion=HTTP1.0&HealthCheckTemplates.N.HealthCheckHttpVersion=HTTP1.1`

HTTP protocol version for health checks.

* This parameter takes effect only when HealthCheckProtocol is set to HTTP.

* Valid values:

   * HTTP1.0

   * HTTP1.1

**HealthCheckTemplates.N.HealthCheckInterval ** integer[]`optional` `Example: HealthCheckTemplates.1.HealthCheckInterval=2&HealthCheckTemplates.2.HealthCheckInterval=3`

The time interval for performing health checks. Value range: 1\-300 seconds.

**HealthCheckTemplates.N.HealthCheckMethod ** string[]`optional` `Example: HealthCheckTemplates.1.HealthCheckMethod=GET&HealthCheckTemplates.2.HealthCheckMethod=HEAD`

Health check method.

* This parameter takes effect only when HealthCheckProtocol is set to HTTP.

* Valid values:

   * GET

   * HEAD

**HealthCheckTemplates.N.HealthCheckProtocol ** string[]`optional` `Example: HealthCheckTemplates.1.HealthCheckProtocol=HTTP&HealthCheckTemplates.2.HealthCheckProtocol=HTTP`

Health check protocol. Valid values:

* HTTP

* TCP

**HealthCheckTemplates.N.HealthCheckTemplateName ** string[]`optional` `Example: HealthCheckTemplates.1.HealthCheckTemplateName=test1&HealthCheckTemplates.2.HealthCheckTemplateName=test2`

Name of the health check template.

* Cannot start with http:// or https://.

* Must start with a letter or Chinese character. May include numbers, periods (.), underscores (_), and hyphens (\-).

* Length must be between 1 and 128 characters.

**HealthCheckTemplates.N.HealthCheckTimeout ** integer[]`optional` `Example: HealthCheckTemplates.1.HealthCheckTimeout=2&HealthCheckTemplates.2.HealthCheckTimeout=3`

The response timeout period for the health check ranges from 1 to 60 seconds.

**HealthCheckTemplates.N.HealthCheckURI ** string[]`optional` `Example: HealthCheckTemplates.1.HealthCheckURI=&HealthCheckTemplates.2.HealthCheckURI=abc`

Health check path.

* This parameter takes effect only when HealthCheckProtocol is set to HTTP.

* Requirements:

   * Must start with '/'.

   * May only contain letters, numbers, '\-', '_', '/', '.', '%', '?', '#', '&', and '='.

   * Length limit is 1 to 128 characters.

   * If left blank, it defaults to "/".

**HealthCheckTemplates.N.HealthyThreshold ** integer[]`optional` `Example: HealthCheckTemplates.1.HealthyThreshold=2&HealthCheckTemplates.2.HealthyThreshold=3`

The healthy threshold for the health check ranges from 2 to 10 times.

**HealthCheckTemplates.N.UnhealthyThreshold ** integer[]`optional` `Example: HealthCheckTemplates.1.UnhealthyThreshold=2&HealthCheckTemplates.2.UnhealthyThreshold=3`

Unhealthy threshold for health check ranges from 2 to 10 times.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** string`Example: 20210816110638****2514606306AF947C`

Request ID.

## Request examples

```text
GET /?Action=ModifyHealthCheckTemplatesAttributes&HealthCheckTemplates.1.Description=test&Version=2020-04-01&HealthCheckTemplates.1.HealthCheckTemplateId=hctpl-123*****876&HealthCheckTemplates.1.HealthCheckTemplateName=test&HealthCheckTemplates.1.HealthCheckHttpCode="http_2xx,http_3xx" HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "20210816110638****2514606306AF947C",
        "Action": "ModifyHealthCheckTemplatesAttributes",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202108161106****22514606306AF947C"
    }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |InvalidIndexOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, 'HealthCheckTemplates.HealthCheckDomain'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as HealthCheckTemplates.HealthCheckDomain. |
|400 |InvalidHealthCheckTemplates.HealthCheckHttpVersion.Malformed |The specified HealthCheckTemplates.HealthCheckHttpVersion is malformed. |The specified HealthCheckTemplates.HealthCheckHttpVersion parameter format is invalid. |
|400 |InvalidHealthCheckTemplates.HealthCheckHttpCode.Malformed |The specified HealthCheckTemplates.HealthCheckHttpCode is malformed. |The specified HealthCheckTemplates.HealthCheckHttpCode parameter format is invalid. |
|400 |InvalidHealthCheckTemplates.UnhealthyThreshold.Malformed |The specified HealthCheckTemplates.UnhealthyThreshold is malformed. |The specified HealthCheckTemplates.UnhealthyThreshold parameter format is invalid. |
|400 |InvalidHealthCheckTemplates.HealthyThreshold.Malformed |The specified HealthCheckTemplates.HealthyThreshold is malformed. |The specified HealthCheckTemplates.HealthyThreshold parameter format is invalid. |
|400 |InvalidHealthCheckTemplates.HealthCheckTimeout.Malformed |The specified HealthCheckTemplates.HealthCheckTimeout is malformed. |The specified HealthCheckTemplates.HealthCheckTimeout parameter format is invalid. |
|400 |InvalidHealthCheckTemplates.HealthCheckInterval.Malformed |The specified HealthCheckTemplates.HealthCheckInterval is malformed. |The specified HealthCheckTemplates.HealthCheckInterval parameter format is invalid. |
|400 |InvalidHealthCheckTemplates.HealthCheckURI.Malformed |The specified HealthCheckTemplates.HealthCheckURI is malformed. |The specified HealthCheckTemplates.HealthCheckURI parameter format is invalid. |
|400 |InvalidHealthCheckTemplates.HealthCheckDomain.Malformed |The specified HealthCheckTemplates.HealthCheckDomain is malformed. |The specified HealthCheckTemplates.HealthCheckDomain parameter format is invalid. |
|400 |InvalidHealthCheckTemplates.HealthCheckMethod.Malformed |The specified HealthCheckTemplates.HealthCheckMethod is malformed. |The specified HealthCheckTemplates.HealthCheckMethod parameter format is invalid. |
|400 |InvalidHealthCheckTemplates.HealthCheckProtocol.Malformed |The specified HealthCheckTemplates.HealthCheckProtocol is malformed. |The specified HealthCheckTemplates.HealthCheckProtocol parameter format is invalid. |
|400 |InvalidHealthCheckTemplates.Description.Malformed |The specified HealthCheckTemplates.Description is malformed. |The specified HealthCheckTemplates.Description parameter format is invalid. |
|400 |InvalidHealthCheckTemplates.HealthCheckTemplateName.Malformed |The specified HealthCheckTemplates.HealthCheckTemplateName is malformed. |The specified HealthCheckTemplates.HealthCheckTemplateName parameter format is invalid. |
|400 |LimitExceed.HealthCheckTemplate |You've reached the limit on the number of health check templates that you can operate at a time. |The maximum number of health check templates that can be operated on in a single operation has been reached. |
|400 |InvalidHealthCheckTemplates.HealthCheckPort.Malformed |The specified HealthCheckTemplates.HealthCheckPort is malformed. |The specified HealthCheckTemplates.HealthCheckPort parameter format is invalid. |
|404 |InvalidHealthCheckTemplate.NotFound |The specified HealthCheckTemplate does not exist. |The specified health check template does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
