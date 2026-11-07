---
title: "Common Error Codes"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-handling-the-response"
---

<span id="28396272"></span>
## Response status code

When an API request is successful, the HTTP response status code is 200.

When an API request fails, one of the following situations may occur:


* The HTTP response status code is 4xx or 5xx.

* The Error field is included in the ResponseMetadata structure of the response body.

* If an exception occurs in the response, the content of the response body is as follows. You can troubleshoot the cause of the issue based on the error information such as CodeN, Code, and Message in the Error structure.



|Category |Code |CodeN |Message |HTTP status code |
|---|---|---|---|---|
|Internal service error |ErrInternalServer |500100 |server internal error |500 |
|Parameter validation error |ErrParsingParams |400100 |parsing params error |400 |
||ErrMissingAccountParameter |400101 |`account` parameter missing |401 |
||ErrParamInvalid |400102 |validation fail: %s |400 |
||ErrDBDuplicated |400103 |duplicated: %s |409 |
||ErrDBNotFound |400104 |record not found :%s |400 |
||ErrZoneNotFound |400105 |zone not found |400 |
|Domain validation error |ErrVipZoneCanNotBeDeleted |400110 |vip zone can not be deleted |400 |
||ErrRequestSizeAboveMax |400111 |zones numbers should be less than or equal to %s |400 |
||ErrAccountZoneCountLimited |400112 |account zone count limited when creating zone |400 |
|Domain retrieval validation error |ErrZoneInactive |400120 |zone is inactive |400 |
||ErrZoneAlreadyRetrieve |400121 |zone already retrieve |400 |
||ErrZoneRetrieveNotFound |400122 |search retrieve zone not found |400 |
||ErrZoneRetrieveRecordExpired |400123 |zone retrieve record expired |400 |
||ErrCreateRetrieveTxtReachingMaxTimes |400124 |create retrieve txt record reaching max times |400 |
||ErrTXTRecordNotFound |400125 |type txt record not found |400 |
|Record validation error |ErrHostCanNotBeEmpty |400130 |host can't be empty, use @ instead |400 |
||ErrSearchParamMissingParams |400131 |request param: rr or type or value or line cannot be empty |400 |
||ErrPageSizeNotValid |400132 |page size must be less than 500 when search |400 |
||ErrAccountRecordCountLimited |400133 |account record count limited when creating record |400 |
||ErrZoneRecordCountLimited |400134 |zone record count limited when creating record |400 |
||ErrSpecNotValid |400135 |record %s not valid when creating record |400 |
||ErrLoadBalancerLimit |400136 |record load balancer count limited when creating record |400 |
|Statistics validation error |ErrNamesNotMatch |400140 |domain name and zone name do not match |400 |
||ErrDomainStatisticsNotValid |400141 |this zone can't view domain statistics |400 |


<span id="74f3f4f6"></span>
## Example response to a successful request

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230411150314CE53198BCFE9484824BA",
        "Action": "QueryZone",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    },
    "Result": {
        "InstanceNo": "DNS71279xxxxx9644332",
        "ZoneName": "xxxxx.com",
        "Remark": "",
        "ExpiredTime": 1691164799000,
        "ConfigurationCode": "monthly_plan_publiczone",
        "Status": 1,
        "AllocateDNSServerList": [
            "ns1.byteplusdns.com",
            "ns2.byteplusdns.com"
        ],
        "RealDNSServerList": [
            "ns1.byteplusdns.com",
            "ns2.byteplusdns.com"
        ],
        "IsNSCorrect": false,
        "Stage": 2,
        "TradeCode": "ultimate_inner",
        "UpdatedAt": "2023-04-03T19:17:32+08:00",
        "RecordCount": 0
    }
}
```


<span id="21f6c2fc"></span>
## Example response to a failed request

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023041116283931DC4B51E4C8C7660227",
        "Action": "QueryZone",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore",
        "Error": {
            "CodeN": 400100,
            "Code": "ErrParsingParams",
            "Message": "parsing params error"
        }
    }
}
```
