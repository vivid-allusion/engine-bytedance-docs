---
title: "ListAllIpGroups"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/ListAllIpGroups"
---

Query the list information of IP address groups under the current account, or query the associated IP address group information by rule ID.

<span id="936d1612"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=ListAllIpGroups&Version=2023\-12\-25


<span id="1502b7e7"></span>
## Request parameters


|**Parameter** |**Data type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Page |Integer |Yes |`1` |The page number you want to query. The default value is set to 1. |
|PageSize |Integer |Yes |`20` |The number of items displayed on each page. The default value is set to 10. The range is 1 to 100. |
|RuleTag |String |No |`92770` |ID of the related rules to be queried. Can be obtained via the allowlist interface. |
|TimeOrderBy |String |Yes |`DESC` |The order of the IP address group.<br><br><br>* Ascending: ASC<br><br>* Descending: DESC |
|Ip |String |No |`1.2.3.4` |The address or address range to query. |


<span id="ed68472b"></span>
## Response parameters


|**Parameter** |**Data type** |**Sample value** |**Description** |
|---|---|---|---|
|TotalCount |Integer |`15` |The total number of items that meet the conditions. |
|PageSize |Integer |`20` |The maximum number of items displayed per page. |
|CurrentPage |Integer |`1` |The page number of the current page. |
|Count |Integer |`10` |The number of entries displayed on the current page. |
|IpGroupCount |Integer |`3` |Current number of address groups. |
|IpGroupQuota |Integer |`600` |The upper limit on the number of IP address groups that can be added. |
|IpLimitQuota |Integer |`1000` |The maximum number of IPs that can be added to a single address group. |
|IpGroupList |Array of [IpGroupList](https://docs.byteplus.com/en/docs/waf/ListAllIpGroups#cd6be85e) objects |\- |IP address group list information. |


<span id="cd6be85e"></span>
### IpGroupList


|**Parameter** |**Data type** |**Sample value** |**Description** |
|---|---|---|---|
|Name |String |`test` |IP address group name. |
|IpGroupId |Integer |`4128` |IP address group ID. |
|IpCount |Integer |`3` |Number of IP addresses in the IP address group. |
|RelatedRules |Array of [RelatedRules](https://docs.byteplus.com/en/docs/waf/ListAllIpGroups#98c87706) objects |\- |Rules information that references this IP address group. |
|UpdateTime |String |`2024-01-30T21:00:02+08:00` |IP address group update time. |


<span id="98c87706"></span>
### RelatedRules


|**Parameter** |**Data type** |**Sample value** |**Description** |
|---|---|---|---|
|Host |String |`*.test.com` |Information related to the protection domain associated with the rule. |
|RuleName |String |`Forbidden access` |Rule name. |
|RuleTag |String |`B000000089801` |Rule ID. |
|RuleType |String |`Black` |Rule types associated with the IP address group.<br><br><br>* Black: blocklist rule<br><br>* White: allowlist rule |


<span id="a97c2290"></span>
## Sample request

```JSON
POST https://waf.byteplusapi.com/?Action=ListAllIpGroups&Version=2023-12-25
X-Date: 20230711T035055Z
Authorization: HMAC-SHA256 Credential=AKLTNGU0OGEyMT***/20230711/ap-southeast-1/waf/request, SignedHeaders=content-type;x-content-sha256;x-date, Signature=da4fac562d00f41ad8***

{
   "Page": 1,
   "ProjectName": "default",
   "PageSize": 20,
   "RuleTag": "92770",
   "TimeOrderBy": "DESC",
   "Ip": "1.2.**.**"
}
```


<span id="a714f6c2"></span>
## Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListAllIpGroups",
        "Version": "2023-12-25",
        "Service": "waf",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "CurrentPage": 2,
        "PageSize": 20,
        "TotalCount": 25,
        "Count": 5,
        "IpGroupCount": 3,
        "IpGroupQuota": 600,
        "IpLimitQuota": 1000,
        "IpGroupList": [
            {
                "Name": "test",
                "IpCount": 3,
                "IpGroupId": 4128,
                "UpdateTime": "2024-01-07T18:46:09+08:00",
                "RelatedRules": [
                    {
                        "RuleTag": "F00000000****",
                        "RuleName": "block_rule",
                        "RuleType": "Block"
                    }
                ]
            }
        ]
    }
}
```
