---
title: "GetRevision"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/GetRevision"
---

Obtain the version information of a function, including the configuration and code information of the current version.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Request method: POST

* Request address: http://open.volcengineapi.com/?Action=GetRevision&Version=2024\-06\-06


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=GetRevision&serviceCode=vefaas&version=2024-06-06&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetRevision |Interface name. The current API is called `GetRevision`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06 `. |
|FunctionId |String |Yes |aj\*\*\*\*\*\* |Function ID. |
|RevisionNumber |Integer |Yes |1 |Function version number. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST http://open.volcengineapi.com/?Action=GetRevision&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "FunctionId": "aj******",
    "RevisionNumber": 1
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |nw\*\*\*\*\*\* |Function ID. |
|Name |String |official\-site |Function name. |
|Description |String |This is a description |Function description. |
|RevisionNumber |Integer |1 |Function version number. |
|RevisionDescription |String |This is a revision description |Function version description. |
|Runtime |String |python3.8/v1 |Function Runtime. |
|ExclusiveMode |Boolean |false |Exclusive mode switch.<br><br><br>* true: Turn off multiple concurrent requests per instance, that is, the exclusive mode in which a single instance can only process one request at a time.<br><br>* false (default): Turn on multiple concurrent requests per instance, that is, the non\-exclusive mode where a single instance can handle multiple requests at the same time, and you can set the maximum number of concurrent requests that a single instance can carry through MaxConcurrency. |
|RequestTimeout |Integer |30 |Request timed out (the unit is second). |
|MaxReplicas |Integer |10 |Maximum number of instances. |
|MaxConcurrency |Integer |100 |Single instance maximum concurrency. When ExclusiveMode=false, this parameter can be set, and the value range is 10\-1,000. |
|MemoryMB |Integer |1,024 |Maximum memory per instance (the unit is MB). |
|CodeSize |Integer |1,024 |Code package size. |
|CodeSizeLimit |Integer |64 |The maximum size of the code package is only exposed to administrators/users who have opened the allowlist. Native function is default 256 MB, and others are default 64 MB. |
|Source |String |templates/vefaas\-python38\-default.zip |Code/image source. |
|SourceLocation |String |tos://tos\-cn\-beijing.volces.com/test.zip |The source address of the code/image. |
|SourceType |String |tos |Code source type. |
|Envs |Array of [EnvVar](https://docs.byteplus.com/en/docs/192/57182#envvar) |\- |Function Environment variables. |
|VpcConfig |Object of [VpcConfig](https://docs.byteplus.com/en/docs/192/57182#vpcconfig) |\- |VPC configuration. |
|HealthCheckConfig |Object of [HealthCheckConfig](https://docs.byteplus.com/en/docs/192/57182#healthcheckconfig) |\- |Health check configuration. |
|CreationTime |String |2020\-05\-20T13:00:55Z |Function creation time. |
|RevisionCreationTime |String |2020\-05\-20T13:00:55Z |Version creation time. |
|TlsConfig |Object of [TlsConfig](https://docs.byteplus.com/en/docs/192/57182#tlsconfig) |\- |Function TLS Logs configuration. |
|InstanceType |String |nvidia\-tesla\-l4 |Function instance type.<br><br><br>* Null value: CPU instance type.<br><br>* Non\-null value: Specific GPU instance type. |
|NasStorage |Object of [NasStorage](https://docs.byteplus.com/en/docs/192/57182#nasstorage) |\- |FileNAS configuration. |
|TosMountConfig |Object of [TosMountConfig](https://docs.byteplus.com/en/docs/192/57182#tosmountconfig) |\- |TOS Object Storage mount configuration. |
|InitializerSec |Integer |30 |Function initialization timeout configuration. |
|FunctionType |String |sandbox |Function type. |
|Role |String |trn:iam::1400000044:role/VeFaaSDefaultRole |Function instance binds IAM role |
|AsyncTaskConfig |Object of [AsyncTaskConfig](https://docs.byteplus.com/en/docs/192/57182#asynctaskconfig) |{"EnableAsyncTask":true,"MaxRetry":3,"DestinationConfig":{"OnFailure":{"Destination":"http://dummyinstanceid.apigateway\-cn\-beijing\-\*\*\*\*.\*\*\*\*.com/failure"},"OnSuccess":{"Destination":"http://dummyinstanceid.apigateway\-cn\-beijing\-inner.volceapi.com/success"}}} |Asynchronous task configuration. |


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
|EnableVpc |Boolean |false |Whether the function enables VPC access. Parameter value:<br><br><br>* **false**: Disabled; the function can access the public network via the default network interface.<br><br>* **true**: Enabled; the function can access resources in the specified VPC. |
|VpcId |String |vpc\-2d73mgm\*\*\*\* |ID of the VPC to which the function belongs. |
|SubnetIds |Array of String |["subnet\-mj1l\*\*\*\*\*\*"] |Subnet ID after the function enables VPC access. |
|SecurityGroupIds |Array of String |["sg\-3re8ffwjclybk5zsk\*\*\*\*"] |Security group ID after the function enables VPC access. |
|EnableSharedInternetAccess |Boolean |false |The switch for the function to access the public network. Whether to access the public network through veFaaS's VPC shared NAT gateway. Parameter values:<br><br><br>* **true**: Turned on, access the public network through the default network interface card. Traffic charges will be incurred on the public network.<br><br>* **false**: Turned off, the function cannot access the public network through the default network interface card. |


<span id="healthcheckconfig"></span>
### HealthCheckConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|EnableHealthCheck |Boolean |true |Whether to turn on health check:<br><br><br>* true: Turn on.<br><br>* **false**: Turn off. |
|ProbeHandler |Object of [ProbeHandler](https://docs.byteplus.com/en/docs/192/57182#probehandler) |\- |Type of health check. |
|InitialDelaySeconds |Integer |5 |Delay time before the first health check, in seconds. |
|PeriodSeconds |Integer |10 |The interval between each health check, in seconds. |
|TimeoutSeconds |Integer |2 |Timeout for each health check, in seconds. |
|FailureThreshold |Integer |3 |The number of consecutive failures required before a probe is judged to fail. |
|SuccessThreshold |Integer |3 |The number of consecutive successes required before a probe is judged to be successful. |


<span id="tlsconfig"></span>
### TlsConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|EnableLog |Boolean |false |Whether to enable the log feature, parameter values:<br><br><br>* **true**: Turned on, the stdout/stderr logs of the function will be collected into the specified logs project and logs topic of the Torch Log Service.<br><br>* **false**: Turned off, the logs are not collected.  |
|TlsTopicId |String |0cd4e4c4\-5436\-4b05\-b39e\-\*\*\*\* |TLS Logs theme ID. |
|TlsProjectId |String |48f49d74\-cd50\-4591\-a3d0\-\*\*\*\* |TLS Logs project ID. |


<span id="nasstorage"></span>
### NasStorage


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|EnableNas |Boolean |false |Whether to enable NAS storage mount, parameter value:<br><br><br>* **true**: Turned on, store data to NAS.<br><br>* **false**: Do not turn on. |
|NasConfigs |Array of [NasConfig](https://docs.byteplus.com/en/docs/192/57182#nasconfig) |\- |NAS storage configuration. |


<span id="tosmountconfig"></span>
### TosMountConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|EnableTos |Boolean |false |Whether to enable TOS storage mount, parameter values:<br><br><br>* **true**: Turn on, store data in TOS.<br><br>* **false**: Do not turn on. |
|Credentials |Object of [Credentials](https://docs.byteplus.com/en/docs/192/57182#credentials) |\- |After turning on TOS storage mount, you need to provide an access key (AK/SK) with TOS domain access permission. |
|MountPoints |Array of [TosMountPoint](https://docs.byteplus.com/en/docs/192/57182#tosmountpoint) |\- |After enabling TOS storage mount, you need to provide a TOS storage configuration list. No more than 5 items. |


<span id="asynctaskconfig"></span>
### AsyncTaskConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|MaxRetry |Integer |3 |Number of asynchronous task failure retries, selectable values are 0–3. |
|EnableAsyncTask |Boolean |true |Whether to enable asynchronous task. |
|DestinationConfig |Object of [DestinationConfig](https://docs.byteplus.com/en/docs/192/57182#destinationconfig) |\- |Asynchronous task callback target configuration. |


<span id="probehandler"></span>
### ProbeHandler


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|HTTPGet |Object of [HTTPGetAction](https://docs.byteplus.com/en/docs/192/57182#httpgetaction) |\- |Survival detection using the HTTP protocol. |
|TCPSocket |Object of [TCPSocketAction](https://docs.byteplus.com/en/docs/192/57182#tcpsocketaction) |\- |Survival detection using TCP protocol. |


<span id="nasconfig"></span>
### NasConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Gid |Long |1,000 |User group in the file system; custom settings are not supported yet. If this parameter is provided, the parameter value must be consistent with the GID of the function's run user, and the value must be: 1000. |
|Uid |Long |1,000 |User in the file system; custom values are not supported for now. If this parameter is provided, its value must be consistent with the function run user uid, and the value must be: 1000. |
|RemotePath |String |/ |File system remote directory. Length: 1–128 characters, must start with “`/`”, supports uppercase and lowercase letters, digits, and special characters (`- . _ ~ / : @ = + ? #`). |
|FileSystemId |String |enas\-cns\*\*\*\*\*\* |NAS file system ID. |
|MountPointId |String |mount\-63\*\*\*\*\*\* |NAS mount point ID. |
|LocalMountPath |String |/mnt/nas |Function local mount directory. Length: 1–128 characters, must start with “`/`”, supports uppercase and lowercase letters, digits, and special characters (`- . _ ~ / : @ = + ? #`). |


