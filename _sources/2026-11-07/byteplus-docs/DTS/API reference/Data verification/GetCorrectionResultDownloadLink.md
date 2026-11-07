---
title: " GetCorrectionResultDownloadLink"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/GetCorrectionResultDownloadLink"
---

Call the GetCorrectionResultDownloadLink interface to get the data correction SQL download link.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|TaskID |String |Yes |3722f27c2baf4ef489ff51b442a5\*\*\*\* |Data correction task ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Link |String |https://dts\-row\-compare.tos\-s3\-cn\-boe.volces.com/diff_patch/\*\*\*\*\*\*\*\*\*\*\*\*\*\*/patch.log?X\-Amz\-Algorithm=AWS4\-HMAC\-SHA256\u0026X\-Amz\-Credential=\*\*\*\*\*\*\*\*\*%2F20251124%2Fdefault%2Fs3%2Faws4_request\u0026X\-Amz\-Date=20251124T074506Z\u0026X\-Amz\-Expires=600\u0026X\-Amz\-SignedHeaders=host\u0026X\-Amz\-Signature=\*\*\*\*\*\*\* |Download link of corrected SQL. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=GetCorrectionResultDownloadLink&Version=2022-10-01 HTTP/1.1
Content-Type: application/json
Host: dts.cn-beijing.byteplusapi.com.cn
X-Date: 20221001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20221001/cn-beijing/dts/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "TaskID": "3722f27c2baf4ef489ff51b442a5****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20251124154506A11D8D4F09149C2A5645-90e913",
        "Action": "GetCorrectionResultDownloadLink",
        "Version": "2022-10-01",
        "Service": "dts",
        "Region": "cn-beijing"
    },
    "Result": {
        "Link": "https://dts-row-compare.tos-s3-cn-boe.volces.com/diff_patch/**************/patch.log?X-Amz-Algorithm=AWS4-HMAC-SHA256\u0026X-Amz-Credential=*********%2F20251124%2Fdefault%2Fs3%2Faws4_request\u0026X-Amz-Date=20251124T074506Z\u0026X-Amz-Expires=600\u0026X-Amz-SignedHeaders=host\u0026X-Amz-Signature=*******"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/DTS/error_codes).
