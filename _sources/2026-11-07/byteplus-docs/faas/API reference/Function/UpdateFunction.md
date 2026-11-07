---
title: "UpdateFunction"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/UpdateFunction"
---

Update a function, including function configurations and code.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Request method: POST

* Request address: http://open.volcengineapi.com/?Action=UpdateFunction&Version=2024\-06\-06


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=UpdateFunction&serviceCode=vefaas&version=2024-06-06&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UpdateFunction |Interface name. The current API is called `UpdateFunction`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06 `. |
|Id |String |Yes |pq\*\*\*\*\*\* |Function ID. You can call the [ListFunctions](https://docs.byteplus.com/en/docs/faas/ListFunctions) interface to obtain function ID (`Items.Id`). |
|Description |String |No |Lightweight official website |Function description. |
|ExclusiveMode |Boolean |No |false |Exclusive mode switch.<br><br><br>* **true**: Turn off multiple concurrent requests per instance, that is, the exclusive mode in which a single instance can only process one request at a time.<br><br>* **false** (default): Turn on multiple concurrent requests per instance, that is, the non\-exclusive mode where a single instance can handle multiple requests at the same time, and you can set the maximum number of concurrent requests that a single instance can carry through MaxConcurrency. |
|RequestTimeout |Integer |No |30 |Request timed out.<br><br><br>* Unit: second.<br><br>* Value range: 1 to 900.<br><br>* Default value: 30. |
|MaxConcurrency |Integer |No |100 |Single instance maximum concurrency. When `ExclusiveMode = false`, it can be set.<br><br><br>* Value range: 10~1,000.<br><br>* Default value: 100. |
|MemoryMB |Integer |No |1,024 |Maximum memory per instance, in MiB. When the calculation mode of the function is CPU instance, the memory specification of a single CPU instance can be configured. |
|Source |String |No |pqxxxxxx/3kw1\*\*\*\*\*\* |Code source.<br><br><br>* **zip**: Base64 encoded binary zip.<br><br>* **tos**: String in the format `bucket_name: object_key`, e.g.: `vefaas-test: vefaas-python38-default.zip`.<br><br>* **image**: The image address in the format `host/namespace/repo: tag`. E.g.: `cp-enterprise-cn-beijing.cr.volces.com/demo/nginx: latest`. |
|SourceType |String |No |tos |Code source type, optional values are:<br><br><br>* **tos**: Torch Object Storage.<br><br>* **zip**: Local compressed file.<br><br>* **image**: Container Registry. Native/v1 custom image is a beta feature. To try it, please [submit a ticket](https://docs.byteplus.com/en/docs/faas/How_do_I_apply_for_beta_features). |
|Envs |Array of [EnvVar](https://docs.byteplus.com/en/docs/192/57190#envvar) |No |\- |Environment variables. |
|VpcConfig |Object of [VpcConfig](https://docs.byteplus.com/en/docs/192/57190#vpcconfig) |No |\- |VPC configuration. |
|TlsConfig |Object of [TlsConfig](https://docs.byteplus.com/en/docs/192/57190#tlsconfig) |No |\- |TLS Logs configuration. |
|SourceAccessConfig |Object of [SourceAccessConfig](https://docs.byteplus.com/en/docs/192/57190#sourceaccessconfig) |No |\- |When users are setting cross\-accounts custom images, access configuration is required. |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/192/57190#tag) |No |\- | |
|NasStorage |Object of [NasStorage](https://docs.byteplus.com/en/docs/192/57190#nasstorage) |No |\- |FileNAS mount configuration. |
|TosMountConfig |Object of [TosMountConfig](https://docs.byteplus.com/en/docs/192/57190#tosmountconfig) |No |\- |Torch Object Storage TOS mount configuration. After changing the TOS mount configuration, the response result is returned synchronously. |
|InitializerSec |Integer |No |30 |Function initialization timeout configuration. |
|Port |Integer |No |8,000 |Custom listening port for the instance. Only supported in native/v1 runtime. |
|ProjectName |String |No |default |The name of the project where the function is located. |
|CpuMilli |Integer |No |10 |Maximum CPU per instance, measured in milli CPU. 1 milli CPU = 0.001 CPU。 When the function's computing mode is set to CPU instance, you can configure the CPU specifications for a single CPU instance. |
|Role |String |No |trn:iam::1400000044:role/VeFaaSDefaultRole |Function instances bind IAM role |
|EnableApmplus |Boolean |No |false |Turn on application Monitoring. |
|AsyncTaskConfig |Object of [UpdateFunctionAsyncConfig](https://docs.byteplus.com/en/docs/192/57190#updatefunctionasyncconfig) |No |{"MaxRetry":3,"DestinationConfig":{"OnFailure":{"Destination":"http://dummyinstanceid.apigateway\-cn\-beijing\-\*\*\*\*.\*\*\*\*.com/failure"},"OnSuccess":{"Destination":"http://dummyinstanceid.apigateway\-cn\-beijing\-inner.volceapi.com/success"}}} |Asynchronous task configuration. |


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
|EnableVpc |Boolean |Yes |false |Whether the function enables VPC access. Parameter values:<br><br><br>* **false**: Not enabled. The function can access the public network via the default network interface.<br><br>* **true**: Enabled. The function can access resources in the specified VPC. |
|VpcId |String |No |vpc\-2d73mgm\*\*\*\* |ID of the VPC to which the function belongs. |
|SubnetIds |Array of String |No |["subnet\-mj1l\*\*\*\*\*\*"] |Subnet ID corresponding to the function after turning on VPC access. |
|SecurityGroupIds |Array of String |No |["sg\-3re8ffwjclybk5zsk\*\*\*\*"] |Security group ID after the function enables VPC access. |
|EnableSharedInternetAccess |Boolean |No |false |The switch for the function to access the public network. Whether to access the public network through veFaaS's VPC shared NAT gateway. Parameter values:<br><br><br>* **true**: Turned on, access the public network through the default network interface card. Traffic charges will be incurred on the public network.<br><br>* **false**: Turned off, the function cannot access the public network through the default network interface card. |


<span id="tlsconfig"></span>
### TlsConfig


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|EnableLog |Boolean |Yes |false |Whether to enable log feature. Parameter values:<br><br><br>* **true**: Turned on, the stdout/stderr logs of the function will be collected into the specified logs project and logs topic of the Torch Log Service.<br><br>* **false**: Turned off, the logs are not collected.  |
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
|EnableNas |Boolean |Yes |false |Whether to turn on NAS storage mount. Parameter values:<br><br><br>* **true**: Turned on, store data to NAS.<br><br>* **false**: Do not turn on. |
|NasConfigs |Array of [NasConfig](https://docs.byteplus.com/en/docs/192/57190#nasconfig) |No |\- |NAS storage configuration. |


<span id="tosmountconfig"></span>
### TosMountConfig


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|EnableTos |Boolean |Yes |false |Whether to turn on TOS storage mount. Parameter values:<br><br><br>* **true**: Turn on. Data will be stored in TOS.<br><br>* **false**: Do not turn on. |
|Credentials |Object of [Credentials](https://docs.byteplus.com/en/docs/192/57190#credentials) |No |\- |After turning on TOS storage mount, you need to provide access keys (AK/SK) with TOS domain access permission. |
|MountPoints |Array of [TosMountPoint](https://docs.byteplus.com/en/docs/192/57190#tosmountpoint) |No |\- |After turning on TOS storage mount, you need to provide a TOS storage configuration list. No more than 5. |


<span id="updatefunctionasyncconfig"></span>
### UpdateFunctionAsyncConfig


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|MaxRetry |Integer |No |3 |Number of asynchronous task failure retries. Selectable values: 0–3. |
|DestinationConfig |Object of [DestinationConfig](https://docs.byteplus.com/en/docs/192/57190#destinationconfig) |No |\- |Asynchronous task callback destination configuration. |


<span id="nasconfig"></span>
### NasConfig


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|Gid |Long |No |1,000 |User group in the file system; custom configuration is not supported for now. If this parameter is provided, its value must be consistent with the function run user gid, with a value of: 1000. |
|Uid |Long |No |1,000 |User in the file system. Customization is not supported for now. If this parameter is provided, its value must be consistent with the function run user uid. The value is: 1000. |
|RemotePath |String |Yes |/ |File system remote directory. Length: 1–128 characters. Must start with "`/`", supports uppercase and lowercase letters, digits, and special characters (`- . _ ~ / : @ = + ? #`). |
|FileSystemId |String |Yes |enas\-cns\*\*\*\*\*\* |NAS file system ID. |
|MountPointId |String |Yes |mount\-63\*\*\*\*\*\* |NAS mount point ID. |
|LocalMountPath |String |Yes |/mnt/nas |Function local mount directory. Length: 1–128 characters. Must start with "`/`", supports uppercase and lowercase letters, digits, and special characters (`- . _ ~ / : @ = + ? #`). |


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
|ReadOnly |Boolean |No |true |Function local directory permission. After mounting the TOS Bucket, whether the function's local mount directory permission is read\-only. Parameter values:<br><br><br>* **true**: Read only<br><br>* **false**(default): Read and write |
|BucketName |String |Yes |ai\-model |TOS bucket name |
|BucketPath |String |Yes |/ |The mount TOS Bucket path. |
|LocalMountPath |String |Yes |/mnt/tos |Function local mount directory. |


