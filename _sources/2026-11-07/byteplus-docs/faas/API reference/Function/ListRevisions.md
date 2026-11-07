---
title: "ListRevisions"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/ListRevisions"
---

Obtain the version configurations of functions in batch.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Request method: POST

* Request address: http://open.volcengineapi.com/?Action=ListRevisions&Version=2024\-06\-06


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListRevisions&serviceCode=vefaas&version=2024-06-06&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListRevisions |Interface name. The current API is called `ListRevisions`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06 `. |
|FunctionId |String |Yes |pqy\*\*\*\*\*\* |Function ID. |
|PageNumber |Integer |No |1 |Paging parameter, the current page number is default 1. |
|PageSize |Integer |No |10 |Paging parameter, the size per page is default 10. |
|Filters |Array of [Filter](https://docs.byteplus.com/en/docs/192/57188#filter) |No |\- |Query filter criteria. |


<span id="filter"></span>
### Filter


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|Name |String |No |RevisionNumber |The filter key name of the query, only RevisionNumber (version number) is supported.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Filtered values do not support fuzzy queries.</div><br> |
|Values |Array of String |No |["2"] |Filter value for the query (Value). Multiple values are separated by half\-width commas (`,`). |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST http://open.volcengineapi.com/?Action=ListRevisions&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "FunctionId": "",
    "PageNumber": 1,
    "PageSize": 10,
    "Filters": [
        {
            "Name": "Ids",
            "Values": [
                "q06****",
                "rx1****"
            ]
        }
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Items |Array of [FunctionRevision](https://docs.byteplus.com/en/docs/192/57188#functionrevision) |\- |Function revision details list. |
|Total |Integer |1 |The total amount of the data in the response list. |


<span id="functionrevision"></span>
### FunctionRevision


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |nw\*\*\*\*\*\* |Function ID. |
|Envs |Array of [EnvVar](https://docs.byteplus.com/en/docs/192/57188#envvar) |\- |Function Environment variables. |
|Name |String |official\-site |Function name. |
|Source |String |templates/vefaas\-python38\-default.zip |Code/image source. |
|Runtime |String |python3.8/v1 |Function Runtime. |
|CodeSize |Integer |1,024 |Code package size. |
|MemoryMB |Integer |1,024 |Maximum memory per instance.<br><br><br>* Unit: MiB.<br><br>* Value range: 512~4,096.<br><br>   <div data-tips="true" data-tips-type="default">Description   </div><br>   <br><br><br><div data-tips="true" data-tips-type="default">The value takes 512 as the gradient.</div><br><br><br><br>* Default value: 1,024. |
|TlsConfig |Object of [TlsConfig](https://docs.byteplus.com/en/docs/192/57188#tlsconfig) |\- |Function TLS Logs configuration. |
|VpcConfig |Object of [VpcConfig](https://docs.byteplus.com/en/docs/192/57188#vpcconfig) |\- |VPC configuration. |
|NasStorage |Object of [NasStorage](https://docs.byteplus.com/en/docs/192/57188#nasstorage) |\- |FileNAS configuration. |
|SourceType |String |tos |Code Source type. |
|Description |String |This is a description |Function description. |
|MaxReplicas |Integer |10 |Maximum number of instances. |
|CreationTime |String |2020\-05\-20T13:00:55Z |Function creation time. |
|InstanceType |String |nvidia\-tesla\-l4 |Function instance type.<br><br><br>* Null value: CPU instance.<br><br>* Non\-null value: GPU instance. |
|CodeSizeLimit |Integer |64 |The code package size limit.<br><br><br>* Only the BytePlus root user can be configured.<br><br>* Default value: 64 MiB.<br><br>* Native function default value: 256 MiB. |
|ExclusiveMode |Boolean |false |Exclusive mode switch.<br><br><br>* true: Turn off multiple concurrent requests per instance, that is, the exclusive mode in which a single instance can only process one request at a time.<br><br>* false (default): Turn on multiple concurrent requests per instance, that is, the non\-exclusive mode where a single instance can handle multiple requests at the same time, and you can set the maximum number of concurrent requests that a single instance can carry through MaxConcurrency. |
|InitializerSec |Integer |30 |Function initialization timeout configuration. |
|MaxConcurrency |Integer |100 |Single instance maximum concurrency. It takes effect when `ExclusiveMode=false`, and the value range: 10~1,000. |
|RequestTimeout |Integer |30 |Request timed out.<br><br><br>* Unit: second.<br><br>* Value range: 1 to 900.<br><br>* Default value: 30. |
|RevisionNumber |Integer |1 |Function version number. |
|SourceLocation |String |tos://tos\-cn\-beijing.volces.com/test.zip |The source address of the code/image. |
|TosMountConfig |Object of [TosMountConfig](https://docs.byteplus.com/en/docs/192/57188#tosmountconfig) |\- |TOS Torch Object Storage mount configuration. |
|RevisionDescription |String |This is a revision description |Function version description. |
|RevisionCreationTime |String |2020\-05\-20T13:00:55Z |Version creation time. |
|Role |String |trn:iam::1400000044:role/VeFaaSDefaultRole |Function instance binds IAM role |
|FunctionType |String |sandbox |Function type. |
|AsyncTaskConfig |Object of [AsyncTaskConfig](https://docs.byteplus.com/en/docs/192/57188#asynctaskconfig) |{"EnableAsyncTask":true,"MaxRetry":3,"DestinationConfig":{"OnFailure":{"Destination":"http://dummyinstanceid.apigateway\-cn\-beijing\-\*\*\*\*.volceapi.com/failure"},"OnSuccess":{"Destination":"http://dummyinstanceid.apigateway\-cn\-beijing\-inner.volceapi.com/success"}}} |Asynchronous task configuration. |
|HealthCheckConfig |Object of [HealthCheckConfig](https://docs.byteplus.com/en/docs/192/57188#healthcheckconfig) |\- |Health check configuration. |


<span id="envvar"></span>
### EnvVar


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Key |String |business_type |The key of an environment variable for sandbox instances. |
|Value |String |free |The value of the environment variable for sandbox instances. |


<span id="tlsconfig"></span>
### TlsConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|EnableLog |Boolean |false |Whether to enable the log feature. Parameter values:<br><br><br>* **true**: Turned on, the stdout/stderr logs of the function will be collected into the specified logs project and logs topic of the Torch Log Service.<br><br>* **false**: Turned off, the logs are not collected.  |
|TlsTopicId |String |0cd4e4c4\-5436\-4b05\-b39e\-\*\*\*\* |TLS Logs theme ID. |
|TlsProjectId |String |48f49d74\-cd50\-4591\-a3d0\-\*\*\*\* |TLS Logs project ID. |


<span id="vpcconfig"></span>
### VpcConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|EnableVpc |Boolean |false |Whether to enable VPC access for the function. Parameter values:<br><br><br>* **false**: Not enabled; the function can access the public network via the default network interface.<br><br>* **true**: Enabled; the function can access resources in the specified VPC. |
|VpcId |String |vpc\-2d73mgm\*\*\*\* |ID of the VPC to which the function belongs. |
|SubnetIds |Array of String |["subnet\-mj1l\*\*\*\*\*\*"] |Subnet ID corresponding to the function after VPC access is enabled. |
|SecurityGroupIds |Array of String |["sg\-3re8ffwjclybk5zsk\*\*\*\*"] |Security group ID corresponding to the function after VPC access is enabled. |
|EnableSharedInternetAccess |Boolean |false |The switch for the function to access the public network. Whether to access the public network via veFaaS's VPC shared NAT gateway. Parameter values:<br><br><br>* **true**: Turned on, access the public network through the default network interface card. Traffic charges will be incurred on the public network.<br><br>* **false**: Turned off, the function cannot access the public network through the default network interface card. |


<span id="nasstorage"></span>
### NasStorage


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|EnableNas |Boolean |false |Whether to enable NAS storage mount, parameter values:<br><br><br>* **true**: Turned on, store data to NAS.<br><br>* **false**: Do not turn on. |
|NasConfigs |Array of [NasConfig](https://docs.byteplus.com/en/docs/192/57188#nasconfig) |\- |NAS storage configuration. |


<span id="tosmountconfig"></span>
### TosMountConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|EnableTos |Boolean |false |Whether to enable TOS storage mount, parameter values:<br><br><br>* **true**: Enabled; data is stored in TOS.<br><br>* **false**: Do not turn on. |
|Credentials |Object of [Credentials](https://docs.byteplus.com/en/docs/192/57188#credentials) |\- |After enabling TOS storage mount, you need to provide access keys (AK/SK) with TOS domain access permission. |
|MountPoints |Array of [TosMountPoint](https://docs.byteplus.com/en/docs/192/57188#tosmountpoint) |\- |After enabling TOS storage mount, you need to provide the TOS storage configuration list. A maximum of 5. |


<span id="asynctaskconfig"></span>
### AsyncTaskConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|MaxRetry |Integer |3 |Number of retry attempts for asynchronous task failure. Selectable values: 0~3. |
|EnableAsyncTask |Boolean |true |Whether to enable asynchronous task. |
|DestinationConfig |Object of [DestinationConfig](https://docs.byteplus.com/en/docs/192/57188#destinationconfig) |\- |Asynchronous task callback target configuration. |


<span id="healthcheckconfig"></span>
### HealthCheckConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|EnableHealthCheck |Boolean |true |Whether to turn on health check:<br><br><br>* true: Turn on.<br><br>* **false**: Turn off. |
|ProbeHandler |Object of [ProbeHandler](https://docs.byteplus.com/en/docs/192/57188#probehandler) |\- |Type of health check. |
|InitialDelaySeconds |Integer |5 |Delay before the first health check, in seconds. |
|PeriodSeconds |Integer |10 |The interval between each health check, in seconds. |
|TimeoutSeconds |Integer |2 |Timeout for each health check, in seconds. |
|FailureThreshold |Integer |3 |The number of consecutive failures required before a probe is judged to fail. |
|SuccessThreshold |Integer |3 |The number of consecutive successes required before a probe is judged to be successful. |


<span id="nasconfig"></span>
### NasConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Gid |Long |1,000 |User group in the file system. Customization is not supported for now. If this parameter is provided, its value must match the function run user gid, which is: 1000. |
|Uid |Long |1,000 |User in the file system; custom settings are not supported at this time. If this parameter is provided, the parameter value must be consistent with the function run user uid, with a value of: 1000. |
|RemotePath |String |/ |File system remote directory. Length: 1~128 characters. Must start with "`/`", supports uppercase and lowercase letters, numbers, and special characters (`- . _ ~ / : @ = + ? #`). |
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
|ReadOnly |Boolean |true |Function local directory access permission. After mounting the TOS Bucket, whether the function local mount directory is read\-only. Parameter values:<br><br><br>* **true**: Read only<br><br>* **false**(default): Read and write |
|BucketName |String |ai\-model |TOS bucket name |
|BucketPath |String |/ |The mount TOS Bucket path. |
|LocalMountPath |String |/mnt/tos |Function local mount directory. |


