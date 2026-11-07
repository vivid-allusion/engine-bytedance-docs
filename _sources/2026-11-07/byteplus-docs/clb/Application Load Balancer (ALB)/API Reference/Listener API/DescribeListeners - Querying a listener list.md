---
title: "DescribeListeners - Querying a listener list"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-DescribeListeners"
---

Call the DescribeListeners API to query the listener list.

## Instructions

* Submit up to 200 API requests per second.

* If multiple request parameters are provided, the query will return listener entries that match all the specified conditions. If no matching entry is found, an empty value is returned.

* If none of the optional request parameters are provided, the query will be performed under the current logged\-in account and return all listeners belonging to this account.

## Request description

* Method: **GET**

* URL:  **/?Action=DescribeListeners&Version=2020\-04\-01**

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeListeners&groupName=%E7%9B%91%E5%90%AC%E5%99%A8&serviceCode=alb&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: DescribeListeners`

Action to execute. Set the value to DescribeListeners.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**TagFilters.N.Key ** string[]`optional` `Example: TagFilters.1.Key=k1&TagFilters.2.Key=k2`

The tag key.

* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. Multiple tag keys have a logical AND relationship. The query returns ALB listeners tagged with all the specified keys.

* Duplicate values are not allowed.

**TagFilters.N.Values.N ** string[]`optional` `Example: TagFilters.1.Value.1=v1&TagFilters.1.Value.2=v2&TagFilters.2.Value.1=v3`

The tag value.

* The first N specifies the serial number of a tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns ALB listeners that have any of the specified tag values for that key.

* Separate multiple tag values with an ampersand (&).

> **tip**

> If this parameter is passed in, TagFilters.N.Key must be passed in first.

> Passing an empty string queries for listeners with an empty tag value.

**ListenerName ** string`optional` `Example: test`

Listener name.

**LoadBalancerId ** string`optional` `Example: alb-*********`

ALB instance ID.

**PageNumber ** integer`optional` `Example: 1`

The page number of the list. Default: 1.

**PageSize ** integer`optional` `Example: 20`

Number of records per page for paginated queries, with a value range of 1\-100 (default: 10).

**ListenerIds.N ** string[]`optional` `Example: ListenerIds.1=lsn-abc*****&ListenerIds.2=lsn-def*******`

Listener ID.

* Parameter \-N: Represents the sequence number of a listener. A maximum of 20 can be queried in a single request.

* Separate multiple listener IDs with ampersands (&).

**Protocol ** string`optional` `Example: HTTPS`

Listener protocol. Valid values:

* HTTP.

* HTTPS.

**ProjectName ** string`optional` `Example: default`

The project name that the listener belongs to.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** string`Example: 20210816110638****2514606306AF947C`

Request ID.

**PageSize ** integer`Example: 20`

The number of records on the current page.

**PageNumber ** integer`Example: 1`

Current page number.

**TotalCount ** integer`Example: 26`

Total number of matching listeners.

**Listeners ** object[]`Example: --`

Detailed information of listeners that meet the criteria.

**XRealIpEnabled ** string`Example: on`

Enable/disable the X\-Real\-IP header field in requests for the listener. Valid values:

* on: Enable.

* off: Disable.

**ListenerId ** string`Example: lsn-*******`

Listener ID.

**ListenerName ** string`Example: test`

Listener name.

**CreateTime ** string`Example: 2021-12-29T16:37:37Z`

Creation time of listener.

**UpdateTime ** string`Example: 2021-12-29T16:37:37Z`

Last operation time of the listener.

**Status ** string`Example: Active`

Listener status.

* Creating

* Active: Running.

* Pending: Modifying.

* Disabled: Stopped.

* Deleting

**Enabled ** string`Example: on`

Enable the listener.

* on: Enable.

* off: Disable.

**Protocol ** string`Example: HTTP`

Listener protocol.

**Port ** integer`Example: 80`

The listening port of the listener.

**ServerGroupId ** string`Example: rsp-*******`

Default server group of the listener.

**ServerGroups ** object[]`Example: --`

Information about all server groups associated with the listener.

**ServerGroupId ** string`Example: rsp-888888`

Server group ID.

**ServerGroupName ** string`Example: pool`

Name of the server group.

**LoadBalancerId ** string`Example: alb-**********`

The ALB instance ID to which the listener belongs.

**Description ** string`Example: test`

Description of the listener.

**CertificateSource ** string`Example: cert_center`

Source of the default certificate associated with the HTTPS listener.

* alb: Indicates the certificate uploaded via ALB.

* cert_center: Represents an SSL certificate purchased from or uploaded to the BytePlus Certificate Center.

**CertificateId ** string`Example: cert-******`

ID of the certificate bound to the HTTPS listener. Effective when the certificate source is alb.

**CertCenterCertificateId ** string`Example: cert-******`

ID of the certificate bound to the HTTPS listener. Effective when the certificate source is cert_center.

**CACertificateSource ** string`Example: pca_root`

Source of the CA certificate associated with the HTTPS listener.

* alb: Indicates the certificate uploaded via ALB.

* pca_root: Represents a private root CA certificate purchased from or uploaded to the BytePlus Certificate Center.

* pca_sub: Represents a private sub CA certificate purchased from or uploaded to the BytePlus Certificate Center.

**CACertificateId ** string`Example: cert-******`

CA certificate ID associated with the HTTPS listener. Effective when the certificate source is alb.

**PcaRootCACertificateId ** string`Example: cert-******`

CA certificate ID associated with the HTTPS listener. Effective when the certificate source is pca_root.

**PcaSubCACertificateId ** string`Example: cert-******`

CA certificate ID associated with the HTTPS listener. Effective when the certificate source is pca_sub.

**EnableHttp2 ** string`Example: off`

HTTP2.0 feature switch.

* on: Enable.

* off: Disable.

**EnableQuic ** string`Example: off`

QUIC feature switch.

* on: Enable.

* off: Disable.

**AclStatus ** string`Example: off`

Enable access control.

* on: Enable.

* off: Disable.

**AclType ** string`Example: black`

Method of access control.

* white: Allowlist method. Indicates that the listener forwards requests only from the IP addresses or CIDR blocks set in the selected access control policy group. If no IPs are added to the selected policy group, the listener does not forward any requests.

* black: Denylist method. Indicates that the listener denies requests only from the IP addresses or CIDR blocks set in the selected access control policy group. If no IPs are added to the selected policy group, the listener forwards all requests.

**AclIds ** string[]`Example: ["acl-2fe5excqgk6ww5oxruvcv****","acl-2febxt4pu0zy85oxruw0t****"]`

The ID of the Access Control List (ACL) bound to the listener. Returned only when the AclStatus parameter is on.

**CustomizedCfgId ** string`Example: ccfg-****`

Custom configuration ID.

**DomainExtensions ** object[]`Example: --`

The list of additional domains associated with the HTTPS listener.

**DomainExtensionId ** string`Example: dc-*******`

Additional domain ID.

**CertificateSource ** string`Example: cert_center`

Source of the default certificate associated with the HTTPS listener.

* alb: Indicates the certificate uploaded via ALB.

* cert_center: Represents an SSL certificate purchased from or uploaded to the BytePlus Certificate Center.

**CertificateId ** string`Example: cert-*****`

ID of the server certificate used by the domain. Effective when the certificate source is alb.

**CertCenterCertificateId ** string`Example: cert-******`

ID of the server certificate used by the domain. Effective when the certificate source is cert_center.

**Domain ** string`Example: abc.com`

The domain name.

**ListenerId ** string`Example: lsn-****`

The ID of the listener to which the additional domain belongs.

**San ** string`Example: www.test.com,api.test.com,192.168.1.100`

The certificate's CommonName, additional domains, and IP addresses, separated by commas (,).

**PcaLeafCertificateId ** string`Example: cert-********`

ID of the server certificate used by the domain. Effective when the certificate source is pca_leaf.

**ProjectName ** string`Example: default`

The project name that the listener belongs to.

**Tags ** object[]`Example: --`

Tags associated with the listener.

**Key ** string`Example: key`

The tag key of the custom tag.

**Value ** string`Example: value`

Custom tag

**AccessLogRecordCustomizedHeadersEnabled ** string`Example: on`

Whether the "record custom headers in access logs" feature is enabled for the listener.

* on: This feature is enabled.

* off: This feature is not enabled.

**PcaLeafCertificateId ** string`Example: cert-********`

ID of the certificate bound to the HTTPS listener. Effective when the certificate source is pca_leaf.

## Request example

```text
GET /?Action=DescribeListeners&Version=2020-04-01&LoadBalancerId=alb-1g1f1c6aevm****buxws5k0k3&PageSize=20&PageNumber=1&ListenerIds.1=lsn-1g0swrgw****88ibuxwmboj9h&ListenerIds.2=lsn-1g0swrgw****88ibuxwmboj9h HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20260514193453156097164082FB6467",
    "Action": "DescribeListeners",
    "Version": "2020-04-01",
    "Service": "alb",
    "Region": "cn-beijing"
  },
  "Result": {
    "RequestId": "20210816110638****2514606306AF947C",
    "PageSize": 20,
    "PageNumber": 1,
    "TotalCount": 26,
    "Listeners": [
      {
        "XRealIpEnabled": "on",
        "ListenerId": "lsn-*******",
        "ListenerName": "test",
        "CreateTime": "2021-12-29T16:37:37Z",
        "UpdateTime": "2021-12-29T16:37:37Z",
        "Status": "Active",
        "Enabled": "on",
        "Protocol": "HTTP",
        "Port": 80,
        "ServerGroupId": "rsp-*******",
        "ServerGroups": [
          {
            "ServerGroupId": "rsp-888888",
            "ServerGroupName": "pool"
          }
        ],
        "LoadBalancerId": "alb-**********",
        "Description": "test",
        "CertificateSource": "cert_center",
        "CertificateId": "cert-******",
        "CertCenterCertificateId": "cert-******",
        "CACertificateSource": "pca_root",
        "CACertificateId": "cert-******",
        "PcaRootCACertificateId": "cert-******",
        "PcaSubCACertificateId": "cert-******",
        "EnableHttp2": "off",
        "EnableQuic": "off",
        "AclStatus": "off",
        "AclType": "black",
        "AclIds": [
            "acl-2fe5excqgk6ww5oxruvcv****","acl-2febxt4pu0zy85oxruw0t****"
        ],
        "CustomizedCfgId": "ccfg-****",
        "DomainExtensions": [
          {
            "DomainExtensionId": "dc-*******",
            "CertificateSource": "cert_center",
            "CertificateId": "cert-*****",
            "CertCenterCertificateId": "cert-******",
            "Domain": "abc.com",
            "ListenerId": "lsn-****",
            "San": "www.test.com,api.test.com,192.168.1.100",
            "PcaLeafCertificateId": "cert-********"
          }
        ],
        "ProjectName": "default",
        "Tags": [
          {
            "Key": "key",
            "Value": "value"
          }
        ],
        "AccessLogRecordCustomizedHeadersEnabled": "on",
        "PcaLeafCertificateId": "cert-********"
      }
    ]
  }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request does not contain the required parameter. Please ensure the request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|400 |InvalidListenerName.Malformed |The specified ListenerName is malformed. |The specified ListenerName format is invalid. |
|400 |LimitExceed.Listener |You've reached the limit on the number of listeners that you can operate at a time. |The maximum number of listeners that can be operated on in a single request has been reached. |
|400 |InvalidProtocol.Malformed |The specified Protocol is malformed. |The specified Protocol format is invalid. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
