---
title: "DescribeNLBServerGroupAttributes - Viewing the server group details"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeNLBServerGroupAttributes"
---

Call the DescribeNLBServerGroupAttributes API to query details of a server group.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeNLBServerGroupAttributes&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|PKuU1s">必选</span> `Example: DescribeNLBServerGroupAttributes`

Action to execute. Set the value to DescribeNLBServerGroupAttributes.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|LbVURA">必选</span> `Example: 2020-04-01`

Current API version is 2020\-04\-01.



**ServerGroupId ** <span data-label="purple">String </span><span data-api-tag="require|Ru8692">必选</span> `Example: rsp-bp1o94dp5i6ea****`

Server group ID.

You can call the [DescribeNLBServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeNLBServerGroups) API to get the server group ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2024092952539010225146063030****`

Request ID.



**ServerGroupName ** <span data-label="purple">String </span>`Example: myservergroup`

Name of the server group.



**Description ** <span data-label="purple">String </span>`Example: test`

Description of the server group.



**ServerGroupId ** <span data-label="purple">String </span>`Example: rsp-bp1o94dp5i6ea****`

Server group ID.



**AccountId ** <span data-label="purple">String </span>`Example: 2100066126`

The account ID to which the server group belongs.



**Protocol ** <span data-label="purple">String </span>`Example: TCP`

The protocol used by NLB to forward traffic to backend server.


* TCP

* UDP



**Type ** <span data-label="purple">String </span>`Example: instance`

Server group type.


* instance: Server type. Support adding ECS instances and secondary network interfaces of associated ECS instances as servers.

* ip: IP address type. Support adding any network\-reachable VPC or IDC servers as servers.



**IpAddressVersion ** <span data-label="purple">String </span>`Example: ipv4`

IP version of the server group.



**Scheduler ** <span data-label="purple">String </span>`Example: wrr`

Scheduling algorithm.



**VpcId ** <span data-label="purple">String </span>`Example: vpc-p2ed5i6eaefh****`

The Virtual Private Cloud (VPC) ID to which the server group belongs.



**ServerCount ** <span data-label="purple">Integer </span>`Example: 1`

The number of backend servers in the server group.



**Servers ** <span data-label="purple">Object[] </span>`Example: --`

Information about backend servers in the server group.


**ServerId ** <span data-label="purple">String </span>`Example: rs-wgftyj4fk****`

The ID of the backend server.



**InstanceId ** <span data-label="purple">String </span>`Example: eni-wghjtfg4rth5****`

The instance ID or IP address of the backend server.



**Type ** <span data-label="purple">String </span>`Example: eni`

Type of backend server.


* ecs: Elastic Compute Service (ECS) instance (i.e., primary network interface)

* eni: Secondary network interface

* ip: IP address



**Weight ** <span data-label="purple">Integer </span>`Example: 100`

Weight of the backend server.


* Value range: 0 to 100.

* A weight of 0 indicates that requests will not be forwarded to this server.



**Ip ** <span data-label="purple">String </span>`Example: 192.XX.XX.3`

Private IP address of the backend server.



**Port ** <span data-label="purple">Integer </span>`Example: 80`

The port on which the backend server provides services.



**Description ** <span data-label="purple">String </span>`Example: test`

Description of the backend server.




**HealthCheck ** <span data-label="purple">Object </span>`Example: --`

Health check information of the backend server in the server group.


**Enabled ** <span data-label="purple">Boolean </span>`Example: true`

Whether the health check feature is enabled for the listener.


* true: Enable.

* false: Disable.



**Type ** <span data-label="purple">String </span>`Example: HTTP`

Health check type.


* TCP: Send SYN handshake packets to detect whether the backend server port status is normal.

* HTTP: Send HEAD or GET requests to simulate browsing behavior and verify if the backend server application is functioning properly.

* UDP: Send ICMP or UDP probe packets to check if the backend server is functioning properly.



**Port ** <span data-label="purple">Integer </span>`Example: 10`

Health check port.

0 indicates the port of the backend server is used for health checks.



**Interval ** <span data-label="purple">Integer </span>`Example: 2`

The interval for health check.



**HealthyThreshold ** <span data-label="purple">Integer </span>`Example: 3`

Health check healthy threshold.

The backend server that continuously runs the specified number of health checks and returns all results as "normal" will be marked as "normal".



**Timeout ** <span data-label="purple">Integer </span>`Example: 2`

The response timeout of the health check.

If the backend server does not respond correctly within the specified time, the health check will be marked as exception.



**Method ** <span data-label="purple">String </span>`Example: GET`

Health check method.


* GET: The server must support the GET method.

* HEAD: The server returns only the HEAD header information, which reduces backend overhead but requires the server to support the HEAD method.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only the parameter <code>Type</code> is set to HTTP, this parameter is returned.</div>




**Uri ** <span data-label="purple">String </span>`Example: /`

Health check path.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only the parameter <code>Type</code> is set to HTTP, this parameter is returned.</div>




**Domain ** <span data-label="purple">String </span>`Example: www.test`

Health check domain name.



**HttpCode ** <span data-label="purple">String </span>`Example: http_2xx, http_3xx`

The HTTP status code indicates a successful health check.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only the parameter <code>Type</code> is set to HTTP, this parameter is returned.</div>




**UdpRequest ** <span data-label="purple">String </span>`Example: Request123`

The request string for UDP health check.



**UdpExpect ** <span data-label="purple">String </span>`Example: Expect123`

The expected response string for UDP health check.



**UnhealthyThreshold ** <span data-label="purple">Integer </span>`Example: 3`

Unhealthy threshold for health check.

The backend server that continuously runs the specified number of health checks and returns all results as "exception" will be marked as "exception".




**RelatedLoadBalancerIds ** <span data-label="purple">String[] </span>`Example: ["nlb-qwdekht56fvb****", "nlb-wtglishtbg0oi****"]`

NLB instance associated with the server group.



**BypassSecurityGroupEnabled ** <span data-label="purple">Boolean </span>`Example: false`

Enable the **Allow Backend Security Group Traffic** feature.


* true: enable.

* false: Disabled.



**ProxyProtocolType ** <span data-label="purple">String </span>`Example: off`

Enable the Proxy\-Protocol. Valid values:


* off: Disable.

* standard: Enable. NLB will forward the Source IP address of the client to the server using the Proxy\-Protocol; you also need to configure Proxy\-Protocol on the server.



**AnyPortEnabled ** <span data-label="purple">Boolean </span>`Example: true`

Enable all\-port forwarding.


* true: Enable.

* false: Disable.



**ConnectionDrainEnabled ** <span data-label="purple">Boolean </span>`Example: true`

Enable Connection Draining


* true: enable.

* false: Disable.



**ConnectionDrainTimeout ** <span data-label="purple">Integer </span>`Example: 60`

Connection draining timeout period.



**PreserveClientIpEnabled ** <span data-label="purple">Boolean </span>`Example: true`

Enable Source IP Preservation.


* true: Enable.

* false: Disable.



**SessionPersistenceEnabled ** <span data-label="purple">Boolean </span>`Example: true`

Enable session persistence



**SessionPersistenceTimeout ** <span data-label="purple">Integer </span>`Example: 60`

Session persistence timeout period.



**TimestampRemoveEnabled ** <span data-label="purple">Boolean </span>`Example: false`

Whether to enable the function of stripping TCP/HTTP/HTTPS packet timestamps.


* true: enable.

* false: Disable.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is currently in Beta stage. For trial requests, please contact your account manager.</div>




**Tags ** <span data-label="purple">Object[] </span>`Example: --`

Tag information of the server group.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.




**ProjectName ** <span data-label="purple">String </span>`Example: default`

The name of the project to which the server group belongs.



**Status ** <span data-label="purple">String </span>`Example: Active`

Status of the server group.



**CreateTime ** <span data-label="purple">String </span>`Example: 2024-08-11T16:37:37Z`

Creation time of the server group.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2024-08-11T16:37:37Z`

