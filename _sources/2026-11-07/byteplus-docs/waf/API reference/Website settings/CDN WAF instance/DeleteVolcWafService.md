---
title: "DeleteVolcWafService"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/DeleteVolcWafService"
---

You can delete a domain by its project name and domain name if you no longer need to protect it.

<span id="60cc365f"></span>
## Note

This API is applicable to **BytePlus WAF** and is designed to delete domain names previously added via BytePlus CDN, which refers to domain names under the region of Edge (CDN).

<span id="145478bb"></span>
## Requirements


* The domain name to be deleted has been added to BytePlus WAF.

* You have obtained the project name to which the protected domain belongs.


<span id="563eb442"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=DeleteVolcWafService&Version=2023\-12\-25


<span id="9bc3db38"></span>
## Request parameters


|**Parameter** |**Data type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|ProjectName |String |No |`default` |The project name of the project to which it belongs. You can refer to [ListDomain](https://docs.byteplus.com/docs/waf/ListDomain) to get the specific project name. |
|Host |String |Yes |`example.volcwaf001.com` |Domains to be deleted. |
|AccessMode |Integer |No |`6` |Access mode. If your domain is added from BytePlus CDN, this parameter should be set to 6. |


<span id="c7504aa5"></span>
## Response parameters

Null

<span id="d6c2073a"></span>
## Sample request

```JSON
POST /?Action=DeleteVolcWafService&Version=2023-12-25 HTTP/1.1
Host: waf.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20240815T161319Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240815/byteplus-global/waf/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
{
  "ProjectName": "default",
  "Host": "example.volcwaf001.com",
  "AccessMode": 6
}
```


<span id="d94dfa3b"></span>
## Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202408160021332392451011050C****",
        "Action": "DeleteVolcWafService",
        "Version": "2023-12-25",
        "Service": "waf",
        "Region": "byteplus-global"
    },
    "Result": {}
}
```
