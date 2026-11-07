---
title: "DescribeCertificates - Querying a certificate list"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeCertificates"
---

Call the DescribeCertificates API to query certificates that meet the specified conditions.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* If multiple request parameters are provided, the query will return certificates that match all the specified conditions. If no matching certificate is found, an empty value is returned.

* If none of the optional request parameters are provided, the query will be performed under the current logged\-in account and return all certificates belonging to this account.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeCertificates&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|yj97nt">必选</span> `Example: DescribeCertificates`

Action to execute. Set the value to **DescribeCertificates**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|fKDcxo">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**CertificateIds.N ** <span data-label="purple">String </span>`optional` `Example: cert-3tjuxoukkq3vj0ww****`

Certificate ID. You can call this API to get the certificate ID.


* Parameter \- N: Represents the serial number of the certificate. The valid range is 1\-100.

* Connect multiple certificate IDs with ampersands (&).



**CertificateName ** <span data-label="purple">String </span>`optional` `Example: mycert`

Certificate name.



**ProjectName ** <span data-label="purple">String </span>`optional` `Example: default`

The name of the project to which the certificate belongs.



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The tag key.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. Multiple tag keys have a logical AND relationship. The query returns certificates tagged with all the specified keys.

* Duplicate values are not allowed.



**TagFilters.N.Values.N ** <span data-label="purple">String </span>`optional` `Example: v1`

The tag value.


* The first N specifies the serial number of a tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns certificates that have any of the specified tag values for that key.

* Separate multiple tag values with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If this parameter is passed in, <code>TagFilters.N.Key</code> must be passed in first.</div>


* <div data-tips="true" data-tips-type="tip">Passing an empty string queries for certificates with an empty tag value.</div>




**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 10`

The number of rows per page for paginated queries. Valid range: 1\-100. Default value: 10.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID



**PageSize ** <span data-label="purple">Integer </span>`Example: 20`

The number of rows on the current page.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

Current page number.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 50`

Total number of certificates that meet the criteria.



**Certificates ** <span data-label="purple">Object[] </span>`Example: -`

Details of the certificates that meet the conditions.


**CertificateId ** <span data-label="purple">String </span>`Example: cert-3tigvwjuzu3vj0wt****`

The ID of the certificate.



**CertificateName ** <span data-label="purple">String </span>`Example: mycert01`

Certificate name.



**Description ** <span data-label="purple">String </span>`Example: This is a cert.`

Certificate description.



**CreateTime ** <span data-label="purple">String </span>`Example: 2021-08-11T16:37:37Z`

Creation time of the certificate.



**ExpiredAt ** <span data-label="purple">String </span>`Example: 2021-08-11T16:37:37Z`

Expiration time of the certificate.



**DomainName ** <span data-label="purple">String </span>`Example: www.a123.xxx.com`

The root domain of the certificate.



**SubjectAlternativeNames ** <span data-label="purple">String[] </span>`Example: ["www.abc.xxx.com","www.abc.xxx.cn"]`

List of alternative domain names for the certificate.



**Listeners ** <span data-label="purple">String[] </span>`Example: ["lsn-rrhsh4vegr9cv0x591p****","lsn-mioicx8e1jpc5smt1ayy****"]`

ID of the listener associated with the certificate.



**ProjectName ** <span data-label="purple">String </span>`Example: default`

The name of the project to which the certificate belongs.



**ServiceManaged ** <span data-label="purple">Boolean </span>`Example: false`

It is a managed resource.


* true: Managed resource.

* false: Not a managed resource.



**Tags ** <span data-label="purple">Object[] </span>`Example: -`

Tag information.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.





&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeCertificates&Version=2020-04-01&CertificateIds.1=cert-3tjuxoukkq3vj0ww****&CertificateName=mycert&ProjectName=default&TagFilters.1.Key=k1&TagFilters.1.Values.1=v1&PageNumber=1&PageSize=10
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeCertificates",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "Certificates": [
            {
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ],
                "ExpiredAt": "2021-08-11T16:37:37Z",
                "Listeners": [
                    "lsn-rrhsh4vegr9cv0x591p****",
                    "lsn-mioicx8e1jpc5smt1ayy****"
                ],
                "CreateTime": "2021-08-11T16:37:37Z",
                "DomainName": "www.a123.xxx.com",
                "Description": "This is a cert.",
                "ProjectName": "default",
                "CertificateId": "cert-3tigvwjuzu3vj0wt****",
                "ServiceManaged": false,
                "CertificateName": "mycert01",
                "SubjectAlternativeNames": [
                    "www.abc.xxx.com",
                    "www.abc.xxx.cn"
                ]
            }
        ],
        "PageNumber": 1,
        "PageSize": 20,
        "RequestId": "20210811152539010225146063030****",
        "TotalCount": 50
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidName.Malformed |The specified Name is malformed. |The format specified for Name is invalid. |
|400 |InvalidPageNumber.Malformed |The specified PageNumber is malformed. |The specified PageNumber parameter format is invalid. |
|400 |InvalidPageSize.Malformed |The specified PageSize is malformed. |The specified PageSize parameter format is invalid. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey parameter format is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue parameter format is invalid. |
|400 |LimitExceeded.CertificateId |You've reached the limit on the number of CertificateId that you can operate. |The maximum number of certificate resources that can be operated on in a single request has been reached. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of filter tag keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValues |You've reached the limit on the number of tag values that you can filter. |The maximum tag key\-value pairs for filtering in a single request has been reached. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