Last modified time of the server group.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeNLBServerGroupAttributes&Version=2020-04-01&ServerGroupId=rsp-bp1o94dp5i6ea**** HTTP/1.1
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
        "Action": "DescribeNLBServerGroupAttributes",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "AccountId": "2100066126",
        "AnyPortEnabled": true,
        "BypassSecurityGroupEnabled": false,
        "ConnectionDrainEnabled": true,
        "ConnectionDrainTimeout": 60,
        "CreateTime": "2024-08-11T16:37:37Z",
        "Description": "test",
        "HealthCheck": {
            "Uri": "/",
            "Port": 10,
            "Type": "HTTP",
            "Domain": "www.test",
            "Method": "GET",
            "Enabled": true,
            "Timeout": 2,
            "HttpCode": "http_2xx,http_3xx",
            "Interval": 2,
            "UdpExpect": "Expect123",
            "UdpRequest": "Request123",
            "HealthyThreshold": 3,
            "UnhealthyThreshold": 3
        },
        "IpAddressVersion": "ipv4",
        "PreserveClientIpEnabled": true,
        "ProjectName": "default",
        "Protocol": "TCP",
        "ProxyProtocolType": "off",
        "RelatedLoadBalancerIds": [
            "nlb-qwdekht56fvb****",
            "nlb-wtglishtbg0oi****"
        ],
        "RequestId": "2024092952539010225146063030****",
        "Scheduler": "wrr",
        "ServerCount": 1,
        "ServerGroupId": "rsp-bp1o94dp5i6ea****",
        "ServerGroupName": "myservergroup",
        "Servers": [
            {
                "Ip": "192.XX.XX.3",
                "Port": 80,
                "Type": "eni",
                "Weight": 100,
                "ServerId": "rs-wgftyj4fk****",
                "InstanceId": "eni-wghjtfg4rth5****",
                "Description": "test"
            }
        ],
        "SessionPersistenceEnabled": true,
        "SessionPersistenceTimeout": 60,
        "Status": "Active",
        "Tags": [
            {
                "Key": "k1",
                "Value": "v1"
            }
        ],
        "TimestampRemoveEnabled": false,
        "Type": "instance",
        "UpdateTime": "2024-08-11T16:37:37Z",
        "VpcId": "vpc-p2ed5i6eaefh****"
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
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken format is invalid. |
|404 |InvalidServerGroup.NotFound |The specified ServerGroup does not exist. |The specified server group does not exist. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
