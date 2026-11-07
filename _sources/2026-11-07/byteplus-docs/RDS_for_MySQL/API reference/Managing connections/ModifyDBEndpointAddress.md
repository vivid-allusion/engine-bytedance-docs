---
title: "ModifyDBEndpointAddress"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbendpointaddress"
---

Call the ModifyDBEndpointAddress API to modify the prefix or port of a connection address.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The new connection address takes effect after the API is called successfully. The original connection address will become invalid three minutes after the new connection address takes effect. Update the connection configuration in your application accordingly. Otherwise, the business may be affected. Proceed with caution.

* After the new port takes effect, the old port will be closed immediately. Modify the connection configuration of the application synchronously, otherwise it may affect the business. Proceed with caution.

* You cannot modify the connection address prefix and port in the same call.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBEndpointAddress&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-935479e57cbf\*\*\* |Instance ID. |
|EndpointId |String |Yes |mysql\-935479e5\*\*\*\*\-cluster |Instance ID. |
|NetworkType |String |Yes |Private |Network address type, values are:<br><br><br>* `Private`: private network connection address.<br><br>* `Public`: public network connection address. |
|DomainPrefix |String |No |mysql935479e57cbf\*\*\* |Connection address prefix. The connection address prefix must meet the following rules:<br><br><br>* Start with a lowercase letter and end with a lowercase letter or number.<br><br>* Consists of at least two of the following: lowercase letters, digits, and hyphens (\-).<br><br>* The connection address prefix must contain at least 8 characters, and the total length (prefix + suffix) must not exceed 63 characters. |
|Port |Integer |No |3306 |Port. The value range for the port number is 1000\-65534.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If not specified, the private network address port of the Default_endpoint is automatically configured as the default port.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=ModifyDBEndpointAddress&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-935479e57cbf***",
    "EndpointId": "mysql-935479e5****-cluster",
    "NetworkType": "Private",
    "Port": 3306
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230111161007B09FD872D02C2F8AE508",
        "Action": "ModifyDBEndpointAddress",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
