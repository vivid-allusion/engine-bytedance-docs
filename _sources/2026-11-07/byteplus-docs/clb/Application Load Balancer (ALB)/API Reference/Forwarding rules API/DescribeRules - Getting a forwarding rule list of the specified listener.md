---
title: "DescribeRules - Getting a forwarding rule list of the specified listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-DescribeRules"
---

Call the DescribeRules API to get the forwarding rule list of the specified listener.

## Instructions

Submit up to 40 API requests per second.

## Debug

[去调试](https://api.volcengine.com/tools/api-explorer/?action=DescribeRules&groupName=%E8%BD%AC%E5%8F%91%E8%A7%84%E5%88%99&serviceCode=alb&version=2020-04-01)

## Request parameters

The table below lists only the request parameters unique to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: DescribeRules`

Action to execute. Set the value to DescribeRules.

**Version ** string必选 `Example: 2020-04-01`

Current API version is 2020\-04\-01.

**ListenerId ** string必选 `Example: lsn-2fea4ayvu2g3k5oxruuz****`

Listener ID.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** string`Example: 20210811152539010225146063030****`

Request ID.

**Rules ** object[]`Example: --`

Details of matching forwarding rules.

**Description ** string`Example: rule1`

Description of the forwarding rule.

**Domain ** string`Example: www.test.com`

Forwarding rule domain name.

**RewriteEnabled ** string`Example: on`

Forwarding rule rewrite configuration switch.

* on: Enable.

* off: Disable.

**RuleAction ** string`Example: Redirect`

Forwarding rule action.

* Empty: Defaults to forwarding to a server group.

* Redirect

**RuleId ** string`Example: rule-****`

Forwarding rule ID.

**ServerGroupId ** string`Example: rsp-2fel9y8pxr56o5oxruuuu****`

The backend server group ID associated with the forwarding rule.

**TrafficLimitEnabled ** string`Example: on`

Forwarding rule QPS rate limit switch.

* on: Enable.

* off: Disable.

**TrafficLimitQPS ** integer`Example: 100`

Requests per second. Value range: 100\-100000.

**Url ** string`Example: \`

URL for the forwarding rule.

**RedirectConfig ** object`Example: --`

Redirection\-related configuration information.

**RedirectHttpCode ** string`Example: 301`

Redirect status code.

* 301

* 302

* 307

* 308

**RedirectProtocol ** string`Example: HTTP`

Protocol used for redirection.

* HTTP

* HTTPS

**RedirectUri ** string`Example: /`

Redirect URI.

If the redirection URI is set to empty when creating or modifying a redirection\-type forwarding rule, the API will return ${request_uri}. This variable indicates that the redirection URI is consistent with the request URI. However, it is not supported to set the redirection URI to ${request_uri} during creation or modification.

**RedirectPort ** string`Example: 80`

Redirect port.

If the redirection port is set to empty when creating or modifying a redirection\-type forwarding rule, the API will return ${port}. This variable indicates that the redirection port is consistent with the request port (listener port). However, it is not supported to set the redirection port to ${port} during creation or modification.

**RedirectDomain ** string`Example: www.test.com`

Redirect domain name.

If the redirection domain name is set to empty when creating or modifying a redirection\-type forwarding rule, the API will return ${host}. This variable indicates that the redirection domain name is consistent with the request domain name. However, it is not supported to set the redirection domain name to ${host} during creation or modification.

**RewriteConfig ** object`Example: --`

Redirection\-related configuration information.

**RewritePath ** string`Example: /abc`

Rewrite path.

**ForwardGroupConfig ** object`Example: --`

Forwarding rule server group configuration.

**ServerGroupTuples ** object[]`Example: --`

List of destination server groups to forward to.

**ServerGroupId ** string`Example: rsp-j23jl2hh52ljllfksjl`

ID of the destination server group to forward to.

**Weight ** integer`Example: 99`

Server group weight.

**StickySessionEnabled ** string`Example: on`

Whether to enable group\-level session persistence.

* on: Enable.

* off: Disable.

**StickySessionTimeout ** integer`Example: 1000`

Component session persistence timeout. Unit: seconds.

**Priority ** integer`Example: 1`

Standard Edition forwarding rule priority.

**RuleConditions ** object[]`Example: --`

Standard edition forwarding rule conditions.

**SourceIpConfig ** object`Example: --`

Source IP configuration.

**Values ** string[]`Example: 192.168.1.0/24`

IPv4 address or IPv4 address range.

**CookieConfig ** object`Example: --`

Cookie configuration.

**Values ** object[]`Example: --`

Cookie configuration.

**Key ** string`Example: username`

Cookie string key.

**Value ** string`Example: zhangsan`

Cookie string value.

**Type ** string`Example: Host`

Standard Edition forwarding rule condition type.

* Host: domain name.

* Path

* Header: HTTP header.

* QueryString

* Cookie

* SourceIP

**HostConfig ** object`Example: --`

Domain configuration.

**Values ** string[]`Example: www.test.com`

Domain names for forwarding rules, supporting wildcard and exact domains.

**PathConfig ** object`Example: --`

Path configuration.

**Values ** string[]`Example: /foo`

URL of the forwarding rule, only absolute paths are supported.

**HeaderConfig ** object`Example: --`

HTTP header configuration.

**Values ** string[]`Example: test`

Header field value.

**Key ** string`Example: X-Forwarded-For`

Header field key.

**MethodConfig ** object`Example: --`

Request method.

**Values ** string[]`Example: GET`

Request method.

The following request methods are supported: HEAD, GET, POST, OPTIONS, PUT, PATCH, DELETE.

**QueryStringConfig ** object`Example: --`

Query string.

**Values ** object[]`Example: --`

String information.

**Key ** string`Example: version`

Query string key.

**Value ** string`Example: 1.0.0`

Query string value.

**RuleActions ** object[]`Example:--`

Standard edition forwarding rule actions.

**CorsConfig ** object`Example: --`

Cross\-domain configuration.

**AllowCredentials ** string`Example: on`

Allow credentials for cross\-origin requests.

* on

* off

**ExposeHeaders ** string[]`Example: test`

Response headers allowed to be accessed by browsers and JavaScript scripts.

**AllowHeaders ** string[]`Example: test`

Besides the browser's built\-in basic headers, the headers allowed for cross\-origin access.

**MaxAge ** integer`Example: 300`

Browser cache duration. Unit: second(s).

**AllowMethods ** string[]`Example: GET`

Allowed HTTP methods for cross\-domain access.

Supports GET, POST, PUT, DELETE, HEAD, OPTIONS, and PATCH.

**AllowOrigin ** string[]`Example: http://www.test.com`

Sites allowed to access server resources via a browser.

**InsertHeaderConfig ** object`Example: --`

Write header configuration.

**Key ** string`Example: test`

Name of the header field.

**Value ** string`Example: remote_addr`

Header field content.

**ValueType ** string`Example: UserDefined`

Header field content type.

* Custom: Custom header field content.

* SystemDefined: System defined header field content.

**Type ** string`Example: Rewrite`

Forwarding rule action type.

* ForwardGroup: Forward to. ALB forwards the request to the backend server group you specified.

* Redirect: Redirect to. The ALB redirects the request.

* Rewrite ALB rewrites the request path and requests content from the new path on the backend server.

* TrafficLimit: Rate limiting. When the number of requests exceeds the configured QPS, ALB discards new requests.

* FixedResponse: Return fixed content. Customize the response status code and response body.

* Cors: Cross\-domain. Supports cross\-domain requests, i.e., when any of the protocol, domain, or port of the client request differs from the address of the page returned by the server.

* InsertHeader: Write Header. Add a `key:value` pair to the request header, which will be sent to the backend server along with the request.

**TrafficLimitConfig ** object`Example: --`

Rate limiting configuration information.

**QPS ** integer`Example: 1000`

Requests per second.

**RewriteConfig ** object`Example: --`

Rewrite configuration information.

**Host ** string`Example: www.test.com`

Rewrite domain name.

**Path ** string`Example: /test`

Rewrite path.

**RedirectConfig ** object`Example: --`

Redirection configuration information.

**Query ** string`Example: test`

Redirect query string.

**Host ** string`Example: www.test.com`

Redirection domain name, only exact domain names are supported.

**Path ** string`Example: /test`

Redirect URI.

**Protocol ** string`Example: HTTP`

Protocol used for redirection, supports HTTP and HTTPS.

**HttpCode ** string`Example: 301`

Redirect status code, supports 301, 302, 307, 308.

**Port ** string`Example: 88`

Redirect port.

**ForwardGroupConfig ** object`Example: --`

Forward\-to forwarding action configuration information.

**ServerGroupTuples ** object[]`Example: --`

Server group configuration.

**ServerGroupId ** string`Example: rsp-j23jl2hh52ljllfksjl`

ID of the destination server group to forward to.

**Weight ** integer`Example: 99`

Server group weight.

**ServerGroupStickySession ** object`Example: --`

Session persistence configuration.

**Enabled ** string`Example: on`

Whether to enable group\-level session persistence.

* on: Enable.

* off: Disable.

**Timeout ** integer`Example: 10`

Component session persistence timeout. Unit: seconds.

**FixedResponseConfig ** object`Example: --`

Fixed response configuration information.

**Content ** string`Example: esponse_ok`

Return fixed content.

**HttpCode ** string`Example: 200`

HTTP response status code.

**ContentType ** string`Example: text/plain`

Format of the return fixed content.

* text/plain

* text/css

* text/html

* application/javascript

* application/json

## Request example

```text
GET /?Action=DescribeRules&ListenerId=lsn-1g0puwcxu****8ibuxxw2pmf7&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20210813182653****2514214204001104",
        "Action": "DescribeRules",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210813182653****2514214204001104",
        "Rules": [
            {
                "RuleId": "rule-2fegss1cplxxc5oxruvvqzvyu",
                "Domain": "%abc.com",
                "Url": "/abcc",
                "ServerGroupId": "rsp-3ciynvqsspiww6c6rrsz73tzn",
                "Description": "TEST"
            }
        ]
    }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The format of the specified %s parameter is invalid. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as: %s. |
|404 |InvalidListener.NotFound |The specified Listener does not exist. |The specified listener does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
