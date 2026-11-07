---
title: "UpdateComponentStep"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/UpdateComponentStep"
---

Update custom steps. This action allows updating certain descriptive fields, such as the description, the default value for inputs, and more. It is recommended for use in compatibility upgrade scenarios.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended to select the service address that corresponds to the Region where your resources are located. For details, refer to [Service Address](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=UpdateComponentStep&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UpdateComponentStep |The API name. The name of the current API is `UpdateComponentStep`. |
|Version |String |Yes |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|Identifier |String |Yes |custom@1.0.0/\*\*\*\* |Unique identifier for custom step. |
|ComponentStepYaml |String |no |c3RlcDogdjJjdXN0b21zdGVwCmRpc3BsYXlOYW1lOiDoh6rlrprkuYnmraXpqqR2Mi3mm7TmlrAKaW1hZ2U6IGJ1c3lib3g6bGF0ZXN0CmlucHV0czoKICAtIG5hbWU6IGNvbW1hbmQKICAgIGRpc3BsYXlOYW1lOiDlkb3ku6TmiafooYwKICAgIHR5cGU6IHN0cmluZwogICAgZGVmYXVsdFZhbHVlOiBlY2hvIGhlbGxvIHdvcmxkCiAgICByZXF1aXJlZDogdHJ1ZQogICAgZGVzY3JpcHRpb246IOi+k+WHuuasoui/juWRveS7pAogICAgdWlDb25maWc6CiAgICAgIHR5cGU6IElucHV0CnNjcmlwdDogfAogICQoaW5wdXRzLmNvbW1hbmQpCmR\*\*\*\*\*\* |The Base64\-encoded YAML description file for custom steps. For a detailed explanation of the Custom steps YAML, see [Create Custom steps](https://docs.byteplus.com/en/docs/cp/Create_custom_steps). |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=UpdateComponentStep&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "ComponentStepYaml": "c3RlcDogdjJjdXN0b21zdGVwCmRpc3BsYXlOYW1lOiDoh6rlrprkuYnmraXpqqR2Mi3mm7TmlrAKaW1hZ2U6IGJ1c3lib3g6bGF0ZXN0CmlucHV0czoKICAtIG5hbWU6IGNvbW1hbmQKICAgIGRpc3BsYXlOYW1lOiDlkb3ku6TmiafooYwKICAgIHR5cGU6IHN0cmluZwogICAgZGVmYXVsdFZhbHVlOiBlY2hvIGhlbGxvIHdvcmxkCiAgICByZXF1aXJlZDogdHJ1ZQogICAgZGVzY3JpcHRpb246IOi+k+WHuuasoui/juWRveS7pAogICAgdWlDb25maWc6CiAgICAgIHR5cGU6IElucHV0CnNjcmlwdDogfAogICQoaW5wdXRzLmNvbW1hbmQpCmR******",
    "Identifier": "custom@1.0.0/****"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This interface does not have any unique return parameters.

<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "202404071710430739950998FB2847****",
        "Action": "UpdateComponentStep",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API does not currently have independent error codes. If an exception occurs during an API call, refer to [public error codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
