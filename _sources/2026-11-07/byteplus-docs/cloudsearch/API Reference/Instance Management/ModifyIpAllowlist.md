---
title: "ModifyIpAllowlist"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/ModifyIpAllowlist"
---

Call ModifyIpAllowlist to configure an IP allowlist for accessing an instance or Kibana.

<span id="2bbb985f"></span>
## Precautions

Cerebro and Kibana/Dashboards share the same IP Allowlist configuration, and adding or removing allowlist IPs takes effect simultaneously.

<span id="cf389e63"></span>
## Request Description


* Request method: POST

* Request URL: /?Action=ModifyIpAllowlist&Version=2023\-01\-01 HTTP/1.1


<span id="bc4c6d00"></span>
## Request parameters

<span id="c1b897bc"></span>
### Query


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ModifyIpAllowlist` |The action that you want to perform. Value: `ModifyIpAllowlist`. |
|Version |String |Yes |`2023-01-01` |The version of the API. Value: `2023-01-01`. |


<span id="bbcf19ce"></span>
### Body


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |o\-0080\*\*iu98 |The ID of the instance for which you want to configure an IP allowlist. |
|Component |String |Yes |es |The object to which you want to apply the IP allowlist.<br><br><br>* es<br><br>* kibana |
|Type |String |Yes |public |The network type of the IP allowlist.<br><br><br>* public<br><br>* private |
|IpList |String |Yes |10.23. *.* ,10.43. *.*  |The IP address entries in the allowlist. Separate multiple IP address entries with commas ( , ).<br><br>To clear the allowlist, set `IpList` to an empty string. |


<span id="3369f7b2"></span>
## Response parameters


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Status |String |`SUCCESSFUL` |Whether the request is successful or failed. |
|Message |String |`-` |The message returned. |


<span id="61ab06f4"></span>
## Sample request

```HTTP
POST https://open.ap-southeast-1.byteplusapi.com/?Action=ModifyIpAllowlist&Version=2023-01-01
Content-Type: application/json
X-Date: 20231003T104027Z
Authorization: HMAC-SHA256 
Credential=AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZ****/20231003/ap-southeast-1/ESCloud/request, SignedHeaders=content-type;host;x-date, Signature=88dd0a9ea555d8609ec83eb46054b52f6cd4f79b8d5094fa784c66fa3f2b****
{
    "Component": "es",
    "InstanceId": "o-0080**iu98",
    "IpList": "10.23..,10.43..",
    "Type": "public"
}
```


<span id="7f1e3c9a"></span>
## Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20231116142743C5B***0555A5BABA",
        "Action": "ModifyIpAllowlist",
        "Version": "2023-01-01",
        "Service": "escloud",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Status": "SUCCESSFUL",
        "Message": ""
    }
}
```
