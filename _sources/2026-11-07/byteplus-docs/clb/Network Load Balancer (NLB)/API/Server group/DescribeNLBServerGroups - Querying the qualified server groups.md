---
title: "DescribeNLBServerGroups - Querying the qualified server groups"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeNLBServerGroups"
---

Call the DescribeNLBServerGroups API to query server groups that meet the specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeNLBServerGroups&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|LAUCbN">必选</span>`Example: DescribeNLBServerGroups`

Action to execute. Set the value to DescribeNLBServerGroups.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|9boEl6">必选</span> `Example: 2020-04-01`

Current API version is 2020\-04\-01.



**VpcId ** <span data-label="purple">String </span>`optional` `Example: vpc-bp1o94dp5i6ea****`

Virtual Private Cloud (VPC) ID to which the server belongs.



**ServerGroupName ** <span data-label="purple">String </span>`optional` `Example: myservergroup`

Name of the server group.



**Type ** <span data-label="purple">String </span>`optional` `Example: instance`

Server group type.



**ServerGroupIds.N ** <span data-label="purple">String </span>`optional` `Example: rsp-2fel9y8pxr56o5oxruuuu****`

Server group ID.


* Parameter \- N specifies the serial number of the server group. The value ranges from 1 to 20.

* Separate server group IDs with ampersands (&).



**InstanceIds.N ** <span data-label="purple">String </span>`optional` `Example: i-3tkuehz8oa3vj0wz****`

The ID of the backend server.


* Parameter \- N specifies the serial number of the backend server ID. The value ranges from 1 to 20.

* Separate multiple backend server IDs ampersands ( & ).



**ServerIps.N ** <span data-label="purple">String </span>`optional` `Example: 192.168.1.20`

The IP address of the backend server.


* Parameter \- N specifies the serial number of the backend server IP. The value ranges from 1 to 20.

* Separate server group IDs with ampersands (&).



**NextToken ** <span data-label="purple">String </span>`optional` `Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token that marks the position for paginated queries. Leave it empty for the initial call. For subsequent queries, set this value to the `NextToken` parameter returned by the previous API call.



**ProjectName ** <span data-label="purple">String </span>`optional` `Example: default`

The name of the project to which the server group belongs.



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The tag key. When multiple tag keys are specified, this action queries the server group associated with all of the provided tag keys.


* N specifies the serial number of a tag key. Values: 1\-10.

* Separate multiple tag keys with ampersands ( & ).



**TagFilters.N.Values.N ** <span data-label="purple">String </span>`optional` `Example: v1`

The tag value.


* The first N indicates the serial number of the tag key, valid values: 1 to 10.

* The second N indicates the serial number of the tag value, valid values: 1 to 3. The relationship between multiple tag values for the same tag key is a logical "OR". That is, the query returns resources tagged with any one of the specified values for that key.

* Separate multiple tags with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To provide this parameter, you must first provide <code>TagFilters.N.Key</code>.</div>


* <div data-tips="true" data-tips-type="tip">When an empty value is set for this parameter, it means querying resources where the tag value is empty under the specified tag key.</div>




**MaxResults ** <span data-label="purple">Integer </span>`optional` `Example: 10`

The number of query results. Default: 10. Maximum: 100.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2024092952539010225146063030****`

Request ID.



**NextToken ** <span data-label="purple">String </span>`Example: caeba0bbb2be03f84eb48b699f0a****`

The query token returned by this API call. An empty value indicates that there is no next page.



**ServerGroups ** <span data-label="purple">Object[] </span>`Example: --`

Detailed information about the eligible server groups.


**CreateTime ** <span data-label="purple">String </span>`Example: 2024-08-11T16:37:37Z`

