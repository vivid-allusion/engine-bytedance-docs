---
title: "DescribeDBProxyConfig"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbproxyconfig"
---

Call the DescribeDBProxyConfig API to query the database proxy information of a specified MySQL instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDBProxyConfig&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-46609cf2\*\*\*\* |Instance ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|BinlogDump |Boolean |true |Indicates whether the binlog feature is supported. Possible values:<br><br><br>* `true`: yes.<br><br>* `false`: no.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is returned only after the database proxy is enabled.</div><br> |
|CheckModifyDBProxyAllowed |Object of [CheckModifyDBProxyAllowed](https://docs.byteplus.com/en/docs/40/15476#checkmodifydbproxyallowed) |Refer to the Sample response. |Indicates whether you can call the ModifyDBProxy API.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field is deprecated.</div><br> |
|CheckModifyDBProxyAllowedV2 |Array of [CheckModifyDBProxyAllowedV2](https://docs.byteplus.com/en/docs/40/15476#checkmodifydbproxyallowedv2) |Refer to the Sample response. |The check result of whether the ModifyDBProxy API is allowed to be executed. |
|ConnectionPoolType |String |Transaction |The connection pool type. This parameter is returned only after the database proxy is enabled. Value range:<br><br><br>* `Direct`: direct connection mode.<br><br>* `Transaction`: Transaction\-level connection pool. |
|DBProxyStatus |String |Creating |The state of the proxy instance. Values:<br><br><br>* `Creating`: proxy is enabling.<br><br>* `Running`: the database proxy is running.<br><br>* `Shutdown`: the database proxy is closed.<br><br>* `Deleting`: the database proxy is disabling.<br><br>* `Updating`: modifying.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is returned only when the database proxy feature for the instance is enabled,</div><br> |
|FeatureStates |Array of [FeatureStatesObject](https://docs.byteplus.com/en/docs/40/15476#featurestatesobject) |Refer to the Sample response. |Feature state. |
|GlobalReadOnly |Boolean |true |Whether to enable global read\-only.<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|InstanceId |String |mysql\-46609cf2\*\*\*\* |Instance ID. |
|ProxyResourceInfo |Object of [ProxyResourceInfo](https://docs.byteplus.com/en/docs/40/15476#proxyresourceinfo) |Refer to the Sample response. |Configuration of the database proxy for the instance. |


<span id="checkmodifydbproxyallowed"></span>
### CheckModifyDBProxyAllowed


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Allowed |Boolean |true |Indicates whether you can enable or disable the database proxy feature. Values:<br><br><br>* `true`: allowed.<br><br>* `false`: not allowed. |
|Reason |String |Other |When Allowed is `false`, this parameter returns the category of the reason why the database proxy cannot be enabled or disabled. |
|Message |String |The database proxy cannot be enabled or disabled because the instance is not in the Running state. |When Allowed is `false`, the specific reason why the database proxy cannot be enabled or disabled is returned. |


<span id="checkmodifydbproxyallowedv2"></span>
### CheckModifyDBProxyAllowedV2


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Allowed |Boolean |false |Indicates whether you can enable or disable the database proxy feature. Values:<br><br><br>* `true`: allowed.<br><br>* `false`: not allowed. |
|CheckItem |String |InstanceConfig |Check items for enabling or disabling the database proxy.<br><br><br>* `InstanceVersion`: instance version<br><br>* `InstanceStatus`: instance state<br><br>* `AllowlistLimit`: allowlist limit<br><br>* `InstanceConfig`: instance configuration<br><br>* `SystemConstraint`: system constraints<br><br>* `Other`: others |
|Reason |String |The transaction\-level connection pool is enabled for the current instance and does not support enabling or disabling the proxy |The detailed reason why the database proxy cannot be enabled or disabled. |


<span id="featurestatesobject"></span>
### FeatureStatesObject


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|FeatureName |String |ProxyBinlogDump |Function name. |
|Enable |Boolean |false |Whether it is enabled. Values:<br><br><br>* `true`: enable.<br><br>* `false`: disable. |
|Support |Boolean |true |Indicates whether the feature is supported. Values:<br><br><br>* `true`: supported.<br><br>* `false`: not supported. |


<span id="proxyresourceinfo"></span>
### ProxyResourceInfo


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|CurrentProxyCpuNum |Integer |2 |The current number of cores for the database proxy service of the instance. |
|MaxProxyCpuNum |Integer |1024 |The maximum number of cores that can be configured for the database proxy service. |
|MinProxyCpuNum |Integer |2 |The minimum number of cores that can be configured for the database proxy service. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeDBProxyConfig&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-46609cf2****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230809195305F4B9418A25C0D091AECF",
        "Action": "DescribeDBProxyConfig",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "BinlogDump": false,
        "CheckModifyDBProxyAllowed": {
            "Allowed": false,
            "Message": "当前实例已开启事务级连接池，不支持开关代理",
            "Reason": "Other"
        },
        "CheckModifyDBProxyAllowedV2": [
            {
                "Allowed": false,
                "CheckItem": "InstanceConfig",
                "Reason": "当前实例已开启事务级连接池，不支持开关代理"
            }
        ],
        "ConnectionPoolType": "Transaction",
        "DBProxyStatus": "Running",
        "FeatureStates": [
            {
                "Enable": false,
                "FeatureName": "ProxyBinlogDump",
                "Support": true
            }
        ],
        "GlobalReadOnly": false,
        "InstanceId": "mysql-46609cf2****",
        "ProxyResourceInfo": {
            "CurrentProxyCpuNum": 6,
            "MaxProxyCpuNum": 1024,
            "MinProxyCpuNum": 2
        }
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
