---
title: "ListFunctions"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/ListFunctions"
---

Obtain function information in batch. Contains only the basic configuration of a function, but not the function code.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Request method: POST

* Request address: http://open.volcengineapi.com/?Action=ListFunctions&Version=2024\-06\-06


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListFunctions&serviceCode=vefaas&version=2024-06-06&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListFunctions |Interface name. The current API is called `ListFunctions`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06 `. |
|PageNumber |Integer |No |1 |Paging parameter, the current page number is default 1. |
|PageSize |Integer |No |10 |Paging parameter, the size per page is default 10. |
|Filters |Array of [Filter](https://docs.byteplus.com/en/docs/192/57185#filter) |No |[{"Name":"Ids","Values":["q06q\*\*\*\*","rx1b\*\*\*\*"]}] |Function filter criteria. |
|TagFilters |Array of [TagFilter](https://docs.byteplus.com/en/docs/192/57185#tagfilter) |No |[{"Key":"business","Values":["ecommerce"]}] |Function label. |


<span id="filter"></span>
### Filter


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|Name |String |No |Ids |Filter key (Key) for queries. Available values are as follows:<br><br><br>* **Id**: Function ID.<br><br>* **Ids**: Multiple function IDs.<br><br>* **Name**: Function name. |
|Values |Array of String |No |["q06\*\*\*\*","rx1\*\*\*\*"] |Filter value for the query (Value). Multiple values are separated by half\-width commas (`,`). |


<span id="tagfilter"></span>
### TagFilter


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|Key |String |No |business |Tag key specified when querying resources by tag. |
|Values |Array of String |No |["ecommerce"] |Tag value specified when querying resources by tag. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST http://open.volcengineapi.com/?Action=ListFunctions&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "PageNumber": 1,
    "PageSize": 10,
    "Filters": [
        {
            "Name": "Ids",
            "Values": [
                "q06q****",
                "rx1b****"
            ]
        }
    ],
    "TagFilters": [
        {
            "Key": "business",
            "Values": [
                "ecommerce"
            ]
        }
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Items |Array of [Function](https://docs.byteplus.com/en/docs/192/57185#function) |\- |Function list. |
|Total |Integer |180 |Total number of functions. |


<span id="function"></span>
### Function


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |pq\*\*\*\*\*\* |Function ID. |
|Envs |Array of [EnvVar](https://docs.byteplus.com/en/docs/192/57185#envvar) |\- |Function Environment variables. |
|Name |String |official\-site |Function name. |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/192/57185#tag) |\- |Function label. |
|Owner |String |22\*\*\*\*\*\* |Function owner (account Id). |
|Source |String |pqy\*\*\*\*\*\*/3kwem\*\*\*\*\*\*.zip |Code/image address entered by the user. |
|Runtime |String |python3.8/v1 |Function Runtime. |
|CodeSize |Integer |473 |Code package size. |
|MemoryMB |Integer |1,024 |Maximum memory per instance. |
|TlsConfig |Object of [TlsConfig](https://docs.byteplus.com/en/docs/192/57185#tlsconfig) |\- |Function logs configuration. |
|VpcConfig |Object of [VpcConfig](https://docs.byteplus.com/en/docs/192/57185#vpcconfig) |\- |VPC configuration. |
|NasStorage |Object of [NasStorage](https://docs.byteplus.com/en/docs/192/57185#nasstorage) |\- |FileNAS configuration. |
|SourceType |String |tos |Code Source type, supports tos, zip, image (allowlist account supports native/v1 custom image). |
|Description |String |Lightweight official website |Function description. |
|CreationTime |String |2024\-06\-14 15:31:07.143863441 +0800 CST m=+88714.902440864 |Function creation time. |
|InstanceType |String |nvidia\-tesla\-l4 |Function instance type.<br><br><br>* Null value: CPU instance type.<br><br>* Non\-null value: specific GPU instance type. |
|CodeSizeLimit |Integer |256 |The code package size limit:<br><br><br>* SourceType=zip，CodeSizeLimit=15MB.<br><br>* SourceType=tos，CodeSizeLimit=256MB. |
|ExclusiveMode |Boolean |false |Exclusive mode switch.<br><br><br>* true: Turn off multiple concurrent requests per instance, that is, the exclusive mode in which a single instance can only process one request at a time.<br><br>* false (default): Turn on multiple concurrent requests per instance, that is, the non\-exclusive mode where a single instance can handle multiple requests at the same time, and you can set the maximum number of concurrent requests that a single instance can carry through MaxConcurrency. |
|TriggersCount |Integer |0 |The number of triggers for this function. |
|InitializerSec |Integer |30 |Function initialization timeout configuration. |
|LastUpdateTime |String |2024\-06\-14 15:31:07.143863491 +0800 CST m=+88714.902440914 |Update time. |
|MaxConcurrency |Integer |100 |Single instance maximum concurrency. |
|RequestTimeout |Integer |30 |Request timed out (the unit is second). |
|SourceLocation |String |https://vefaas.tos\-s3\-cn.volces.com/template_dir/666ad75b9124c400072abcvefaas\-python3.9\-default.zip?X\-Amz\-\*\*\*\*\*\* |The source address of the code/image. |
|TosMountConfig |Object of [TosMountConfig](https://docs.byteplus.com/en/docs/192/57185#tosmountconfig) |\- |TOS Object Storage mount configuration. |
|Port |Integer |8,000 |Custom listening port for the instance, supported only in native/v1 runtime. |
|Command |String |./run.sh |Custom start command for the instance. Only supported by native/v1 runtime. |
|CpuStrategy |String |always |Function CPU billing policy, when the function is of microservices applications type, this field is `always`, indicating that at least one instance is running. |
|ProjectName |String |default |Function project name. |
|Cell |String |2 |The CELL that the function belongs to. |
|Role |String |trn:iam::1400000044:role/VeFaaSDefaultRole |Function instances bind to IAM role |
|FunctionType |String |sandbox |Function type. |
|EnableApmplus |Boolean |false |Turn on application Monitoring. |
|AsyncTaskConfig |Object of [AsyncTaskConfig](https://docs.byteplus.com/en/docs/192/57185#asynctaskconfig) |{"EnableAsyncTask":true,"MaxRetry":3,"DestinationConfig":{"OnFailure":{"Destination":"http://dummyinstanceid.apigateway\-cn\-beijing\-\*\*\*\*\*.volceapi.com/failure"},"OnSuccess":{"Destination":"http://dummyinstanceid.apigateway\-cn\-beijing\-inner.volceapi.com/success"}}} |Asynchronous task configuration. |


<span id="envvar"></span>
### EnvVar


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Key |String |business_type |The key of an environment variable for sandbox instances. |
|Value |String |free |The value of the environment variable for sandbox instances. |


<span id="tag"></span>
### Tag


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Key |String |business |Label key. |
|Value |String |ecommerce |Label value. |


<span id="tlsconfig"></span>
### TlsConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|EnableLog |Boolean |false |Whether to enable the logging feature. Parameter values:<br><br><br>* **true**: Turned on, the stdout/stderr logs of the function will be collected into the specified logs project and logs topic of the Torch Log Service.<br><br>* **false**: Turned off, the logs are not collected.  |
|TlsTopicId |String |0cd4e4c4\-5436\-4b05\-b39e\-\*\*\*\* |TLS Logs theme ID. |
|TlsProjectId |String |48f49d74\-cd50\-4591\-a3d0\-\*\*\*\* |TLS Logs project ID. |


<span id="vpcconfig"></span>
### VpcConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|EnableVpc |Boolean |false |Whether VPC access is enabled for the function. Parameter values:<br><br><br>* **false**: Disabled. The function can access the public network via the default network interface.<br><br>* **true**: Enabled. The function can access resources in the specified VPC. |
|VpcId |String |vpc\-2d73mgm\*\*\*\* |Function's VPC ID. |
|SubnetIds |Array of String |["subnet\-mj1l\*\*\*\*\*\*"] |Subnet ID corresponding to the function after turning on VPC access. |
|SecurityGroupIds |Array of String |["sg\-3re8ffwjclybk5zsk\*\*\*\*"] |Security group ID after the function turns on VPC access. |
|EnableSharedInternetAccess |Boolean |false |The switch for the function to access the public network. Whether to access the public network through the VPC shared NAT gateway of veFaaS. Parameter values:<br><br><br>* **true**: Turned on, access the public network through the default network interface card. Traffic charges will be incurred on the public network.<br><br>* **false**: Turned off, the function cannot access the public network through the default network interface card. |


<span id="nasstorage"></span>
### NasStorage


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|EnableNas |Boolean |false |Whether to turn on NAS storage mount. Parameter values:<br><br><br>* **true**: Turned on, store data to NAS.<br><br>* **false**: Do not turn on. |
|NasConfigs |Array of [NasConfig](https://docs.byteplus.com/en/docs/192/57185#nasconfig) |\- |NAS storage configuration. |


<span id="tosmountconfig"></span>
### TosMountConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|EnableTos |Boolean |false |Whether to turn on TOS storage mount. Parameter values:<br><br><br>* **true**: Turn on, store data in TOS.<br><br>* **false**: Do not turn on. |
|Credentials |Object of [Credentials](https://docs.byteplus.com/en/docs/192/57185#credentials) |\- |After enabling TOS storage mount, you need to provide an access key (AK/SK) with permission to access the TOS domain name. |
|MountPoints |Array of [TosMountPoint](https://docs.byteplus.com/en/docs/192/57185#tosmountpoint) |\- |After turning on TOS storage mount, you need to provide a list of TOS storage configurations. No more than 5. |


<span id="asynctaskconfig"></span>
### AsyncTaskConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|MaxRetry |Integer |3 |Number of asynchronous task retry attempts on failure. Selectable values are 0~3. |
|EnableAsyncTask |Boolean |true |Whether to turn on asynchronous tasks. |
|DestinationConfig |Object of [DestinationConfig](https://docs.byteplus.com/en/docs/192/57185#destinationconfig) |\- |Asynchronous task callback target configuration. |


<span id="nasconfig"></span>
### NasConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Gid |Long |1,000 |User group in the file system. Customization is currently not supported. If this parameter is provided, its value must be consistent with the function run user gid, and the value must be: 1000. |
|Uid |Long |1,000 |User in the file system. Customization is currently not supported. If this parameter is provided, the parameter value must be consistent with the function run user uid, and the value must be: 1000. |
|RemotePath |String |/ |File system remote directory. Length 1~128 characters, must start with "`/`", supports uppercase and lowercase letters, numbers, and special characters (`- . _ ~ / : @ = + ? #`). |
|FileSystemId |String |enas\-cns\*\*\*\*\*\* |NAS file system ID. |
|MountPointId |String |mount\-63\*\*\*\*\*\* |NAS mount point ID. |
|LocalMountPath |String |/mnt/nas |Function local mount directory. Length: 1–128 characters. Must start with "`/`", supports uppercase and lowercase letters, digits, and special characters (`- . _ ~ / : @ = + ? #`). |