<span id="credentials"></span>
### Credentials


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|AccessKeyId |String |\*\*\*\*\*\* |AccessKey ID (AK) of the BytePlus root user. For the obtaining method, please refer to the [Access key usage guide ](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-access-keys). |
|SecretAccessKey |String |\*\*\*\*\*\* |Secret Access Key (SK) for the BytePlus root user. For the obtaining method, please refer to the [Access key usage guide ](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-access-keys). |


<span id="tosmountpoint"></span>
### TosMountPoint


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Endpoint |String |http://tos\-cn\-beijing.ivolces.com |TOS accesses the domain name. |
|ReadOnly |Boolean |true |Function local directory access permission. After mounting the TOS Bucket, specifies whether the function's local mount directory access permission is read\-only. Parameter values:<br><br><br>* **true**: Read only<br><br>* **false**(default): Read and write |
|BucketName |String |ai\-model |TOS bucket name |
|BucketPath |String |/ |The mount TOS Bucket path. |
|LocalMountPath |String |/mnt/tos |Function local mount directory. |


<span id="destinationconfig"></span>
### DestinationConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|OnFailure |Object of [Destination](https://docs.byteplus.com/en/docs/192/57182#destination) |\- |Callback target configuration when the task executes successfully. |
|OnSuccess |Object of [Destination](https://docs.byteplus.com/en/docs/192/57182#destination) |\- |Callback target configuration when task execution fails. |


<span id="httpgetaction"></span>
### HTTPGetAction


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Path |String |/hello |The path to access the HTTP server. |
|Port |Integer |8,080 |The port number or port name to be accessed.<br><br><br>* The number must be in the range of 1 to 65535.<br><br>* The name must be IANA_SVC_NAME. |
|Scheme |String |HTTP |Protocol scheme for connecting to the host; supports the following values:<br><br><br>* `HTTP`: Use HTTP protocol.<br><br>* `HTTPS`: Use HTTPS protocol.<br><br>* `TCP`: Use TCP protocol.<br><br>   Default value is `HTTP`. |
|HTTPHeaders |Array of [HTTPHeader](https://docs.byteplus.com/en/docs/192/57182#httpheader) |\- |Custom header set in the request. HTTP allows duplicate headers. |


<span id="tcpsocketaction"></span>
### TCPSocketAction


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Port |Integer |8,080 |The port number or port name to be accessed.<br><br><br>* Number must be in the range 1 to 65535.<br><br>* Name must be IANA_SVC_NAME. |


<span id="destination"></span>
### Destination


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Destination |String |http://dummyinstanceid.apigateway\-cn\-beijing\-\*\*\*\*.volceapi.com |Specific callback target; setting the value to empty (“”) disables the callback. |


<span id="httpheader"></span>
### HTTPHeader


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Name |String |Content\-Type |HTTP Header name. |
|Value |String |application/json |HTTP Header value. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetRevision",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "nw******",
        "Name": "official-site",
        "Description": "This is a description",
        "RevisionNumber": 1,
        "RevisionDescription": "This is a revision description",
        "Runtime": "python3.8/v1",
        "ExclusiveMode": true,
        "RequestTimeout": 30,
        "MaxReplicas": 10,
        "MaxConcurrency": 100,
        "MemoryMB": 1024,
        "CodeSize": 1024,
        "CodeSizeLimit": 64,
        "Source": "templates/vefaas-python38-default.zip",
        "SourceLocation": "tos://tos-cn-beijing.volces.com/test.zip",
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
            "EnableSharedInternetAccess": true
        },
        "HealthCheckConfig": {
            "ProbeHandler": {
                "HTTPGet": {
                    "Path": "/hello ",
                    "Port": 8080,
                    "Scheme": "HTTP",
                    "HTTPHeaders": [
                        {
                            "Name": "Content-Type",
                            "Value": "application/json"
                        }
                    ]
                },
                "TCPSocket": {
                    "Port": 8080
                }
            },
            "PeriodSeconds": 10,
            "TimeoutSeconds": 2,
            "FailureThreshold": 3,
            "SuccessThreshold": 3,
            "EnableHealthCheck": true,
            "InitialDelaySeconds": 5
        },
        "CreationTime": "2020-05-20T13:00:55Z",
        "RevisionCreationTime": "2020-05-20T13:00:55Z",
        "TlsConfig": {
            "EnableLog": false,
            "TlsTopicId": "0cd4e4c4-5436-4b05-b39e-****",
            "TlsProjectId": "48f49d74-cd50-4591-a3d0-****"
        },
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
        "FunctionType": "",
        "Role": "trn:iam::1400000044:role/VeFaaSDefaultRole",
        "AsyncTaskConfig": {
            "EnableAsyncTask": true,
            "MaxRetry": 3,
            "DestinationConfig": {
                "OnFailure": {
                    "Destination": "http://dummyinstanceid.apigateway-cn-beijing-****.****.com/failure"
                },
                "OnSuccess": {
                    "Destination": "http://dummyinstanceid.apigateway-cn-beijing-****.****.com/success"
                }
            }
        }
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There is no error code dedicated to this interface currently. If you encounter an exception when calling the interface, you can refer to [Public error codes](https://docs.byteplus.com/en/docs/faas/Public_error_code) for troubleshooting.
