---
title: "DescribeListenerAttributes - Querying the details of specified listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-DescribeListenerAttributes"
---

Call the DescribeListenerAttributes API to view details of the specified listener.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Submit up to 200 API requests per second.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeListenerAttributes&groupName=%E7%9B%91%E5%90%AC%E5%99%A8&serviceCode=alb&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|cA5YEu">必选</span> `Example: DescribeListenerAttributes`

Action to execute. Set the value to DescribeListenerAttributes.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|iEpcBf">必选</span> `Example: 2020-04-01`

Current API version is 2020\-04\-01.



**ListenerId ** <span data-label="purple">string </span><span data-api-tag="require|lZQykM">必选</span> `Example: lsn-*******`

Listener ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**XRealIpEnabled ** <span data-label="purple">string </span>`Example: on`

The listener enables/disables the X\-real\-ip header.


* on: Enable.

* off: Disable.



**RequestId ** <span data-label="purple">string </span>`Example: 20210816110638****2514606306AF947C`

Request ID.



**ListenerId ** <span data-label="purple">string </span>`Example: lsn-*********`

Listener ID.



**ListenerName ** <span data-label="purple">string </span>`Example: test`

Listener name.



**CreateTime ** <span data-label="purple">string </span>`Example: 2021-12-14T11:13:40+08:00`

Creation time of listener.



**UpdateTime ** <span data-label="purple">string </span>`Example: 2021-12-14T11:13:40+08:00`

Last operation time of the listener.



**LoadBalancerId ** <span data-label="purple">string </span>`Example: alb-**********`

The CLB instance ID to which the listener belongs.



**Status ** <span data-label="purple">string </span>`Example: Active`

Listener status.


* Creating

* Active: Running.

* Pending: Modifying.

* Disabled: Stopped.

* Deleting



**Enabled ** <span data-label="purple">string </span>`Example: off`

Enable the listener.


* on: Enable.

* off: Disable.



**Protocol ** <span data-label="purple">string </span>`Example: HTTPS`

Listener protocol.


* HTTP

* HTTPS



**Port ** <span data-label="purple">integer </span>`Example: 80`

The listening port of the listener.



**ServerGroupId ** <span data-label="purple">string </span>`Example: rsp-*******`

Default server group of the listener.



**ServerGroups ** <span data-label="purple">object[] </span>`Example: -`

All server groups associated with the listener.


**ServerGroupId ** <span data-label="purple">string </span>`Example: rsp-888888`

Server group ID.



**ServerGroupName ** <span data-label="purple">string </span>`Example: pool`

Name of the server group.




**Description ** <span data-label="purple">string </span>`Example: test`

Description of the listener.



**CertificateSource ** <span data-label="purple">string </span>`Example: cert_center`

The source of the default certificate associated with the HTTPS listener. Valid values:


* alb: Indicates the certificate uploaded via ALB.

* cert_center: Represents an SSL certificate purchased from or uploaded to the BytePlus Certificate Center.



**CertificateId ** <span data-label="purple">string </span>`Example: cert-******`

ID of the certificate bound to the HTTPS listener. Effective when the certificate source is alb.



**CertCenterCertificateId ** <span data-label="purple">string </span>`Example: cert-******`

ID of the certificate bound to the HTTPS listener. Effective when the certificate source is cert_center.



**CACertificateSource ** <span data-label="purple">string </span>`Example: pca_root`

Source of the CA certificate associated with the HTTPS listener.


* alb: Indicates the certificate uploaded via ALB.

* pca_root: Represents a private root CA certificate purchased from or uploaded to the BytePlus Certificate Center.

* pca_sub: Represents a private sub CA certificate purchased from or uploaded to the BytePlus Certificate Center.



**CACertificateId ** <span data-label="purple">string </span>`Example: cert-******`

CA certificate ID associated with the HTTPS listener. Effective when the certificate source is alb.



**PcaRootCACertificateId ** <span data-label="purple">string </span>`Example: cert-******`

CA certificate ID associated with the HTTPS listener. Effective when the certificate source is pca_root.



**PcaSubCACertificateId ** <span data-label="purple">string </span>`Example: cert-******`

CA certificate ID associated with the HTTPS listener. Effective when the certificate source is pca_sub.



**EnableHttp2 ** <span data-label="purple">string </span>`Example: off`

HTTP2.0 feature switch.


* on: Enable.

* off: Disable.



**EnableQuic ** <span data-label="purple">string </span>`Example: off`

QUIC feature switch.


* on: Enable.

* off: Disable.



**AclStatus ** <span data-label="purple">string </span>`Example: off`

Enable access control.


* on: Enable.

* off: Disable.



**AclType ** <span data-label="purple">string </span>`Example: black`

Method of access control.


