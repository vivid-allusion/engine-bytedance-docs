---
title: "DownloadValidationTaskResult"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/DownloadValidationTaskResult"
---

Call the DownloadValidationTaskResult API to download inconsistent data.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Incremental verification tasks (`IncrDataValidation`) support downloading only when they are in progress and inconsistent data exists. Other verification tasks support downloading only after the verification task has ended and inconsistent data exists.

* Before downloading the inconsistent data of increment validation, you must generate diff data and then download it. Otherwise, you will not be able to download inconsistent data. You can call the [GenerateValidationResultFile](https://docs.byteplus.com/en/docs/DTS/GenerateValidationResultFile) API to generate diff data.

* For verification tasks that are completed with consistent results, it indicates that there is no differing data between the source and target ends, thus no download is necessary.


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|TaskId |String |Yes |3e26d2f0970745ef9247acd9d8\*\*\*\*\*\* |Verification task ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/DTS/describevalidationtasks">DescribeValidationTasks</a> interface to query data verification tasks.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Link |String |https://dts\-test.tos\-s3\-cn\-beijing.volces.com/3e26d2f0970745ef\*\*\*\*\*/3e26d2f0970745ef9247acd\*\*\*\*\*.\*\*\*\*\* |download link for the data. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=DownloadValidationTaskResult&Version=2022-10-01 HTTP/1.1
Content-Type: application/json
Host: dts.cn-beijing.byteplusapi.com.cn
X-Date: 20221001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20221001/cn-beijing/dts/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "TaskId": "3e26d2f0970745ef9247acd9d8******"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "Action": "DownloadValidationTaskResult",
        "Region": "cn-beijing",
        "Service": "dts",
        "Version": "2022-10-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Link": "https://dts-test.tos-s3-cn-beijing.volces.com/3e26d2f0970745ef*****/3e26d2f0970745ef9247acd*****.*****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/DTS/error_codes).
