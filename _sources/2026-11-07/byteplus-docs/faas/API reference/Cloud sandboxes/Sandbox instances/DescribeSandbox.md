---
title: "DescribeSandbox"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/DescribeSandbox"
---

Obtain sandbox instance details.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Request method: POST

* Request URL: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=DescribeSandbox&Version=2024\-06\-06


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |DescribeSandbox |Interface name. The name of the current API is `DescribeSandbox`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06 `. |
|SandboxId |String |Yes |vefaas\-fnhyb3lm\-ku58oo12ls\-\*\*\*\* |Sandbox instance ID/name.<br><br>To obtain sandbox instance IDs, you can go to [Function Service Console](https://console.byteplus.com/vefaas) \> **Cloud sandbox** \> **Sandbox application** page, click the target sandbox application, and switch to **Sandbox example** tab. |
|FunctionId |String |Yes |fnhy\*\*\*\* |The ID of the sandbox application to which sandbox instances belong.<br><br>To obtain sandbox application IDs, you can go to [BytePlus Function Service (FaaS) console](https://console.byteplus.com/vefaas) \> **Cloud sandbox** \> **Sandbox application** page. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=DescribeSandbox&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "SandboxId": "vefaas-fnhyb3lm-ku58oo12ls-****",
    "FunctionId": "fnhy****"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |vefaas\-fnhyb3lm\-ku58oo12ls\-\*\*\*\* |Sandbox instance ID/name. |
|FunctionId |String |fnhy\*\*\*\* |The ID of the sandbox application to which sandbox instances belong. |
|Metadata |JSON Map |{"app":"test"} |The metadata of sandbox instance labels. |
|CreatedAt |String |2025\-04\-25 11:11:29.376 +0000 UTC |The creation time of sandbox instances. |
|ExpireAt |String |2025\-04\-25 11:31:29.376 +0000 UTC |Sandbox instance lifetime. |
|Status |String |Ready |Sandbox instance status:  <br><br><br>* **Starting**: in progress of starting<br><br>* **Ready**: started already<br><br>* **Failed**: failed to start<br><br>* **Terminating**: in progress of terminating |
|RevisionNumber |Integer |1 |Function instance version number. |
|AvailabilityZone |String |ap\-southeast\-1a |The availability zone ID of sandbox instances. |
|InstanceType |String |elastic |Sandbox instance types. Parameter value description:<br><br><br>* **elastic**: elastic instance<br><br>* **frozen**: frozen instance<br><br>* **activated**: activated instance<br><br>* **reserved**: reserved instance |
|ErrorCode |String |function_health_check_failed |Error codes for start failures of the sandbox instance:  <br><br><br>* `internal_load_request_error`: Internal system error<br><br>* `function_initialize_failed`: Business process initialization error<br><br>* `function_health_check_failed`: Health check error<br><br>* `route_terminating`: in progress of deleting route<br><br><br>This field is empty if the sandbox instance starts normally. |
|ErrorMessage |String |function_health_check_failed |Details of the error code for the start failures of sandbox instances.<br><br>This field is empty if sandbox instances start normally. |
|Pending |Boolean |true |Whether a sandbox instance is in **Pending** status:  <br><br><br>* **true**: yes<br><br>* **false**: no |
|RequestTimeout |Integer |60 |Maximum request timeout for sandbox instances. |
|MaxConcurrency |Integer |100 |Maximum concurrent requests per sandbox instance. |
|MemoryMB |Integer |1,024 |The memory specification of a sandbox instance, measured in MiB. |
|CpuMilli |Integer |500 |The CPU specification of a sandbox instance, measured in milliCPU. |
|ImageInfo |Object of [InstanceImageInfo](https://docs.byteplus.com/en/docs/192/69678#instanceimageinfo) |\- |Image information of sandbox instances, including image address, start command, and listening port. |
|Envs |Array of [EnvVar](https://docs.byteplus.com/en/docs/192/69678#envvar) |\- |The environment variables for sandbox instances. |
|InstanceTosMountConfig |Object of [InstanceTosMountConfig](https://docs.byteplus.com/en/docs/192/69678#instancetosmountconfig) |\- |The TOS mount information of the sandbox instance, which is the information of TOS Bucket mount directory at the instance level. |


<span id="instanceimageinfo"></span>
### InstanceImageInfo


|**Parameter** |**Type** |**sample value** |**Description** |
|---|---|---|---|
|Id |String |xGWv9\*\*\*\* |The ID of the preheated image used by sandbox instances. |
|Port |Integer |8,080 |Listening ports of sandbox instances.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Note that these ports are already occupied by FaaS: 9000, 9001, 9990.</div><br> |
|Image |String |cr\-vefaas\-<br><br>ap\-southeast\-1.cr.bytepluses.com/wdf/test/\*\*\*\*:latest |The address of the preheated image used by sandbox instances. |
|Command |String |bash /root/sandbox/scripts/run.sh |The start command for sandbox instances. If you need to execute a script file instead, ensure entering an absolute path and the script file has execute permission. |


<span id="envvar"></span>
### EnvVar


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Key |String |business_type |The key of an environment variable for sandbox instances. |
|Value |String |free |The value of the environment variable for sandbox instances. |


<span id="instancetosmountconfig"></span>
### InstanceTosMountConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Enable |Boolean |true |Whether TOS mount is enabled for sandbox instances:<br><br><br>* **true**: Yes<br><br>* **false**: No |
|TosMountPoints |Array of [TosMountPoint](https://docs.byteplus.com/en/docs/192/69678#tosmountpoint) |\- |The detailed information of TOS mount directories used by sandbox instances. |


<span id="tosmountpoint"></span>
### TosMountPoint


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|BucketPath |String |/sandbox |The TOS remote directory mounted to sandbox instances. |
|LocalMountPath |String |/mnt/tos |The local directory for the TOS storage bucket mounted to sandbox instances.<br><br>If this directory is the local mount directory for TOS storage configured in the sandbox application, the system will modify TOS BucketPath accordingly. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeSandbox",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Id": "vefaas-fnhyb3lm-ku58oo12ls-****",
        "FunctionId": "fnhy****",
        "Metadata": {
            "app": "test"
        },
        "CreatedAt": "2025-04-25 11:11:29.376 +0000 UTC",
        "ExpireAt": "2025-04-25 11:31:29.376 +0000 UTC",
        "Status": "Ready",
        "RevisionNumber": 1,
        "AvailabilityZone": "ap-southeast-1a",
        "InstanceType": "elastic",
        "ErrorCode": "function_health_check_failed",
        "ErrorMessage": "function_health_check_failed",
        "Pending": true,
        "RequestTimeout": 60,
        "MaxConcurrency": 100,
        "MemoryMB": 1024,
        "CpuMilli": 500,
        "ImageInfo": {
            "Id": "xGWv9****",
            "Port": 8080,
            "Image": "cr-vefaas-ap-southeast-1.cr.bytepluses.com/wdf/test/****:latest",
            "Command": "bash /root/sandbox/scripts/run.sh"
        },
        "Envs": [
            {
                "Key": "business_type",
                "Value": "free"
            }
        ],
        "InstanceTosMountConfig": {
            "Enable": true,
            "TosMountPoints": [
                {
                    "BucketPath": "/sandbox",
                    "LocalMountPath": "/mnt/tos"
                }
            ]
        }
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There is no error code dedicated to this interface currently. If you encounter an exception when calling the interface, you can refer to [Public error codes](https://docs.byteplus.com/en/docs/faas/Public_error_code) for troubleshooting.
