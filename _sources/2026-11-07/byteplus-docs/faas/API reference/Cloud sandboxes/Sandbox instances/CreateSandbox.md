---
title: "CreateSandbox"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/CreateSandbox"
---

Create sandbox instances.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Request method: POST

* Request URL: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=CreateSandbox&Version=2024\-06\-06


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateSandbox |Interface name. The name of the current API is `CreateSandbox`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The version of the current API is `2024-06-06`. |
|FunctionId |String |Yes |wrws\*\*\*\* |The ID of the sandbox application to which sandbox instances belong.<br><br>To obtain sandbox application IDs, you can go to [BytePlus Function Service (FaaS) console](https://console.byteplus.com/vefaas) \> **Cloud sandbox** \> **Sandbox application** page. |
|Timeout |Integer |No |60 |The lifetime of sandbox instances:<br><br><br>* Unit: minutes<br><br>* Value range: 3–1440<br><br>* Default value: 60 |
|Metadata |JSON Map |No |{"app":"test"} |The metadata of the sandbox instance label, which is used to mark and filter instances. The format is `<"key":"value">`. |
|InstanceTosMountConfig |Object of [InstanceTosMountConfig](https://docs.byteplus.com/en/docs/192/69670#instancetosmountconfig) |No |\- |Torch Object Storage (TOS) mount configuration of the sandbox instance.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If you need to include this parameter in requests, ensure TOS storage has been mounted to the sandbox application to which the instance belongs.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Sandbox instances can mount the subdirectories of TOS buckets based on TOS mount configuration of the sandbox application.</div><br> |
|Envs |Array of [EnvVar](https://docs.byteplus.com/en/docs/192/69670#envvar) |No |\- |Environment variables for sandbox instances. |
|InstanceImageInfo |Object of [InstanceImageInfo](https://docs.byteplus.com/en/docs/192/69670#instanceimageinfo) |No |\- |Image information of sandbox instances, including image address, start command, and listening port. |
|CpuMilli |Integer |No |1,000 |CPU specification of the sandbox instance :<br><br><br>* Unit: milliCPU<br><br>* Value range: 250–16000<br><br>* Default value: 1000 |
|MemoryMB |Integer |No |2048 |The memory specification of a sandbox instance:<br><br><br>* Unit: MiB<br><br>* Value range: 512–131072<br><br>* Default value: 2048 |
|MaxConcurrency |Integer |No |100 |Maximum concurrent requests per instance:<br><br><br>* Value range: 10–1000<br><br>* Default value: 100 |
|RequestTimeout |Integer |No |30 |Request timeout period:<br><br><br>* Unit: seconds<br><br>* Value range: positive integers from 1 to 900<br><br>* Default value: 30 |


<span id="instancetosmountconfig"></span>
### InstanceTosMountConfig


|**Parameter** |**Type** |**Required** |**sample value** |**Description** |
|---|---|---|---|---|
|Enable |Boolean |Yes |true |Whether to enable TOS mount for sandbox instances<br><br><br>* **true**: Yes<br><br>* **false**: No |
|TosMountPoints |Array of [TosMountPoint](https://docs.byteplus.com/en/docs/192/69670#tosmountpoint) |Yes |\- |The detailed information of TOS mount directory used by sandbox instances. |


<span id="envvar"></span>
### EnvVar


|**parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |business_type |Keys for sandbox instance environment variables. |
|Value |String |Yes |free |The value of the environment variable for the sandbox instance. |


<span id="instanceimageinfo"></span>
### InstanceImageInfo


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Id |String |No |xGWv9\*\*\*\* |ID of the preheated image used by the sandbox instance. |
|Port |Integer |Yes |8,080 |Listening port of the sandbox instance.<br><br>&nbsp;<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Note that these ports are already occupied by FaaS: 9000,9001,9990.</div><br> |
|Image |String |No |cr\-vefaas\-ap\-southeast\-1.cr.bytepluses.com/wdf/test/\*\*\*\*:latest |The address of the preheated image used by sandbox instances. |
|Command |String |Yes |bash /root/sandbox/scripts/run.sh |The start command for the sandbox instance. If you need to execute a script file instead, ensure entering an absolute path and the script file has execute permission. |


<span id="tosmountpoint"></span>
### TosMountPoint


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|BucketPath |String |Yes |/sandbox |The remote TOS directory mounted to the sandbox instance. |
|LocalMountPath |String |Yes |/mnt/tos |The local directory of the TOS storage bucket mounted to the sandbox instance.<br><br>If this directory is the local mount directory for TOS storage configured in the sandbox application, the system will modify TOS BucketPath accordingly. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=CreateSandbox&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "FunctionId": "wrws****",
    "Timeout": 60,
    "Metadata": {
        "app": "test"
    },
    "InstanceTosMountConfig": {
        "Enable": true,
        "TosMountPoints": [
            {
                "BucketPath": "/sandbox",
                "LocalMountPath": "/mnt/tos"
            }
        ]
    },
    "Envs": [
        {
            "Key": "business_type",
            "Value": "free"
        }
    ],
    "InstanceImageInfo": {
        "Id": "xGWv****",
        "Port": 8080,
        "Image": "cr-vefaas-ap-southeast-1.cr.bytepluses.com/wdf/test/****:latest",
        "Command": "bash /root/sandbox/scripts/run.sh"
    },
    "CpuMilli": 500,
    "MemoryMB": 1024,
    "MaxConcurrency": 20,
    "RequestTimeout": 30
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|SandboxId |String |vefaas\-e8m6xarn\-p2zamuv2fr\-\*\*\*\*\*\* |The ID, which is also the name of the sandbox instance. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateSandbox",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "SandboxId": "vefaas-e8m6xarn-p2zamuv2fr-******"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There is no error code dedicated to this interface currently. If you encounter an exception when calling the interface, you can refer to [Public error codes](https://docs.byteplus.com/en/docs/faas/Public_error_code) for troubleshooting.