Creation time of the server group.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2024-08-11T16:37:37Z`

Last modified time of the server group.



**AccountId ** <span data-label="purple">String </span>`Example: 2100066126`

The account ID to which the server group belongs.



**ProjectName ** <span data-label="purple">String </span>`Example: default`

The name of the project to which the server group belongs.



**ServerGroupId ** <span data-label="purple">String </span>`Example: rsp-bp1o94dp5i6ea****`

Server group ID.



**Protocol ** <span data-label="purple">String </span>`Example: TCP`

The protocol used by NLB to forward traffic to backend server.


* TCP

* UDP



**Status ** <span data-label="purple">String </span>`Example: Active`

Status of the server group.



**VpcId ** <span data-label="purple">String </span>`Example: vpc-p2ed5i6eaefh****`

The Virtual Private Cloud (VPC) ID to which the server group belongs.



**ServerGroupName ** <span data-label="purple">String </span>`Example: myservergroup`

Name of the server group.



**Type ** <span data-label="purple">String </span>`Example: instance`

Server group type.


* instance: Server type. Support adding Elastic Compute Service (ECS) instances and secondary network interfaces associated with ECS instances as backend servers.

* ip: IP address type. Support adding any network\-reachable VPC or IDC servers as backend servers.



**Description ** <span data-label="purple">String </span>`Example: test`

Description of the server group.



**Scheduler ** <span data-label="purple">String </span>`Example: wrr`

Scheduling algorithm.



**IpAddressVersion ** <span data-label="purple">String </span>`Example: ipv4`

IP version of the server group.



**AnyPortEnabled ** <span data-label="purple">Boolean </span>`Example: true`

Enable all\-port forwarding.



**ConnectionDrainEnabled ** <span data-label="purple">Boolean </span>`Example: true`

Enable Connection Draining



**ConnectionDrainTimeout ** <span data-label="purple">Integer </span>`Example: 60`

Connection draining timeout period.



**PreserveClientIpEnabled ** <span data-label="purple">Boolean </span>`Example: true`

Enable Source IP Preservation.



**SessionPersistenceEnabled ** <span data-label="purple">Boolean </span>`Example: true`

Enable session persistence



**SessionPersistenceTimeout ** <span data-label="purple">Integer </span>`Example: 60`

Session persistence timeout period.



**ProxyProtocolType ** <span data-label="purple">String </span>`Example: off`

Enable the Proxy\-Protocol. Valid values:


* off: Disable.

* standard: Enable. NLB will forward the Source IP address of the client to the server using the Proxy\-Protocol; you also need to configure Proxy\-Protocol on the server.



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



**interval ** <span data-label="purple">integer </span>`Example: 2`

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



**ServerCount ** <span data-label="purple">Integer </span>`Example: 1`

The number of backend servers in the server group.



**BypassSecurityGroupEnabled ** <span data-label="purple">Boolean </span>`Example: false`

Enable the **Allow Backend Security Group Traffic** feature.


* true: enable.

* false: Disabled.



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





&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeNLBServerGroups&Version=2020-04-01&VpcId=vpc-bp1o94dp5i6ea****&ServerGroupName=myservergroup&Type=instance&ServerGroupIds.1=rsp-2fel9y8pxr56o5oxruuuu****&InstanceIds.1=i-3tkuehz8oa3vj0wz****&ServerIps.1=192.168.1.20&NextToken=caeba0bbb2be03f84eb48b699f0a****&ProjectName=default&TagFilters.1.Key=k1&TagFilters.1.Values.1=v1&MaxResults=10 HTTP/1.1
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
        "Action": "DescribeNLBServerGroups",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "RequestId": "2024092952539010225146063030****",
        "ServerGroups": [
            {
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ],
                "Type": "instance",
                "VpcId": "vpc-p2ed5i6eaefh****",
                "Status": "Active",
                "Protocol": "TCP",
                "AccountId": "2100066126",
                "Scheduler": "wrr",
                "CreateTime": "2024-08-11T16:37:37Z",
                "UpdateTime": "2024-08-11T16:37:37Z",
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
                "ProjectName": "default",
                "ServerCount": 1,
                "ServerGroupId": "rsp-bp1o94dp5i6ea****",
                "AnyPortEnabled": true,
                "ServerGroupName": "myservergroup",
                "IpAddressVersion": "ipv4",
                "ProxyProtocolType": "off",
                "ConnectionDrainEnabled": true,
                "ConnectionDrainTimeout": 60,
                "RelatedLoadBalancerIds": [
                    "nlb-qwdekht56fvb****",
                    "nlb-wtglishtbg0oi****"
                ],
                "TimestampRemoveEnabled": false,
                "PreserveClientIpEnabled": true,
                "SessionPersistenceEnabled": true,
                "SessionPersistenceTimeout": 60,
                "BypassSecurityGroupEnabled": true
            }
        ]
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
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidMaxResult.Malformed |The specified MaxResult is malformed. |The specified MaxResult parameter format is invalid. |
|400 |InvalidMaxResults.Malformed |The specified MaxResults is malformed. |The specified MaxResults parameter format is invalid. |
|400 |InvalidNextToken.Malformed |The specified NextToken is malformed. |The specified NextToken parameter format is invalid. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|400 |InvalidServerGroupName.Malformed |The specified ServerGroupName is malformed. |The specified ServerGroupName format is invalid. |
|400 |InvalidServers.Ip.Malformed |The specified Servers.Ip is malformed. |The specified Servers.Ip parameter format is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue parameter format is invalid. |
|400 |InvalidType.Malformed |The specified Type is malformed. |The specified Type parameter format is invalid. |
|400 |LimitExceeded.ServerGroupId |You've reached the limit on the number of ServerGroupId that you can operate. |The maximum number of backend server group resources that can be operated on in a single request has been reached. |
|400 |LimitExceeded.ServerInstanceIdNumber |You've reached the limit on the number of description ServerInstanceId that you can operate. |The maximum number of server IDs that can be queried in a single request has been reached. |
|400 |LimitExceeded.ServerIpNumber |You've reached the limit on the number of description ServerIp that you can operate. |The maximum number of server IPs that can be queried in a single request has been reached. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of filter tag keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValues |You've reached the limit on the number of tag values that you can filter. |The maximum tag key\-value pairs for filtering in a single request has been reached. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
