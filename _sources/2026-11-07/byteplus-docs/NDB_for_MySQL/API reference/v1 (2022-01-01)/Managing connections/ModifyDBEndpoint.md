---
title: "ModifyDBEndpoint"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBEndpoint"
---

Call the ModifyDBEndpoint to modify the connection endpoint.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The primary node endpoint **only supports** modifying the `EndpointName` and `Description` parameters. If values are provided for other parameters, they are ignored and no error is reported.

* The default endpoint **does not support** modifying the `ReadWriteMode`, `AutoAddNewNodes`, and `Nodes` parameters. If values are provided for these parameters, they are ignored and no error is reported.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBEndpoint&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-2pf2xk5v\*\*\*\* |Instance ID. |
|EndpointId |String |Yes |vedbm\-2pf2xk5v\*\*\*\*\-Custom\-50yv |Connection endpoint ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBEndpoint">DescribeDBEndpoint</a> API to get the details of the endpoint, including the endpoint ID.</div><br> |
|ReadWriteMode |String |No |ReadOnly |Endpoint read/write mode. Value:<br><br><br>* `ReadWrite`: Read/write endpoint.<br><br>* `ReadOnly`: Read\-only endpoint.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you modify the read/write mode, you need to provide a list of nodes in the Nodes parameter.</div><br> |
|EndpointName |String |No |Custom read\-only endpoint |The name of the instance connection endpoint. The endpoint name setting rules are as follows:<br><br><br>* Cannot start with digits or hyphen (\-).<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length is 1~64 characters. |
|Description |String |No |Description |Endpoint description. The length cannot exceed 200 characters. |
|Nodes |String |No |vedbm\-2pf2xk5v\*\*\*\*\-0,vedbm\-2pf2xk5v\*\*\*\*\-1 |The node IDs of the nodes associated with the connection endpoint. Separate multiple node IDs with commas (,). The rules are as follows:<br><br><br>* When you modify the `ReadWriteMode` from `ReadOnly` to `ReadWrite`, you must pass in the primary node. You can optionally pass in read\-only nodes.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is recommended to associate a primary node and at least one read\-only node. When only the primary node is associated, read\-write separation is not supported.   </div><br>   <br><br>* When you modify the `ReadWriteMode` from `ReadWrite` to `ReadOnly`, you can pass in one or more read\-only Nodes, but not the primary node.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Required when you modify the Read/Write mode of the endpoint, i.e., when the value of <code>ReadWriteMode</code> is changed.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceDetail">DescribeDBInstanceDetail</a> API to query the detailed information of a specified instance, including node IDs.</div><br> |
|AutoAddNewNodes |Boolean |No |true |Specifies whether to automatically add newly created read\-only nodes to the endpoint. Value:<br><br><br>* `true`: Joins automatically.<br><br>* `false`: Does not join automatically.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only default endpoints and custom endpoints support setting this parameter. The endpoint type can be determined from the <code>EndpointId</code>. If the <code>EndpointId</code> contains the <code>default</code> or <code>custom</code> field, the endpoint is a default endpoint or a custom endpoint.</div><br> |
|MasterAcceptReadRequests |Boolean |No |true |Primary node accepts read requests. Value range:<br><br><br>* `true`: (Default) When the **Primary node accepts read requests** function is enabled, non\-transactional read requests are sent to the primary node or read\-only node in a load\-balanced manner based on the number of active requests.<br><br>* `false`: When the **Primary node accepts read requests** function is disabled, the primary node only accepts transaction read requests, and non\-transaction read requests will not be sent to the primary node.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This is only valid for the default endpoint and custom Read/Write endpoints.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Modifications to the primary node accepts read requests feature take immediate effect on all connections.</div><br> |
|DistributedTransaction |Boolean |No |true |Specifies whether to enable transaction splitting. For more details, refer to [Transaction splitting](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Transaction_splitting). Value range:<br><br><br>* `true`: Enable (default).<br><br>* `false`: Disabled.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Transaction splitting is supported only when <code>ReadWriteMode</code> is set to <code>ReadWrite</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Changes to the transaction splitting state apply only to new connections. Existing connections retain their original configuration.</div><br> |
|ConsistLevel |String |No |Session |Consistency levels. For more information about consistency levels, see [Consistency levels](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Consistency_levels). Value range:<br><br><br>* `Eventual`: Eventual consistency.<br><br>* `Session`: Session consistency.<br><br>* `Global`: Global consistency.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When <code>ReadWriteMode</code> is set to <code>ReadWrite</code>, the available consistency levels are <code>Eventual</code>, <code>Session</code>, and <code>Global</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When <code>ReadWriteMode</code> is <code>ReadOnly</code>, the consistency level defaults to <code>Eventual</code> and cannot be changed.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The consistency level can be adjusted from eventual consistency to session consistency or global consistency, which takes effect only for new connections. When the session consistency or global consistency is adjusted to the eventual consistency, the existing connections take effect immediately.</div><br> |
|ConsistTimeout |Integer |No |10000 |When the delay is large, the timeout time for the read\-only node to synchronize the latest data, in units of us, ranges from 1us to 100000000us, and the default value is 10000us.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter takes effect only when <code>ConsistLevel</code> is set to <code>Global</code> or <code>Session</code>.</div><br> |
|ConsistTimeoutAction |String |No |ReadMaster |The read\-only node synchronization data timeout policy supports the following two policies:<br><br><br>* `ReturnError`: returns an SQL error (`wait replication complete timeout, please retry`).<br><br>* `ReadMaster`: sends the request to the primary node(default).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter takes effect only when <code>ConsistLevel</code> is set to <code>Global</code> or <code>Session</code>.</div><br> |
|ConnectionPool |String |No |Off |Set the connection pool based on your business scenario. For more information about the connection pool, refer to [Connection pool](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Connection_pool). Value range:<br><br><br>* `Off`: Disable the connection pool.<br><br>* `Session`: Enables the session\-level connection pool.<br><br>* `Transaction`: Enables the transaction\-level connection pool.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Changes to the connection pool configuration apply only to new connections.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Request example 1

