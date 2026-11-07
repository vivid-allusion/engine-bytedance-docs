---
title: "ListIpGroup"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/ListIpGroup"
---

Query the details of the IP under a specified address group based on the address group ID.

<span id="936d1612"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=ListIpGroup&Version=2023\-12\-25


<span id="1502b7e7"></span>
## Request parameters


|**Parameter** |**Data type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Page |Integer |Yes |`1` |The page number you want to query. The default value is set to 1. |
|PageSize |Integer |Yes |`20` |The number of items displayed on each page. The default value is set to 10. The range is 1 to 100. |
|IpGroupId |Integer |Yes |`1523` |IP address group ID. How to obtain the IP address group ID, you can refer to [ListAllIpGroups - Query all IP address groups](https://docs.byteplus.com/en/docs/waf/ListAllIpGroups). |
|Ip |String |No |`1.2.3.4` |The queried address or address segment. |


<span id="ed68472b"></span>
## Response parameters


|**Parameter** |**Data type** |**Sample value** |**Description** |
|---|---|---|---|
|IpList |Array of Strings |["1.1.1.1","1.1.1.2"] |IP details under this address group. |
|Count |Integer |`5` |Current page displays the number of IP address groups. |
|CurrentPage |Integer |`1` |The page number of the current page. |
|PageSize |Integer |`10` |Maximum number of IP address groups displayed on a single page. |
|TotalCount |Integer |`15` |Total number of IP address groups that meet the criteria. |


<span id="a97c2290"></span>
## Sample request

```JSON
POST https://waf.byteplusapi.com/?Action=ListIpGroup&Version=2023-12-25
X-Date: 20230711T035055Z
Authorization: HMAC-SHA256 Credential=AKLTNGU0OGEyMT***/20230711/ap-southeast-1/waf/request, SignedHeaders=content-type;x-content-sha256;x-date, Signature=da4fac562d00f41ad8***

{
    "Page":1,
    "PageSize":20,  
    "IpGroupId":1529
}
```


<span id="a714f6c2"></span>
## Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20240130212419A25B8B1A283C5B5B****",
        "Action": "ListIpGroup",
        "Version": "2020-12-09",
        "Service": "waf",
        "Region": "ap-southeast-1"
    },
      "Result": {
        "IpList": [
            "1.1.1.1",
            "1.1.1.2"
        ],
        "PageSize": 20,
        "Count": 1,
        "CurrentPage": 1,
        "TotalCount": 1
    }
}
```
