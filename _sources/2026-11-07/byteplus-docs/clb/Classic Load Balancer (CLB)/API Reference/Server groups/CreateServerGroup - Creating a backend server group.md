---
title: "CreateServerGroup - Creating a backend server group"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/CreateServerGroup"
---

Call the CreateServerGroup API to create a backend server group.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* Each CLB instance can create up to 200 backend server groups by default.

* Each API call can add up to 20 backend servers.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateServerGroup&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|mx5ANQ">必选</span> `Example: CreateServerGroup`

Action to execute. Set the value to **CreateServerGroup**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|vkpwrS">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**LoadBalancerId ** <span data-label="purple">String </span><span data-api-tag="require|hRCbR2">必选</span> `Example: clb-bp1b6c719dfa08ex****`

CLB instance.

You can call the [DescribeLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancers) API to query the ID of the CLB instance.



**ServerGroupName ** <span data-label="purple">String </span>`optional` `Example: myservergroup`

Backend server group name.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: periods (.), underscores (_), and hyphens (\-).

* Length limit: 1 to 128 characters.

* If left blank, defaults to the backend server group ID.



**Description ** <span data-label="purple">String </span>`optional` `Example: This is a servergroup.`

Description of the backend server group.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas ( ， ), and full\-width periods ( 。 ).

* The length limit is 0 to 255 characters.

* If left blank, it defaults to an empty string.



**AddressIpVersion ** <span data-label="purple">String </span>`optional` `Example: ipv4`

IP address type of the backend server group. Values:


* ipv4 (default): Indicates the backend server group is of IPv4 type.

* ipv6: Indicates the backend server group is of IPv6 type.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The feature supporting IPv6 backends is currently in beta stage. If you need a trial, please contact your account manager.</div>




**Type ** <span data-label="purple">String </span>`optional` `Example: instance`

Type of the backend server group. Values:


* instance (default): Elastic Compute Service instance.

* ip: IP address.

> The feature using an IP address as a backend server is currently in beta stage. If you need a trial, please contact your account manager.



**Servers.N.Type ** <span data-label="purple">String </span><span data-api-tag="require|UUspYi">必选</span> `Example: ecs`

Type of backend server.


* When the parameter `Type` is set to instance, the values are as follows:

   * ecs: Elastic Compute Service instance.

   * eni: Network interface.

* When the parameter `Type` is set to ip, this parameter takes the value ip.

* Parameter \- N: Indicates the serial number of the backend server. Value range: 1 to 20.



**Servers.N.InstanceId ** <span data-label="purple">String </span><span data-api-tag="require|Usl82j">必选</span> `Example: i-3tkuehz8oa3vj0wz****`

Backend server.


* Values:

   * When `Servers.N.Type` is set to ecs, pass the ID of the ECS instance. You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) API to query the ECS instance ID.

   * When `Servers.N.Type` is set to eni, pass the ID of the secondary ENI attached to the ECS. You can call the [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) API to query the network interface ID.

   * When `Servers.N.Type` is set to ip, pass the IP address as the backend server.

* Parameter \- N: Indicates the serial number of the backend server. Value range: 1 to 20.

* Separate multiple backend server IDs with ampersands (&).



**Servers.N.Weight ** <span data-label="purple">Integer </span>`optional` `Example: 100`

Weight of the backend server, with a value range of 0 to 100.


* If left blank, it defaults to 0. 0 indicates that requests will not be forwarded to this backend server.

* Parameter \- N: Indicates the serial number of the backend server. Value range: 1 to 20.



**Servers.N.Ip ** <span data-label="purple">String </span><span data-api-tag="require|MdKOpO">必选</span> `Example: 192.XX.XX.2`

Private IP address of the backend server.


* You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) API to get the private IP addresses of backend servers of type "ecs", and call the [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) API to get the private IP addresses of backend servers of type "eni".

* Parameter \- N: Indicates the serial number of the backend server. Value range: 1 to 20.

* Separate multiple backend server IPs with ampersands (&).