Modify the Read\-only endpoint in the request example for the [CreateDBEndpoint](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateDBEndpoint#.6K-35rGC56S65L6L) API to a Read/Write endpoint. Set `ReadWriteMode` to `ReadWrite`, add the primary node ID to the `Nodes` parameter, set the consistency level to session consistency, and enable primary node accepts read requests and transaction splitting.

```json
POST /?Action=ModifyDBEndpoint&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceId": "vedbm-cxj2z00l****",
    "EndpointId": "vedbm-cxj2z00l****-Custom-wmes",
    "EndpointName": "只读终端修改为读写终端",
    "Nodes": "vvedbm-cxj2z00l****-0,vedbm-cxj2z00l****-1,vedbm-cxj2z00l****-2",
    "AutoAddNewNodes": true,
    "ReadWriteMode": "ReadWrite",
    "MasterAcceptReadRequests": true,
    "DistributedTransaction": true,
    "ConsistLevel": "Global",
    "ConsistTimeout": 20000,
    "ConsistTimeoutAction": "ReadMaster"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example 1

```json
{
    "ResponseMetadata": {
        "RequestId": "2023082311123288FB7868EDA41036FCD7",
        "Action": "ModifyDBEndpoint",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": null
}
```


<span id=".6K-35rGC56S65L6LLTI="></span>
### Request example 2

Modify the read/write endpoint from the preceding example to a read\-only endpoint. Set `ReadWriteMode` to `ReadOnly` and delete the primary node ID from the `Nodes` parameter.

```json
POST /?Action=ModifyDBEndpoint&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceId": "vedbm-cxj2z00l****",
    "EndpointId": "vedbm-cxj2z00l****-Custom-wmes",
    "EndpointName": "自定义终端",
    "Nodes": "vedbm-cxj2z00l****-1,vedbm-cxj2z00l****-2",
    "ReadWriteMode": "ReadOnly",
    "AutoAddNewNodes": true
}
```


<span id=".6L-U5Zue56S65L6LLTI="></span>
### Response example 2

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyDBEndpoint",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
