---
title: "CopyFunction"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/CopyFunction"
---

Copy function.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Request method: POST

* Request URL: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=CopyFunction&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**parameter** |**Type** |**Require or Not** |**sample value** |**Description** |
|---|---|---|---|---|
|Action |String  |Yes |CopyFunction |Interface name. The current name of the API is `CopyFunction`. |
|Version |String  |Yes |2021\-03\-03 |Interface version. The current version of the API is `2021-03-03`. |
|SourceFunctionId |String  |Yes |pqy\*\*\*\*\*\* |Source function ID. You can call the [ListFunctions](https://docs.byteplus.com/en/docs/faas/ListFunctions) interface to obtain Function ID (`Items.Id`). |
|SourceRevisionNumber |Integer |Yes |1 |The version number of the source function. You can call the [ListRevisions](https://docs.byteplus.com/en/docs/faas/ListRevisions) API to obtain the function version number (`RevisionNumber`). |
|Name |String  |Yes |new\-function |The name of the new function.<br><br><br>* The function name must be only in the same account.<br><br>* It supports uppercase and lowercase English letters, numbers, dashes (\-), and underscores (_), the length limit is 4 to 64 characters. |
|CopyConfig |Boolean |No |true |Whether to copy the function configuration. The available values are as follows:<br><br><br>* **true**: (default value) Copy function configuration.<br><br>* **false**: Do not copy. |
|ProjectName |String  |No |default |The name of the project to which the new function belongs. |


<span id=".6K-35rGC56S65L6L"></span>
## sample request

```json
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=CopyFunction&Version=2021-03-03 HTTP/1.1
Content-Type: application/json
{
    "SourceFunctionId": "pqy******",
    "SourceRevisionNumber": 1,
    "Name": "new-function",
    "CopyConfig": true,
    "ProjectName": "default"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**parameter** |**Type** |**sample value** |**Description** |
|---|---|---|---|
|Id |String  |aye\*\*\*\*\*\* |The ID of the new function. |
|Name |String  |new\-function |The name of the new function. |
|Description |String  |Copy function |Function description. |
|Runtime |String  |python3.8/v1 |Function Runtime. |
|ExclusiveMode |Boolean |false |Exclusive mode switch: parameter values:<br><br><br>* **false**: Turn off multiple concurrent requests per instance, that is, at any given time, a single instance can only process one request exclusively.<br><br>* **true**: Turn on multiple concurrent requests per instance, that is, a single instance can handle multiple requests simultaneously in a non\-exclusive mode. |
|RequestTimeout |Integer |30 |Request timeout (unit: seconds). |
|MaxConcurrency |Integer |30 |Single instance maximum concurrency. |
|MemoryMB |Integer |1,024 |Maximum memory per instance (unit: MiB). |
|CodeSize |Integer |473 |Code package size (unit: MiB). |
|CodeSizeLimit |Integer |15 |Maximum code package size (unit: MiB), parameter value:<br><br><br>* When `SourceType=zip`, the maximum code package size is 15 MiB.<br><br>* When `SourceType=tos`, the maximum code package size is 256 MiB. |
|Source |String  |pqy\*\*\*\*\*\*/3kwem\*\*\*\*\*\*.zip |Code source. |
|SourceLocation |String  |https://vefaas.tos\-s3\-cn.ibytepluses.com/template_dir/666ad2abcvefaas\-python3.9\-default.zip?X\-Amz\*\*\*\*\*\* |The source address of the code/image. |
|SourceType |String  |zip |Type of code source: parameter value:<br><br><br>* **zip**: Local compressed file.<br><br>* **tos**: Torch Object Storage (TOS).<br><br>* **image**: Container Registry (CR). |
|Envs |Array of [EnvVar](https://docs.byteplus.com/en/docs/192/65922#envvar) |\- |Function environment variables. |
|VpcConfig |Object of [VpcConfig](https://docs.byteplus.com/en/docs/192/65922#vpcconfig) |\- |Virtual Private Cloud (VPC) configuration for the function. |
|CreationTime |String  |2020\-05\-20T13:00:55Z |The function creation time. |
|LastUpdateTime |String  |2020\-05\-20T13:00:55Z |The time of the last function update. |
|TlsConfig |Object of [TlsConfig](https://docs.byteplus.com/en/docs/192/65922#tlsconfig) |\- |Torch Log Service\-related configuration in a function. |
|TriggersCount |Integer |0 |Number of function triggers. |
|NasStorage |Object of [NasStorage](https://docs.byteplus.com/en/docs/192/65922#nasstorage) |\- |FileNAS mount configuration. |
|TosMountConfig |Object of [TosMountConfig](https://docs.byteplus.com/en/docs/192/65922#tosmountconfig) |\- |Torch Object Storage (TOS) mount configuration. |
|Command |String  |./run.sh |Custom start command for function instances. |
|Port |Integer |8,000 |Custom listening ports for function instances. |
|CpuStrategy |String  |always |CPU operation and billing policies for function instances. Parameter value:<br><br><br>* **always**: CPU is always allocated, which means that at least one function instance is running.<br><br>* **request**: CPU is allocated only when requested. |
|ProjectName |String  |default |Project name for the new function. |
|Cell |String  |2 |The Cell to which the function belongs. |


<span id="envvar"></span>
### EnvVar


|**parameter** |**Type** |**sample value** |**Description** |
|---|---|---|---|
|Key |String  |business_type |The environment variable key. |
|Value |String  |free |The values for environment variables. |


<span id="vpcconfig"></span>
### VpcConfig


|**parameter** |**Type** |**sample value** |**Description** |
|---|---|---|---|
|EnableVpc |Boolean |false |Whether VPC access is enabled for the function. Parameter value:<br><br><br>* **false**: Not enabled; the function can access the public network through the default network interface card.<br><br>* **true**: Enable, the function can access resources in the specified VPC. |
|VpcId |String  |vpc\-2d73mgm\*\*\*\* |ID of the VPC to which the function belongs. |
|SubnetIds |Array of String |["subnet\-mj1l\*\*\*\*\*\*"] |Subnet ID corresponding to the function after VPC access is enabled. |
|SecurityGroupIds |Array of String |["sg\-3re8ffwjclybk5zsk\*\*\*\*"] |The security group ID for the function after VPC access is enabled. |
|EnableSharedInternetAccess |Boolean |false |The switch for the function to access the public network. Access the public network via the VPC shared NAT gateway provided by BytePlus Function Service Parameter value:<br><br><br>* **true**: Turned on, access the public network through the default network interface card. Traffic charges will be incurred on the public network.<br><br>* **false**: Turned off, the function cannot access the public network through the default network interface card. |


<span id="tlsconfig"></span>
### TlsConfig


|**parameter** |**Type** |**sample value** |**Description** |
|---|---|---|---|
|EnableLog |Boolean |false |Whether to enable the Logs feature. Parameter value:<br><br><br>* **true**: Turned on, the stdout/stderr logs of the function will be collected into the specified logs project and logs topic of the Torch Log Service.<br><br>* **false**: Turned off, the logs are not collected.  |
|TlsTopicId |String  |0cd4e4c4\-5436\-4b05\-b39e\-\*\*\*\* |TLS Logs theme ID. |
|TlsProjectId |String  |48f49d74\-cd50\-4591\-a3d0\-\*\*\*\* |TLS Logs project ID. |


<span id="nasstorage"></span>
### NasStorage


|**parameter** |**Type** |**sample value** |**Description** |
|---|---|---|---|
|EnableNas |Boolean |false |Whether to enable NAS storage mount; parameter value:<br><br><br>* **true**: Turned on, store data to NAS.<br><br>* **false**: Do not turn on. |
|NasConfigs |Array of [NasConfig](https://docs.byteplus.com/en/docs/192/65922#nasconfig) |\- |NAS storage configuration. |


<span id="tosmountconfig"></span>
### TosMountConfig


|**parameter** |**Type** |**sample value** |**Description** |
|---|---|---|---|
|EnableTos |Boolean |false |Whether to enable TOS storage mount. Parameter value:<br><br><br>* **true**: Turn on to store data in TOS.<br><br>* **false**: Do not turn on. |
|Credentials |Object of [Credentials](https://docs.byteplus.com/en/docs/192/65922#credentials) |\- |After turning on TOS storage mount, configure the access keys (AK/SK) required for TOS domain access permissions. |
|MountPoints |Array of [TosMountPoint](https://docs.byteplus.com/en/docs/192/65922#tosmountpoint) |\- |List of TOS storage configurations after enabling the TOS storage mount |


<span id="nasconfig"></span>
### NasConfig


|**parameter** |**Type** |**sample value** |**Description** |
|---|---|---|---|
|RemotePath |String  |/ |File system remote directory. |
|FileSystemId |String  |enas\-cns\*\*\*\*\*\* |NAS file system ID. |
|MountPointId |String  |mount\-63\*\*\*\*\*\* |NAS mount point ID. |
|LocalMountPath |String  |/mnt/nas |Function local mount directory. |


<span id="credentials"></span>
### Credentials


|**parameter** |**Type** |**sample value** |**Description** |
|---|---|---|---|
|AccessKeyId |String  |\*\*\*\*\*\* |AccessKey ID (AK) of the BytePlus root user. |
|SecretAccessKey |String  |\*\*\*\*\*\* |Secret Access Key (SK) for the BytePlus root user. |


<span id="tosmountpoint"></span>
### TosMountPoint


|**parameter** |**Type** |**sample value** |**Description** |
|---|---|---|---|
|Endpoint |String  |http://tos\-ap\-southeast\-1.ibytepluses.com |TOS accesses the domain name. |
|ReadOnly |Boolean |true |Function's local directory access permission: After mounting a TOS Bucket, is the function's local mount directory read\-only? Parameter values:<br><br><br>* **true**: Read only<br><br>* **false**(default): Read and write |
|BucketName |String  |ai\-model |The TOS bucket name |
|BucketPath |String  |/ |The mount TOS Bucket path. |
|LocalMountPath |String  |/mnt/tos |Function local mount directory. |


<span id=".6L-U5Zue56S65L6L"></span>
## sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CopyFunction",
        "Version": "2021-03-03",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Id": "aye******",
        "Name": "new-function",
        "Description": "Copy function",
        "Runtime": "python3.8/v1",
        "ExclusiveMode": true,
        "RequestTimeout": 30,
        "MaxConcurrency": 30,
        "MemoryMB": 1024,
        "CodeSize": 473,
        "CodeSizeLimit": 15,
        "Source": "pqy******/3kwem******.zip",
        "SourceLocation": "https://vefaas.tos-s3-cn.ibytepluses.com/template_dir/666ad2abcvefaas-python3.9-default.zip?X-Amz******",
        "SourceType": "zip",
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
            "EnableSharedInternetAccess": true
        },
        "CreationTime": "2020-05-20T13:00:55Z",
        "LastUpdateTime": "2020-05-20T13:00:55Z",
        "TlsConfig": {
            "EnableLog": false,
            "TlsTopicId": "0cd4e4c4-5436-4b05-b39e-****",
            "TlsProjectId": "48f49d74-cd50-4591-a3d0-****"
        },
        "TriggersCount": 0,
        "NasStorage": {
            "EnableNas": false,
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
            "EnableTos": true,
            "Credentials": {
                "AccessKeyId": "******",
                "SecretAccessKey": "******"
            },
            "MountPoints": [
                {
                    "Endpoint": "http://tos-ap-southeast-1.ibytepluses.com",
                    "ReadOnly": true,
                    "BucketName": "ai-model",
                    "BucketPath": "/",
                    "LocalMountPath": "/mnt/tos"
                }
            ]
        },
        "Command": "./run.sh",
        "Port": 8000,
        "CpuStrategy": "always",
        "ProjectName": "default",
        "Cell": "2"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Code

There is no error code dedicated to this interface currently. If you encounter an exception when calling the interface, you can refer to [public error code](https://docs.byteplus.com/en/docs/faas/Public_error_code) for troubleshooting.
