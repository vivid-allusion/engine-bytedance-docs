---
title: "RemoveTagsFromResource"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/removetagsfromresource"
---

Call the RemoveTagsFromResource API to unbind tags from one or more MySQL instances.

## Request type

Asynchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceIds |String[] |Yes |["mysql\-46609cf2\*\*\*\*","mysql\-5564bc65\*\*\*\*"] |The instance ID(s) from which tags need to be unbound.<br><br>tip<br><br>Supports passing multiple instance IDs at once, with a maximum of 20 instance IDs allowed simultaneously. |
|TagKeys |String[] |Yes |Please refer to the request example. |The tag key(s) to be unbound.<br><br>tip<br><br><br>* Supports passing multiple tag keys at once, with multiple tag keys separated by commas (,). A maximum of 20 tag keys can be passed simultaneously.<br><br>* When multiple instance IDs are specified in InstanceIds, all tags matching the provided tag keys across these instances will be unbound. Please proceed with caution. |

## Response parameters

null

## Sample request

```json
POST /?Action=RemoveTagsFromResource&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceIds": [
        "mysql-46609cf2****",
        "mysql-5564bc65****"
    ],
    "TagKeys": [
        "Key1",
        "Key2"
    ]
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230809191430E0F9D50DC6B6CA8D3B8B",
        "Action": "RemoveTagsFromResource",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
