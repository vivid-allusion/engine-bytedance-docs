---
title: "DescribeAllCertificates - Querying all certificate lists"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeAllCertificates"
---

Call the DescribeAllCertificates API to query all certificate lists.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* A single account can query up to 100 certificates at a time.

* Submit up to 40 API requests per second.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeAllCertificates&serviceCode=alb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|1oOH9S">必选</span>`Example: DescribeAllCertificates`

The interface name. The current API name is `DescribeAllCertificates`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|LUOOn_">必选</span> `Example: 2020-04-01`

The interface version. Current API version is `2020-04-01`.



**CertificateIds.N ** <span data-label="purple"> String[]  </span>`optional` `Example: CertificateIds.1=cert-123***765&CertificateIds.2=cert-234****876`

Certificate ID.


* Parameter \- N: Represents the serial number of certificate. The valid range is 1 to 100.

* Separate multiple certificates with ampersands (&).



**CertificateName ** <span data-label="purple"> String </span>`optional` `Example: test`

Certificate name.



**CertificateType ** <span data-label="purple"> String </span>`optional` `Example: CA`

Certificate type, the values are as follows:


* CA: CA certificate.

* Server: Server certificate.



**PageSize ** <span data-label="purple"> Integer  </span>`optional` `Example: 20`

Number of rows per page for paginated queries. Valid range: 1 to 100. Default value: 10.



**PageNumber ** <span data-label="purple"> Integer </span>`optional` `Example value: 1`

The page number of the list. Default: 1.



**TagFilters.N.Key ** <span data-label="purple"> String[] </span>`optional` `Example: TagFilters.1.Key=k1&TagFilters.2.Key=k2`

The tag key.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. Multiple tag keys have a logical AND relationship. The query returns certificates tagged with all the specified keys.

* Duplicate values are not allowed.



**TagFilters.N.Values.N ** <span data-label="purple"> String[]  </span>`optional` `Example: TagFilters.1.Value.1=v1&TagFilters.1.Value.2=v2&TagFilters.2.Value.1=v3`

The tag value.


* The first N specifies the serial number of a tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns certificates that have any of the specified tag values for that key.

* Separate multiple tag values with an ampersand (&).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">If this parameter is passed in, TagFilters.N.Key must be passed in first.</div>


* <div data-tips="true" data-tips-type="default">Passing an empty string queries for certificates with an empty tag value.</div>




**ProjectName ** <span data-label="purple">String</span> `optional` `Example value: default`

Name of the project the certificate belongs to.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple"> String  </span>`Example: 20210816110638****2514606306AF947C`

Request ID.



**PageSize ** <span data-label="purple"> Integer  </span>`Example: 20`

The number of rows on the current page.



**PageNumber** <span data-label="purple">Integer</span> `Example: 1`

Current page number.



**TotalCount ** <span data-label="purple"> Integer </span>`Example: 50`

Total number of certificates that meet the criteria.



**Certificates ** <span data-label="purple"> Object[]  </span>`Example: -`

List of certificates that meet the criteria.


**CertificateId ** <span data-label="purple"> String  </span>`Example: cert-123***765`

Certificate ID.



**CertificateName ** <span data-label="purple"> String  </span>`Example: test`

Certificate name.



**CertificateType ** <span data-label="purple"> String </span>`Example: CA`

Certificate type.


* CA: CA certificate.

* Server: Server certificate.



**Description ** <span data-label="purple"> String </span>`Example: test`

The certificate description.



**CreateTime ** <span data-label="purple"> String  </span>`Example: 2021-12-14T11:13:40+08:00`

Creation time of the certificate.



**ExpiredAt ** <span data-label="purple"> String </span>`Example: 2021-12-14T11:13:40+08:00`

Expiration time of the certificate.



**DomainName ** <span data-label="purple"> String </span>`Example: test.com`

The domain name of the certificate.



**San ** <span data-label="purple"> String  </span>`Example: www.test.com,*.test.com`

List of certificate additional domain names, with multiple domains separated by commas (','), including (commonName, DnsName, IP).



**Listeners ** <span data-label="purple"> String[]  </span>`Example: [lsn-123*****112,lsn-234*****567]`

List of the listener associated with the certificate.



**Status ** <span data-label="purple"> String </span>`Example: Active`

Status of the certificate.


* Creating

* Active: Running.

* Deleting



**Tags ** <span data-label="purple"> Object[] </span>`Example: -`

List of tags associated with the certificate.


**Key ** <span data-label="purple"> String </span>`Example: key`

The tag key of the custom tag.



**Value ** <span data-label="purple"> String </span>`Example: value`

The tag value of the custom tag.




**ProjectName** <span data-label="purple">String</span> `Example: default`

Name of the project the certificate belongs to.




<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DescribeAllCertificates&CertificateIds.1=cert-2fe5jqh****hs5oxruwk7x9ze&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20210816110638****2514606306AF947C",
        "Action": "DescribeAllCertificates",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210816110638****2514606306AF947C",
        "PageNumber": 1,
        "PageSize": 10,
        "TotalCount": 1,
        "Certificates": [
            {
                "CACertificateId": "cert-2fe5k****c16o5oxruvtk3qf5",
                "CACertificateName": "test",
                "CertificateType": "server",
                "Description": "test",
                "CreateTime": "2021-12-14T11:13:40+08:00",
                "ExpiredAt": "2021-12-14T11:13:40+08:00",
                "DomainName": "*.a.cdn-build.net",
                "Listeners": [
                    "lsn-1g0e0p14****88ibuxxpnwden",
                    "lsn-1g0e0p90e****8ibuxwy36kc1"
                ]
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

If the response body contains an Error field, it indicates the API request failed. This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Error-codes).


|**Status code** |**Error codes** |**Error message** |**Notes** |
|---|---|---|---|
|400 |LimitExceed.Certificate |You've reached the limit on the number of certificates that you can operate at a time. |You have reached the maximum number of certificates that can be operated in a single operation. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|400 |InvalidCertificateName.Malformed |The specified CertificateName is malformed. |The specified CertificateName parameter format is invalid. |
|400 |LimitExceed.TagFilters.Values |You've reached the limit on the number of tag filter values that you can operate at a time. |You have reached the maximum number of tag values that can be operated on in a single request. |
|400 |InvalidTagFilters.Key.Malformed |The specified TagFilters.Key is malformed. |The specified TagFilters.Key parameter format is invalid. |
|400 |InvalidTagFilters.Value.Malformed |The specified TagFilters.Value is malformed. |The specified TagFilters.Value parameter format is invalid. |
|400 |InvalidTagFilters.Key.Duplicated |The specified TagFilters.Key is duplicated. |The specified TagFilters.Key is duplicated. |
