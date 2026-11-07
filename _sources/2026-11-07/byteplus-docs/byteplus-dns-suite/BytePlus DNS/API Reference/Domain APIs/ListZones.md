---
title: "ListZones"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-listzones"
---

Gets a list of domains.

## Usage

* Rate limit: 20 calls per second.

## Request

* Method: GET

* Address: https://dns.byteplusapi.com/?Action=ListZones?Version=2018\-08\-01

## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

### Query

|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ListZones` |The name of the API. The value of this parameter is `ListZones`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |
|PageSize |Integer |No |`10` |The number of domains per page. The system displays the domains in pages. The page number is determined by the total number of domains and `PageSize`. The default value is `10`, and the maximum value is `500`. |
|PageNumber |Integer |No |`1` |The page number. The API returns the domains included in this page. The default value is `1`. |
|Key |String |No |`example` |The keyword included in domains. |
|SearchMode |String |No |`like` |The matching mode for the `Key` parameter. The value can be:<br><br><br>* `like`: Fuzzy matching.<br><br>* `exact`: Exact matching. The default value is `like`. |
|Remark |String |No |`remark` |The remark of the domain. If you do not set this parameter, the API will not filter the query results based on the parameter. |
|TradeCode |String |No |`free_edition_global` |The edition of the domain. If you do not set this parameter, the API will not filter the query results based on the parameter. The possible values are:<br><br><br>* `free_edition_global`: Free edition.<br><br>* `professional_edition_global`: Professional edition.<br><br>* `enterprise_edition_global`: Enterprise edition.<br><br>* `ultimate_edition_global`: Ultimate edition.<br><br>* `exclusive_edition_global`: Exclusive edition. |
|AboutToExpire |Boolean |No |`true` |Whether the domain is about to expire. If you do not set this parameter, the API will not filter the query results based on the parameter.The possible values are:<br><br><br>* `true`: The domain will expire in 15 days or less.<br><br>* `false`: The domain will expire in more than 15 days. |
|Stage |Integer |No |`1` |The status of the domain. If you do not set this parameter, the API will not filter the query results based on the parameter. The possible values are:<br><br><br>* `0`: Active.<br><br>* `1`: DNS is managed by another account.<br><br>* `2`: Not using BytePlus DNS servers.<br><br>* `3`: DNS unavailable.<br><br>* `5`: Please change DNS servers. |
|SearchOrder |String |No |`asc` |The sorting order of the results. The possible values are:<br><br><br>* `asc`: Ascending order.<br><br>* `dsc`: (Default) Descending order. |
|OrderKey |String |No |`Remark` |The key for sorting the results. The possible values are:<br><br><br>* `ZoneName`: Sort by domain name.<br><br>* `Remark`: Sort by domain remark.<br><br>* `TradeCode`: Sort by domain edition.<br><br>* `UpdatedAt`: (Default) Sort by the most recent update time of the domain.<br><br>* `ExpiredTime`: Sort by the expiration time of the domain. Free edition domains do not expire.<br><br>* `Stage`: Sort by the status of the domain.<br><br>* `RecordCount`: Sort by the number of record values of the domain. |

## Response body

### ResponseMetadata object

|**Name** |**Type** |**Description** |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The version of the API. |
|Service |String |The type of service. |
|Region |String |The region where the service is located. |

### Result Object

|Name |Type |Description |
|---|---|---|
|Total |Integer |Indicates the number of domains retrieved. |
|Zones |Array of Objects |List of retrieved domains. |
|CreatedAt |String |The creation time of the domain. |
|UpdatedAt |String |The most recent update time of the domain. Update operations include:<br><br><br>* Updating domain remarks<br><br>* Creating DNS records under the domain |
|ZID |Integer |The ID of the domain. |
|ZoneName |String |The domain name. |
|InstanceID |String |The ID of the instance. For the free version of BytePlus DNS, the value of this field is `null`. |
|Remark |String |The remarks for the domain. |
|ConfigurationCode |String |This parameter is deprecated. |
|RecordCount |Integer |The total number of DNS records contained in the domain. As newly added domains do not contain any DNS records yet, the value of this parameter is `0`. |
|ExpiredTime |Integer |The expiration time of the domain. Currently, the value of this parameter is `0`, indicating that the domain will not expire. |
|LastOperator |String |The ID of the BytePlus account that last updated this domain. Update operations include updating domain remarks, creating DNS records under the domain, etc. If a IAM account updates the domain, the value of this parameter is the ID of the IAM account. |
|CacheStage |Integer |The status of domain ownership. This parameter has the following values:<br><br><br>* `0`: You are the owner of the domain.<br><br>* `1`: You are not the owner of the domain. You can call the [RetrieveZone API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-retrievezone) to verify domain ownership. |
|TradeCode |String |The edition of the domain. This parameter has the following values:<br><br><br>* `free_edition_global`: Free edition.<br><br>* `professional_edition_global`: Professional edition.<br><br>* `enterprise_edition_global`: Enterprise edition.<br><br>* `ultimate_edition_global`: Ultimate edition.<br><br>* `ultimate_exclusive_edition_global`: Exclusive edition. |
|DnsSecurity |String |This parameter is not used. Please ignore this parameter. |
|IsSubDomain |Boolean |Whether the domain is a subdomain.<br><br><br>* `true`: Subdomain.<br><br>* `false`: Root domain. |

## Example

### Request example

```HTTP
GET https://dns.byteplusapi.com/?Version=2018-08-01&Action=ListZones&Version=2018-08-01&PageSize=1&PageNumber=1
```

### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20240627073729D567A58BB5D28E0354D6",
        "Action": "ListZones",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    },
    "Result": {
        "Zones": [
            {
                "CreatedAt": "2024-05-07T02:48:08Z",
                "UpdatedAt": "2024-06-24T11:19:02Z",
                "ZID": 454458,
                "ZoneName": "*****.com",
                "InstanceID": null,
                "Remark": "",
                "ConfigurationCode": "free",
                "RecordCount": 4,
                "ExpiredTime": 0,
                "LastOperator": "30xxxxx32",
                "CacheStage": 0,
                "TradeCode": "free_edition_global",
                "DnsSecurity": "",
                "IsSubDomain": false
            }
        ],
        "Total": 7
    }
}
```

## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-handling-the-response).
