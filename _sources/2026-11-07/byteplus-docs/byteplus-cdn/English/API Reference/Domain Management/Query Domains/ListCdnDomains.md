---
title: "ListCdnDomains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListCdnDomains_en-us"
---

Gets the list of domain names in BytePlus CDN and the general information for each domain name, including the business type, running status, CNAME address, service area, etc. You can specify filter conditions to filter the domain list. If you need to get the detailed domain configuration, call [DescribeCdnConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnConfig_en-us).

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=ListCdnDomains&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `ListCdnDomains`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Domain |String |No |The domain name to be queried. Fuzzy matching is supported. |`example` |
|ServiceType |String |No |Indicates a service type used to filter domain names and obtain domain names of this service type. This parameter has the following values:<br><br><br>* `download`: Indicates file download.<br><br>* `web`: Indicates a web page.<br><br>* `video`: Indicates audio and video on demand. |`web` |
|ResourceTags |String[] |No |Indicates a list of tags used to filter domain names and obtain domain names with any tag in the list. The list can contain up to 10 tags, and the format of each tag is `key:value`. See the example of this parameter on the right. |`["key1:val1","key2:val2"]` |
|Status |String |No |Indicates a domain name status, which is used to filter domain names and obtain domain names in this status. This parameter has the following values:<br><br><br>* `online`: Indicates that the status is "Enabled".<br><br>* `configuring`: Indicates that the status is "Configuring".<br><br>* `offline`: Indicates that the status is "Disabled". |`offline` |
|Project |String |No |Indicates a project to obtain the domain names belonging to this project. |`default` |
|OriginProtocol |String |No |Indicates a protocol. Obtains the domain names that use this protocol for origin requests. This parameter has the following values:<br><br><br>* `http`: Indicates the HTTP protocol.<br><br>* `https`: Indicates the HTTPS protocol.<br><br>* `followclient`: Indicates the protocol used by the user request. |`http` |
|IPv6 |Boolean |No |Indicates whether to filter domain names based on whether the IPv6 feature is enabled. This parameter has the following values:<br><br><br>* `true`: Indicates that IPv6 is enabled.<br><br>* `false`: Indicates that IPv6 is not enabled. |`true` |
|HTTPS |Boolean |No |Indicates whether to filter domain names based on whether the HTTPS encryption service is enabled. This parameter has the following values:<br><br><br>* `true`: Indicates that the HTTPS encryption service is enabled.<br><br>* `false`: Indicates that the HTTPS encryption service is not enabled. |`true` |
|PrimaryOrigin |String |No |Indicates a primary origin. This parameter is used to obtain the domain names that contain this primary origin in their configurations. The value of this parameter can be an IP address or a domain name. |`helloworld.example.com` |
|PageNum |Long |No |Indicates a page number, which is used to obtain the list of domain names on that page. The default value of this parameter is `1`.<br><br>CDN paginates the domain names that meet the filter conditions. You can calculate the number of pages returned by this API based on the response parameter `Total` and the request parameter `PageSize`. |`1` |
|PageSize |Long |No |Indicates the number of domain names contained on each page. The value range of this parameter is 1\-100, and the default value is `10`. |`10` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|PageNum |Long |Indicates `PageNum` in the request parameters. |`1` |
|PageSize |Long |Indicates `PageSize` in the request parameters. |`10` |
|Total |Long |Indicates the number of domain names that meet the filter conditions. The value of this parameter is not affected by the request parameters `PageSize` and `PageNum`. |`100` |
|Data |Object[] |Indicates the list of domain names that meet the filter conditions. | |
|Domain |String |Indicates a domain name in the list. |`www.example.com` |
|ServiceType |String |Indicates the service type of the domain name. This parameter has the following values:<br><br><br>* `download`: Indicates file download.<br><br>* `web`: Indicates a web page.<br><br>* `video`: Indicates audio and video on demand. |`web` |
|Status |String |Indicates the status of the domain name. This parameter has the following values:<br><br><br>* `online`: Indicates that the status is "Enabled".<br><br>* `configuring`: Indicates that the status is "Configuring".<br><br>* `offline`: Indicates that the status is "Disabled". |`online` |
|Cname |String |Indicates the CNAME assigned to the domain name by CDN. |`www.example.com.bplslb.com` |
|ServiceRegion |String |Indicates the service area of the domain name. This parameter has the following values:<br><br><br>* `chinese_mainland`: Indicates Chinese mainland.<br><br>* `global`: Indicates global.<br><br>* `outside_chinese_mainland`: Indicates global (excluding Chinese mainland). |`outside_chinese_mainland` |
|CreateTime |Long |Indicates the time when the domain name was added to CDN, in Unix timestamp format. |`1625587200` |
|UpdateTime |Long |Indicates the time of the last update of the domain name, in Unix timestamp format. Update operations include enabling, disabling, and modifying the domain name configuration. |`1601371409` |
|Project |String |Indicates the project to which the domain name belongs. |`default` |
|OriginProtocol |String |Indicates the protocol used for origin requests. This parameter has the following values:<br><br><br>* `http`: Indicates the HTTP protocol.<br><br>* `https`: Indicates the HTTPS protocol.<br><br>* `followclient`: Indicates the protocol used by the user request. |`http` |
|IPv6 |Boolean |Indicates whether the IPv6 feature is enabled for the domain name. This parameter has the following values:<br><br><br>* `true`: Indicates that IPv6 is enabled.<br><br>* `false`: Indicates that IPv6 is not enabled. |`true` |
|HTTPS |Boolean |Indicates whether the HTTPS encryption service is enabled for the domain name. This parameter has the following values:<br><br><br>* `true`: Indicates that the HTTPS encryption service is enabled.<br><br>* `false`: Indicates that the HTTPS encryption service is not enabled. |`true` |
|PrimaryOrigin |String[] |Indicates the list of primary origins configured for the domain name. |`"xxx.xx.xxx.xx","helloworld1.example.com"` |
|BackupOrigin |String[] |Indicates the list of secondary origins configured for the domain name. If no secondary origin is configured for the domain name, the value of this parameter is `null`. |`"xxx.xx.xxx.xx","helloworld2.example.com"` |
|ResourceTags |Object[] |Indicates the list of tags carried by the domain name. If the domain name does not carry any tags, the value of this parameter is `null`. | |
|Key |String |Indicates the key of a tag in the tag list. |`userKey` |
|Value |String |Indicates the value of the tag. |`userValue` |
|CacheShared |String |Indicates the role of the domain name in the shared cache configuration. This parameter has the following values:<br><br><br>* `target_host`: Indicates that a shared cache configuration exists, in which the role of the domain name is the target domain name.<br><br>* `cache_shared_on`: Indicates that a shared cache configuration exists, in which the role of the domain name is the configured domain name.<br><br>* `""`: The value of this parameter is empty, indicating that the domain name does not exist in any shared cache configuration. |`cache_shared_on` |
|CacheSharedTargetHost |String |If `CacheShared` is `cache_shared_on`, it indicates the target domain name that shares the cache with this domain name. If `CacheShared` is `target_host` or an empty value (""), the value of this parameter is empty (""). |`www.example.net` |
|Waf |Boolean |Indicates whether WAF Protection is enabled for the domain name. This parameter has the following values:<br><br><br>* `true`: Indicates that WAF Protection is enabled.<br><br>* `false`: Indicates that WAF Protection is not enabled. |`false` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=ListCdnDomains&Version=2021-03-01
{
    "Domain": "example",
    "ResourceTags": [
        "key1:val1",
        "key2:val2"
    ]
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250821112545F5890E6D640605A33280",
        "Action": "ListCdnDomains",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": [
            {
                "BackupOrigin": [
                    "203.0.113.9",
                    "img2.example.com"
                ],
                "CacheShared": "",
                "CacheSharedTargetHost": "",
                "Cname": "www.example.com.bplslb.com",
                "CreateTime": 1755585663,
                "Domain": "www.example.com",
                "HTTPS": true,
                "IPv6": true,
                "OriginProtocol": "https",
                "PrimaryOrigin": [
                    "203.0.113.8",
                    "img.example.com",
                    "bpcntest.tos-ap-southeast-3.bytepluses.com",
                    "mybucket.oss-ap-southeast-1.aliyuncs.com",
                    "mybucket.cos.ap-singapore.myqcloud.com",
                    "my-bucket.s3.ap-southeast-1.amazonaws.com",
                    "myazstorage.blob.core.windows.net"
                ],
                "Project": "default",
                "ResourceTags": [
                    {
                        "Key": "mykey",
                        "Value": "myvalue"
                    }
                ],
                "ServiceRegion": "outside_chinese_mainland",
                "ServiceType": "web",
                "Status": "online",
                "UpdateTime": 1755585663,
                "Waf": false
            }
        ],
        "PageNum": 1,
        "PageSize": 10,
        "Total": 1
    }
}
```


&nbsp;