<span id="destinationconfig"></span>
### DestinationConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|OnFailure |Object of [Destination](https://docs.byteplus.com/en/docs/192/57188#destination) |\- |Callback destination configuration for successful task execution. |
|OnSuccess |Object of [Destination](https://docs.byteplus.com/en/docs/192/57188#destination) |\- |Callback destination configuration for failed task execution. |


<span id="probehandler"></span>
### ProbeHandler


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|HTTPGet |Object of [HTTPGetAction](https://docs.byteplus.com/en/docs/192/57188#httpgetaction) |\- |Survival detection using the HTTP protocol. |
|TCPSocket |Object of [TCPSocketAction](https://docs.byteplus.com/en/docs/192/57188#tcpsocketaction) |\- |Survival detection using TCP protocol. |


<span id="destination"></span>
### Destination


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Destination |String |http://dummyinstanceid.apigateway\-cn\-beijing\-\*\*\*\*.volceapi.com |Specific callback target. Setting the value to empty ("") disables the callback. |


<span id="httpgetaction"></span>
### HTTPGetAction


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Path |String |/hello |The path to access the HTTP server. |
|Port |Integer |8,080 |The port number or port name to be accessed.<br><br><br>* The number must be in the range of 1 to 65535.<br><br>* The name must be IANA_SVC_NAME. |
|Scheme |String |HTTP |Protocol scheme for connecting to the host. Supported values:<br><br><br>* `HTTP`: Use the HTTP protocol.<br><br>* `HTTPS`: Use the HTTPS protocol.<br><br>* `TCP`: Use the TCP protocol.<br><br>   Default value is `HTTP`. |
|HTTPHeaders |Array of [HTTPHeader](https://docs.byteplus.com/en/docs/192/57188#httpheader) |\- |Custom header set in the request. HTTP allows duplicate headers. |


<span id="tcpsocketaction"></span>
### TCPSocketAction


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Port |Integer |8,080 |The port number or port name to be accessed.<br><br><br>* Numbers must be in the range 1 to 65535.<br><br>* Name must be IANA_SVC_NAME. |


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
        "Action": "ListRevisions",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "cn-beijing"
    },
    "Result": {
        "Items": [
            {
                "Id": "nw******",
                "Envs": [
                    {
                        "Key": "ENV_NAME",
                        "Value": "ENV_VALUE"
                    }
                ],
                "Name": "official-site",
                "Source": "templates/vefaas-python38-default.zip",
                "Runtime": "python3.8/v1",
                "CodeSize": 1024,
                "MemoryMB": 1024,
                "TlsConfig": {
                    "EnableLog": true,
                    "TlsProjectId": "a40202c5-fe22-4ea7-******",
                    "TlsTopicId": "2ff955cb-1f03-4b9b-******"
                },
                "VpcConfig": {
                    "EnableVpc": true,
                    "VpcId": "vpc-rrag******",
                    "SubnetIds": [
                        "subnet-milb******"
                    ],
                    "SecurityGroupIds": [
                        "sg-rrag******"
                    ],
                    "EnableSharedInternetAccess": true
                },
                "NasStorage": {
                    "EnableNas": true,
                    "NasConfigs": [
                        {
                            "FileSystemId": "cnas-cnb******",
                            "MountPointId": "mount-bce15678",
                            "RemotePath": "/",
                            "LocalMountPath": "/mnt/nas",
                            "Uid": 1000,
                            "Gid": 1000
                        }
                    ]
                },
                "SourceType": "tos",
                "Description": "This is a description",
                "MaxReplicas": 10,
                "CreationTime": "2020-05-20T13:00:55Z",
                "CodeSizeLimit": 64,
                "ExclusiveMode": true,
                "InitializerSec": 30,
                "MaxConcurrency": 100,
                "RequestTimeout": 30,
                "RevisionNumber": 1,
                "SourceLocation": "tos://tos-cn-beijing.volces.com/test.zip",
                "TosMountConfig": {
                    "EnableTos": true,
                    "MountPoints": [
                        {
                            "BucketPath": "/",
                            "LocalMountPath": "/mnt/tos",
                            "ReadOnly": false,
                            "BucketName": "ai-models",
                            "Endpoint": "http://tos-cn-beijing.ivolces.com"
                        }
                    ],
                    "Credentials": {
                        "AccessKeyId": "******",
                        "SecretAccessKey": "******"
                    }
                },
                "RevisionDescription": "This is a revision description",
                "RevisionCreationTime": "2020-05-20T13:00:55Z"
            }
        ],
        "Total": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There is no error code dedicated to this interface currently. If you encounter an exception when calling the interface, you can refer to [Public error codes](https://docs.byteplus.com/en/docs/faas/Public_error_code) for troubleshooting.
