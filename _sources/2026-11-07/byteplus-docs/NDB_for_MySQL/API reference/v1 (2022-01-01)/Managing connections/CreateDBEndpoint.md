---
title: "CreateDBEndpoint"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateDBEndpoint"
---

Call the CreateDBEndpoint to create a connection endpoint for instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDBEndpoint&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-2pf2xk5v\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the Instance ID.</div><br> |
|EndpointType |String |Yes |Custom |Connection endpoint type. The value is fixed as `Custom`, which indicates a custom endpoint. |
|ReadWriteMode |String |No |ReadOnly |Endpoint read/write mode. Value:<br><br><br>* `ReadWrite`: Read/write endpoint.<br><br>* `ReadOnly`: Read\-only endpoint (Default). |
|EndpointName |String |No |Customized_endpoint |The name of the endpoint. The naming rules are as follows:<br><br><br>* Cannot start with digits or hyphen (\-).<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length is 1~64 characters. |
|Description |String |No |The description of the endpoint. |The description of the endpoint. The length cannot exceed 200 characters. |
|Nodes |String |No |vedbm\-2pf2xk5v\*\*\*\*\-0,vedbm\-2pf2xk5v\*\*\*\*\-1 |The node IDs associated with the endpoint. Use a comma (,) to separate multiple node IDs. The rules are as follows:<br><br><br>* When `ReadWriteMode` is set to `ReadWrite`, you must specify the primary node and can optionally specify one or more read\-only nodes.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is recommended to associate a primary node and at least one read\-only node. When only the primary node is associated, read\-write separation is not supported.   </div><br>   <br><br>* When `ReadWriteMode` is set to `ReadOnly`, you can specify one or more read\-only nodes.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceDetail">DescribeDBInstanceDetail</a> API to query the detailed information of a specified instance, including node IDs.</div><br> |
|AutoAddNewNodes |Boolean |No |true |Specifies whether to automatically add newly created read\-only nodes to the endpoint. Value:<br><br><br>* `true`: Joins automatically.<br><br>* `false`: Does not join automatically (Default). |
|MasterAcceptReadRequests |Boolean |No |true |Primary node accepts read requests. Value range:<br><br><br>* `true`: (Default) When the Primary node accepts read requests function is enabled, non\-transactional read requests are sent to the primary node or read\-only node in a load\-balanced manner based on the number of active requests.<br><br>* `false`: When the Primary node accepts read requests function is disabled, the primary node only accepts transaction read requests, and non\-transaction read requests will not be sent to the primary node.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Primary node accepts read requests is supported only when <code>ReadWriteMode</code> is set to <code>ReadWrite</code>.</div><br> |
|DistributedTransaction |Boolean |No |true |Specifies whether to enable transaction splitting. For more details, refer to [Transaction splitting](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Transaction_splitting). Value range:<br><br><br>* `true`: Enable (default).<br><br>* `false`: Disabled.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Transaction splitting is supported only when <code>ReadWriteMode</code> is set to <code>ReadWrite</code>.</div><br> |
|ConsistLevel |String |No |Session |Consistency levels. For more information about consistency levels, see [Consistency levels](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Consistency_levels). Value range:<br><br><br>* `Eventual`: Eventual consistency.<br><br>* `Session`: Session consistency.<br><br>* `Global`: Global consistency.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When <code>ReadWriteMode</code> is <code>ReadWrite</code>, the selectable consistency levels are <code>Eventual</code> (default), <code>Session</code>, and <code>Global</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When <code>ReadWriteMode</code> is <code>ReadOnly</code>, the consistency level defaults to <code>Eventual</code> and cannot be changed.</div><br> |
|ConsistTimeout |Integer |No |10000 |When the delay is large, the timeout time for the read\-only node to synchronize the latest data, in units of us, ranges from 1us to 100000000us, and the default value is 10000us.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter takes effect only when <code>ConsistLevel</code> is set to <code>Global</code> or <code>Session</code>.</div><br> |
|ConsistTimeoutAction |String |No |ReadMaster |The read\-only node synchronization data timeout policy supports the following two policies:<br><br><br>* `ReturnError`: returns an SQL error (`wait replication complete timeout, please retry`).<br><br>* `ReadMaster`: sends the request to the primary node(default).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter takes effect only when <code>ConsistLevel</code> is set to <code>Global</code> or <code>Session</code>.</div><br> |
|ConnectionPool |String |Yes |Off |Set the connection pool based on your business scenario. For more information about the connection pool, refer to [Connection pool](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Connection_pool). Value range:<br><br><br>* `Off`: Disable the connection pool (default).<br><br>* `Session`: Enables the session\-level connection pool.<br><br>* `Transaction`: Enables the transaction\-level connection pool. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|Name |Type |Example |Description |
|---|---|---|---|
|EndpointId |String |vedbm\-2pf2xk5v\*\*\*\*\-Custom\-50yv |The ID of the created connection endpoint. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Request example 1

Create a Read/Write endpoint, associate it with the primary node and read\-only node 1, set the consistency level to session consistency, and enable transaction splitting, primary node accepts read requests, and the automatic association of new nodes.

```json
POST /?Action=CreateDBEndpoint&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceId": "vedbm-iqnh3a7z****",
    "EndpointName": "自定义的读写终端",
    "EndpointType": "Custom",
    "Nodes": "vedbm-iqnh3a7z****-1,vedbm-iqnh3a7z****-0",
    "ReadWriteMode": "ReadWrite",
    "AutoAddNewNodes": true,
    "ConsistLevel": "Session",
    "DistributedTransaction": true,
    "MasterAcceptReadRequests": true,
    "ConsistTimeout": 10000,
    "ConsistTimeoutAction": "ReadMaster",
    "ConnectionPool": "Off"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example 1

```json
{
    "ResponseMetadata": {
        "RequestId": "20230424195109B8E5E7E8FA0AC9583F6E",
        "Action": "CreateDBEndpoint",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "EndpointId": "vedbm-2pf2xk5v****-Custom-50yv"
    }
}
```


<span id=".6K-35rGC56S65L6LLTI="></span>
### Request example 2

```json
POST /?Action=CreateDBEndpoint&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceId": "vedbm-cxj2z00l****",
    "EndpointName": "自定义只读终端",
    "EndpointType": "Custom",
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
        "RequestId": "20230424195109B8E5E7E8FA0AC9583F6E",
        "Action": "CreateDBEndpoint",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "EndpointId": "vedbm-2pf2xk5v****-Custom-50yv"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
