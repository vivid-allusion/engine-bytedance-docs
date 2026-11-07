---
title: "ListDomain"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-listdomain"
---

This interface is used to obtain domain information of different domain types and origin types within a specified space.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=ListDomain&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListDomain` |The API action. For the current API, the value is `ListDomain`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceName |String |Yes |`test` |The VOD space name. You can obtain the space name through the following methods:<br><br><br>* View the names of all spaces under the current account on the [Space](https://console.byteplus.com/vodpaas/overview/?) of the BytePlus VOD console.<br><br>* Call the [ListSpace](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listspace) interface to obtain the names of all spaces under the current account. |
|DomainType |String |No |`play` |Domain type. The values are as follows:<br><br><br>* `play`: Playback domain<br><br>* `image`: Cover domain |
|SourceStationType |Integer |No |`1` |Source site type. The values are as follows:<br><br><br>* `1`: VOD source site<br><br>* `2`: Custom source site |
|Offset |Integer |No |`0` |Set the cross\-domain page number. Passing 0 means getting the first page. The default page size is 10 domain name results.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The domain information obtained varies depending on the parameters passed to <code>DomainType</code>, <code>SourceStationType</code>, and <code>Offset</code>, as follows:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">(Recommended) Passing all parameters will paginate the domain information. Each page returns up to 10 detailed domain name information.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Passing some parameters will retrieve all domain information under the space, without pagination. If there are too many domains under the space, it may cause a timeout error.</div><br> |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|SpaceName |String |`test` |VOD space name. |
|PlayInstanceInfo |Object of [DomainInstanceInfos](https://docs.byteplus.com/en/docs/25/8048#domaininstanceinfos) |`-` |Domain name information playback. |
|ImageInstanceInfo |Object of [DomainInstanceInfos](https://docs.byteplus.com/en/docs/25/8048#domaininstanceinfos) |`-` |Cover domain information. |
|DefaultPlayDomain |String |`www.example.vod.com` |Default playback domain. |
|Total |Long |`1` |The total number of domain names that meet the requirements. |
|Offset |Long |`1` |The number of returned domain names. |


#{.custom\-md\-table\-4}#

<span id="domaininstanceinfos"></span>
### DomainInstanceInfos


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|ByteInstances |Array of [DomainInstanceInfo](https://docs.byteplus.com/en/docs/25/8048#domaininstanceinfo) |`-` |Domain information for back\-to\-origin on\-demand acceleration. |
|OtherInstances |Array of [DomainInstanceInfo](https://docs.byteplus.com/en/docs/25/8048#domaininstanceinfo) |`-` |Custom origin source acceleration for domain information. |


#{.custom\-md\-table\-4}#

<span id="domaininstanceinfo"></span>
### DomainInstanceInfo


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Domains |Array of [DomainoInfo](https://docs.byteplus.com/en/docs/25/8048#domainoinfo) |`-` |Domain list. |


#{.custom\-md\-table\-4}#

<span id="domainoinfo"></span>
### DomainoInfo


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Domain |String |`test.com` |Domain name. |
|Cname |String |`test.com.vdn.com` |CNAME domain. |
|ConfigStatus |String |`enable` |Configuration status. The values are as follows:<br><br><br>* `enable`: Enabled.<br><br>* `disable`: Disabled. |
|CnameStatus |String |`enable` |Parsing status. The values are as follows:<br><br><br>* `enable`: Success.<br><br>* `disable`: Failure. |
|Status |String |`enable` |Running status. The values are as follows:<br><br><br>* `enable`: Running.<br><br>* `disable`: Disabled. |
|Certificate |Object of [DomainCertificateInfo](https://docs.byteplus.com/en/docs/25/8048#domaincertificateinfo) |`-` |Certificate. |
|CreateTime |String |`2024-09-29T10:59:03Z` |Creation time. UTC timezone. |
|UpdateTime |String |`2024-09-29T10:59:03Z` |Update time. Time zone: UTC timezone. |
|Region |String |`cn` |Acceleration region. The values are as follows:<br><br><br>* `cn`: China.<br><br>* `overseas`: Overseas.<br><br>* `global`: Global. |
|LockStatus |String |`off` |Whether it is in locked status. The values are as follows:<br><br><br>* `off`: Unlocked.<br><br>* `on`: Locked. |
|CdnStatus |String |`disable` |CDN status. The values are as follows:<br><br><br>* `enable`: Enabled.<br><br>* `disable`: Disabled. |


#{.custom\-md\-table\-4}#

<span id="domaincertificateinfo"></span>
### DomainCertificateInfo


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|CertificateId |String |`cert_hosting-7269` |Certificate ID. |
|HttpsStatus |String |`enable` |HTTPS status. The values are as follows:<br><br><br>* `enable`: Enabled.<br><br>* `configuring`: Configuring. |
|ExpiredAt |String |`2024-09-29T10:59:03Z` |Certificate expiration time, format "yyyy\-MM\-dd HH:mm:ss" |
|CertificateCenterCertificateId |String |`cert-xxxx` |Certificate Authority Certificate ID |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=ListDomain&Version=2023-01-01&SpaceName=test&DomainType=play&SourceStationType=1&Offset=0&Limit=
```


<span id="sample-response"></span>
### Sample response

```json
{
    "Result": {
        "Total": 1,
        "Offset": 1,
        "SpaceName": "test",
        "PlayInstanceInfo": {
            "ByteInstances": [
                {
                    "Domains": [
                        {
                            "Cname": "test.com.vdn.com",
                            "Domain": "test.com",
                            "Region": "cn",
                            "Status": "enable",
                            "CdnStatus": "disable",
                            "CreateTime": "2024-09-29T10:59:03Z",
                            "LockStatus": "off",
                            "UpdateTime": "2024-09-29T10:59:03Z",
                            "Certificate": {
                                "ExpiredAt": "2024-09-29T10:59:03Z",
                                "HttpsStatus": "enable",
                                "CertificateId": "cert_hosting-7269",
                                "CertificateCenterCertificateId": "cert-xxxx"
                            },
                            "CnameStatus": "enable",
                            "ConfigStatus": "enable"
                        }
                    ]
                }
            ],
            "OtherInstances": []
        },
        "DefaultPlayDomain": "www.example.vod.com",
        "ImageInstanceInfo": {
            "ByteInstances": [],
            "OtherInstances": []
        }
    },
    "ResponseMetadata": {
        "Action": "ListDomain",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see the [shared errors of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParameter.InvalidAccountId |\- |Invalid account ID, please adjust and try again. |
|400 |InvalidParameter.InvalidDomainTypeOrSourceStationType |\- |Invalid domain type or source site type, please adjust and try again. |


#{.custom\-md\-table\-4}#

&nbsp;
