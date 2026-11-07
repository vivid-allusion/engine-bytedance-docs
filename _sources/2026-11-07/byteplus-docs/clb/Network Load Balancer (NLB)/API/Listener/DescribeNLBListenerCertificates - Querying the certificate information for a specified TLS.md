---
title: "DescribeNLBListenerCertificates - Querying the certificate information for a specified TLS listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeNLBListenerCertificates"
---

Call the DescribeNLBListenerCertificates API to query the certificate information under a specified TLS listener.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeNLBListenerCertificates&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|EwlgCI">必选</span> `Example: DescribeNLBListenerCertificates`

Action to execute. Set the value to DescribeNLBListenerCertificates.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|jICTfo">必选</span> `Example: 2020-04-01`

Current API version is 2020\-04\-01.



**ListenerId ** <span data-label="purple">String </span><span data-api-tag="require|nxKEmG">必选</span> `Example: lsn-cam1lg536fhkll****`

Listener ID.



**CertificateType ** <span data-label="purple">String </span>`optional` `Example: Server`

Certificate type. Values:


* Server: Server certificate.

* CA: CA certificate.



**CertificateIds.N ** <span data-label="purple">String </span>`optional` `Example: cert-wuytp9pa****`

Certificate ID.


* Parameter \- N: Represents the serial number of the certificate. The valid range is 1\-20.

* Separate multiple certificate IDs with ampersands (&).



**Domain ** <span data-label="purple">String </span>`optional` `Example: www.test.com`

Certificate Common Name (CN).



**NextToken ** <span data-label="purple">String </span>`optional` `Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token that is used to mark the position in pagination queries.


* If left blank, the query starts from the beginning.

* Provide the NextToken returned from a previous call to this API, the query continues from that pagination position.



**MaxResults ** <span data-label="purple">Integer </span>`optional` `Example: 50`

The number of query results. Default: 10. Maximum: 100.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID.



**NextToken ** <span data-label="purple">String </span>`Example: caeba0bbb2be03f84eb48b699f0a****`

Pagination token used to mark the position in paginated results. Leave this empty for the initial API call. For subsequent queries, set this value to the NextToken parameter returned by the previous API call.



**ListenerId ** <span data-label="purple">String </span>`Example: lsn-bpn0kn908w4nbw****`

Listener ID.



**Certificates ** <span data-label="purple">Object[] </span>`Example: --`

Certificate lists associated with the TLS listener.


**CertificateType ** <span data-label="purple">String </span>`Example: Server`

Certificate type.



**CertificateSource ** <span data-label="purple">String </span>`Example: SSL`

The source of the server certificate for the TLS listener.


* SSL: Certificate Center \- SSL certificate.

* PCALeaf: Certificate Center \- Private certificate of the private CA.



**CertificateId ** <span data-label="purple">String </span>`Example: cert-xxx`

ID of the server certificate.



**Status ** <span data-label="purple">String </span>`Example: Associated`

Certificate\-Listener association status.


* Associating

* Associated

* Disassociating



**Domain ** <span data-label="purple">String </span>`Example: www.test.com`

Certificate domain name.



**IsDefault ** <span data-label="purple">Boolean </span>`Example: true`

Default certificate of the listener


* true: Yes

* false: No.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeNLBListenerCertificates&Version=2020-04-01&ListenerId=lsn-cam1lg536fhkll****&CertificateType=Server&CertificateIds.1=cert-wuytp9pa****&Domain=www.test.com&NextToken=caeba0bbb2be03f84eb48b699f0a****&MaxResults=50 HTTP/1.1
Host: clb.cn-beijing.byteplusapi.com.cn
Date: 20260310T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeNLBListenerCertificates",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "Certificates": [
            {
                "Domain": "www.test.com",
                "Status": "Associated",
                "IsDefault": true,
                "CertificateId": "cert-xxx",
                "CertificateType": "Server",
                "CertificateSource": "SSL"
            }
        ],
        "ListenerId": "lsn-bpn0kn908w4nbw****",
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "RequestId": "20210811152539010225146063030****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/NLB-Common-Error-Codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken format is invalid. |
|400 |InvalidMaxResult.Malformed |The specified MaxResult is malformed. |The specified MaxResult parameter format is invalid. |
|400 |InvalidMaxResults.Malformed |The specified MaxResults is malformed. |The specified MaxResults parameter format is invalid. |
|400 |InvalidNextToken.Malformed |The specified NextToken is malformed. |The specified NextToken parameter format is invalid. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|404 |InvalidListener.NotFound |The specified Listener does not exist. |The specified listener does not exist. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
