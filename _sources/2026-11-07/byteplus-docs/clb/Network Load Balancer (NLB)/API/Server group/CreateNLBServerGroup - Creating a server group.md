---
title: "CreateNLBServerGroup - Creating a server group"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/CreateNLBServerGroup"
---

You can call the CreateNLBServerGroup API to create a server group.

## Instructions

* Each NLB instance can create up to 200 server groups by default.

* You can add up to 20 backend servers in a single API call.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateNLBServerGroup&serviceCode=clb&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: CreateNLBServerGroup`

Action to execute. Set the value to CreateNLBServerGroup.

**Version ** String必选 `Example: 2020-04-01`

Current API version is 2020\-04\-01.

**ProjectName ** String`optional` `Example: default`

The name of the project to which the server group belongs.

**VpcId ** String必选 `Example: vpc-bp1b6c719dfa08ex****`

ID of the Virtual Private Cloud (VPC) to which the server group belongs.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to obtain the VPC ID.

**ServerGroupName ** String`optional` `Example: servergroup01`

Name of the server group.

* Must start with a letter, number, or Chinese character. May include the following symbols: periods (.), underscore (_), and hyphen (\-).

* Length limit: 1 to 128 characters.

* If this parameter is not provided, it defaults to the server group ID.

**Type ** String`optional` `Example: instance`

Server group type. Valid values:

* instance (default value): Server type. Support adding ECS instances and secondary network interfaces of associated ECS instances as backend servers.

* ip: IP address type. Support adding any network\-reachable VPC or IDC servers as backend servers.

**Protocol ** String必选 `Example: TCP`

The protocol used by NLB to forward traffic to backend server.

* TCP

* UDP

**Description ** String`optional` `Example: servergroup-test`

Description of the server group.

* Must start with a letter, number, or Chinese character. It may contain the following special characters: comma ( , ), period ( . ), underscore ( _ ), space ( ), equal sign ( = ), hyphen ( \- ), full\-width comma ( ， ), and full\-width period ( 。 )

* The length limit is 0 to 255 characters.

* If this parameter is not provided, it defaults to an empty string.

**Scheduler ** String`optional` `Example: wrr`

The rules followed by NLB when forwarding traffic. Valid values:

* wrr (default): Weighted Round Robin. A load balancing algorithm where backend servers with higher weights values receive more frequent polling attempts (higher probability).

* wlc (Weighted Least Connection): This method maintains minimum connections and assigns a weight to each server based on its processing capacities of the server. Servers with higher weights receive a proportionally larger share of incoming requests.

* sh (Source address hashing): A consistency hash based on the Source IP address, allowing the same source to be scheduled to the same backend server.

**IpAddressVersion ** String`optional` `Example: ipv4`

The IP address type of the server group. Valid values:

* ipv4 (default): Indicate that this server group only supports adding IPv4\-type backend servers.

* ipv6: Indicate that this server group only supports adding IPv6\-type backend servers.

> **tip**

> The NLB IPv6 feature is currently in the beta stage. To request a trial, please contact your account manager.

**AnyPortEnabled ** Boolean`optional` `Example: true`

Enable all\-port forwarding.

Type the enumerated values strictly in the case form as follows. Do not set other values.

* true: Enable. Backend servers within the group do not need to specify a port. By default, the NLB forwards traffic to the backend servers based on the listener port.

* false (default): Disable.

**ConnectionDrainEnabled ** Boolean`optional` `Example: true`

Enable Connection Draining

Please input the enumerated values strictly in case as follows, and do not pass in other values.

* true: Enable.

* false (default): Disable.

**ConnectionDrainTimeout ** Integer`optional` `Example: 60`

The timeout for connection draining ranges from 0 to 900 seconds.

When the parameter `ConnectionDrainEnabled` is set to "true", this parameter is required.

**PreserveClientIpEnabled ** Boolean`optional` `Example: true`

Enable Source IP Preservation.

Please strictly follow the case of the enumerated values below; do not pass any other values.

* true: Enable. The packets forwarded by NLB to the backend server will carry the client's source IP address.

* false: Disable.

> **tip**

* > The parameter `Type` is set to "instance", and the default value of this parameter is true.

* > The parameter `Type` is set to "ip", and the default value of this parameter is false.

**SessionPersistenceEnabled ** Boolean`optional` `Example: true`

Enable session persistence

Type the enumerated values strictly in the case form as follows. Do not set other values.

* true: Enable. NLB supports session persistence based on source IP addresses.

* false (default): Disable.

**SessionPersistenceTimeout ** Integer`optional` `Example: 10`

The timeout period for session persistence ranges from 1 to 3600 seconds, with a default value of 1000 seconds.

**ProxyProtocolType ** String`optional` `Example: off`

Enable Proxy\-Protocol protocol. Valid values:

* off (default): Disable.

* standard: Enable. The NLB will forward the client's source IP address to the backend servers using the Proxy\-Protocol. Additionally, the Proxy\-Protocol must be configured on the backend servers.

**BypassSecurityGroupEnabled ** Boolean`optional` `Example: true`

Enable the **Allow Backend Security Group** feature. This parameter can be configured only when the `Type` parameter is "instance".

* true: Enable. The security group of backend servers in the server group no longer checks NLB traffic; it is allowed by default.

* false (default): Not enabled.

**TimestampRemoveEnabled ** Boolean`optional` `Example: true`

Whether to enable the function of stripping TCP/HTTP/HTTPS packet timestamps.

Type the enumerated values strictly in the case form as follows. Do not set other values.

* true (default): Enable.

* false: Disable.

> **tip**

> This feature is currently in Beta stage. For trial requests, please contact your account manager.

**Tags.N.Key ** String`optional` `Example: k1`

The tag key of the custom tag.

* Parameter \- N: Indicates the serial number of the tag value, value range: 1 to 20. Separate multiple tag keys with ampersands (&).

* Must be 1 to 128 characters.

* Case\-sensitive. Must not start with `volc:` or `sys:` in any case form.

* Must not start or end with a space.

* May include letters, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), and at signs (@).

> **tip**

> Duplicate tag keys are not allowed for the same resource.

**Tags.N.Value ** String`optional` `Example: v1`

The tag value of the custom tag.

* Parameter \- N: Indicates the serial number of the tag value, value range: 1 to 20. Separate multiple tags with ampersands (&). Each tag key pairs one tag value.

* Must be 0 to 255 characters.

* Case\-sensitive. Must not start or end with a space.

* May include letters, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), minus signs (\-) and at signs (@).

> **tip**

> To provide this parameter, provide `Tags.N.Key` first.

**Servers.N.Type ** String必选 `Example: ecs`

Type of backend server.

* ecs: Elastic Compute Service instance.

* eni: Secondary network interface attached to the backend server.

* ip: IP address.

> **tip**

> When the server group type is "instance", this parameter can be set to "ecs" or "eni"; when the server group type is "ip", this parameter can be set to "ip".

**Servers.N.InstanceId ** String必选 `Example: i-2zebbhyczzaweeval****`

Backend servers to be added.

* When `Servers.N.Type` is set to "ecs", pass in the Elastic Compute Service (ECS) instance ID. You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) API to obtain the ECS instance ID.

* When `Servers.N.Type` is set to "eni", pass in the secondary network interface ID. You can call the [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) API to obtain the ENI ID.

* When `Servers.N.Type` is set to "ip", pass in the IP address of the backend server. Supported IP address ranges are `10.0.0.0/8`, `172.16.0.0/12`, and `192.168.0.0/16`.

**Servers.N.Ip ** String必选 `Example: 192.XX.XX.2`

Private IP address of the backend server.

* You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) API to obtain the private IP address of the backend server of type ecs.

* You can call the [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) API to obtain the private IP address of the backend server of type eni.

**Servers.N.Port ** Integer必选 `Example: 22`

Port used by the backend server to process requests. Value range: 1 to 65535.

* The parameter `AnyPortEnabled` is set to "false", indicating full port forwarding is disabled for the server group, this parameter is required.

* When the parameter `AnyPortEnabled` is set to "true", indicating full port forwarding is enabled for the server group, this parameter defaults to 0.

**Servers.N.Weight** Integer `optional` `Example: 100`

Weight of the backend server, with a value range of 0 to 100.

* A weight of 0 indicates that the NLB will not forward requests to this backend server.

* If this parameter is not provided, it defaults to 0.

**Servers.N.ZoneId ** String`optional` `Example: cn-beijing-a`

Availability zones from which the backend server receives access traffic.

When multiple availability zones are specified, regardless of whether cross\-az forwarding is enabled for the NLB, this backend server can receive access traffic from all specified availability zones.

**Servers.N.Description ** string`optional` `Example: ecs1`

Description of the backend server.

* Must start with a letter, number, or Chinese character. It may contain the following special characters: comma ( , ), period ( . ), underscore ( _ ), space ( ), equal sign ( = ), hyphen ( \- ), full\-width comma ( ， ), and full\-width period ( 。 ).

* Must be 1 to 255 characters.

* If this parameter is not provided, it defaults to an empty string.

**HealthCheck.Enabled ** Boolean`optional` `Example: true`

Whether to enable the health check feature. Valid values:

* true (default): Enable.

* false: Disable.

> **tip**

> The following parameters are valid only when the value of this parameter is "true".

**HealthCheck.Type ** String`optional` `Example: TCP`

The protocol type for health check. Valid values:

* TCP (default)

* HTTP

* UDP

**HealthCheck.Port ** String`optional` `Example: 10`

The port for health check ranges from 1 to 65535.

* When the server group does not enable full port forwarding, this parameter defaults to 0, which indicates using the backend server's port for health check.

* When the server group enables full port forwarding, this parameter must be specified.

**HealthCheck.Method ** String`optional` `Example: GET`

Health check method. Valid values:

* GET (default): The server must support the GET method.

* HEAD: The server returns only the HEAD header information, which reduces backend overhead but requires the server to support the HEAD method.

> **tip**

> Only when `HealthCheck.Type` is set to "HTTP", this parameter takes effect.

**HealthCheck.URI ** String`optional` `Example: /`

Health check path.

* Must start with the character "/".

* It may contain letters, numbers, hyphens ( \- ), underscores ( _ ), slashes ( / ), periods ( . ), percent signs ( % ), question marks ( ? ), hash symbols ( # ), ampersands ( & ), and equal signs ( = ).

* Length limit: 1 to 128 characters.

* If this parameter is not provided, it defaults to "/".

> **tip**

> When `HealthCheck.Type` is set to "HTTP", this parameter takes effect.

**HealthCheck.Domain ** String`optional` `Example: www.test`

The domain name for health checks must be configured as the actual externally accessible address of the server.

* Must contain at least one dot (.) and cannot start or end with a dot (.).

* Only uppercase and lowercase letters, digits, hyphens (\-), and periods (.) are supported. The hyphen '\-' cannot appear at the beginning or end of the string.

* Length limit: 1 to 80 characters.

* If this parameter is not provided, the private IP address of the backend server is used for health checks by default.

**HealthCheck.HttpCode ** String`optional` `Example: http_2xx,http_3xx`

The HTTP status code indicates a successful health check. Valid values:

* http_2xx

* http_3xx

* http_4xx

* http_5xx

> **tip**

> When `HealthCheck.Type` is set to "HTTP", this parameter takes effect. Separate multiple status codes with commas ( , ).

**HealthCheck.UdpRequest ** String`optional` `Example: Request123`

The request string for UDP health check.

* Only letters and digits are allowed, with a maximum length of 64 characters.

* This parameter takes effect when the parameter Protocol is set to UDP and the parameter HealthCheck.Enabled is set to on.

* The values of the parameters HealthCheck.UdpRequest and HealthCheck.UdpExpect must either both be empty or both be non\-empty.

**HealthCheck.UdpExpect ** String`optional` `Example: Expect123`

Expected response string for UDP health checks.

* Only letters and digits are allowed, with a maximum length of 64 characters.

* This parameter takes effect when the parameter Protocol is set to UDP and the parameter HealthCheck.Enabled is set to on.

* The values of the parameters HealthCheck.UdpRequest and HealthCheck.UdpExpect must either both be empty or both be non\-empty.

**HealthCheck.Interval** Integer `optional` `Example: 2`

The time interval for the health check. Value range: 1 to 300. Default value: 10 seconds.

**HealthCheck.Timeout ** Integer`optional` `Example: 2`

The response timeout period for the health check ranges from 1 to 60 seconds, with a default value of 3 seconds.

If the backend server does not correctly respond within the specified time, the health check will be marked as "exception".

**HealthCheck.HealthyThreshold ** Integer`optional` `Example: 3`

Healthy threshold of the health check, ranging from 2 to 10 times, with a default of 3 times.

The backend server that continuously runs the specified number of health checks and returns all results as "normal" will be marked as "normal".

**HealthCheck.UnhealthyThreshold ** Integer`optional` `Example: 3`

The unhealthy threshold of the health check, ranging from 2 to 10 times, with a default of 3 times.

The backend server that continuously runs the specified number of health checks and returns all results as "exception" will be marked as exception.

## Response parameters

**RequestId ** String`Example: 2024092952539010225146063030****`

Request ID.

**ServerGroupId ** String`Example: rsp-bp1o94dp5i6ea****`

Server group ID.

## Request examples

```json
GET /?Action=CreateNLBServerGroup&Version=2020-04-01&VpcId=vpc-bp1b6c719dfa08ex****&Protocol=TCP&Servers.1.Type=ecs&Servers.1.InstanceId=i-2zebbhyczzaweeval****&Servers.1.Ip=192.XX.XX.2&Servers.1.Port=22 HTTP/1.1 
Host: clb.cn-beijing.byteplusapi.com.cn 
Date: 20260310T094038Z 
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateNLBServerGroup",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2024092952539010225146063030****",
        "ServerGroupId": "rsp-bp1o94dp5i6ea****"
    }
}
```

## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/NLB-Common-Error-Codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidAnyPortEnabled.Malformed |The specified AnyPortEnabled is malformed. |The specified AnyPortEnabled parameter format is invalid. |
|400 |InvalidBackendServer.ServerVpcMismatch |The specified BackendServer and Vpc are not matched. |The specified backend server does not match the VPC. |
|400 |InvalidBypassSecurityGroupEnabled.Malformed |The specified BypassSecurityGroupEnabled is malformed. |The specified BypassSecurityGroupEnabled parameter format is invalid. |
|400 |InvalidBypassSecurityGroupEnabled.UnSupportAction |The specified Type of ServerGroup does not support this action. |The specified Server Group type does not support the current action. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken format is invalid. |
|400 |InvalidConnectionDrainEnabled.Malformed |The specified ConnectionDrainEnabled is malformed. |The specified ConnectionDrainEnabled parameter format is invalid. |
|400 |InvalidConnectionDrainTimeout.Malformed |The specified ConnectionDrainTimeout is malformed. |The specified ConnectionDrainTimeout parameter format is invalid. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format specified for Description is invalid. |
|400 |InvalidEni.UnSupportAction |The specified Eni does not support this action. |The specified network interface does not support the current operation. |
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
|400 |InvalidIPAddressVersion.TypeMismatch |The specified IPAddressVersion and Type are not matched. |The specified IP type is incompatible with the server group type. |
|400 |InvalidIPAddressVersion.VpcMismatch |The specified IPAddressVersion and Vpc are not matched. |The specified IP type does not match the VPC. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidIpAddressVersion.Malformed |The specified IpAddressVersion is malformed. |The specified IpAddressVersion format is invalid. |
|400 |InvalidPreserveClientIpEnabled.Malformed |The specified PreserveClientIpEnabled is malformed. |The specified PreserveClientIpEnabled parameter format is invalid. |
|400 |InvalidProject.Malformed |The specified Project is malformed. |The format of the specified Project is invalid. |
|400 |InvalidProtocol.Malformed |The specified Protocol is malformed. |The specified Protocol format is invalid. |
|400 |InvalidProxyProtocolType.Malformed |The specified ProxyProtocolType is malformed. |The specified ProxyProtocolType parameter format is invalid. |
|400 |InvalidQuotaCode.Malformed |The specified QuotaCode is malformed. |The specified QuotaCode parameter format is invalid. |
|400 |InvalidScheduler.Malformed |The specified Scheduler is malformed. |The specified Scheduler parameter format is invalid. |
|400 |InvalidServer.Type |The specified Server type not match with ServerGroup. |The specified backend server type does not match the server group type. |
|400 |InvalidServerGroupName.Malformed |The specified ServerGroupName is malformed. |The specified ServerGroupName format is invalid. |
|400 |InvalidServerId.ServerIPMismatch |The specified serverIP and InstanceId are not matched. |The specified backend server ID does not match the IP. |
|400 |InvalidServerIp.UnSupportAction |The specified Server Ip does not support this action. |The specified backend server IP does not support the current operation. |
|400 |InvalidServers.Description.Malformed |The specified Servers.Description is malformed. |The specified Servers.Description parameter format is invalid. |
|400 |InvalidServers.Ip.Malformed |The specified Servers.Ip is malformed. |The specified Servers.Ip parameter format is invalid. |
|400 |InvalidServers.Port.Malformed |The specified Servers.Port is malformed. |The specified Servers.Port parameter format is invalid. |
|400 |InvalidServers.Type.Malformed |The specified Servers.Type is malformed. |The specified Servers.Type parameter format is invalid. |
|400 |InvalidServers.Weight.Malformed |The specified Servers.Weight is malformed. |The specified Servers.Weight parameter format is invalid. |
|400 |InvalidServers.ZoneId.Malformed |The specified Servers.ZoneId is malformed. |The specified Servers.ZoneId parameter format is invalid. |
|400 |InvalidSessionPersistenceEnabled.Malformed |The specified SessionPersistenceEnabled is malformed. |The specified SessionPersistenceEnabled parameter format is invalid. |
|400 |InvalidSessionPersistenceTimeout.Malformed |The specified SessionPersistenceTimeout is malformed. |The specified SessionPersistenceTimeout parameter format is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey parameter format is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue parameter format is invalid. |
|400 |InvalidTimestampRemoveEnabled.Malformed |The specified TimestampRemoveEnabled is malformed. |The specified TimestampRemoveEnabled parameter format is invalid. |
|400 |InvalidType.Malformed |The specified Type is malformed. |The specified Type parameter format is invalid. |
|400 |LimitExceeded.ServerNumber |You've reached the limit on the number of add servers that you can operate |The maximum number of backend servers that can be operated on in a single request has been reached. |
|400 |LimitExceeded.ServiceManagedTag |You've reached the limit on the number of service managed tags that you can create. |You have reached the limit for the number of managed resource tag key\-value pairs that can be created in a single request. |
|400 |LimitExceeded.TagOperation |You've reached the limit on the number of tags that you can operate at a time. |You have reached the maximum number of tag entries that can be operated on in a single request. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'VpcId'. |This request is missing a required parameter. Confirm that this request contains all required parameters (such as VpcId). |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'InstanceId'. |This request does not contain required parameters. Please ensure the request includes all required parameters, such as InstanceId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ConnectionDrainTimeout'. |This request does not contain required parameters. Please ensure your API request includes all required parameters, such as ConnectionDrainTimeout. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'Protocol'. |This request is missing a required parameter. Please ensure your API request includes all required parameters, such as Protocol. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request does not contain required parameters. Ensure the request includes all required parameters, such as . |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'HealthCheck.Port'. |This request is missing a required parameter. Please ensure your API request includes all required parameters, such as HealthCheck.Port. |
|400 |QuotaExceed.ServerGroupNumber |You've reached the limit on the number of ServerGroups that you can create. |The quota limit for the number of backend server groups that can be created has been reached. |
|400 |QuotaExceed.ServerNumberEachServerGroup |You've reached the limit on the number of servers that you can create. |The quota limit for the number of backend servers that can be created in a single server group has been reached. |
|403 |Forbidden |You are not authorized to perform operations on the service managed tag. |No permission to tag the specified resource with managed tags. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |Forbidden |You are not authorized to perform operations on the system tag. |No permission to tag the specified resource with a system tag. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidServer.NotFound |The specified Server does not exist. |The specified backend server does not exist. |
|404 |InvalidSharedVPC.UnSupportAction |The specified shared VPC does not support this action. |The specified shared VPC does not support the current action. |
|404 |InvalidVPC.NotFound |The specified VPC does not exist. |The specified VPC does not exist. |
|404 |ServiceRoleForLoadBalancer.NotFound |ServiceRoleForLoadBalancer does not exist. |The service\-attached role of the load balancer does not exist. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|409 |InvalidServer.Conflict |The specified Server already exists. |The specified backend server already exists. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
