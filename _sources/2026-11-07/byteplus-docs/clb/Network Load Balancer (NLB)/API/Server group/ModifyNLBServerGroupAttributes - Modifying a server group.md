---
title: "ModifyNLBServerGroupAttributes - Modifying a server group"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ModifyNLBServerGroupAttributes"
---

You can call the ModifyNLBServerGroupAttributes API to modify the name, description, or health check information of the server group.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

You can modify up to 20 backend servers in a single API call.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyNLBServerGroupAttributes&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

If an optional parameter in the table below is not provided, it indicates that the value of this parameter will retain its original configuration.



**Action ** <span data-label="purple">String </span><span data-api-tag="require|1reqVl">必选</span> `Example: ModifyNLBServerGroupAttributes`

Action to execute. Set the value to ModifyNLBServerGroupAttributes.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|dsK9MK">必选</span> `Example: 2020-04-01`

Current API version is 2020\-04\-01.



**ServerGroupId ** <span data-label="purple">String </span><span data-api-tag="require|2m1z1g">必选</span> `Example: rsp-bp1o94dp5i6ea****`

Server group ID.

You can call the [DescribeNLBServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeNLBServerGroups) API to get the server group ID.



**ServerGroupName ** <span data-label="purple">String </span>`optional` `Example: myservergroup`

Name of the server group.


* Must start with a letter, number, or Chinese character. May include the following symbols: periods (.), underscore (_), and hyphen (\-).

* Length limit is 1 to 128 characters.



**Description ** <span data-label="purple">String </span>`optional` `Example: This is a servergroup.`

Description of the server group.


* Must start with a letter, number, or Chinese character. It may contain the following special characters: comma ( , ), period ( . ), underscore ( _ ), space ( ), equal sign ( = ), hyphen ( \- ), full\-width comma ( ， ), and full\-width period ( 。 ).

* Length limit: 0 to 255 characters.



**Scheduler ** <span data-label="purple">String </span>`optional` `Example: wrr`

The rules followed by NLB when forwarding traffic.


* wrr (Weighted Round Robin): A load balancing algorithm where backend servers with higher weights values receive more frequent polling attempts (higher probability).

* wlc (Weighted Least Connection): This method maintains minimum connections and assigns a weight to each server based on its processing capacities of the server. Servers with higher weights receive a proportionally larger share of incoming requests.

* sh (Source address hashing): A consistency hash based on the Source IP address, allowing the same source to be scheduled to the same backend server.



**ConnectionDrainEnabled ** <span data-label="purple">Boolean </span>`optional` `Example: true`

Enable Connection Draining

Type the enumerated values strictly in the case form as follows. Do not set other values.


* true: Enable.

* false: Disable.



**ConnectionDrainTimeout ** <span data-label="purple">Integer </span>`optional` `Example: 60`

The timeout for connection draining ranges from 0 to 900 seconds.

When the parameter `ConnectionDrainEnabled` is changed from "false" to "true", this parameter is required.



**PreserveClientIpEnabled ** <span data-label="purple">Boolean </span>`optional` `Example: true`

Enable Source IP Preservation.

Type the enumerated values strictly in the case form as follows. Do not set other values.


* true: Enable. The packets forwarded by NLB to the backend server will carry the client's source IP address.

* false: Disable.



**SessionPersistenceEnabled** <span data-label="purple">Boolean</span> `optional` `Example: true`

Enable session persistence

Type the enumerated values strictly in the case form as follows. Do not set other values.


* true: Enable, supports session persistence based on source IP addresses.

* false: Disable.



**SessionPersistenceTimeout ** <span data-label="purple">Integer </span>`optional` `Example: 10`

The timeout period for session persistence ranges from 1 to 3600 seconds.



**ProxyProtocolType ** <span data-label="purple">String </span>`optional` `Example: off`

Enable the Proxy\-Protocol. Values:


* off: Disable.

* standard: Enable. NLB will forward the Source IP address of the client to the server using the Proxy\-Protocol; you also need to configure Proxy\-Protocol on the server.



