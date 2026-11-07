---
title: "QueryZone"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-queryzone"
---

Gets detailed information about a domain.

<span id="usage"></span>
## Usage


* Rate limit: 20 calls per second.


<span id="request"></span>
## Request


* Method: GET

* Address: https://dns.byteplusapi.com/?Action=QueryZone?Version=2018\-08\-01


<span id="d1327502"></span>
## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

<span id="query"></span>
### Query


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`QueryZone` |The name of the API. The value of this parameter is `QueryZone`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |
|ZID |Integer |Yes |`1234` |The ID of the domain for which you want to retrieve information. You can get the domain ID by [CreateZone API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-createzone) or [ListZones API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-listzones). |


<span id="0eb22a73"></span>
## Response body

<span id="0f1d99f2"></span>
### ResponseMetadata object


|**Name** |**Type** |**Description** |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The version of the API. |
|Service |String |The type of service. |
|Region |String |The region where the service is located. |


<span id="d021f4ef"></span>
### Result object


|**Name** |**Type** |**Description** |
|---|---|---|
|InstanceNo |String |The ID of the instance. For free edition, the value of this field is `null`. |
|ZoneName |String |The domain name. |
|Remark |String |The remark of the domain. |
|ConfigurationCode |String |This parameter is deprecated. |
|Status |Integer |This parameter is deprecated. |
|AllocateDNSServerList |String[] |The list of DNS servers allocated to the domain by BytePlus DNS. |
|RealDNSServerList |String[] |The list of DNS servers actually used by the domain. |
|IsNSCorrect |Boolean |Indicates whether the configuration of NS servers is correct. If the configuration is correct, the status of the domain in BytePlus DNS is **Active**. This parameter can have the following values:<br><br><br>* `true`: The DNS server list in `RealDNSServerList` is the same as the DNS server list in `AllocateDNSServerList`. In this case, the DNS server configuration is correct.<br><br>* `false`: The DNS server list in `RealDNSServerList` is not the same as the DNS server list in `AllocateDNSServerList`. In this case, the DNS server configuration is incorrect. |
|ExpiredTime |Integer |The expiration time of the instance. The format is Unix timestamp. For BytePlus DNS Free Edition, the value of this field is `null`. |
|Stage |Integer |The status of the domain. This parameter can have the following values:<br><br><br>* `0`: **Active**. In this state, the DNS records of the domain are effective.<br><br>* `1`: **DNS is managed by another account**. In this state, the DNS records of the domain are not effective. This state indicates that you are not the owner of the domain. If you need to manage the domain's DNS resolution, you need to verify your domain ownership.<br><br>* `2`: **Not using BytePlus DNS servers**. In this state, the DNS records of the domain are not effective. This state indicates that the DNS servers assigned to the domain are not BytePlus DNS servers. In this case, the DNS records you create in BytePlus DNS will not take effect.<br><br>* `3`: **DNS unavailable**. In this state, the DNS records of the domain are not effective. The common causes for this state are as follows:<br><br>   * The domain is deactivated by the registrar or registry.<br><br>   * The domain does not have DNS servers.<br><br>   * The domain is not registered.<br><br>   * The API times out when querying the domain. The timeout may be caused by network issues.<br><br>* `5`: **Please change DNS servers**. This state indicates that you need to update the DNS servers of the domain to the new DNS servers assigned by BytePlus DNS due to service upgrades or changes. |
|TradeCode |String |The edition of the domain. This parameter can have the following values:<br><br><br>* `free_edition_global`: Free Edition.<br><br>* `professional_edition_global`: Professional Edition.<br><br>* `enterprise_edition_global`: Enterprise Edition.<br><br>* `ultimate_edition_global`: Ultimate Edition.<br><br>* `exclusive_edition_global`: Exclusive Edition. |
|UpdatedAt |String |The last update time of the domain. Update operations include:<br><br><br>* Updating domain comments<br><br>* Creating DNS records for the domain |
|RecordCount |Integer |The total number of DNS records contained in the domain. |
|DnsSecurity |String |This parameter is not used. Please ignore this parameter. |
|AutoRenew |Boolean |Whether automatic domain renewal is enabled.<br><br><br>* `true`: Automatic domain renewal is enabled.<br><br>* `false`: Automatic domain renewal is disabled. |
|IsSubDomain |Boolean |Whether the domain is a subdomain.<br><br><br>* `true`: Subdomain.<br><br>* `false`: Root domain. |
|SubDomainHost |String |The domain prefix of the subdomain. If the domain is not a subdomain, this parameter is null. |


<span id="9e7dffc2"></span>
## Example

<span id="4c35703c"></span>
### Request example

```HTTP
GET https://dns.byteplusapi.com/?Version=2018-08-01&Action=QueryZone&ZID=1376
```


<span id="b5d66b55"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202406270932436E61F1363F2066042321",
        "Action": "QueryZone",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    },
    "Result": {
        "InstanceNo": null,
        "ZoneName": "xxxx.com",
        "Remark": "create a domain2",
        "ExpiredTime": null,
        "ConfigurationCode": "free",
        "Status": null,
        "AllocateDNSServerList": [
            "ns1.byteplusdns.com",
            "ns2.byteplusdns.com"
        ],
        "RealDNSServerList": null,
        "IsNSCorrect": false,
        "Stage": 3,
        "TradeCode": "free_edition_global",
        "UpdatedAt": "2024-06-27T09:11:55Z",
        "RecordCount": 0,
        "DnsSecurity": "",
        "AutoRenew": null,
        "IsSubDomain": false,
        "SubDomainHost": null
    }
```


<span id="common-error-codes"></span>
## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-handling-the-response).
