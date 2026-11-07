---
title: "DownloadSSLCertificate - Download an SSL certificate"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/DownloadSSLCertificate_-_Download_an_SSL_certificate"
---

Call the DownloadSSLCertificate API to download the SSL CA certificate for an instance.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DownloadSSLCertificate&groupName=%E6%95%B0%E6%8D%AE%E5%AE%89%E5%85%A8&serviceCode=rds_mssql&version=2022-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This section describes only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span><span data-api-tag="require|s2SVpe">必选</span> `Example value: DownloadSSLCertificate`

The operation to perform. Value: `DownloadSSLCertificate`.



**Version** <span data-label="purple">string</span><span data-api-tag="require|HTq5cG">必选</span> `Example value: 2022-01-01`

The API version is `2022-01-01`.



**InstanceId** <span data-label="purple">string</span><span data-api-tag="require|gZOfAn">必选</span> `Example value: mssql-6474c9******`

Instance ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call the DescribeDBInstances operation to query the instance ID.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This section describes only the response parameters specific to this API. For more information, refer to [Return structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Certificate ** <span data-label="purple">integer[] </span>`Example value: mssql-123abc***.zip.`

The byte stream of the ZIP archive of the instance's SSL CA certificate.



<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=DownloadSSLCertificate&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mssql.volcengineapi.com
X-Date: 20230131T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****

{
    "InstanceId":"mssql-6474c9******"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2025021021045419B3A82D673D4888A154-******",
        "Action": "DownloadSSLCertificate",
        "Version": "2022-01-01",
        "Service": "rds_mssql",
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

The following table lists the business logic\-related error codes for this API. For public error codes, see the [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) document.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter |The specified parameter %s is not valid. |The value of Parameter {parameter1} is invalid. |
|404 |InstanceNotFound |The specified instance does not exist. |Instance not found. |
