---
title: "CheckZone"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-checkzone"
---

Before creating a domain, you can use this API to check the status of the domain. If the check result meets the requirements, you can add the domain.

<span id="usage"></span>
## Usage


* Rate limit: 5 call per second.


<span id="request"></span>
## Request


* Method: GET

* Address: https://dns.byteplusapi.com/?Action=CheckZone?Version=2018\-08\-01


<span id="request-parameters"></span>
## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

<span id="query"></span>
### Query


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`CheckZone` |The name of the API. The value of this parameter is `CheckZone`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |
|ZoneName |String |Yes |`example.com` |The domain to be checked. |


<span id="ced317e9"></span>
## Response body

<span id="f19176a3"></span>
### ResponseMetadata object


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The version of the API. |
|Service |String |The type of service. |
|Region |String |The region where the service is located. |


<span id="174a232e"></span>
### Result object


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|ZoneName |String |The domain name being checked. |
|NameServer |String[] |The list of NS servers assigned to the domain by the domain registrar. |
|Registered |Boolean |Whether the domain is registered. This parameter can have the following values:<br><br><br>* `true`: The domain is registered.<br><br>* `false`: The domain is not registered. |
|Message |String |Information about the domain check result. This parameter can have the following values:<br><br><br>* `DNS servers cannot be found for the domain name`: An exception occurred during the domain check. This exception is usually caused by the following reasons:<br><br>   * The domain is suspended by the domain registrar or registrar.<br><br>   * The domain is not configured with DNS servers.<br><br>   * The domain is not registered.<br><br>   * The API timed out during the query. The timeout reason may be due to network issues.<br><br>* `The Domain already exists`: The domain already exists in BytePlus DNS. You do not need to add it again.<br><br>* Empty string (""): The domain meets the requirements. You can call the [CreateZone API](https://docs.byteplus.com/byteplus-dns-suite/reference/createzone) to add the domain. |
|ZoneOwnedByOtherUser |Boolean |Whether the DNS ownership for this domain are held by another BytePlus account.<br><br><br>* true: The DNS ownership for this domain are held by another BytePlus account.<br><br>* false: The DNS ownership for this domain are not held by any other BytePlus account. |
|isSubDomain |Boolean |Whether the domain is a subdomain.<br><br><br>* `true`: subdomain<br><br>* `false`: root domain |


<span id="c985da00"></span>
## Example

<span id="f4fe49d1"></span>
### Request example

```HTTP
GET https://dns.byteplusapi.com/?Version=2018-08-01&Action=CheckZone&ZoneName=example.com
```


<span id="bc047494"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20211215143549010225110011003276CE",
        "Action": "CheckZone",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    },
    "Result": {
        "ZoneName": "example.com",
        "NameServer": ["ns1.aaab-test.com","ne2.aaab-test.com"],
        "Registered": true,
        "Message":"The Domain already exists",        
        "ZoneOwnedByOtherUser": false,
        "IsSubDomain": false
    }
}
```


<span id="common-error-codes"></span>
## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-handling-the-response).
