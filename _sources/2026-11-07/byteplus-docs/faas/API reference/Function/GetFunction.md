---
title: "GetFunction"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/GetFunction"
---

Obtain function details, including function configurations and code.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Request method: POST

* Request address: http://open.volcengineapi.com/?Action=GetFunction&Version=2024\-06\-06


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=GetFunction&serviceCode=vefaas&version=2024-06-06&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetFunction |Interface name. The current API is called `GetFunction`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06 `. |
|Id |String |Yes |pqyqo9qa |Function ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST http://open.volcengineapi.com/?Action=GetFunction&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "Id": "pqyq****"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |pqyqo9qa |Function ID. |
|Name |String |official\-site |Function name. |
|Description |String |Lightweight official website |Function description. |
|Runtime |String |python3.8/v1 |Function Runtime. |
|ExclusiveMode |Boolean |false |Exclusive mode switch.<br><br><br>* true: Turn off multiple concurrent requests per instance, that is, the exclusive mode in which a single instance can only process one request at a time.<br><br>* false (default): Turn on multiple concurrent requests per instance, that is, the non\-exclusive mode where a single instance can handle multiple requests at the same time, and you can set the maximum number of concurrent requests that a single instance can carry through MaxConcurrency. |
|RequestTimeout |Integer |30 |Request timed out (the unit is second). |
|MaxConcurrency |Integer |100 |Single instance maximum concurrency. |
|MemoryMB |Integer |1,024 |Maximum memory per instance. |
|CodeSize |Integer |473 |Code package size. |
|CodeSizeLimit |Integer |256 |The code package size limit.<br><br><br>* SourceType=zip，CodeSizeLimit=15MB.<br><br>* SourceType=tos，CodeSizeLimit=256MB. |
|SourceLocation |String |https://vefaas.tos\-s3\-cn.volces.com/template_dir/666ad75b9124c400072abcvefaas\-python3.9\-default.zip?X\-Amz\*\*\*\*\*\* |The source address of the code/image. |
|SourceType |String |tos |Code source type:<br><br><br>* tos: Torch Object Storage.<br><br>* zip: Local compressed file.<br><br>* image: Container Registry. |
|Envs |Array of [EnvVar](https://docs.byteplus.com/en/docs/192/57189#envvar) |\- |Function Environment variables. |
|VpcConfig |Object of [VpcConfig](https://docs.byteplus.com/en/docs/192/57189#vpcconfig) |\- |VPC configuration. |
|CreationTime |String |2024\-06\-14 15:31:07.143863441 +0800 CST m=+88714.902440864 |Creation time. |
|LastUpdateTime |String |2024\-06\-14 15:31:07.143863491 +0800 CST m=+88714.902440914 |Update time. |
|TlsConfig |Object of [TlsConfig](https://docs.byteplus.com/en/docs/192/57189#tlsconfig) |\- |Function logs configuration. |
|Owner |String |22\*\*\*\*\*\* |Account ID of the function owner. |
|TriggersCount |Integer |0 |The number of triggers for this function. |
|InstanceType |String |nvidia\-tesla\-l4 |Function instance type.<br><br><br>* Empty value: CPU instance type.<br><br>* Non\-empty value: Specific GPU instance type. |
|NasStorage |Object of [NasStorage](https://docs.byteplus.com/en/docs/192/57189#nasstorage) |\- |FileNAS mount configuration. |
|TosMountConfig |Object of [TosMountConfig](https://docs.byteplus.com/en/docs/192/57189#tosmountconfig) |\- |Torch Object Storage TOS mount configuration. |
|InitializerSec |Integer |30 |Function initialization timeout configuration. |
|Command |String |./run.sh |Custom start command for the instance, only supported by native/v1 runtime. |
|Port |Integer |8,000 |Custom listening port for the instance, supported only by native/v1 runtime. |
|CpuStrategy |String |always |Function CPU billing policy, when the function is of microservices applications type, this field is `always`, indicating that at least one instance is running. |
|ProjectName |String |default |Project name. |
|FunctionType |String |sandbox |Function type. |
|Cell |String |2 |Cell to which the function belongs. |
|Role |String |trn:iam::1400000044:role/VeFaaSDefaultRole |Bind IAM role to function instances. |
|EnableApmplus |Boolean |ture |Turn on application monitoring. |
|AsyncTaskConfig |Object of [AsyncTaskConfig](https://docs.byteplus.com/en/docs/192/57189#asynctaskconfig) |{"EnableAsyncTask":true,"MaxRetry":3,"DestinationConfig":{"OnFailure":{"Destination":"http://dummyinstanceid.apigateway\-cn\-beijing\-\*\*\*\*.\*\*\*\*.com/failure"},"OnSuccess":{"Destination":"http://dummyinstanceid.apigateway\-cn\-beijing\-inner.volceapi.com/success"}}} |Asynchronous task configuration. |


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
|EnableVpc |Boolean |false |Whether the function enables VPC access. Parameter value:<br><br><br>* **false**: Not enabled; the function can access the public network via the default network interface.<br><br>* **true**: Enabled; the function can access resources in the specified VPC. |
|VpcId |String |vpc\-2d73mgm\*\*\*\* |ID of the VPC to which the function belongs. |
|SubnetIds |Array of String |["subnet\-mj1l\*\*\*\*\*\*"] |Subnet ID after the function turns on VPC access. |
|SecurityGroupIds |Array of String |["sg\-3re8ffwjclybk5zsk\*\*\*\*"] |Security group ID after the function turns on VPC access. |
|EnableSharedInternetAccess |Boolean |false |The switch for the function to access the public network. Whether to access the public network through veFaaS's VPC shared NAT gateway. Parameter value:<br><br><br>* **true**: Turned on, access the public network through the default network interface card. Traffic charges will be incurred on the public network.<br><br>* **false**: Turned off, the function cannot access the public network through the default network interface card. |


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
|EnableNas |Boolean |false |Whether to enable NAS storage mount, parameter value:<br><br><br>* **true**: Turned on, store data to NAS.<br><br>* **false**: Do not turn on. |
|NasConfigs |Array of [NasConfig](https://docs.byteplus.com/en/docs/192/57189#nasconfig) |\- |NAS storage configuration. |


<span id="tosmountconfig"></span>
### TosMountConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|EnableTos |Boolean |false |Whether to enable TOS storage mount, parameter value:<br><br><br>* **true**: Enabled; data will be stored in TOS.<br><br>* **false**: Do not turn on. |
|Credentials |Object of [Credentials](https://docs.byteplus.com/en/docs/192/57189#credentials) |\- |After turning on TOS storage mount, you need to provide an access key (AK/SK) with TOS domain name access permission. |
|MountPoints |Array of [TosMountPoint](https://docs.byteplus.com/en/docs/192/57189#tosmountpoint) |\- |After turning on TOS storage mount, you need to provide a TOS storage configuration list. No more than 5. |


<span id="asynctaskconfig"></span>
### AsyncTaskConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|MaxRetry |Integer |3 |Number of asynchronous task retry attempts after failure, selectable values are 0~3. |
|EnableAsyncTask |Boolean |true |Whether to enable asynchronous tasks. |
|DestinationConfig |Object of [DestinationConfig](https://docs.byteplus.com/en/docs/192/57189#destinationconfig) |\- |Asynchronous task callback target configuration. |


<span id="nasconfig"></span>
### NasConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Gid |Long |1,000 |User group in the file system. Custom settings are currently not supported. If this parameter is provided, the parameter value must be consistent with the function's run user GID, and the value must be: 1000. |
|Uid |Long |1,000 |User in the file system; custom user configuration is not supported for now. If this parameter is provided, its value must match the UID of the function's run user and must be: 1000. |
|RemotePath |String |/ |File system remote directory. Length 1~128 characters, must start with "`/`", supports uppercase and lowercase letters, numbers, and special characters (`- . _ ~ / : @ = + ? #`). |
|FileSystemId |String |enas\-cns\*\*\*\*\*\* |NAS file system ID. |
|MountPointId |String |mount\-63\*\*\*\*\*\* |NAS mount point ID. |
|LocalMountPath |String |/mnt/nas |Function local mount directory. Length 1~128 characters, must start with "`/`", supports uppercase and lowercase letters, digits, and special characters (`- . _ ~ / : @ = + ? #`). |


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
|ReadOnly |Boolean |true |Function local directory access permission. After mounting the TOS Bucket, specifies whether the function's local mount directory is read\-only. Parameter values:<br><br><br>* **true**: Read only<br><br>* **false**(default): Read and write |
|BucketName |String |ai\-model |TOS bucket name |
|BucketPath |String |/ |The mount TOS Bucket path. |
|LocalMountPath |String |/mnt/tos |Function local mount directory. |


<span id="destinationconfig"></span>
### DestinationConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|OnFailure |Object of [Destination](https://docs.byteplus.com/en/docs/192/57189#destination) |\- |Callback destination configuration when the task is executed successfully. |
|OnSuccess |Object of [Destination](https://docs.byteplus.com/en/docs/192/57189#destination) |\- |Callback target configuration when task execution fails. |


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
        "Action": "GetFunction",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "pqyqo9qa",
        "Name": "official-site",
        "Description": "lightweight official website",
        "Runtime": "python3.8/v1",
        "ExclusiveMode": false,
        "RequestTimeout": 30,
        "MaxConcurrency": 100,
        "MemoryMB": 1024,
        "CodeSize": 473,
        "CodeSizeLimit": 256,
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
            "EnableVpc": false,
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
            "EnableLog": true,
            "TlsTopicId": "0cd4e4c4-5436-4b05-b39e-****",
            "TlsProjectId": "48f49d74-cd50-4591-a3d0-****"
        },
        "Owner": "22******",
        "TriggersCount": 0,
        "InstanceType": "nvidia-tesla-l4",
        "NasStorage": {
            "EnableNas": false,
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
                    "Destination": "http://dummyinstanceid.apigateway-cn-beijing-****.****.com/failure"
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