**BypassSecurityGroupEnabled** <span data-label="purple">Boolean</span> `optional` `Example: true`

Enable **Allow Backend Security Group Traffic** feature. Only server\-type server groups can configure this parameter.


* true: Enable. The security group of backend servers in the server group no longer checks NLB traffic; it is allowed by default.

* false: Disabled.



**TimestampRemoveEnabled ** <span data-label="purple">Boolean </span>`optional` `Example: true`

Whether to enable the function of stripping TCP/HTTP/HTTPS packet timestamps.

Type the enumerated values strictly in the case form as follows. Do not set other values.


* true: Enable.

* false: Disable.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is currently in Beta stage. For trial requests, please contact your account manager.</div>




**HealthCheck.Enabled ** <span data-label="purple">Boolean </span>`optional` `Example: true`

Whether the health check feature is enabled for the listener.

Type the enumerated values strictly in the case form as follows. Do not set other values.


* true: Enable.

* false: Disable.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following parameters are valid only when the value of this parameter is "true".</div>




**HealthCheck.Type ** <span data-label="purple">String </span>`optional` `Example: TCP`

Health check type. Values:


* TCP: Send SYN handshake packets to detect whether the backend server port status is normal.

* HTTP: Send HEAD or GET requests to simulate browsing behavior and verify if the backend server application is functioning properly.

* UDP: Send ICMP or UDP probe packets to check if the backend server is functioning properly.



**HealthCheck.Port ** <span data-label="purple">String </span>`optional` `Example: 10`

The port for health check ranges from 1 to 65535.


* When the server group does not enable full port forwarding, this parameter defaults to 0, which indicates using the backend server's port for health check.

* When the server group enables all\-port forwarding, this parameter must be specified.



**HealthCheck.Method ** <span data-label="purple">String </span>`optional` `Example: GET`

Health check method. Values:


* GET: The server must support the GET method.

* HEAD: The server returns only the HEAD header information, which reduces backend overhead but requires the server to support the HEAD method.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>HealthCheck.Type</code> is set to "HTTP", this parameter takes effect.</div>




**HealthCheck.URI** <span data-label="purple">String</span> `optional` `Example: /`

Health check path.


* Must start with the character "/".

