---
title: "CreateFunction"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/CreateFunction"
---

Create a function, including function configurations and function code.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Request method: POST

* Request address: http://open.volcengineapi.com/?Action=CreateFunction&Version=2024\-06\-06


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateFunction&serviceCode=vefaas&version=2024-06-06&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateFunction |Interface name. The current API is called `CreateFunction`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06 `. |
|Name |String |Yes |official\-site |Function name.<br><br><br>* The function name must be only in the same account.<br><br>* It supports uppercase and lowercase English letters, numbers, dashes (\-), and underscores (_), the length limit is 4 to 64 characters. |
|Description |String |No |Lightweight official website |Function description. The length limit is 1,000 Unicode characters or less. |
|Runtime |String |Yes |python3.8/v1 |Function Runtime. Available values:<br><br><br>* **golang/v1**<br><br>* **native/v1**<br><br>* **nativejava8/v1**<br><br>* **node14/v1**<br><br>* **node20/v1**<br><br>* **nodeprime14/v1**<br><br>* **python3.12/v1**<br><br>* **python3.8/v1**<br><br>* **python3.9/v1**<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>SourceType = image</code>, the runtime must be <code>native/v1</code>.</div><br> |
|ExclusiveMode |Boolean |No |false |Exclusive mode switch. Available values:<br><br><br>* **true**: Turn off multiple concurrent requests per instance, that is, the exclusive mode in which a single instance can only process one request at a time.<br><br>* **false**: (default) Turn on multiple concurrent requests per instance, that is, the non\-exclusive mode in which a single instance can handle multiple requests at the same time, and you can set the maximum number of concurrent requests that a single instance can carry through MaxConcurrency. |
|RequestTimeout |Integer |No |30 |Request timed out.<br><br><br>* Unit: second.<br><br>* Value range: 1 to 900.<br><br>* Default value: 30. |
|MaxConcurrency |Integer |No |100 |Single instance maximum concurrency. It takes effect when `ExclusiveMode = false`.<br><br><br>* Value range: 10~1,000.<br><br>* Default value: 100. |
|MemoryMB |Integer |No |1,024 |Maximum memory per instance.<br><br><br>* Unit: MiB.<br><br>* Value range: 512~4,096.<br><br>   <div data-tips="true" data-tips-type="default">Description   </div><br>   <br><br><br><div data-tips="true" data-tips-type="default">The value takes 512 as the gradient.</div><br><br><br><br>* Default value: 1,024. |
|SourceType |String |No |tos |Code source type, optional values are:<br><br><br>* tos: Torch Object Storage.<br><br>* zip: Local compressed file.<br><br>* image: Container Registry. |
|Source |String |No |pqyqo9qa/3kwem\*\*\*\*\*\*.zip |Code source, value:<br><br><br>* **zip**: Base64 encoded binary ZIP file.<br><br>* **tos**: String in the format `bucket_name: object_key`, e.g.: `vefaas-test: vefaas-python38-default.zip`.<br><br>* **image**: The image address in the format `host/namespace/repo: tag`. E.g.: `cp-enterprise-cn-beijing.cr.volces.com/demo/nginx: latest`. |
|Envs |Array of [EnvVar](https://docs.byteplus.com/en/docs/192/57177#envvar) |No |\- |Environment variables. |
|VpcConfig |Object of [VpcConfig](https://docs.byteplus.com/en/docs/192/57177#vpcconfig) |No |\- |Virtual Private Cloud (VPC) configuration. |
|TlsConfig |Object of [TlsConfig](https://docs.byteplus.com/en/docs/192/57177#tlsconfig) |No |\- |Torch Log Service (TLS) relevant configuration. |
|SourceAccessConfig |Object of [SourceAccessConfig](https://docs.byteplus.com/en/docs/192/57177#sourceaccessconfig) |No |\- |Container Registry access configuration.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You need to provide access configuration when setting custom images across accounts.</div><br> |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/192/57177#tag) |No |\- |Function label. |
|NasStorage |Object of [NasStorage](https://docs.byteplus.com/en/docs/192/57177#nasstorage) |No |\- |FileNAS mount configuration. |
|TosMountConfig |Object of [TosMountConfig](https://docs.byteplus.com/en/docs/192/57177#tosmountconfig) |No |\- |Torch Object Storage (TOS) mount configuration. |
|InitializerSec |Integer |No |30 |Function initialization timeout configuration. |
|Command |String |No |./run.sh |Custom start command for the instance (currently only supports native/v1 runtimes). |
|Port |Integer |No |8,000 |Custom listening port for the instance (currently only native/v1 runtime is supported). |
|CpuStrategy |String |No |always |Function CPU billing policy, when creating a function of microservices applications type, this field must be set to `always` to indicate that at least one instance is running. |
|ProjectName |String |No |default |Function associated project name. |
|CpuMilli |Integer |No |10 |Maximum CPU per instance, unit: milli CPU. 1 milli CPU = 0.001 CPU。 When the function's compute mode is CPU instance, you can configure the CPU specification for a single CPU instance. |
|Cell |String |No |2 |Specify the CELL cluster to which the function is assigned. |
|Role |String |No |trn:iam::140\*\*\*\*\*\*:role/VeFaaSDefaultRole |Function instances bind IAM role. |
|EnableApmplus |Boolean |No |true |Enable application monitoring. |
|AsyncTaskConfig |Object of [AsyncTaskConfig](https://docs.byteplus.com/en/docs/192/57177#asynctaskconfig) |No |{"EnableAsyncTask":true,"MaxRetry":3,"DestinationConfig":{"OnFailure":{"Destination":"http://dummyinstanceid.apigateway\-cn\-beijing\-\*\*\*\*.\*\*\*\*.com/failure"},"OnSuccess":{"Destination":"http://dummyinstanceid.apigateway\-cn\-beijing\-\*\*\*\*\*.\*\*\*\*\*.com/success"}}} |Asynchronous task configuration. |


<span id="envvar"></span>
### EnvVar


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |business_type |The key of an environment variable for sandbox instances. |
|Value |String |Yes |free |The value of the environment variable for sandbox instances. |


<span id="vpcconfig"></span>
### VpcConfig


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|EnableVpc |Boolean |Yes |false |Whether the function turns on VPC access. Parameter values:<br><br><br>* **false**: Disabled. The function can access the public network via the default network interface.<br><br>* **true**: Enabled. The function can access resources in the specified VPC. |
|VpcId |String |No |vpc\-2d73mgm\*\*\*\* |ID of the Virtual Private Cloud to which the function belongs. |
|SubnetIds |Array of String |No |["subnet\-mj1l\*\*\*\*\*\*"] |Subnet ID after the function enables VPC access. |
|SecurityGroupIds |Array of String |No |["sg\-3re8ffwjclybk5zsk\*\*\*\*"] |Security group ID corresponding to the function after VPC access is enabled. |
|EnableSharedInternetAccess |Boolean |No |false |The switch for the function to access the public network. Whether to access the public network through veFaaS's VPC shared NAT gateway. Parameter values:<br><br><br>* **true**: Turned on, access the public network through the default network interface card. Traffic charges will be incurred on the public network.<br><br>* **false**: Turned off, the function cannot access the public network through the default network interface card. |


<span id="tlsconfig"></span>
### TlsConfig


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|EnableLog |Boolean |Yes |false |Whether to enable the log feature, parameter values:<br><br><br>* **true**: Turned on, the stdout/stderr logs of the function will be collected into the specified logs project and logs topic of the Torch Log Service.<br><br>* **false**: Turned off, the logs are not collected.  |
|TlsTopicId |String |No |0cd4e4c4\-5436\-4b05\-b39e\-\*\*\*\* |TLS Logs theme ID. |
|TlsProjectId |String |No |48f49d74\-cd50\-4591\-a3d0\-\*\*\*\* |TLS Logs project ID. |


<span id="sourceaccessconfig"></span>
### SourceAccessConfig


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|Password |String |Yes |password |Container Registry password. |
|Username |String |Yes |operator |Container Registry user name. |


<span id="tag"></span>
### Tag


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |business |Label key. |
|Value |String |Yes |ecommerce |Label value. |


<span id="nasstorage"></span>
### NasStorage


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|EnableNas |Boolean |Yes |false |Whether to turn on NAS storage mount, parameter values:<br><br><br>* **true**: Turned on, store data to NAS.<br><br>* **false**: Do not turn on. |
|NasConfigs |Array of [NasConfig](https://docs.byteplus.com/en/docs/192/57177#nasconfig) |No |\- |NAS storage configuration. |


<span id="tosmountconfig"></span>
### TosMountConfig


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|EnableTos |Boolean |Yes |false |Whether to enable TOS storage mount. Parameter values:<br><br><br>* **true**: Turn on. Store data in TOS.<br><br>* **false**: Do not turn on. |
|Credentials |Object of [Credentials](https://docs.byteplus.com/en/docs/192/57177#credentials) |No |\- |After TOS storage mount is enabled, you need to provide an access key (AK/SK) with permission to access the TOS domain name. |
|MountPoints |Array of [TosMountPoint](https://docs.byteplus.com/en/docs/192/57177#tosmountpoint) |No |\- |After enabling Torch Object Storage mount, you need to provide a Torch Object Storage configuration list. No more than 5 items. |


<span id="asynctaskconfig"></span>
### AsyncTaskConfig


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|MaxRetry |Integer |No |3 |Number of asynchronous task failure retries. Selectable values are 0~3. |
|EnableAsyncTask |Boolean |Yes |true |Whether to enable asynchronous tasks. |
|DestinationConfig |Object of [DestinationConfig](https://docs.byteplus.com/en/docs/192/57177#destinationconfig) |No |\- |Asynchronous task callback destination configuration. |


<span id="nasconfig"></span>
### NasConfig


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|Gid |Long |No |1,000 |User groups in the file system do not currently support customization. If this parameter is provided, its value must be consistent with the function's run user GID, and the value must be: 1000. |
|Uid |Long |No |1,000 |User in the file system; custom users are not supported at this time. If this parameter is provided, its value must match the function's run user UID and be set to 1000. |
|RemotePath |String |Yes |/ |File system remote directory. Length: 1~128 characters. Must start with "`/`", supports uppercase and lowercase letters, numbers, and special characters (`- . _ ~ / : @ = + ? #`). |
|FileSystemId |String |Yes |enas\-cns\*\*\*\*\*\* |NAS file system ID. |
|MountPointId |String |Yes |mount\-63\*\*\*\*\*\* |NAS mount point ID. |
|LocalMountPath |String |Yes |/mnt/nas |Function local mount directory. Length: 1–128 characters, must start with "`/`", supports uppercase and lowercase letters, digits, and special characters (`- . _ ~ / : @ = + ? #`). |