**AnyPortEnabled ** <span data-label="purple">String </span>`optional` `Example: on`

Enable full port forwarding for the backend server group.


* on: Enable.

* off (default): Disable.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is currently in Beta stage. For trial requests, please contact your account manager.</div>




**Servers.N.Port ** <span data-label="purple">Integer </span><span data-api-tag="require|hOZyzx">必选</span> `Example: 88`

Port number on which the backend server receives requests. Value range: 1 to 65535.

Parameter \- N: Indicates the serial number of the backend server. Value range: 1 to 20.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When the parameter AnyPortEnabled is set to "off" and you need to add backend servers at the same time, this parameter must be provided; when AnyPortEnabled is set to "on", this parameter defaults to 0.</div>


* <div data-tips="true" data-tips-type="tip">If you do not wish to add backend servers while creating the backend server group, you may omit this parameter.</div>


* <div data-tips="true" data-tips-type="tip">Separate multiple backend server IPs with ampersands (&).</div>




**Servers.N.Description ** <span data-label="purple">String </span>`optional` `Example: ecs1`

Description of the backend server.


* Parameter \- N: Indicates the serial number of the backend server. Value range: 1 to 20.

* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas ( ， ), and full\-width periods ( 。 ).

* The length limit is 0 to 255 characters.

* If left blank, it defaults to an empty string.



**Tags.N.Key ** <span data-label="purple">String </span>`optional` `Example: key1`

The tag key of the custom tag.


* N represents the sequence number of a tag key. Valid range: 1 to 20.

* Separate multiple tag keys with &.

* Must not start with `volc:` or `sys:` in any case form.

* Must be 1 to 128 characters. May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* If a tag key contains leading or trailing spaces, the system will automatically delete them.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Duplicate tag keys are not allowed for the same resource.</div>




**Tags.N.Value ** <span data-label="purple">String </span>`optional` `Example: value1`

The tag value of the custom tag.


* N represents the sequence number of a tag value. Valid range: 1–20.

* Separate multiple tag values with ampersands (&).

* Must be 0 to 256 characters. If left blank, this parameter defaults to an empty string.

* The following characters are allowed: characters from all languages, numbers, spaces ( ), underscores (_), periods (.), colons (:), forward slashes (/), equal signs (=), plus signs (+), hyphens (\-), and the at symbol (@).

* Case\-sensitive.

* If a tag value starts or ends with a space, the system will automatically delete it.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in <code>Tags.N.Key</code> first.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID.



**ServerGroupId ** <span data-label="purple">String </span>`Example: rsp-bp1o94dp5i6ea****`

Backend server group ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=CreateServerGroup&Version=2020-04-01&LoadBalancerId=clb-bp1b6c719dfa08ex****&Servers.1.Type=ecs&Servers.1.InstanceId=i-3tkuehz8oa3vj0wz****&Servers.1.Ip=192.XX.XX.2&Servers.1.Port=88
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateServerGroup",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210811152539010225146063030****",
        "ServerGroupId": "rsp-bp1o94dp5i6ea****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidAddressIpVersion.LoadBalancerMismatch |The specified AddressIpVersion and LoadBalancer are not matched. |The specified IP type does not match CLB. |