* white: Allowlist method. Indicates that the listener forwards requests only from the IP addresses or CIDR blocks set in the selected access control policy group. If no IPs are added to the selected policy group, the listener does not forward any requests.

* black: Denylist method. Indicates that the listener denies requests only from the IP addresses or CIDR blocks set in the selected access control policy group. If no IPs are added to the selected policy group, the listener forwards all requests.



**AclIds ** <span data-label="purple">string[] </span>`Example: ["acl-2fe5excqgk6ww5oxruvcv****","acl-2febxt4pu0zy85oxruw0t****"]`

The ID of the Access Control List (ACL) bound to the listener. Returned only when the AclStatus parameter is on.



**CustomizedCfgId ** <span data-label="purple">string </span>`Example: ccfg-****`

Custom configuration ID.



**DomainExtensions ** <span data-label="purple">object[] </span>`Example: -`

The list of additional domains associated with the HTTPS listener.


**PcaLeafCertificateId ** <span data-label="purple">string </span>`Example: cert-********`

ID of the server certificate used by the domain. Effective when the certificate source is pca_leaf.



**San ** <span data-label="purple">string</span>

The certificate's CommonName, additional domains, and IP addresses, separated by commas (,).



**DomainExtensionId ** <span data-label="purple">string </span>`Example: dc-*******`

Additional domain ID.



**CertificateSource ** <span data-label="purple">string </span>`Example: cert_center`

The server certificate source used by the domain name.


* alb: Indicates the certificate uploaded via ALB.

* cert_center: Indicates a certificate uploaded via BytePlus Certificate Center.

* pca_leaf: Indicates a private certificate uploaded via BytePlus Certificate Center.



**CertificateId ** <span data-label="purple">string </span>`Example: cert-*****`

ID of the server certificate used by the domain. Effective when the certificate source is alb.



**CertCenterCertificateId ** <span data-label="purple">string </span>`Example: cert-******`

ID of the server certificate used by the domain. Effective when the certificate source is cert_center.



**Domain ** <span data-label="purple">string </span>`Example: abc.com`

The domain name.

When the instance's SniAutoMatch is "off", it is the domain name entered by the user.



**ListenerId ** <span data-label="purple">string </span>`Example: lsn-****`

The ID of the listener to which the additional domain belongs.




**ProjectName ** <span data-label="purple">string </span>`Example: default`

The project name that the listener belongs to.



**Tags ** <span data-label="purple">object[] </span>`Example: -`

Tags associated with the listener.


**Key ** <span data-label="purple">string </span>`Example: key`

The tag key of the custom tag. The specific rules are as follows:

Must be 1 to 128 characters.

Case\-sensitive.

It cannot start with volc: or sys: in any case form.

Must not start or end with a space.

May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), minus signs (\-) and at signs (@).

Duplicate tag keys are not allowed for the same resource.



**Value ** <span data-label="purple">string </span>`Example: value`

The tag key of the custom tag. The specific rules are as follows:

Must be 1 to 128 characters.

Case\-sensitive.

It cannot start with volc: or sys: in any case form.

Must not start or end with a space.

May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), minus signs (\-) and at signs (@).

Duplicate tag keys are not allowed for the same resource.




**AccessLogRecordCustomizedHeadersEnabled ** <span data-label="purple">string </span>`Example: on`

Whether the "record custom headers in access logs" feature is enabled for the listener.


* on: This feature is enabled.

* off: This feature is not enabled.



**PcaLeafCertificateId ** <span data-label="purple">string </span>`Example: cert-*********`

ID of the certificate bound to the HTTPS listener. Effective when the certificate source is pca_leaf.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DescribeListenerAttributes&ListenerId=lsn-12345678****A7&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "20210816110638****2514606306AF947C",
        "Action": "DescribeListenerAttributes",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210814160835****2514606300FFE0F3",
        "ListenerId": "lsn-12345678****A7",
        "ListenerName": "test",
        "CreateTime": "2021-12-14T11:13:40+08:00",
        "UpdateTime": "2021-12-14T11:13:41+08:00",
        "LoadBalancerId": "alb-**********",
        "Status": "Active",
        "Enabled": "on",
        "Protocol": "HTTP",
        "Port": 80,
        "ServerGroupId": "rsp-2ff2u228****w5oxruwe33hdz",
        "ServerGroups": [
            {
                "ServerGroupId": "rsp-2134****1234",
                "ServerGroupName": "pool-1"
            },
            {
                "ServerGroupId": "rsp-2134****1234",
                "ServerGroupName": "pool-2"
            }
        ],
        "Description": "test",
        "CertificateId": "cert-123****989",
        "CACertificateId": "cert-123****999",
        "AclStatus": "on",
        "AclType": "black",
        "AclIds": [
            "acl-2fecyh9olyp6o5oxruw586umy"
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Explain |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|404 |InvalidListener.NotFound |The specified Listener does not exist. |The specified listener does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
