---
title: "DescribeServerGroupAttributes - Querying the server group details"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeServerGroupAttributes"
---

Call the DescribeServerGroupAttributes API to view details of the specified backend server group.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeServerGroupAttributes&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|SzacpL">必选</span> `Example: DescribeServerGroupAttributes`

Action to execute. Set the value to **DescribeServerGroupAttributes**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|wF0Xg4">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**ServerGroupId ** <span data-label="purple">String </span><span data-api-tag="require|3b4lQH">必选</span> `Example: rsp-bp1o94dp5i6ea****`

Backend server group ID.

You can call the [DescribeServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeServerGroups) API to query the backend server group ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID.



**LoadBalancerId ** <span data-label="purple">String </span>`Example: clb-bp1o94dp5i6ea****`

ID of the CLB instance to which the backend server group belongs.



**ServerGroupId ** <span data-label="purple">String </span>`Example: rsp-bp1o94dp5i6ea****`

Backend server group ID.



**ServerGroupName ** <span data-label="purple">String </span>`Example: myservergroup`

Backend server group name.



**Description ** <span data-label="purple">String </span>`Example: test`

Description of the backend server group.



**Listeners ** <span data-label="purple">String[] </span>`Example: ["lsn-2fek3rgsxhrsw5oxruwec****"]`

Information about the listener associated with the backend server group.



**Servers ** <span data-label="purple">Object[] </span>`Example: -`

Information about servers in the backend server group.


**ServerId ** <span data-label="purple">String </span>`Example: rs-3cig8e5o0kxs06c6rrsqn****`

Backend server ID.



**InstanceId ** <span data-label="purple">String </span>`Example: i-3tkuehz8oa3vj0wz****`

ID of the ECS instance or network interface.



**Type ** <span data-label="purple">String </span>`Example: ecs`

Backend server instance type.


* ecs: Elastic Compute Service instance.

* eni: Secondary network interface.

* ip: IP address.



**Weight ** <span data-label="purple">Integer </span>`Example: 100`

Weight of the backend server.



**Ip ** <span data-label="purple">String </span>`Example: 192.XX.XX.2`

Private IP address of the backend server.



**Port ** <span data-label="purple">Integer </span>`Example: 88`

Port number on which the backend server receives requests.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the parameter AnyPortEnabled is set to "on", this parameter returns empty.</div>




**Description ** <span data-label="purple">String </span>`Example: This is a server.`

Description of the backend server.




**Type ** <span data-label="purple">String </span>`Example: instance`

Type of the backend server group.


* instance: Indicates that the backend server group can only add primary or secondary network interfaces of ECSs as backend servers.

* ip: Indicates that the backend server group can only add IP addresses as backend servers.



**AddressIpVersion ** <span data-label="purple">String </span>`Example: ipv4`

IP address type of the backend server group.


* ipv4: IPv4 type.

* ipv6: IPv6 type.

> The feature supporting IPv6 backends is currently in beta stage. If you need a trial, please contact your account manager.



**Tags ** <span data-label="purple">Object[] </span>`Example: -`

Tag information.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.




**AnyPortEnabled ** <span data-label="purple">String </span>`Example: on`

Enable full port forwarding for the backend server group.


* on: Enable.

* off: Disable.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is currently in beta stage. For trial requests, please contact your account manager.</div>




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeServerGroupAttributes&Version=2020-04-01&ServerGroupId=rsp-bp1o94dp5i6ea****
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
        "Action": "DescribeServerGroupAttributes",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "AddressIpVersion": "ipv4",
        "AnyPortEnabled": "on",
        "Description": "test",
        "Listeners": [
            "lsn-2fek3rgsxhrsw5oxruwec****"
        ],
        "LoadBalancerId": "clb-bp1o94dp5i6ea****",
        "RequestId": "20210811152539010225146063030****",
        "ServerGroupId": "rsp-bp1o94dp5i6ea****",
        "ServerGroupName": "myservergroup",
        "Servers": [
            {
                "Ip": "192.XX.XX.2",
                "Port": 88,
                "Type": "ecs",
                "Weight": 100,
                "ServerId": "rs-3cig8e5o0kxs06c6rrsqn****",
                "InstanceId": "i-3tkuehz8oa3vj0wz****",
                "Description": "This is a server."
            }
        ],
        "Tags": [
            {
                "Key": "k1",
                "Value": "v1"
            }
        ],
        "Type": "instance"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ServerGroupId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as ServerGroupId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|404 |InvalidServerGroup.NotFound |The specified ServerGroup does not exist. |The specified server group does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
