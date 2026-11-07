---
title: "AddIpGroup"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/AddIpGroup"
---

Create IP address group. You can create an IP address group by adding manually or uploading a file, and the uploaded file must meet the template requirements. This article introduces uploading the IP address group by manual addition.

<span id="24d284d0"></span>
## Precautions


* A maximum of 100 IP address groups can be added for each region.

* The number of IP addresses that can be added to the IP address group varies by different versions of the instance.



|Instance version |The number of IPs supported by each address group |
|---|---|
|Basic version |10 entries |
|Premium version |100 items |
|Enterprise Edition |500 entries |
|Flagship Edition |1000 entries |


<span id="6bf6d6f1"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=AddIpGroup&Version=2023\-12\-25


<span id="9bea91c5"></span>
## Request parameters


|**Parameter** |**Data type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Name |String |Yes |`123` |IP address group name, supports English, Chinese characters, and numbers, does not support special characters. The length must be between 3 and 63 characters. |
|AddType |String |Yes |`List` |Addition method.<br><br><br>* List: Manual addition, please refer to;<br><br>* File: File upload |
|IpList |Array of Strings |Yes |`["1.2.3.4","5.6.7.8"]` |IP addresses to be added.<br><br><br>* Support input of IP addresses or IP address segments.<br><br>* Support input of IPv4 and IPv6. |


<span id="6c6743b2"></span>
## Response parameters


|**Parameter** |**Data type** |**Sample value** |**Description** |
|---|---|---|---|
|IpGroupId |Integer |`1526` |IP address group ID. |


<span id="d182ac80"></span>
## Sample request

```JSON
POST https://waf.byteplusapi.com/?Action=AddIpGroup&Version=2023-12-25
X-Date: 20230711T035055Z
Authorization: HMAC-SHA256 Credential=AKLTNGU0OGEyMT***/20230711/ap-southeast-1/waf/request, SignedHeaders=content-type;x-content-sha256;x-date, Signature=da4fac562d00f41ad8***

{
  "Name":"123"，
  "AddType":"List"，
  "IpList":["1.2.3.4","5.6.7.8"]
}
```


<span id="4ec3d6a6"></span>
## Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20240107184608C0B578CE50777514****",
        "Action": "AddIpGroup",
        "Version": "2023-12-25",
        "Service": "waf",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "IpGroupId": 1526
    }
}
```
