---
title: "UpdateIpGroup"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/UpdateIpGroup"
---

Update the IP information of the specified address group. You can update the address group by manually adding or uploading a file. The uploaded file must meet the template requirements. This article introduces how to update the IP address group by manual addition.

<span id="936d1612"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=UpdateIpGroup&Version=2023\-12\-25


<span id="1502b7e7"></span>
## Request parameters


|**Parameter** |**Data type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Name |String |Yes |`123` |Address name, supporting English, Chinese characters, and numbers, special characters are not supported. The length is limited to 25 characters. |
|AddType |String |Yes |`List` |Addition method.<br><br><br>* List: Manual addition, please refer to<br><br>* File: File upload |
|IpGroupId |Integer |Yes |`1524` |IP group ID. |
|IpList |Array of Strings |Yes |`["1.1.1.1","2.2.2.2"]` |IP addresses that need to be updated.<br><br><br>* Supports inputting IP addresses or IP address ranges.<br><br>* Supports inputting IPv4 and IPv6. |


<span id="ed68472b"></span>
## Response parameters\nNone

<span id="a97c2290"></span>
## Sample request

```JSON
POST https://waf.byteplusapi.com/?Action=AddIpGroup&Version=2023-12-25
X-Date: 20230711T035055Z
Authorization: HMAC-SHA256 Credential=AKLTNGU0OGEyMT***/20230711/ap-southeast-1/waf/request, SignedHeaders=content-type;x-content-sha256;x-date, Signature=da4fac562d00f41ad8***

{
  "Name":"123"，
  "AddType":"List"，
  "IpGroupId":1524；
  "IpList":["1.1.1.1","2.2.2.2"]
}
```


<span id="a714f6c2"></span>
## Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20240130210001747E9C8D64200B56****",
        "Action": "UpdateIpGroup",
        "Version": "2020-12-09",
        "Service": "waf",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```
