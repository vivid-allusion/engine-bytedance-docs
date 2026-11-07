---
title: "ModifyDBEndpointAddress"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBEndpointAddress"
---

Call the ModifyDBEndpointAddress API to modify the connection address port or prefix.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* After the new address takes effect, the old address will be closed three minutes later. Modify the connection configuration of the application synchronously, otherwise it may affect the business, so proceed with caution.

* Changing the port number will change the port numbers of the public and private networks simultaneously. After the new port takes effect, the old port will be closed immediately. Modify the connection configuration of the application synchronously, otherwise it may affect the business. Proceed with caution.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBEndpointAddress&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-6subnyth\*\*\*\* |Instance ID. |
|EndpointId |String |Yes |vedbm\-6subnyth\*\*\*\*\-Custom\-0cul |Connection endpoint ID. |
|NetworkType |String |Yes |Private |The network address type. The value is fixed to `Private`, which indicates a private network address. |
|DomainPrefix |String |No |vedbm\-55556hhh |The new private network address prefix. The connection address prefix rules are as follows:<br><br><br>* The connection address prefix must contain between 8 and 63 characters.<br><br>* The total length of the connection address cannot exceed 253 characters.<br><br>* Begin with a lowercase letter and end with a lowercase letter or number.<br><br>* Consists of lowercase letters, numbers, and hyphens (\-).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Only the private network connection address prefix can be modified, and the public network connection address prefix cannot be modified.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After the new address takes effect, the old address will be closed three minutes later. Modify the connection configuration of the application synchronously, otherwise it may affect the business, so proceed with caution.</div><br> |
|Port |Integer |No |3307 |Enter a new port number. The port number range is 1000 to 65534.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Changing the port number will also change the port numbers of the private network and the public network simultaneously. After the new port takes effect, the old port will be closed immediately. Modify the connection configuration of the application synchronously, otherwise it may affect the business. Proceed with caution.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=ModifyDBEndpointAddress&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceId": "vedbm-6subnyth****",
    "NetworkType": "Private",
    "EndpointId": "vedbm-6subnyth****-Custom-0cul",
    "DomainPrefix": "vedbm-55556hhh",
    "Port": 3307
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202507301130483757D4D5820D32C11554-4010bd",
        "Action": "ModifyDBEndpointAddress",
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