<span id="credentials"></span>
### Credentials


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|AccessKeyId |String |Yes |\*\*\*\*\*\* |AccessKey ID (AK) of the BytePlus root user. For the obtaining method, please refer to the [Access key usage guide](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-access-keys). |
|SecretAccessKey |String |Yes |\*\*\*\*\*\* |Secret Access Key (SK) for the BytePlus root user. For the obtaining method, please refer to the [Access key usage guide](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-access-keys). |


<span id="tosmountpoint"></span>
### TosMountPoint


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|Endpoint |String |Yes |http://tos\-cn\-beijing.ivolces.com |TOS accesses the domain name. |
|ReadOnly |Boolean |No |true |Function local directory access permission. After mounting the TOS Bucket, whether the function's local mount directory is read\-only. Parameter values:<br><br><br>* **true**: Read only<br><br>* **false**(default): Read and write |
|BucketName |String |Yes |ai\-model |TOS bucket name |
|BucketPath |String |Yes |/ |The mount TOS Bucket path. |
|LocalMountPath |String |Yes |/mnt/tos |Function local mount directory. |


<span id="destinationconfig"></span>
### DestinationConfig


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|OnFailure |Object of [Destination](https://docs.byteplus.com/en/docs/192/57177#destination) |No |\- |Callback target configuration when task execution fails. |
|OnSuccess |Object of [Destination](https://docs.byteplus.com/en/docs/192/57177#destination) |No |\- |Callback target configuration when the task is executed successfully. |


<span id="destination"></span>
### Destination


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|Destination |String |No |http://dummyinstanceid.apigateway\-cn\-beijing\-\*\*\*\*.volceapi.com |Specific callback destination. Setting the value to an empty string ("") disables the callback. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST http://open.volcengineapi.com/?Action=CreateFunction&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "Name": "official-site",
    "Description": "Lightweight Official Website",
    "Runtime": "python3.8/v1",
    "ExclusiveMode": false,
    "RequestTimeout": 30,
    "MaxConcurrency": 100,
    "MemoryMB": 1024,
    "SourceType": "tos",
    "Source": "pqyqo9qa/3kwem******.zip",
    "Envs": [
        {
            "Key": "business_type",
            "Value": "free"
        }
    ],
    "VpcConfig": {
        "VpcId": "vpc-2d73mgm****",
        "EnableVpc": true,
        "SubnetIds": [
            "subnet-mj1l******"
        ],
        "SecurityGroupIds": [
            "sg-3re8ffwjclybk5zsk****"
        ],
        "EnableSharedInternetAccess": true
    },
    "TlsConfig": {
        "EnableLog": true,
        "TlsTopicId": "0cd4e4c4-5436-4b05-b39e-****",
        "TlsProjectId": "48f49d74-cd50-4591-a3d0-****"
    },
    "SourceAccessConfig": {
        "Password": "password ",
        "Username": "operator"
    },
    "Tags": [
        {
            "Key": "business",
            "Value": "ecommerce"
        }
    ],
    "NasStorage": {
        "EnableNas": true,
        "NasConfigs": [
            {
                "RemotePath": "/",
                "FileSystemId": "enas-cns******",
                "MountPointId": "mount-63******",
                "LocalMountPath": "/mnt/nas"
            }
        ]
    },
    "TosMountConfig": {
        "EnableTos": false,
        "Credentials": {
            "AccessKeyId": "******",
            "SecretAccessKey": "******"
        },
        "MountPoints": [
            {
                "Endpoint": "http://tos-cn-beijing.ivolces.com",
                "ReadOnly": true,
                "BucketName": "ai-model",
                "BucketPath": "/",
                "LocalMountPath": "/mnt/tos"
            }
        ]
    },
    "InitializerSec": 30,
    "Command": "./run.sh",
    "Port": 8000,
    "CpuStrategy": "always",
    "ProjectName": "default",
    "CpuMilli": 10,
    "Cell": "2",
    "Role": "trn:iam::140******:role/VeFaaSDefaultRole"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |pqy\*\*\*\*\*\* |Function ID. |
|Name |String |official\-site |Function name. |
|Description |String |Lightweight official website |Function description. |
|Runtime |String |python3.8/v1 |Function Runtime. |
|ExclusiveMode |Boolean |false |Exclusive mode switch.<br><br><br>* true: Turn off multiple concurrent requests per instance, that is, the exclusive mode in which a single instance can only process one request at a time.<br><br>* false (default): Turn on multiple concurrent requests per instance, that is, the non\-exclusive mode where a single instance can handle multiple requests at the same time, and you can set the maximum number of concurrent requests that a single instance can carry through MaxConcurrency. |
|RequestTimeout |Integer |30 |Request timed out (the unit is second). |
|MaxConcurrency |Integer |100 |Single instance maximum concurrency. |
|MemoryMB |Integer |1,024 |Maximum memory per instance (the unit is MB). |
|CodeSize |Integer |473 |Code package size (the unit is MB). |
|CodeSizeLimit |Integer |256 |The code package size limit.<br><br><br>* SourceType=zip，CodeSizeLimit=15MB.<br><br>* SourceType=tos，CodeSizeLimit=256MB. |
|Source |String |pqy\*\*\*\*\*\*/3kwem\*\*\*\*\*\*.zip |User\-entered code/image address. |
|SourceLocation |String |https://vefaas.tos\-s3\-cn.volces.com/template_dir/666ad75b9124c400072abcvefaas\-python3.9\-default.zip?X\-Amz\*\*\*\*\*\* |The source address of the code/image. |
|SourceType |String |tos |Code source type, optional values are:<br><br><br>* tos: Torch Object Storage.<br><br>* zip: Local compressed file.<br><br>* image: Container Registry. |
|Envs |Array of [EnvVar](https://docs.byteplus.com/en/docs/192/57177#envvar) |\- |Function Environment variables. |
|VpcConfig |Object of [VpcConfig](https://docs.byteplus.com/en/docs/192/57177#vpcconfig) |\- |VPC configuration. |
|CreationTime |String |2024\-06\-14 15:31:07.143863441 +0800 CST m=+88714.902440864 |Creation time. |
|LastUpdateTime |String |2024\-06\-14 15:31:07.143863491 +0800 CST m=+88714.902440914 |Update time. |
|TlsConfig |Object of [TlsConfig](https://docs.byteplus.com/en/docs/192/57177#tlsconfig) |\- |Function logs configuration. |
|Owner |String |22\*\*\*\*\*\* |Function owner (account Id). |
|TriggersCount |Integer |0 |The number of triggers for this function. |
|InstanceType |String |nvidia\-tesla\-l4 |Function instance type:<br><br><br>* Empty value: CPU instance type.<br><br>* Non\-empty value: Specific type of GPU instance. |
|NasStorage |Object of [NasStorage](https://docs.byteplus.com/en/docs/192/57177#nasstorage) |\- |FileNAS mount configuration. |
|TosMountConfig |Object of [TosMountConfig](https://docs.byteplus.com/en/docs/192/57177#tosmountconfig) |\- |Torch Object Storage TOS mount configuration. |
|InitializerSec |Integer |30 |Function initialization timeout configuration. |
|Command |String |./run.sh |Custom start command for the instance (currently only supports native/v1 runtimes). |
|Port |Integer |8,000 |Custom listening port for the instance (currently only native/v1 runtime is supported). |
|CpuStrategy |String |always |Function CPU billing policy, when the function is of microservices applications type, this field is `always`, indicating that at least one instance is running. |
|ProjectName |String |default |Function associated project name. |
|FunctionType |String |sandbox |Function type. |
|Cell |String |2 |Cell to which the function belongs. |
|Role |String |trn:iam::1400000044:role/VeFaaSDefaultRole |IAM role bound to function instances. |
|EnableApmplus |Boolean | |Turn on application monitoring. |
|AsyncTaskConfig |Object of [AsyncTaskConfig](https://docs.byteplus.com/en/docs/192/57177#asynctaskconfig) |{"EnableAsyncTask":true,"MaxRetry":3,"DestinationConfig":{"OnFailure":{"Destination":"http://dummyinstanceid.apigateway\-cn\-beijing\-inner.volceapi.com/failure"},"OnSuccess":{"Destination":"http://dummyinstanceid.apigateway\-cn\-beijing\-inner.volceapi.com/success"}}} |Asynchronous task configuration. |


<span id="envvar"></span>
### EnvVar


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Key |String |business_type |The key of an environment variable for sandbox instances. |
|Value |String |free |The value of the environment variable for sandbox instances. |


<span id="vpcconfig"></span>
### VpcConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|EnableVpc |Boolean |false |Whether the function enables VPC access. Parameter values:<br><br><br>* **false**: Disabled, the function can access the public network via the default network interface.<br><br>* **true**: Enabled, the function can access resources in the specified VPC. |
|VpcId |String |vpc\-2d73mgm\*\*\*\* |ID of the VPC to which the function belongs. |
|SubnetIds |Array of String |["subnet\-mj1l\*\*\*\*\*\*"] |The corresponding subnet ID after the function turns on VPC access. |
|SecurityGroupIds |Array of String |["sg\-3re8ffwjclybk5zsk\*\*\*\*"] |Security group ID after function enables VPC access. |
|EnableSharedInternetAccess |Boolean |false |The switch for the function to access the public network. Whether to access the public network through veFaaS's VPC shared NAT gateway. Parameter values:<br><br><br>* **true**: Turned on, access the public network through the default network interface card. Traffic charges will be incurred on the public network.<br><br>* **false**: Turned off, the function cannot access the public network through the default network interface card. |


<span id="tlsconfig"></span>
### TlsConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|EnableLog |Boolean |false |Whether to enable the log feature. Parameter values:<br><br><br>* **true**: Turned on, the stdout/stderr logs of the function will be collected into the specified logs project and logs topic of the Torch Log Service.<br><br>* **false**: Turned off, the logs are not collected.  |
|TlsTopicId |String |0cd4e4c4\-5436\-4b05\-b39e\-\*\*\*\* |TLS Logs theme ID. |
|TlsProjectId |String |48f49d74\-cd50\-4591\-a3d0\-\*\*\*\* |TLS Logs project ID. |


<span id="nasstorage"></span>
### NasStorage


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|EnableNas |Boolean |false |Whether to turn on NAS storage mount. Parameter values:<br><br><br>* **true**: Turned on, store data to NAS.<br><br>* **false**: Do not turn on. |
|NasConfigs |Array of [NasConfig](https://docs.byteplus.com/en/docs/192/57177#nasconfig) |\- |NAS storage configuration. |


<span id="tosmountconfig"></span>
### TosMountConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|EnableTos |Boolean |false |Whether to enable Torch Object Storage mount, parameter values:<br><br><br>* **true**: Enable, store data in Torch Object Storage.<br><br>* **false**: Do not turn on. |
|Credentials |Object of [Credentials](https://docs.byteplus.com/en/docs/192/57177#credentials) |\- |After turning on Torch Object Storage mount, you need to provide an access key (AK/SK) with Torch Object Storage domain access permission. |
|MountPoints |Array of [TosMountPoint](https://docs.byteplus.com/en/docs/192/57177#tosmountpoint) |\- |After turning on Torch Object Storage mount, you need to provide a Torch Object Storage configuration list. No more than 5 configurations. |


<span id="asynctaskconfig"></span>
### AsyncTaskConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|MaxRetry |Integer |3 |Number of asynchronous task failure retries. Selectable values are 0~3. |
|EnableAsyncTask |Boolean |true |Whether to turn on asynchronous tasks. |
|DestinationConfig |Object of [DestinationConfig](https://docs.byteplus.com/en/docs/192/57177#destinationconfig) |\- |Asynchronous task callback destination configuration. |


<span id="nasconfig"></span>
### NasConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Gid |Long |1,000 |User group in the file system. Customization is not supported for now. If this parameter is provided, its value must be consistent with the function run user gid, which should be set to: 1000. |
|Uid |Long |1,000 |User in the file system. Customization is not supported for now. If this parameter is provided, its value must be consistent with the function run user uid, which should be set to: 1000. |
|RemotePath |String |/ |File system remote directory. Length: 1–128 characters, must start with "`/`", supports uppercase and lowercase letters, digits, and special characters (`- . _ ~ / : @ = + ? #`). |
|FileSystemId |String |enas\-cns\*\*\*\*\*\* |NAS file system ID. |
|MountPointId |String |mount\-63\*\*\*\*\*\* |NAS mount point ID. |
|LocalMountPath |String |/mnt/nas |Function local mount directory. Length: 1~128 characters. Must start with "`/`", supports uppercase and lowercase letters, numbers, and special characters (`- . _ ~ / : @ = + ? #`). |


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
|ReadOnly |Boolean |true |Permission for the function's local directory. After mounting the Torch Object Storage bucket, specify whether the local mount directory is read\-only. Parameter values:<br><br><br>* **true**: Read only<br><br>* **false**(default): Read and write |
|BucketName |String |ai\-model |TOS bucket name |
|BucketPath |String |/ |The mount TOS Bucket path. |
|LocalMountPath |String |/mnt/tos |Function local mount directory. |


<span id="destinationconfig"></span>
### DestinationConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|OnFailure |Object of [Destination](https://docs.byteplus.com/en/docs/192/57177#destination) |\- |Task callback target configuration when execution is successful. |
|OnSuccess |Object of [Destination](https://docs.byteplus.com/en/docs/192/57177#destination) |\- |Callback target configuration when task execution fails. |


<span id="destination"></span>
### Destination


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Destination |String |http://dummyinstanceid.apigateway\-cn\-beijing\-\*\*\*\*.volceapi.com |Specific callback destination. Setting the value to an empty string ("") disables the callback. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateFunction",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "pqy******",
        "Name": "official-site",
        "Description": "lightweight official website",
        "Runtime": "python3.8/v1",
        "ExclusiveMode": false,
        "RequestTimeout": 30,
        "MaxConcurrency": 100,
        "MemoryMB": 1024,
        "CodeSize": 473,
        "CodeSizeLimit": 256,
        "Source": "pqy******/3kwem******.zip",
        "SourceLocation": "https://vefaas.tos-s3-cn.volces.com/template_dir/666ad75b9124c400072abcvefaas-python3.9-default.zip?X-Amz******",
        "SourceType": "tos",
        "Envs": [
            {
                "Key": "business_type",
                "Value": "free"
            }
        ],
        "VpcConfig": {
            "VpcId": "vpc-2d73mgm****",
            "EnableVpc": true,
            "SubnetIds": [
                "subnet-mj1l******"
            ],
            "SecurityGroupIds": [
                "sg-3re8ffwjclybk5zsk****"
            ],
            "EnableSharedInternetAccess": false
        },
        "CreationTime": "2024-06-14 15:31:07.143863441 +0800 CST m=+88714.902440864",
        "LastUpdateTime": "2024-06-14 15:31:07.143863491 +0800 CST m=+88714.902440914",
        "TlsConfig": {
            "EnableLog": false,
            "TlsTopicId": "0cd4e4c4-5436-4b05-b39e-****",
            "TlsProjectId": "48f49d74-cd50-4591-a3d0-****"
        },
        "Owner": "22******",
        "TriggersCount": 0,
        "InstanceType": "nvidia-tesla-l4",
        "NasStorage": {
            "EnableNas": true,
            "NasConfigs": [
                {
                    "Gid": 1000,
                    "Uid": 1000,
                    "RemotePath": "/",
                    "FileSystemId": "enas-cns******",
                    "MountPointId": "mount-63******",
                    "LocalMountPath": "/mnt/nas"
                }
            ]
        },
        "TosMountConfig": {
            "EnableTos": false,
            "Credentials": {
                "AccessKeyId": "******",
                "SecretAccessKey": "******"
            },
            "MountPoints": [
                {
                    "Endpoint": "http://tos-cn-beijing.ivolces.com",
                    "ReadOnly": true,
                    "BucketName": "ai-model",
                    "BucketPath": "/",
                    "LocalMountPath": "/mnt/tos"
                }
            ]
        },
        "InitializerSec": 30,
        "Command": "./run.sh",
        "Port": 8000,
        "CpuStrategy": "always",
        "ProjectName": "default",
        "FunctionType": "sandbox",
        "Cell": "2",
        "Role": "trn:iam::1400000044:role/VeFaaSDefaultRole",
        "EnableApmplus": false,
        "AsyncTaskConfig": {
            "EnableAsyncTask": true,
            "MaxRetry": 3,
            "DestinationConfig": {
                "OnFailure": {
                    "Destination": "http://dummyinstanceid.apigateway-cn-beijing-inner.volceapi.com/failure"
                },
                "OnSuccess": {
                    "Destination": "http://dummyinstanceid.apigateway-cn-beijing-inner.volceapi.com/success"
                }
            }
        }
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There is no error code dedicated to this interface currently. If you encounter an exception when calling the interface, you can refer to [Public error codes](https://docs.byteplus.com/en/docs/faas/Public_error_code) for troubleshooting.
