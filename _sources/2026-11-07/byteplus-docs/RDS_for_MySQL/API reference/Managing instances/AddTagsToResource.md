---
title: "AddTagsToResource"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/addtagstoresource"
---

Call the AddTagsToResource API to bind tags to one or more MySQL instances.

## Request type

Asynchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceIds |String[] |Yes |[ "mysql\-46609cf2\*\*\*\*", "mysql\-5564bc65\*\*\*\*" ] |The instance IDs to which tags need to be bound.<br><br>tip<br><br>Multiple instance IDs can be passed at once, separated by commas (,). A maximum of 20 instance IDs can be passed in a single request, and a single instance can be bound with up to 50 tags. |
|Tags |Object[] |Yes |Please refer to the request example. |An array of tag key\-value pairs to be bound.<br><br>tip<br><br>Multiple tag key\-value pairs can be passed at once, separated by commas (,). A maximum of 20 tag key\-value pairs can be passed in a single request, and a single instance can be bound with up to 50 tags. |
|Key |String |Yes |tagkey |The tag key of the instance tag. The setting rules of the tag key are as follows:<br><br><br>* Support any language letters or characters (such as Chinese, English letters, etc.), numbers, and spaces.<br><br>* Support special characters: `_.:/=+-@`.<br><br>* `volc:` is the reserved tag key of the system. When adding a tag, the beginning of the tag key cannot be set to any case form of `volc:`.<br><br>* The length of the tag key needs to be 1 to 128 characters. |
|Value |String |No |tagvalue |The tag value of the instance tag. The setting rules for the tag value are as follows:<br><br><br>* Support any language letters or characters (such as Chinese, English letters, etc.), numbers, and spaces.<br><br>* Support special characters: `_.:/=+-@`.<br><br>* The length of the tag value needs to be 0\-256 characters, that is, the tag value can be empty. |

## Response parameters

null

## Sample request

```json
POST /?Action=AddTagsToResource&Version=2022-01-01 HTTP/1.1
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
    "Tags": [
        {
            "Key": "TestKey",
            "Value": "TestValue"
        }
    ]
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2023080919085242905119679E5C8CC6AA",
        "Action": "AddTagsToResource",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
