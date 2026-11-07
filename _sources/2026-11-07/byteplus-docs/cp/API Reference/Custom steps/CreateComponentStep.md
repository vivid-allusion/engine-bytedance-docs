---
title: "CreateComponentStep"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/CreateComponentStep"
---

Create a custom step; only one custom step can be created at a time.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the Region where your resources are located. For details, see [Service Address](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=CreateComponentStep&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateComponentStep |The API name. The name of the current API is `CreateComponentStep`. |
|Version |String |Yes |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|ComponentStepYaml |String |Yes |c3RlcDogdjJjdXN0b21zdGVwCmRpc3BsYXlOYW1lOiDoh6rlrprkuYnmraXpqqR2MgppbWFnZTogYnVzeWJveDpsYXRlc3QKaW5wdXRzOgogIC0gbmFtZTogY29tbWFuZAogICAgZGlzcGxheU5hbWU6IOWRveS7pOaJp+ihjAogICAgdHlwZTogc3RyaW5nCiAgICBkZWZhdWx0VmFsdWU6IGVjaG8gaGVsbG8gd29ybGQKICAgIHJlcXVpcmVkOiB0cnVlCiAgICBkZXNjcmlwd\*\*\*\*\*\*\*\*\*\* |Base64 character encoding of the YAML description file for custom steps. For detailed instructions on the Custom steps YAML, see [create custom steps](https://docs.byteplus.com/en/docs/cp/Create_custom_steps). |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=CreateComponentStep&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "ComponentStepYaml": "c3RlcDogdjJjdXN0b21zdGVwCmRpc3BsYXlOYW1lOiDoh6rlrprkuYnmraXpqqR2MgppbWFnZTogYnVzeWJveDpsYXRlc3QKaW5wdXRzOgogIC0gbmFtZTogY29tbWFuZAogICAgZGlzcGxheU5hbWU6IOWRveS7pOaJp+ihjAogICAgdHlwZTogc3RyaW5nCiAgICBkZWZhdWx0VmFsdWU6IGVjaG8gaGVsbG8gd29ybGQKICAgIHJlcXVpcmVkOiB0cnVlCiAgICBkZXNjcmlwd**********"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Identifier |String |custom@1.0.0/\*\*\*\* |Unique identifier for the custom step. The format is: `custom@1.0.0/{stepname}@{version}`. Here, stepname corresponds to the 'step' field and version corresponds to the 'version' field in the YAML file.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">All existing steps without a specified version number default to version 1.0.0.</div><br> |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "202404071957425A4199174603BF6****",
        "Action": "CreateComponentStep",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Identifier": "custom@1.0.0/****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This interface currently does not have dedicated error codes. If the interface call returns an exception, refer to [public error codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
