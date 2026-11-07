---
title: "DownloadSSLCertificate"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/downloadsslcertificate"
---

Call the DownloadSSLCertificate API to download the SSL certificate of a specified MySQL instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id="4GdplvqJ"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-d4942fd7\*\*\*\* |Instance ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|Parameter |Type |Sample |Description |
|---|---|---|---|
|Certificate |Array of Integer |Refer to the return example. |Certificate compressed package. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DownloadSSLCertificate&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-d4942fd7****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230810115310DD70DDE173403CFB226B",
        "Action": "DownloadSSLCertificate",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "Certificate": [
            -64,
            96,
            47,
            …，
            -124,
            -64,
            105
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).

&nbsp;
