---
title: "DeleteCustomPage"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/DeleteCustomPage"
---

Call the DeleteCustomPage interface to delete the specified custom response intercept rule by rule ID.

<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=DeleteCustomPage&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this interface and some common parameters are listed below. For more information, please see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="query"></span>
### Query



**Action** <span data-label="purple">string</span> <span data-api-tag="require|2YPVqk">必选</span> `Sample value: DeleteCustomPage`

The operation to be performed, value: DeleteCustomPage.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|ctFeiV">必选</span> `Sample value: 2023-12-25`

The version of the API, value: 2023\-12\-25.



&nbsp;

<span id="body"></span>
### Body



**Id** <span data-label="purple">integer</span> <span data-api-tag="require|kxvduP">必选</span> `Sample value: 1876`

Rule ID.



**ProjectName** <span data-label="purple">string</span> `Optional` `Sample value: default`

The resource name of the project.



**Host** <span data-label="purple">string</span> <span data-api-tag="require|ALwoo4">必选</span> `Sample value: example.volcwaf001.com`

The domain name associated with the protection rule.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This interface has no specific response parameters. For more information, please see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
POST /?Action=DeleteCustomPage&Version=2023-12-25 HTTP/1.1
Host: waf.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20250328T095831Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250328/ap-southeast-1/waf/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "Id": 1876,
  "ProjectName": "default",
  "Host": "example.volcwaf001.com"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20250328175847081142086110FC****",
    "Action": "DeleteCustomPage",
    "Version": "2023-12-25",
    "Service": "waf",
    "Region": "ap-southeast-1"
  },
  "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) for more error code information.