* It may contain letters, numbers, hyphens ( \- ), underscores ( _ ), slashes ( / ), periods ( . ), percent signs ( % ), question marks ( ? ), hash symbols ( # ), ampersands ( & ), and equal signs ( = ).

* Length limit: 1 to 128 characters.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>HealthCheck.Type</code> is set to "HTTP", this parameter takes effect.</div>




**HealthCheck.Domain ** <span data-label="purple">String </span>`optional` `Example: www.test`

The domain name for health checks must be configured as the actual externally accessible address of the server.


* Must contain at least one dot (.) and cannot start or end with a dot (.).

* Only uppercase and lowercase letters, digits, hyphens (\-), and periods (.) are supported. The hyphen '\-' cannot appear at the beginning or end of the string.

* Length limit: 1 to 80 characters.

* If this parameter is not provided, the private IP address of the backend server is used for health checks by default.



**HealthCheck.HttpCode ** <span data-label="purple">String </span>`optional` `Example: http_2xx,http_3xx`

The HTTP status code indicates a successful health check. Values:


* http_2xx

* http_3xx

* http_4xx

* http_5xx


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>HealthCheck.Type</code> is set to "HTTP", this parameter takes effect. Separate multiple status codes with commas (,).</div>




**HealthCheck.UdpRequest ** <span data-label="purple">String </span>`optional` `Example: Request123`

The request string for UDP health check.


* Only letters and digits are allowed, with a maximum length of 64 characters.

* This parameter takes effect when the parameter Protocol is set to UDP and the parameter HealthCheck.Enabled is set to on.

* The values of the parameters HealthCheck.UdpRequest and HealthCheck.UdpExpect must either both be empty or both be non\-empty.



**HealthCheck.UdpExpect ** <span data-label="purple">String </span>`optional` `Example: Expect123`

The expected response string for UDP health check.


* Only letters and digits are allowed, with a maximum length of 64 characters.

* This parameter takes effect when the parameter Protocol is set to UDP and the parameter HealthCheck.Enabled is set to on.

* The values of the parameters HealthCheck.UdpRequest and HealthCheck.UdpExpect must either both be empty or both be non\-empty.



**HealthCheck.Interval ** <span data-label="purple">Integer </span>`optional` `Example: 2`

The interval for the health check, with a value range of 1 to 300 seconds.



**HealthCheck.Timeout ** <span data-label="purple">Integer </span>`optional` `Example: 2`

The response timeout period for the health check ranges from 1 to 60 seconds.

If the backend server does not correctly respond within the specified time, the health check will be marked as "exception".



**HealthCheck.HealthyThreshold ** <span data-label="purple">Integer </span>`optional` `Example: 3`

The healthy threshold for the health check ranges from 2 to 10 times.

The backend server that continuously runs the specified number of health checks and returns all results as "normal" will be marked as "normal".



**HealthCheck.UnhealthyThreshold ** <span data-label="purple">Integer </span>`optional` `Example: 3`

Unhealthy threshold for health check ranges from 2 to 10 times.

The backend server that continuously runs the specified number of health checks and returns all results as "exception" will be marked as exception.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2024092952539010225146063030****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifyNLBServerGroupAttributes&Version=2020-04-01&ServerGroupId=rsp-bp1o94dp5i6ea****&ServerGroupName=myservergroup&Description=This is a servergroup.&Scheduler=wrr&ConnectionDrainEnabled=true&ConnectionDrainTimeout=60&PreserveClientIpEnabled=true&SessionPersistenceEnabled=true&SessionPersistenceTimeout=10&ProxyProtocolType=off&BypassSecurityGroupEnabled=true&TimestampRemoveEnabled=true&HealthCheck.Enabled=true&HealthCheck.Type=TCP&HealthCheck.Port=10&HealthCheck.Method=GET&HealthCheck.URI=/&HealthCheck.Domain=www.test&HealthCheck.HttpCode=http_2xx,http_3xx&HealthCheck.UdpRequest=Request123&HealthCheck.UdpExpect=Expect123&HealthCheck.Interval=2&HealthCheck.Timeout=2&HealthCheck.HealthyThreshold=3&HealthCheck.UnhealthyThreshold=3 HTTP/1.1
Host: clb.cn-beijing.byteplusapi.com.cn
Date: 20260310T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyNLBServerGroupAttributes",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2024092952539010225146063030****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/NLB-Common-Error-Codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidBypassSecurityGroupEnabled.Malformed |The specified BypassSecurityGroupEnabled is malformed. |The specified BypassSecurityGroupEnabled parameter format is invalid. |
|400 |InvalidBypassSecurityGroupEnabled.UnSupportAction |The specified Type of ServerGroup does not support this action. |The specified Server Group type does not support the current action. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken format is invalid. |
|400 |InvalidConnectionDrainEnabled.Malformed |The specified ConnectionDrainEnabled is malformed. |The specified ConnectionDrainEnabled parameter format is invalid. |
|400 |InvalidConnectionDrainTimeout.Malformed |The specified ConnectionDrainTimeout is malformed. |The specified ConnectionDrainTimeout parameter format is invalid. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format specified for Description is invalid. |
|400 |InvalidHealthCheck.Domain.Malformed |The specified HealthCheck.Domain is malformed. |The specified HealthCheck.Domain parameter format is invalid. |
|400 |InvalidHealthCheck.Enabled.Malformed |The specified HealthCheck.Enabled is malformed. |The specified HealthCheck.Enabled parameter format is invalid. |
|400 |InvalidHealthCheck.HealthyThreshold.Malformed |The specified HealthCheck.HealthyThreshold is malformed. |The specified HealthCheck.HealthyThreshold parameter format is invalid. |
|400 |InvalidHealthCheck.HttpCode.Malformed |The specified HealthCheck.HttpCode is malformed. |The specified HealthCheck.HttpCode parameter format is invalid. |
|400 |InvalidHealthCheck.Interval.Malformed |The specified HealthCheck.Interval is malformed. |The specified HealthCheck.Interval parameter format is invalid. |
|400 |InvalidHealthCheck.Method.Malformed |The specified HealthCheck.Method is malformed. |The specified HealthCheck.Method parameter format is invalid. |
|400 |InvalidHealthCheck.Port.Malformed |The specified HealthCheck.Port is malformed. |The specified HealthCheck.Port parameter format is invalid. |
|400 |InvalidHealthCheck.Timeout.Malformed |The specified HealthCheck.Timeout is malformed. |The specified HealthCheck.Timeout parameter format is invalid. |
|400 |InvalidHealthCheck.Type.Malformed |The specified HealthCheck.Type is malformed. |The specified HealthCheck.Type parameter format is invalid. |
|400 |InvalidHealthCheck.URI.Malformed |The specified HealthCheck.URI is malformed. |The specified HealthCheck.URI parameter format is invalid. |
|400 |InvalidHealthCheck.UdpExpect.Malformed |The specified HealthCheck.UdpExpect is malformed. |The specified HealthCheck.UdpExpect parameter format is invalid. |
|400 |InvalidHealthCheck.UdpRequest.Malformed |The specified HealthCheck.UdpRequest is malformed. |The specified HealthCheck.UdpRequest parameter format is invalid. |
|400 |InvalidHealthCheck.UdpRequestAndExpectMismatch |The HealthCheck UdpRequest is not matched with HealthCheck UdpExpect. |The UdpRequest and UdpExpect of the specified server group do not match. |
|400 |InvalidHealthCheck.UnhealthyThreshold.Malformed |The specified HealthCheck.UnhealthyThreshold is malformed. |The specified HealthCheck.UnhealthyThreshold parameter format is invalid. |
|400 |InvalidHealthCheckType.ServerGroupProtocolMismatch |The specified HealthCheck type is not matched with ServerGroup protocol. |The specified health check type does not match the server group protocol. |
|400 |InvalidPreserveClientIpEnabled.Malformed |The specified PreserveClientIpEnabled is malformed. |The specified PreserveClientIpEnabled parameter format is invalid. |
|400 |InvalidProxyProtocolType.Malformed |The specified ProxyProtocolType is malformed. |The specified ProxyProtocolType parameter format is invalid. |
|400 |InvalidScheduler.Malformed |The specified Scheduler is malformed. |The specified Scheduler parameter format is invalid. |
|400 |InvalidServerGroup.InvalidLoadBalancerBillingStatus |The related LoadBalancers of the specified ServerGroup are not in the correct billing status for the request. |The Classic Load Balancer (CLB) billing method associated with the specified server group is in a status that cannot respond to the request. |
|400 |InvalidServerGroup.InvalidStatus |The specified ServerGroup is not in the correct status for the request. |The specified server group is in a status that cannot respond to the request. |
|400 |InvalidServerGroupName.Malformed |The specified ServerGroupName is malformed. |The specified ServerGroupName format is invalid. |
|400 |InvalidServerGroupProxyProtocolType.UnSupportAction |The specified ProxyProtocolType of ServerGroup does not support this action. |The specified backend server group does not support the current action due to Proxy\-Protocol. |
|400 |InvalidSessionPersistenceEnabled.Malformed |The specified SessionPersistenceEnabled is malformed. |The specified SessionPersistenceEnabled parameter format is invalid. |
|400 |InvalidSessionPersistenceTimeout.Malformed |The specified SessionPersistenceTimeout is malformed. |The specified SessionPersistenceTimeout parameter format is invalid. |
|400 |InvalidTimestampRemoveEnabled.Malformed |The specified TimestampRemoveEnabled is malformed. |The specified TimestampRemoveEnabled parameter format is invalid. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |InvalidResourceType.ServiceManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidServerGroup.NotFound |The specified ServerGroup does not exist. |The specified server group does not exist. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
