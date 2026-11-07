---
title: "DeleteIpGroup"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/DeleteIpGroup"
---

Delete the specified IP address group based on the group ID; multiple address groups can be deleted simultaneously.

<span id="36f39b5c"></span>
## Precautions


* It is recommended to confirm that the corresponding rules do not need to be associated with the IP address group before deleting. Because once the IP address group is deleted, the associated rules will also delete the reference to that IP address group.

* If the protection rule is only associated with the current IP address group, the corresponding rule will be directly deleted.


<span id="936d1612"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=DeleteIpGroup&Version=2023\-12\-25


<span id="1502b7e7"></span>
## Request parameters


|**Parameter** |**Data type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|IpGroupIds |Array of Integers |Yes |`[1523,1524]` |ID of the IP address group to be deleted. To obtain the IP address group ID, refer to [ListAllIpGroups - Query all address groups](https://docs.byteplus.com/en/docs/waf/ListAllIpGroups). |


<span id="ed68472b"></span>
## Response parameters\nNone

<span id="0a31a3c2"></span>
### Sample request

```JSON
POST https://waf.byteplusapi.com/?Action=DeleteIpGroup&Version=2023-12-25
X-Date: 20230711T035055Z
Authorization: HMAC-SHA256 Credential=AKLTNGU0OGEyMT***/20230711/ap-southeast-1/waf/request, SignedHeaders=content-type;x-content-sha256;x-date, Signature=da4fac562d00f41ad8***

{
    "IpGroupIds":[1523,1524]
}
```


<span id="a714f6c2"></span>
## Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20240130212419A25B8B1A283C5B5B****",
        "Action": "DeleteIpGroup",
        "Version": "2020-12-09",
        "Service": "waf",
        "Region": "ap-southeast-1"
    },
      "Result": {}
}
```