<span id="credentials"></span>
### Credentials


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|AccessKeyId |String |\*\*\*\*\*\* |AccessKey ID (AK) of the BytePlus root user. For the obtaining method, please refer to the [Access key usage guide](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-access-keys). |
|SecretAccessKey |String |\*\*\*\*\*\* |Secret Access Key (SK) for the BytePlus root user. For the obtaining method, please refer to the [Access key usage guide](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-access-keys). |


<span id="tosmountpoint"></span>
### TosMountPoint


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Endpoint |String |http://tos\-cn\-beijing.ivolces.com |TOS accesses the domain name. |
|ReadOnly |Boolean |true |Function local directory permission. After mounting the TOS Bucket, whether the permission of the function's local mount directory is read\-only. Parameter values:<br><br><br>* **true**: Read only<br><br>* **false**(default): Read and write |
|BucketName |String |ai\-model |TOS bucket name |
|BucketPath |String |/ |The mount TOS Bucket path. |
|LocalMountPath |String |/mnt/tos |Function local mount directory. |


<span id="destinationconfig"></span>
### DestinationConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|OnFailure |Object of [Destination](https://docs.byteplus.com/en/docs/192/57185#destination) |\- |Callback target configuration when the task is executed successfully. |
|OnSuccess |Object of [Destination](https://docs.byteplus.com/en/docs/192/57185#destination) |\- |Callback target configuration when task execution fails. |


<span id="destination"></span>
### Destination


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Destination |String |http://dummyinstanceid.apigateway\-cn\-beijing\-\*\*\*\*.volceapi.com |Specific callback target. Setting the value to empty ("") disables the callback. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****",
        "Action": "ListFunctions", 
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "cn-beijing"
    },
    "Result": {
        "Items": [
            {
                "Id": "95hl16re",
                "Name": "official-site",
                "Description": "",
                "Runtime": "vefaas.base.python3.12.v1",
                "ExclusiveMode": false,
                "RequestTimeout": 30,
                "MaxConcurrency": 100,
                "MemoryMB": 1024,
                "CodeSizeLimit": 0,
                "SourceType": "tos",
                "VpcConfig": {
                    "EnableVpc": false
                },
                "CreationTime": "2024-07-02 05:46:38.444 +0000 UTC",
                "LastUpdateTime": "2024-07-02 05:46:38.444 +0000 UTC",
                "TlsConfig": {
                    "EnableLog": false
                },
                "ResourcePoolId": "ujdsugfffv",
                "Owner": "1400000044",
                "UseStatus": "",
                "DebugInstanceEnable": false,
                "InstanceType": "",
                "InitializerSec": 0,
                "MigrateToVciPublic": false,
                "EnableDumaInstance": false
            }
        ],
        "Total": 180
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There is no error code dedicated to this interface currently. If you encounter an exception when calling the interface, you can refer to [Public error codes](https://docs.byteplus.com/en/docs/faas/Public_error_code) for troubleshooting.
