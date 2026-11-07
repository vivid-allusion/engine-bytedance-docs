---
title: "DescribeDBEndpoint"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBEndpoint"
---

Call the DescribeDBEndpoint to query the details of the instance connection endpoint.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDBEndpoint&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-2pf2xk5v\*\*\*\* |Instance ID. |
|EndpointId |String |No |vedbm\-2pf2xk5v\*\*\*\*\-Custom\-50yv |Connection endpoint ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|Name |Type |Example |Description |
|---|---|---|---|
|Total |Integer |2 |Total number of connection endpoints. |
|Endpoints |Array of [EndpointObject](https://docs.byteplus.com/en/docs/265/57361#endpointobject) |Refer to the [Sample response](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBEndpoint#.6L-U5Zue56S65L6L). |Detailed information of the connection endpoint. |


<span id="endpointobject"></span>
### EndpointObject


|Name |Type |Example |Description |
|---|---|---|---|
|Addresses |Array of [AddressObject](https://docs.byteplus.com/en/docs/265/57361#addressobject) |Refer to the Sample response. |Address information. |
|AutoAddNewNodes |Boolean |true |Specifies whether to automatically associate new nodes. The valid values are:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |
|Description |String |Primary address |Address description. |
|EndpointId |String |vedbm\-h441603c68aaa\*\*\*\* |Instance endpoint ID. |
|EndpointName |String |Default_endpoint |The name of the instance connection endpoint. |
|EndpointType |String |Cluster |Connection endpoint type. The value can be:<br><br><br>* `Cluster`: Default endpoint.<br><br>* `Primary`: Primary node endpoint.<br><br>* `Custom`: Custom endpoint. |
|MasterAcceptReadRequests |Boolean |true |Whether the primary node accepts read requests. Only valid for endpoints in Read/Write mode.<br><br><br>* `true`: Yes.<br><br>* `false`: No. |
|NodeIds |Array of String |["vedbm\-r3sar8zi\*\*\*\*\-0", "vedbm\-r3sar8zi\*\*\*\*\-1"] |The list of nodes for the endpoint configuration. |
|ReadWriteMode |String |ReadWrite |The read/write mode of the endpoint. Valid values:<br><br><br>* `ReadWrite`: Read/Write.<br><br>* `ReadOnly`: Read\-only. |
|DistributedTransaction |Boolean |true |Specifies whether to enable transaction splitting. This parameter is valid only for endpoints in Read/Write mode. Value:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |
|ConsistLevel |String |Session |The consistency level, which is valid only for endpoints in Read/Write mode. Value:<br><br><br>* `Eventual`: Eventual consistency.<br><br>* `Session`: Session consistency.<br><br>* `Global`: Global consistency. |
|ConsistTimeout |Integer |10000 |When the delay is large, the timeout time for the read\-only node to synchronize the latest data, in units of us, ranges from 1us to 100000000us.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter takes effect only when <code>ConsistLevel</code> is set to <code>Global</code> or <code>Session</code>.</div><br> |
|ConsistTimeoutAction |String |ReadMaster |The read\-only node synchronization data timeout policy supports the following two policies:<br><br><br>* `ReturnError`: returns an SQL error (wait replication complete timeout, please retry).<br><br>* `ReadMaster`: sends the request to the primary node.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter takes effect only when <code>ConsistLevel</code> is set to <code>Global</code> or <code>Session</code>.</div><br> |
|ConnectionPool |String |Off |Connection pool state. For more information about connection pools, refer to [Connection pool](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Connection_pool). Value range:<br><br><br>* `Off`: Disables the connection pool.<br><br>* `Session`: Enables the session\-level connection pool.<br><br>* `Transaction`: Enables the transaction\-level connection pool. |


<span id="addressobject"></span>
### AddressObject


|Name |Type |Example |Description |
|---|---|---|---|
|DNSVisibility |Boolean |false |Resolution method. The current return value can only be `false` (Volcengine private network resolution). |
|Domain |String |vedbm\-fkfb7ag0\*\*\*\*.master.mysql.vedb.ivolces.com |The internal domain of the instance. |
|IPAddress |String |100. ** *.* ** .\*\*\* |IP address. |
|NetworkType |String |Private |Network type:<br><br><br>* `Private`: Virtual private cloud.<br><br>* `Public`: Public network access. |
|Port |String |3306 |The port for internal access to the instance. |
|SubnetId |String |subnet\-3tfam28a\*\*\*\* |Subnet ID. The subnet must belong to the selected availability zone. |
|EipId |String |eip\-13g56dc5u2uio3n6nu4kb\*\*\*\* |Public network ID. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```json
POST /?Action=DescribeDBEndpoint&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceId": "vedbm-53vb4ido****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230828164117A453591E8C1EBE492369",
        "Action": "DescribeDBEndpoint",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "Endpoints": [
            {
                "Addresses": [
                    {
                        "DNSVisibility": false,
                        "Domain": "vedbm-53vb4ido****.pri.mysql.vedb.ivolces.com",
                        "EipId": "",
                        "IPAddress": "192.***.***.120",
                        "NetworkType": "Private",
                        "Port": "3306",
                        "SubnetId": "subnet-3jhizp4kh5r0g3pncmfdh****"
                    }
                ],
                "AutoAddNewNodes": false,
                "ConsistLevel": "Global",
                "ConsistTimeout": 0,
                "ConsistTimeoutAction": "ReadMaster",
    "ConnectionPool": "Off"
                "Description": "主节点终端",
                "DistributedTransaction": false,
                "EndpointId": "vedbm-53vb4ido****-Primary",
                "EndpointName": "主节点终端",
                "EndpointType": "Primary",
                "MasterAcceptReadRequests": true,
                "NodeIds": [
                    "vedbm-53vb4ido****-1"
                ],
                "ReadWriteMode": "ReadWrite"
            },
            {
                "Addresses": [
                    {
                        "DNSVisibility": false,
                        "Domain": "vedbm-53vb4ido****.default.mysql.vedb.ivolces.com",
                        "EipId": "",
                        "IPAddress": "192.***.***.80",
                        "NetworkType": "Private",
                        "Port": "3306",
                        "SubnetId": "subnet-3jhizp4kh5r0g3pncmfdh****"
                    }
                ],
                "AutoAddNewNodes": true,
                "ConsistLevel": "Session",
                "ConsistTimeout": 20000,
                "ConsistTimeoutAction": "ReadMaster",
    "ConnectionPool": "Off"
                "Description": "默认终端",
                "DistributedTransaction": true,
                "EndpointId": "vedbm-53vb4ido****-ReadWriteSplit",
                "EndpointName": "默认终端",
                "EndpointType": "Cluster",
                "MasterAcceptReadRequests": true,
                "NodeIds": [
                    "vedbm-53vb4ido****-2",
                    "vedbm-53vb4ido****-1"
                ],
                "ReadWriteMode": "ReadWrite"
            },
            {
                "Addresses": [
                    {
                        "DNSVisibility": false,
                        "Domain": "vedbm-53vb4ido****.custom-mwn8.mysql.vedb.ivolces.com",
                        "EipId": "",
                        "IPAddress": "192.***.***.175",
                        "NetworkType": "Private",
                        "Port": "3306",
                        "SubnetId": "subnet-3jhizp4kh5r0g3pncmfdh****"
                    }
                ],
                "AutoAddNewNodes": true,
                "ConsistLevel": "Session",
                "ConsistTimeout": 10000,
                "ConsistTimeoutAction": "ReadMaster",
    "ConnectionPool": "Off"
                "Description": "",
                "DistributedTransaction": false,
                "EndpointId": "vedbm-53vb4ido****-Custom-mwn8",
                "EndpointName": "自定义终端",
                "EndpointType": "Custom",
                "MasterAcceptReadRequests": true,
                "NodeIds": [
                    "vedbm-53vb4ido****-0",
                    "vedbm-53vb4ido****-2",
                    "vedbm-53vb4ido****-1"
                ],
                "ReadWriteMode": "ReadWrite"
            }
        ],
        "Total": 3
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