|400 |InvalidAddressIpVersion.Malformed |The specified AddressIpVersion is malformed. |The specified AddressIpVersion parameter format is invalid. |
|400 |InvalidAddressIpVersion.TypeMismatch |The specified AddressIpVersion and Type are not matched. |The specified IP type is incompatible with the server group type. |
|400 |InvalidAddressIpVersion.VpcMismatch |The specified AddressIpVersion and Vpc are not matched. |The specified IP type does not match VPC. |
|400 |InvalidAnyPortEnabled.Malformed |The specified AnyPortEnabled is malformed. |The specified AnyPortEnabled parameter format is invalid. |
|400 |InvalidBackendServer.ServerVpcMismatch |The specified BackendServer and Vpc are not matched. |The specified backend server does not match the VPC. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format specified for Description is invalid. |
|400 |InvalidEni.UnSupportAction |The specified Eni does not support this action. |The specified network interface does not support the current operation. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified load balancer cannot respond to this request due to its status. |
|400 |InvalidLoadBalancer.UnSupportAction |The specified LoadBalancer does not support this action. |The specified CLB does not support this action. |
|400 |InvalidName.Malformed |The specified Name is malformed. |The format specified for Name is invalid. |
|400 |InvalidProject.Malformed |The specified Project is malformed. |The format of the specified Project is invalid. |
|400 |InvalidQuotaCode.Malformed |The specified QuotaCode is malformed. |The specified QuotaCode parameter format is invalid. |
|400 |InvalidServer.Type |The specified Server type not match with ServerGroup. |The specified backend server type does not match the server group type. |
|400 |InvalidServerId.ServerIPMismatch |The specified serverIP and InstanceId are not matched. |The specified backend server ID does not match the IP. |
|400 |InvalidServerIp.UnSupportAction |The specified Server Ip does not support this action. |The specified backend server IP does not support the current operation. |
|400 |InvalidServers.Description.Malformed |The specified Servers.Description is malformed. |The specified Servers.Description parameter format is invalid. |
|400 |InvalidServers.Ip.Malformed |The specified Servers.Ip is malformed. |The specified Servers.Ip parameter format is invalid. |
|400 |InvalidServers.Port.Malformed |The specified Servers.Port is malformed. |The specified Servers.Port parameter format is invalid. |
|400 |InvalidServers.Type.Malformed |The specified Servers.Type is malformed. |The specified Servers.Type parameter format is invalid. |
|400 |InvalidServers.Weight.Malformed |The specified Servers.Weight is malformed. |The specified Servers.Weight parameter format is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue parameter format is invalid. |
|400 |InvalidType.Malformed |The specified Type is malformed. |The specified Type parameter format is invalid. |
|400 |LimitExceeded.ServerNumber |You've reached the limit on the number of add servers that you can operate |The maximum number of backend servers that can be operated on in a single request has been reached. |
|400 |LimitExceeded.ServiceManagedTag |You've reached the limit on the number of service managed tags that you can create. |You have reached the limit for the number of managed resource tag key\-value pairs that can be created in a single request. |
|400 |LimitExceeded.TagOperation |You've reached the limit on the number of tags that you can operate at a time. |You have reached the maximum number of tag entries that can be operated on in a single request. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'InstanceId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as InstanceId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'LoadBalancerId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as LoadBalancerId. |
|400 |QuotaExceed.ServerGroupNumberEachInstance |You've reached the limit on the number of ServerGroups that you can create. |The quota limit for the number of backend server groups that can be created has been reached. |
|400 |QuotaExceed.ServerNumberEachInstance |You've reached the limit on the number of Servers that you can create. |The quota limit for the number of backend servers that can be created has been reached. |
|400 |UnsupportedOperation.AccountArrears |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|403 |Forbidden |You are not authorized to perform operations on the service managed tag. |No permission to tag the specified resource with managed tags. |
|403 |Forbidden |You are not authorized to perform operations on the system tag. |No permission to tag the specified resource with a system tag. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |InvalidResourceType.ServcieManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidExclusiveCluster.NotFound |The specified ExclusiveCluster does not exist. |The specified Exclusive Cluster does not exist. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified load balancer does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidServer.NotFound |The specified Server does not exist. |The specified backend server does not exist. |
|404 |InvalidVPC.NotFound |The specified VPC does not exist. |The specified VPC does not exist. |
|409 |InvalidServer.Conflict |The specified Server already exists. |The specified backend server already exists. |
|412 |InvalidExclusiveCluster.Expired |The specified ExclusiveCluster has expired. |The specified Exclusive Cluster has expired. |
|412 |InvalidExclusiveCluster.UnPurchased |The specified ExclusiveCluster is not purchased. |The specified Exclusive Cluster is not purchased. |
|412 |InvalidLoadBalancer.Expired |The specified LoadBalancer has expired. |The specified CLB has expired. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
