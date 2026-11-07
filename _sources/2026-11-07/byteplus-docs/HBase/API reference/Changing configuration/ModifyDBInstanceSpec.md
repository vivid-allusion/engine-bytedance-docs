---
title: "ModifyDBInstanceSpec"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/ModifyDBInstanceSpec"
---

Call ModifyDBInstanceSpec to modify the specifications of the specified instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

During the node specification change process, the instance may be disconnected for 1 to 3 minutes. Please proceed with caution. It is recommended to perform conversion operation during off\-peak hours, and ensure clients are configured with proper retry mechanisms. For more details, see [Changing instance configuration](https://docs.byteplus.com/en/docs/HBase/Modify_configuration_instructions#.5Y-Y6YWN5pa55qGI).

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |hb\-cn01762cf4d6\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/HBase/DescribeDBInstances">DescribeDBInstances</a> interface to query the basic information of all HBase instances in the target region, including the instance ID.</div><br> |
|MasterSpec |String |No |hbase.x1.4xlarge |The specification code of the master node.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You must change the specification for at least the Master node or the RegionServer node. You can also change the specifications for both nodes.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For the specific specifications supported by HBase, see <a href="https://docs.byteplus.com/en/docs/HBase/Product_specifications">Product specifications</a>.</div><br> |
|RSSpec |String |No |hbase.x1.4xlarge |The specification code for the RegionServer node.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You must change the specification for at least the Master node or the RegionServer node. You can also change the specifications for both nodes.</div><br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |Ensures the idempotence of the request and prevents repeated submissions. The client generates this parameter value, which must be unique across requests. The value is case\-sensitive and must not exceed 127 ASCII characters. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |hb\-cn01762cf4d6\*\*\*\* |Instance ID. |
|OrderNo |String |Order716536510267754\*\*\*\* |Order ID. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=ModifyDBInstanceSpec&Version=2018-01-01 HTTP/1.1
Host: hbase.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/hbase/request,SignedHeaders=content-type;host;x-date,  Signature=****
{
    "MasterSpec": "hbase.x1.4xlarge",
    "RSSpec": "hbase.x1.4xlarge",
    "InstanceId": "hb-cn01762cf4d6****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2022111314111101017424420900E7****",
        "Action": "ModifyDBInstanceSpec",
        "Version": "2018-01-01",
        "Service": "hbase",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "hb-cn01762cf4d6****",
        "OrderNo": "Order716536510267754****"
    }
}
```