<span id="destinationconfig"></span>
### DestinationConfig


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|OnFailure |Object of [Destination](https://docs.byteplus.com/en/docs/192/57190#destination) |No |\- |Callback destination configuration when the task is executed successfully. |
|OnSuccess |Object of [Destination](https://docs.byteplus.com/en/docs/192/57190#destination) |No |\- |Callback target configuration when task execution fails. |


<span id="destination"></span>
### Destination


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|Destination |String |No |http://dummyinstanceid.apigateway\-cn\-beijing\-\*\*\*\*.volceapi.com |Specific callback target. Setting the value to empty ('') disables the callback. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST http://open.volcengineapi.com/?Action=UpdateFunction&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "Id": "pq123456",
    "Description": "lightweight official website",
    "ExclusiveMode": false,
    "RequestTimeout": 30,
    "MaxConcurrency": 100,
    "MemoryMB": 1024,
    "Source": "vefaas-test:vefaas-python38-default.zip",
    "SourceType": "tos",
    "Envs": [
        {
            "Key": "business_type",
            "Value": "free"
        }
    ],
    "VpcConfig": {
        "VpcId": "vpc-3rf87yoa8yn0g5zsk2hfev****",
        "EnableVpc": false,
        "SubnetIds": [
            "subnet-mj1lxywnkq2o5smt1bhyefgh"
        ],
        "SecurityGroupIds": [
            "sg-rs6schq63nk0v0x57j4****"
        ],
        "EnableSharedInternetAccess": false
    },
    "TlsConfig": {
        "EnableLog": false,
        "TlsTopicId": "tls-vefaas-logstore",
        "TlsProjectId": "tls-vefaas"
    },
    "SourceAccessConfig": {
        "Password": "Feie&ffe123huabcd",
        "Username": "operator"
    },
    "Tags": [
        {
            "Key": "business",
            "Value": "ecommerce"
        }
    ],
    "NasStorage": {
        "EnableNas": false,
        "NasConfigs": [
            {
                "Gid": 1000,
                "Uid": 1000,
                "RemotePath": "/",
                "FileSystemId": "enas-cnsha0a8842997****",
                "MountPointId": "mount-6303defg",
                "LocalMountPath": "/mnt/nas"
            }
        ]
    },
    "TosMountConfig": {
        "EnableTos": false,
        "Credentials": {
            "AccessKeyId": "TZT****",
            "SecretAccessKey": "Fwei****"
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
    "Port": 8080,
    "ProjectName": "default",
    "CpuMilli": 10,
    "Role": "trn:iam::1400000044:role/VeFaaSDefaultRole",
    "EnableApmplus": false,
    "AsyncTaskConfig": {
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
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |pq\*\*\*\*\*\* |Function ID. |
|Name |String |official\-site |Function name. |
|Description |String |Lightweight official website |Function description. |
|Runtime |String |python3.8/v1 |Function Runtime. |
|ExclusiveMode |Boolean |false |Exclusive mode switch.<br><br><br>* **true**: Turn off multiple concurrent requests per instance, that is, the exclusive mode in which a single instance can only process one request at a time.<br><br>* **false**: Turn on multiple concurrent requests per instance, that is, a non\-exclusive mode in which a single instance can handle multiple requests at the same time. |
|RequestTimeout |Integer |30 |Request timed out. Unit: second. |
|MaxConcurrency |Integer |100 |Single instance maximum concurrency. |
|MemoryMB |Integer |1,024 |Maximum memory per instance. Unit: MiB. |
|CodeSize |Integer |473 |Code package size. Unit: MiB. |
|CodeSizeLimit |Integer |256 |The code package size limit.<br><br><br>* SourceType=zip, CodeSizeLimit=15MiB.<br><br>* SourceType=tos, CodeSizeLimit=256MiB. |
|SourceLocation |String |https://vefaas.tos\-s3\-cn.volces.com/template_dir/666ad75bxxxxxxabcvefaas\-python3.9\-default.zip?X\-Amz\-\*\*\*\*\*\* |The source address of the code/image. |
|SourceType |String |tos |Code source type, optional values are:<br><br><br>* tos: Torch Object Storage.<br><br>* zip: Local compressed file.<br><br>* image: Container Registry. |
|Envs |Array of [EnvVar](https://docs.byteplus.com/en/docs/192/57190#envvar) |\- |Function Environment variables. |
|VpcConfig |Object of [VpcConfig](https://docs.byteplus.com/en/docs/192/57190#vpcconfig) |\- |VPC configuration. |
|CreationTime |String |2024\-06\-14 15:31:07.143863441 +0800 CST m=+88714.902440864 |Creation time. |
|LastUpdateTime |String |2024\-06\-14 15:31:07.143863491 +0800 CST m=+88714.902440914 |Update time. |
|TlsConfig |Object of [TlsConfig](https://docs.byteplus.com/en/docs/192/57190#tlsconfig) |\- |Function logs configuration. |
|Owner |String |22\*\*\*\*\*\* |Account ID of the function owner. |
|TriggersCount |Integer |0 |The number of triggers for this function. |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/192/57190#tag) |"Tags":[{"Key":"business","Value":"ecommerce"}] |Function label. |
|InstanceType |String |nvidia\-tesla\-l4 |Function instance type.<br><br><br>* Empty value: CPU instance type.<br><br>* Non\-empty value: Specific GPU instance type. |
|NasStorage |Object of [NasStorage](https://docs.byteplus.com/en/docs/192/57190#nasstorage) |\- |FileNAS mount configuration. |
|TosMountConfig |Object of [TosMountConfig](https://docs.byteplus.com/en/docs/192/57190#tosmountconfig) |\- |Torch Object Storage TOS mount configuration. |
|InitializerSec |Integer |30 |Function initialization timeout configuration. |
|Command |String |./run.sh |Custom start command for the instance. Only supported by native/v1 runtime. |
|Port |Integer |8,000 |Custom listening port for the instance; only supported in native/v1 runtime. |
|CpuStrategy |String |always |Function CPU billing policy, when the function is of microservices applications type, this field is `always`, indicating that at least one instance is running. |
|ProjectName |String |default |The name of the project to which the function belongs. |
|FunctionType |String |sandbox |Function type |
|Cell |String |2 |Cell to which the function belongs. |
|Role |String |trn:iam::1400000044:role/VeFaaSDefaultRole |Function instances bind IAM role |
|EnableApmplus |Boolean | false |Turn on application monitoring. |
|AsyncTaskConfig |Object of [AsyncTaskConfig](https://docs.byteplus.com/en/docs/192/57190#asynctaskconfig) |{"EnableAsyncTask":true,"MaxRetry":3,"DestinationConfig":{"OnFailure":{"Destination":"http://dummyinstanceid.apigateway\-cn\-beijing\-inner.volceapi.com/failure"},"OnSuccess":{"Destination":"http://dummyinstanceid.apigateway\-cn\-beijing\-inner.volceapi.com/success"}}} |Asynchronous task configuration. |


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
|EnableVpc |Boolean |false |Whether to turn on VPC access for the function. Parameter values:<br><br><br>* **false**: Not enabled. The function can access the public network via the default network interface.<br><br>* **true**: Enabled. The function can access resources in the specified VPC. |
|VpcId |String |vpc\-2d73mgm\*\*\*\* |ID of the VPC to which the function belongs. |
|SubnetIds |Array of String |["subnet\-mj1l\*\*\*\*\*\*"] |After the function turns on VPC access, the corresponding subnet ID. |
|SecurityGroupIds |Array of String |["sg\-3re8ffwjclybk5zsk\*\*\*\*"] |Security group ID when VPC access is enabled for the function. |
|EnableSharedInternetAccess |Boolean |false |The switch for the function to access the public network. Whether to access the public network via veFaaS VPC shared NAT gateway. Parameter values:<br><br><br>* **true**: Turned on, access the public network through the default network interface card. Traffic charges will be incurred on the public network.<br><br>* **false**: Turned off, the function cannot access the public network through the default network interface card. |


<span id="tlsconfig"></span>
### TlsConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|EnableLog |Boolean |false |Whether to enable the log feature. Parameter values:<br><br><br>* **true**: Turned on, the stdout/stderr logs of the function will be collected into the specified logs project and logs topic of the Torch Log Service.<br><br>* **false**: Turned off, the logs are not collected.  |
|TlsTopicId |String |0cd4e4c4\-5436\-4b05\-b39e\-\*\*\*\* |TLS Logs theme ID. |
|TlsProjectId |String |48f49d74\-cd50\-4591\-a3d0\-\*\*\*\* |TLS Logs project ID. |


<span id="tag"></span>
### Tag


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Key |String |business |Label key. |
|Value |String |ecommerce |Label value. |


<span id="nasstorage"></span>
### NasStorage


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|EnableNas |Boolean |false |Whether to turn on NAS storage mount. Parameter values:<br><br><br>* **true**: Turned on, store data to NAS.<br><br>* **false**: Do not turn on. |
|NasConfigs |Array of [NasConfig](https://docs.byteplus.com/en/docs/192/57190#nasconfig) |\- |NAS storage configuration. |


<span id="tosmountconfig"></span>
### TosMountConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|EnableTos |Boolean |false |Whether to turn on TOS storage mount. Parameter values:<br><br><br>* **true**: Turned on. Data will be stored in TOS.<br><br>* **false**: Do not turn on. |
|Credentials |Object of [Credentials](https://docs.byteplus.com/en/docs/192/57190#credentials) |\- |After turning on TOS storage mount, you need to provide an access key (AK/SK) with permission to access the TOS domain name. |
|MountPoints |Array of [TosMountPoint](https://docs.byteplus.com/en/docs/192/57190#tosmountpoint) |\- |After turning on TOS storage mount, you need to provide a TOS storage configuration list. No more than 5. |


<span id="asynctaskconfig"></span>
### AsyncTaskConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|MaxRetry |Integer |3 |Number of retries for asynchronous task failure. Selectable values are 0–3. |
|EnableAsyncTask |Boolean |true |Whether to turn on asynchronous task. |
|DestinationConfig |Object of [DestinationConfig](https://docs.byteplus.com/en/docs/192/57190#destinationconfig) |\- |Asynchronous task callback target configuration. |


<span id="nasconfig"></span>
### NasConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Gid |Long |1,000 |User group in the file system. Customization is not supported at this time. If this parameter is provided, its value must be consistent with the function run user gid, and the value must be: 1000. |
|Uid |Long |1,000 |User in the file system; custom configuration is not supported for now. If this parameter is provided, its value must be consistent with the function run user uid, with a value of: 1000. |
|RemotePath |String |/ |File system remote directory. Length: 1~128 characters, must start with "`/`", supports uppercase and lowercase letters, numbers, and special characters (`- . _ ~ / : @ = + ? #`). |
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
|ReadOnly |Boolean |true |Function local directory permission. After mounting the TOS Bucket, whether the access permission of the function's local mount directory is read\-only. Parameter values:<br><br><br>* **true**: Read only<br><br>* **false**(default): Read and write |
|BucketName |String |ai\-model |TOS bucket name |
|BucketPath |String |/ |The mount TOS Bucket path. |
|LocalMountPath |String |/mnt/tos |Function local mount directory. |


<span id="destinationconfig"></span>
### DestinationConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|OnFailure |Object of [Destination](https://docs.byteplus.com/en/docs/192/57190#destination) |\- |Callback destination configuration when the task is executed successfully. |
|OnSuccess |Object of [Destination](https://docs.byteplus.com/en/docs/192/57190#destination) |\- |Callback destination configuration when the task fails to execute. |


<span id="destination"></span>
### Destination


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Destination |String |http://dummyinstanceid.apigateway\-cn\-beijing\-\*\*\*\*.volceapi.com |Specific callback destination. Setting the value to empty ("") disables the callback. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateFunction",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "pq123456",
        "Name": "official-site",
        "Description": "lightweight official website",
        "Runtime": "python3.8/v1",
        "ExclusiveMode": false,
        "RequestTimeout": 30,
        "MaxConcurrency": 100,
        "MemoryMB": 1024,
        "CodeSize": 473,
        "CodeSizeLimit": 256,
        "SourceLocation": "https://vefaas.tos-s3-cn.volces.com/template_dir/666ad75bxxxxxxabcvefaas-python3.9-default.zip?X-Amz-******",
        "SourceType": "tos",
        "Envs": [
            {
                "Key": "business_type",
                "Value": "free"
            }
        ],
        "VpcConfig": {
            "VpcId": "vpc-3rf87yoa8yn0g5zsk2hfevabcd",
            "EnableVpc": false,
            "SubnetIds": [
                "subnet-mj1lxywnkq2o5smt1bhy****"
            ],
            "SecurityGroupIds": [
                "sg-rs6schq63nk0v0x57j4****"
            ],
            "EnableSharedInternetAccess": false
        },
        "CreationTime": "2024-06-14 15:31:07.143863441 +0800 CST m=+88714.902440864",
        "LastUpdateTime": "2024-06-14 15:31:07.143863491 +0800 CST m=+88714.902440914",
        "TlsConfig": {
            "EnableLog": false,
            "TlsTopicId": "tls-vefaas-logstore",
            "TlsProjectId": "tls-vefaas"
        },
        "Owner": "2200000000",
        "TriggersCount": 0,
        "Tags": [
            {
                "Key": "business",
                "Value": "ecommerce"
            }
        ],
        "InstanceType": "nvidia-tesla-l4",
        "NasStorage": {
            "EnableNas": false,
            "NasConfigs": [
                {
                    "Gid": 1000,
                    "Uid": 1000,
                    "RemotePath": "/",
                    "FileSystemId": "enas-cnsha0a8842997****",
                    "MountPointId": "mount-6303defg",
                    "LocalMountPath": "/mnt/nas"
                }
            ]
        },
        "TosMountConfig": {
            "EnableTos": false,
            "Credentials": {
                "AccessKeyId": "TZTJ****",
                "SecretAccessKey": "Fwei****"
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
            "MaxRetry": 3,
            "EnableAsyncTask": true,
            "DestinationConfig": {
                "OnFailure": {
                    "Destination": "http://dummyinstanceid.apigateway-cn-beijing-*****.volceapi.com/failure"
                },
                "OnSuccess": {
                    "Destination": "http://dummyinstanceid.apigateway-cn-beijing-*****.volceapi.com/success"
                }
            }
        }
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There is no error code dedicated to this interface currently. If you encounter an exception when calling the interface, you can refer to [Public error codes](https://docs.byteplus.com/en/docs/faas/Public_error_code) for troubleshooting.
