---
title: "ModifyDBEndpointDNS"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBEndpointDNS"
---

Call the ModifyDBEndpointDNS API to modify the resolution method of a private network address.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBEndpointDNS&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-6subnyth\*\*\*\* |Instance ID. |
|EndpointId |String |Yes |vedbm\-6subnyth\*\*\*\*\-Custom\-0cul |Connection endpoint ID. |
|NetworkType |String |Yes |Private |The network address type. The value is fixed to Private, which indicates a private network address. |
|DNSVisibility |Boolean |Yes |false<br><br> |Resolution method, with the following values:<br><br><br>* `false`: Volcengine private network resolution (Default).<br><br>* `true`: BytePlus private and public network resolution. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=ModifyDBEndpointDNS&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceId": "vedbm-6subnyth****",
    "EndpointId": "vedbm-6subnyth****-Custom-0cul",
    "DNSVisibility": true,
    "NetworkType": "Private"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20250730105732B723CAE9534666C1025E-b7e99e",
        "Action": "ModifyDBEndpointDNS",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
