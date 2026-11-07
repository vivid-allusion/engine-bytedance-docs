---
title: "BatchDeployCert"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/BatchDeployCert_en-us"
---

Associates a specified certificate with one or more domain names.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=BatchDeployCert&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `BatchDeployCert`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Domain |String |Yes |A list of domain names to be associated with `CertId`. The list can contain up to 50 domain names, separated by commas (,).<br><br>If a domain name in the list is not in the SAN field of the certificate, the domain name cannot be associated with the certificate. |`www.example.com,img.example.com` |
|CertId |String |Yes |The ID of the certificate to be associated. |`cert-c195f679cecb4f34tj23dd8c54e6c0a2` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|DeployResult |Object[] |The result of the association for each domain name. | |
|Domain |String |A domain name in `Domain`. |`example.com` |
|Status |String |Indicates whether the association is successful. The possible values are:<br><br><br>* `success`: The association is successful.<br><br>* `fail`: The association failed. The reason for the failure is described in the `ErrorMsg` parameter. |`success` |
|ErrorMsg |String |The reason for the association failure. If `Status` is `success`, this parameter is empty (""). |`some error` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=BatchDeployCert&Version=2021-03-01
{
    "Domain": "www.example.com,docs.example.com",
    "CertId": "cert-a4827a17f0964010a199e74f6e6b6a52"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2025091106370814AF152ABDC20800D531",
        "Action": "BatchDeployCert",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DeployResult": [
            {
                "Domain": "www.example.com",
                "ErrorMsg": "",
                "Status": "success"
            },
            {
                "Domain": "docs.example.com",
                "ErrorMsg": "",
                "Status": "success"
            }
        ]
    }
}
```


&nbsp;
