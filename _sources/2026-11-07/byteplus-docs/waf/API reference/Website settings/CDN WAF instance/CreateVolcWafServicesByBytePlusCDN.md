---
title: "CreateVolcWafServicesByBytePlusCDN "
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/CreateVolcWafServicesByBytePlusCDN"
---

Add the domain names integrated with CDN to the WAF instance. After adding, you can configure various protection strategies to achieve defense effects.

<span id="36e84f25"></span>
## Requirements


* Add the website domain names to BytePlus CDN. For more details, see [Adding your domain name](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-addtemplatedomain).

* The websites that need protection have not been added to the WAF yet.

* Your BytePlus account is not overdue.


<span id="3feb9e2a"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=CreateVolcWafServicesByBytePlusCDN&Version=2023\-12\-25


<span id="8e07ba44"></span>
## Request parameters


|**Parameter** |**Data type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|ProjectName |String |No |`default` |* The name of the project to which your domain names belong. You can refer to [ListDomain](https://docs.byteplus.com/docs/waf/ListDomain) to get the specific project name.<br><br>* If **ProjectFollow** is set to `0`, this parameter can not be empty. |
|ProjectFollow |Integer |No |`1` |* Set whether to follow the project to which other resources belong, such as the CDN's project. The default value is set to `0`.<br><br>   * 0: Disabled<br><br>   * 1: Enabled<br><br>* If **ProjectFollow** is set to `1`, you don't need to enter a **ProjectName**. |
|TLSEnable |Integer |No |`1` |Whether to log requests to the protected domain name. The default value is set to `0`.<br><br><br>* 0: Disabled<br><br>* 1: Enabled |
|TLSFieldsConfig |Object of [HeadersConfig](https://docs.byteplus.com/docs/waf/CreateVolcWafServicesByBytePlusCDN#d0421ee1) |No |\- |It can not be empty when you choose to log all headers. |
|Domains |Array of Strings |Yes |`"bytepluswaf1.com","bytepluswaf2.com"` |List of CDN domain names that need to be protected by WAF. |


<span id="d0421ee1"></span>
### HeadersConfig


|**Parameter** |**Data type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Enable |Integer |Yes |`1` |Whether to log all headers.<br><br><br>* 0: Disabled<br><br>* 1: Enabled |
|ExcludedKeyList |Array of Strings |No |`"Accept-Language", "Content-Type"` |To avoid excessive log storage, you can configure header fields that do not need to be logged.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only letters, digits, and hyphens "\-" are supported, with a length of 1\-128 characters.</div><br> |
|StatisticalKeyList |Array of Strings |No |`"User-Agent"` |Set the header fields that need to be calculated, analyzed, and alerted within the logged headers.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only letters, digits, and hyphens "\-" are supported, with a length of 1\-128 characters.</div><br> |


<span id="b8de32df"></span>
## Response parameters

None

<span id="e7eef2a0"></span>
## Samples

<span id="3de10f0a"></span>
### Sample request 1

```JSON
POST /?Action=CreateVolcWafServicesByBytePlusCDN&Version=2023-12-25 HTTP/1.1
Host: waf.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20240815T161319Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240815/byteplus-global/waf/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "ProjectName": "",
  "ProjectFollow": 1,
  "TLSEnable": 1,
  "TLSFieldsConfig": {
    "HeadersConfig": {
      "Enable": 0,
    }
  },
  "Domains": [
    "bytepluswaf1.com"
  ]
}
```


<span id="cad4c4cd"></span>
### Sample response 1

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20240816001435252151221244D0****",
        "Action": "CreateVolcWafServicesByBytePlusCDN",
        "Version": "2023-12-25",
        "Service": "waf",
        "Region": "byteplus-global"
    },
    "Result": null
}
```


<span id="55fedc1c"></span>
### Sample request 2

```JSON
POST /?Action=CreateVolcWafServicesByBytePlusCDN&Version=2023-12-25 HTTP/1.1
Host: waf.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20240815T161319Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240815/byteplus-global/waf/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "ProjectName": "",
  "ProjectFollow": 1,
  "TLSEnable": 1,
  "TLSFieldsConfig": {
    "HeadersConfig": {
      "Enable": 1,
      "ExcludedKeyList": [
        "Accept-Language"
      ],
      "StatisticalKeyList": [
        "User-Agent"
      ]
    }
  },
  "Domains": [
    "bytepluswaf1.com"
  ]
}
```


<span id="f4c5640a"></span>
### Sample response 2

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20240816001435252151221244D0****",
        "Action": "CreateVolcWafServicesByBytePlusCDN",
        "Version": "2023-12-25",
        "Service": "waf",
        "Region": "byteplus-global"
    },
    "Result": null
}
```
