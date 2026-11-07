---
title: "ModifyServerGroupAttributes - Modifying the specified server group details"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-ModifyServerGroupAttributes"
---

Call the ModifyServerGroupAttributes API to modify the details of a specified server group.

## Instructions

Submit up to 5 API requests per second.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyServerGroupAttributes&groupName=%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%BB%84&serviceCode=alb&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: ModifyServerGroupAttributes`

Action to execute. Set the value to ModifyServerGroupAttributes.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**StickySessionConfig.CookieTimeout ** integer`optional` `Example: 1000`

Session persistence cookie timeout. Only valid when session persistence is enabled and the cookie implant method is selected. Unit: second(s). The specific rules are as follows:

* Timeout value range: 1\-86400. Default value: 1000.

* This parameter is required when StickySessionConfig.StickySessionEnabled is on and StickySessionType is insert.

* This parameter is invalid when StickySessionConfig.StickySessionEnabled is on and StickySessionType is server.

**StickySessionConfig.Cookie ** string`optional` `Example: MY_COOKIE`

The session persistence cookie name configured for the service. Only valid when session persistence is enabled and the cookie rewrite method is selected. The specific rules are as follows:

* Cookie name length: 1 to 200 characters.

* The name can only contain ASCII letters and numbers. It cannot contain commas (,), semicolons (;), or spaces, nor can it start with a dollar sign ($).

* This parameter is required when StickySessionConfig.StickySessionEnabled is on and StickySessionConfig.StickySessionType is server.

* This parameter is invalid when StickySessionConfig.StickySessionEnabled is on and StickySessionConfig.StickySessionType is insert.

**StickySessionConfig.StickySessionType ** string`optional` `Example: insert`

Cookie handling method. This field is required when StickySessionConfig.StickySessionEnabled is **on**. Valid values:

* insert: Implant cookie;

   The ALB records the backend server to which the client's first request is forwarded. The ALB inserts a cookie into the response. When subsequent client requests carry this cookie, the ALB forwards the requests to the previously recorded backend server.

* server: Rewrite cookie;

   After session persistence with cookie rewrite is enabled, when the client's first request is forwarded to the backend server, the ALB, upon finding your custom cookie in the response, rewrites the original cookie. Subsequent client requests carrying the rewritten cookie will cause the ALB to forward the requests to the previously recorded backend server.

**StickySessionConfig.StickySessionEnabled ** string`optional` `Example: off`

Enable session persistence Valid values:

* on: Enable.

* off: Disable.

**HealthCheck.UnhealthyThreshold ** integer`optional` `Example: 3`

The unhealthy threshold for health check.

* Indicates a backend server that continuously runs the specified number of health checks and returns all results as exception will be marked as exception.

* Unit: time(s). Range: 2\-10. Default: 3.

**HealthCheck.HealthyThreshold ** integer`optional` `Example: 3`

The health threshold for health check.

* It means a backend server that continuously runs the specified number of health checks and returns all results as normal will be marked as normal.

* Unit: time(s). Range: 2\-10. Default: 3.

**HealthCheck.Timeout ** integer`optional` `Example: 2`

The response timeout of the health check.

* This indicates that if the backend server does not respond correctly within the specified time, the health check will be marked as exception.

* Unit: seconds. Range: 1\-60. Default: 2.

**HealthCheck.Method ** string`optional` `Example: HEAD`

Health check method. This parameter only takes effect when HealthCheck.Protocol is set to HTTP. Valid values:

* GET: The server must support the GET method.

* HEAD: The server returns only the HEAD header information, which can reduce backend performance consumption, the server must support the HEAD method.

**HealthCheck.Domain ** string`optional` `Example: www.test.com`

The domain name for health checks must be configured as the actual externally accessible address of the backend server. This parameter only takes effect when HealthCheck.Protocol is set to HTTP.

**HealthCheck.URI ** string`optional` `Example: health`

Health check path. It must be configured as the actual path provided on the backend server. Default: /. This parameter only takes effect when HealthCheck.Protocol is set to HTTP.

**HealthCheck.HttpCode ** string`optional` `Example: http_2xx,http_3xx`

The HTTP status codes considered healthy for health checks, with multiple status codes separated by commas (","). This parameter only takes effect when HealthCheck.Protocol is set to HTTP. Valid values:

* http_2xx

* http_3xx

* http_4xx

* http_5xx

**HealthCheck.HttpVersion ** string`optional` `Example: HTTP1.0`

The HTTP protocol version for health check, effective only when HealthCheck.Protocol is set to HTTP. Valid values:

* HTTP1.0 (default HTTP protocol version when using the API).

* HTTP1.1

**HealthCheck.Protocol** string `optional` `Example: HTTP`

Health check protocol.

* HTTP

* TCP

**Description ** string`optional` `Example: This is the default servergroup`

Description of the backend server group.

* Cannot start with http:// or https://.

* Must start with a letter or Chinese character and may include numbers, commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas (，), and Chinese periods (。).

* Must be 1 to 255 characters.

**HealthCheck.Interval ** integer`optional` `Example: 2`

The time interval for performing health checks. Unit: seconds. Range: 1\-300s. Default: 2.

**HealthCheck.Enabled ** string`optional` `Example: on`

Whether the listener has health check enabled. Valid values:

* on: Enable.

* off: Disable.

**Scheduler ** string`optional` `Example: wrr`

Scheduling algorithm. Valid values:

* wrr: Weighted Round Robin.

* wlc: Weighted Least Connection.

* sh: Source Address Hash.

**ServerGroupName ** string`optional` `Example: default_servergroup`

Name of the backend server group.

* Must start with a letter or Chinese character. May include numbers, periods (.), underscores (_), and hyphens (\-).

* Length limit: 1 to 128 characters.

* If this parameter is omitted or left unset, it defaults to server group ID.

**HealthCheck.Port ** integer`optional` `Example: 80`

Health check port. Valid values:

* 0: The port of the backend server is used for health checks.

* 1\-65535: Use the port you specify for health checks.

**CrossZoneEnabled ** string`optional` `Example: on`

Enable the cross\-az load balancing feature for the server group.

* Valid values:

   * on: Enable.

   * off: Disable.

* If you do not enable this feature, the server group can only be associated with Standard Edition ALB instances.

**SlowStartConfig.SlowStartEnabled ** string`optional` `Example: off`

Enable slow start feature. Valid values:

* on: Enable. When enabled, newly added healthy backend servers have their weight gradually increased from 0 to the configured value within a specified period, enabling smooth warmup. Limits:

   * Slow start is supported only when the scheduling algorithm is Weighted Round Robin (WRR).

   * A newly added healthy server enters slow start only when there are already healthy backend servers in the group.

* off: Disable.

> **tip**

> The slow start feature is in the invite\-only Beta. If you need a trial, please contact your account manager.

**SlowStartConfig.SlowStartDuration ** integer`optional` `Example: 30`

Slow start duration. Unit: second(s). Value range: 30\-900.

**ServerGroupId ** string必选`Example: rsp-bp1o94dp5i6ea****`

Backend server group ID.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** string`Example: 20210811152539010225146063030****`

Request ID.

## Request examples

```text
GET /?Action=ModifyServerGroupAttributes&ServerGroupId=rsp-1g1f1g8rwii****uxxxn4h9n&ServerGroupName=test&HealthCheck.HttpCode="http_2xx,http_3xx"&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20210816110638****2514606306AF947C",
        "Action": "ModifyServerGroupAttributes",
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
|400 |InvalidServerGroupName.Malformed |The specified ServerGroupName is malformed. |The specified ServerGroupName format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, 'HealthCheck.Domain'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as HealthCheck.Domain. |
|400 |InvalidHealthCheck.HttpVersion.Malformed |The specified HealthCheck.HttpVersion is malformed. |The specified HealthCheck.HttpVersion parameter format is invalid. |
|400 |InvalidServerGroup.InvalidStatus |The specified ServerGroup is not in the correct status for the request. |The specified server group is in a status that cannot respond to the request. |
|400 |InvalidLoadBalancer.InvalidStatus |The related LoadBalancer is not in the correct status for the request. |The associated ALB instance is in a state that cannot respond to this request. |
|400 |InvalidHealthCheck.Domain.Malformed |The specified HealthCheck.Domain is malformed. |The specified HealthCheck.Domain parameter format is invalid. |
|400 |InvalidHealthCheck.HttpCode.Malformed |The specified HealthCheck.HttpCode is malformed. |The specified HealthCheck.HttpCode format is invalid. |
|400 |InvalidHealthCheck.URI.Malformed |The specified HealthCheck.URI is malformed. |The specified HealthCheck.URI parameter format is invalid. |
|400 |InvalidHealthCheck.Method.Malformed |The specified HealthCheck.Method is malformed. |The specified HealthCheck.Method parameter format is invalid. |
|400 |InvalidHealthCheck.Protocol.Malformed |The specified HealthCheck.Protocol is malformed. |The specified HealthCheck.Protocol parameter format is invalid. |
|400 |InvalidHealthCheck.UnhealthyThreshold.Malformed |The specified HealthCheck.UnhealthyThreshold is malformed. |The specified HealthCheck.UnhealthyThreshold parameter format is invalid. |
|400 |InvalidHealthCheck.Timeout.Malformed |The specified HealthCheck.Timeout is malformed. |The specified HealthCheck.Timeout parameter format is invalid. |
|400 |OperationDenied.AccountArrears |The request on the specified resource is denied due to the account being in arrears status. |The request to operate on this resource was rejected because the account is in an overdue payment state. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format specified for Description is invalid. |
|400 |InvalidScheduler.Malformed |The specified Scheduler is malformed. |The specified Scheduler parameter format is invalid. |
|400 |InvalidStickySessionConfig.StickySessionEnabled.Malformed |The specified StickySessionConfig.StickySessionEnabled is malformed. |The specified StickySessionConfig.StickySessionEnabled parameter format is invalid. |
|400 |InvalidStickySessionConfig.StickySessionType.Malformed |The specified StickySessionConfig.StickySessionType is malformed. |The specified StickySessionConfig.StickySessionType parameter format is invalid. |
|400 |InvalidStickySessionConfig.Cookie.Malformed |The specified StickySessionConfig.Cookie is malformed. |The specified StickySessionConfig.Cookie parameter format is invalid. |
|400 |InvalidStickySessionConfig.CookieTimeout.Malformed |The specified StickySessionConfig.CookieTimeout is malformed. |The specified StickySessionConfig.CookieTimeout parameter format is invalid. |
|400 |InvalidHealthCheck.Enabled.Malformed |The specified HealthCheck.Enabled is malformed. |The specified HealthCheck.Enabled parameter format is invalid. |
|400 |InvalidHealthCheck.Interval.Malformed |The specified HealthCheck.Interval is malformed. |The specified HealthCheck.Interval parameter format is invalid. |
|400 |InvalidHealthCheck.HealthyThreshold.Malformed |The specified HealthCheck.HealthyThreshold is malformed. |The specified HealthCheck.HealthyThreshold parameter format is invalid. |
|400 |InvalidHealthCheckPort.Malformed |The specified HealthCheck.Port is malformed. |The specified HealthCheck.Port parameter format is invalid. |
|400 |InvalidProtocol.CrossZoneEnabled |The specified CrossZoneEnabled is malformed. |The specified CrossZoneEnabled format is invalid. |
|400 |OperationDenied.BackendServerRemoteOnNotSupport |The request on the specified BackendServer is denied due to enabling Remote is prohibited when cross\-zone forwarding disabled. |The operation request for this backend server was rejected because remote mode is not supported when cross\-AZ forwarding is disabled. |
|400 |OperationDenied.StickySessionConfigEnabledUnsupported |The request on the specified ServerGroup is denied due to enabling StickySessionConfig is prohibited when cross\-zone forwarding disabled. |Because session persistence cannot be enabled when cross\-AZ forwarding is disabled for the server group, the operation request for this server group was rejected. |
|400 |InvalidSlowStartConfig.SlowStartEnabled.Malformed |The specified SlowStartConfig.SlowStartEnabled is malformed. |The specified SlowStartConfig.SlowStartEnabled parameter format is invalid. |
|400 |InvalidSlowStartConfig.SlowStartDuration.Malformed |The specified SlowStartConfig.SlowStartDuration is malformed. |The specified SlowStartConfig.SlowStartDuration parameter format is invalid. |
|400 |InvalidScheduler.SlowStartEnabledMismatch |he specified Scheduler and SlowStartEnabled of ServerGroup do not match. Slow start only supports the WRR scheduling algorithm. |The specified scheduling algorithm does not match the slow start switch. Slow start is supported only with the WRR scheduling algorithm. |
|403 |Forbidden |You are not authorized to configure the ServerGroup with cross\-zone forwarding disabled. |No permission to disable cross\-AZ forwarding for the server group. |
|403 |Forbidden |You are not authorized to configure the ServerGroup with slow start config. |You do not have permission to enable slow start configuration for the server group. |
|404 |InvalidServerGroup.NotFound |The specified ServerGroup does not exist. |The specified server group does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
