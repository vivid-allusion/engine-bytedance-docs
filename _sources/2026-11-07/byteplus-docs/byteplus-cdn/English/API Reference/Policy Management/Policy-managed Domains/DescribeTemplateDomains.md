---
title: "DescribeTemplateDomains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describetemplatedomains-7f84f"
---

Obtain a list of domain names that meet the filtering criteria.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DescribeTemplateDomains&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DescribeTemplateDomains`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Filters |Object[] |No |Indicates a set of filtering conditions to obtain a list of domain names that meet the criteria. If no filtering conditions are specified, this API returns all domain names under your account.<br><br>Multiple filtering conditions are in an `AND` relationship, meaning only domain names that satisfy all filtering conditions will be included in the list returned by this API.<br><br>In the response of this API, the actual list of returned domain names is affected by `PageNum` and `PageSize`. | |
|Fuzzy |Boolean |No |Indicates the matching method. This parameter can take the following values:<br><br><br>* `true`: Indicates fuzzy matching. In the matching process for domain names, if the value corresponding to `Name` contains any value from the `Value` array, then the domain name is considered to meet the filtering conditions.<br><br>* `false`: Indicates exact matching. If the value corresponding to `Name` contains a value identical to that in the `Value` array, then the domain name is considered to meet the filtering conditions.<br><br><br>Additionally, the `Fuzzy` value you can specify is affected by the `Name` value. See the description of `Name`.<br><br>The default value for this parameter is `false`. |`false` |
|Name |String |No |Indicates the filtering type. This parameter can take the following values:<br><br><br>* `TemplateTitle`: Filters domain names by the name of the bound policy.<br><br>* `TemplateId`: Filters domain names by the ID of the bound policy. For this parameter value, the `Fuzzy` value can only be `false`.<br><br>* `TemplateType`: Filters domain names by the type of the bound policy. For this parameter value, the `Fuzzy` value can only be `false`.<br><br>* `Domain`: Filters domain names by name.<br><br>* `Status`: Filters domain names by status. For this parameter value, the `Fuzzy` value can only be `false`.<br><br>* `HTTPSSwitch`: Filters domain names by the status of the `HTTPS encryption service`. For this parameter value, the `Fuzzy` value can only be `false`.<br><br>* `WAFStatus`: Filters domain names by the status of `WAF protection`. For this parameter value, the `Fuzzy` value can only be `false`.<br><br><br>Multiple filtering conditions can be specified at the same time, but the `Name` in different filtering conditions cannot be the same. |`TemplateTitle` |
|Value |String[] |No |Indicates the values corresponding to `Name`, which is an array. The values in the array are used to match against the object value. If the object value matches any value in the array, it is considered a match. Values are case\-sensitive when matching.<br><br><br>* When `Name` is `TemplateTitle` or `Domain`, each value in `Value` cannot exceed 100 characters. Furthermore,<br><br>   * When `Fuzzy` is `false`, `Value` can contain multiple values.<br><br>   * When `Fuzzy` is `true`, `Value` can only contain one value.<br><br>* When `Name` is `TemplateId`, `Value` can only contain one value.<br><br>* When `Name` is `TemplateType`, `Value` can contain one or more of the following values:<br><br>   * `cipher`: Indicates an encryption policy.<br><br>   * `service`: Indicates a delivery policy.<br><br>* When `Name` is `Status`, `Value` can contain one of the following values:<br><br>   * `online`: Indicates that the status of the domain name is `Enabled`.<br><br>   * `offline`: Indicates that the status of the domain name is `Disabled`.<br><br>   * `configuring`: Indicates that the status of the domain name is `Configuring`.<br><br>* When `Name` is `HTTPSSwitch`, `Value` can contain one of the following values:<br><br>   * `on`: Indicates that the `HTTPS encryption service` is enabled.<br><br>   * `off`: Indicates that the `HTTPS encryption service` is disabled.<br><br>* When `Name` is `WAFStatus`, `Value` can contain one of the following values:<br><br>   * `on`: Indicates that `WAF protection` is enabled.<br><br>   * `off`: Indicates that `WAF protection` is disabled. |`["TestPolicy"]` |
|PageNum |Long |No |For the returned result set, this parameter indicates a page number. The actual domain names returned by this API are the ones on the page specified by this page number.<br><br>The domain names returned by this API are paginated according to `PageSize`. Assuming the API returns 100 domain names and you have specified a `PageSize` of `10`, then the returned domain names are distributed across 10 pages. If you have specified a `PageNum` of `2`, it means you are requesting the domain names on the second page.<br><br>If there are no domain names on the specified page, the `Domains` parameter in the result will be `null`.<br><br>The default value for `PageNum` is 1. |`1` |
|PageSize |Long |No |Indicates the number of domain names included in each page.<br><br>The range for this parameter is 1\-200, with a default value of `10`. |`10` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|Domains |Object[] |Indicates the list of domain names returned by this API.<br><br>Note that the domain names in the list are those on the page represented by the `PageNum` request parameter, and are not necessarily all domain names that meet the filter criteria. | |
|CertInfo |Object |Indicates information about the certificate associated with the domain name specified by `Domain`.<br><br>If `HTTPSSwitch` is `off`, the value of this parameter is `null`. | |
|CertId |String |Indicates the ID of the certificate associated with the domain name. This certificate is hosted in the BytePlus Certificate Center. |`cert-044833503b2349b4b42a5e80b0aa8c23` |
|Source |String |证书来源。enums: cert_center、cdn_cert_hosting | |
|Cname |String |Indicates the CNAME assigned to the domain name by CDN. |`www.example.com.bplslb.com` |
|Domain |String |Represents one of the domain names in the `Domains` list. |`www.example.com` |
|HTTPSSwitch |String |Indicates whether the domain name has enabled `HTTPS Encryption Service`. This parameter can be:<br><br><br>* `on`: Indicates that the service is enabled.<br><br>* `off`: Indicates that the service is disabled. |`off` |
|LockStatus |String |Indicates whether the domain name is locked. This parameter can be:<br><br><br>* `on`: Indicates that the domain name is locked. In this case, you cannot use [UpdateTemplateDomain](https://docs.byteplus.com/byteplus-cdn/reference/updatetemplatedomain-05d27) to change the configurations of this domain name.<br><br>* `off`: Indicates that the domain name is not locked. |`off` |
|Remark |String |Indicates the reason why the domain name is locked.<br><br><br>* If `LockStatus` is `on`, this parameter indicates the reason why the domain name is locked.<br><br>* If `LockStatus` is `off`, the value of this parameter is empty (""). |`This is a test.` |
|ServiceRegion |String |Indicates the service region enabled for the domain name. This parameter can be:<br><br><br>* `outside_chinese_mainland`: Indicates `Global (Excluding Chinese Mainland)`.<br><br>* `chinese_mainland`: Indicates `Chinese Mainland`.<br><br>* `global`: Indicates `Global`. |`outside_chinese_mainland` |
|Status |String |Indicates the status of the domain name. This parameter can be:<br><br><br>* `online`: Indicates the status is `Enabled`.<br><br>* `offline`: Indicates the status is `Disabled`.<br><br>* `configuring`: Indicates the status is `Configuring`. |`online` |
|Templates |Object[] |Indicates the list of policies bound to the domain name.<br><br>A domain name must and can only be bound to one delivery policy, and optionally to one encryption policy. | |
|TemplateId |String |Indicates the ID of a policy. |`tpl-s2DVaW` |
|Title |String |Indicates the name of the policy. |`NetTVPlayer002` |
|Type |String |Indicates the type of the policy. This parameter can be:<br><br><br>* `cipher`: Indicates an encryption policy.<br><br>* `service`: Indicates a delivery policy. |`service` |
|Exception |Boolean |Indicates whether the policy contains special configurations. Special configurations refer to those configurations that are operated by BytePlus engineers instead of users. This parameter can be:<br><br><br>* `true`: Indicates it contains special configurations.<br><br>* `false`: Indicates it does not contain special configurations. |`false` |
|ProdVersion |String |Indicates the version number of the published version of the policy. |`P-250804.86120` |
|WAFStatus |String |Indicates whether the domain name has enabled `WAF Protection`. This parameter can be:<br><br><br>* `on`: Indicates that `WAF Protection` is enabled.<br><br>* `off`: Indicates that `WAF Protection` is disabled. |`off` |
|Project |String |Indicates the project to which the domain name belongs. |`default` |
|Tags |Object[] |Indicates the list of tags added to the `Domain`. A tag is a key\-value pair. If the `Domain` has no tags, the value of this parameter is `null`. | |
|Key |String |Indicates the key of a tag in the list. |`myKey` |
|Value |String |Indicates the value of the tag. |`myValue` |
|TotalCount |Long |Indicates the number of domain names that meet the filter criteria. The value of this parameter is not affected by `PageSize` and `PageNum`. |`1` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DescribeTemplateDomains&Version=2021-03-01
{
    "Filters": [
        {
            "Name": "Domain",
            "Value": [
                "example"
            ],
            "Fuzzy": true
        },
        {
            "Name": "TemplateTitle",
            "Value": [
                "NetTVPlayer"
            ],
            "Fuzzy": true
        },
        {
            "Name": "TemplateId",
            "Value": [
                "tpl-s2DVaW"
            ],
            "Fuzzy": false
        },
        {
            "Name": "TemplateType",
            "Value": [
                "service",
                "cipher"
            ],
            "Fuzzy": false
        },
        {
            "Name": "HTTPSSwitch",
            "Value": [
                "off"
            ],
            "Fuzzy": false
        },
        {
            "Name": "WAFStatus",
            "Value": [
                "off"
            ]
        },
        {
            "Name": "Status",
            "Value": [
                "online"
            ],
            "Fuzzy": false
        }
    ]
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20240305044725DD2386782EADAD775440",
        "Action": "DescribeTemplateDomains",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Domains": [
            {
                "CertInfo": null,
                "Cname": "www.example.com.bplslb.com",
                "Domain": "www.example.com",
                "HTTPSSwitch": "off",
                "LockStatus": "off",
                "Project": "default",
                "Remark": "",
                "ServiceRegion": "outside_chinese_mainland",
                "Status": "online",
                "Templates": [
                    {
                        "Exception": false,
                        "TemplateId": "tpl-s2DVaW",
                        "Title": "NetTVPlayer002",
                        "Type": "service"
                    }
                ],
                "WAFStatus": "off",
                "Tags": [
                    {
                        "Key": "myKey1",
                        "Value": "myValue1"
                    },
                    {
                        "Key": "myKey2",
                        "Value": "myValue2"
                    }
                ]
            }
        ],
        "TotalCount": 1
    }
}
```


&nbsp;
