---
title: "DescribeSslVpnClientCertAttributes - Querying an SSL client certificate"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/DescribeSslVpnClientCertAttributes"
---

Call DescribeSslVpnClientCertAttributes to query information about a specified SSL client certificate.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeSslVpnClientCertAttributes&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|tQTbql">必选</span> `Example: DescribeSslVpnClientCertAttributes`

The action that you want to perform. Value: DescribeSslVpnClientCertAttributes.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|WumRSR">必选</span> `Example: 2020-04-01`

The API version.



**SslVpnClientCertId ** <span data-label="purple">String </span><span data-api-tag="require|PyDm69">必选</span> `Example: vsc-zm55pqtvk17oq32zd****`

ID of the SSL client certificate to be queried. You can call [DescribeSslVpnClientCerts](https://docs.byteplus.com/en/docs/vpn/DescribeSslVpnClientCerts) to query the ID of the SSL client certificate.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">String </span>`Example: 202307272000497643F762AB49C889****`

Request ID.



**SslVpnClientCertId ** <span data-label="purple">String </span>`Example: vsc-zm55pqtvk17oq32zd****`

ID of the SSL client certificate.



**SslVpnClientCertName ** <span data-label="purple">String </span>`Example: example_ssl_client_cert`

Name of the SSL client certificate.



**Description ** <span data-label="purple">String </span>`Example: example_ssl_vpn_client_cert_description`

Description of the SSL client certificate.



**SslVpnServerId ** <span data-label="purple">String </span>`Example: vss-zm55pqtvk17oq32zd****`

ID of the SSL VPN server.



**Status ** <span data-label="purple">String </span>`Example: Available`

Status of the SSL client.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**CertificateStatus ** <span data-label="purple">String </span>`Example: Available`

Status of the SSL client certificate.


* Available

* Expiring: Displayed when the resource expires within 1 week (inclusive).

* Expired



**CaCertificate ** <span data-label="purple">String </span>`Example: -----BEGIN CERTIFICATE-----\nMIIDPTCCAiWgAwIBAgIFAPYCuPgwDQYJKoZIhvcNAQELBQAwTjEQMA4GA1UEBhMH\0kiLwglC1aYQsdjTGuqM/wT+N9nHI5Eu99NvKhu4\n0Gq/oDuxom+*************=\n-----END CERTIFICATE-----\n`

Information about the CA certificate.



**ClientCertificate ** <span data-label="purple">String </span>`Example: -----BEGIN CERTIFICATE-----\nMIIDXDCCAkSgAwIBAgIEGn5UZjANBgkqhkiG9w0BAQsFADBOMRAwDgYDVQQGEwdC\nZIEwdCZWlqaW5nMQswCQYDVQQHEwJDTjEbMBkGA1UEAxqg58tSQENg3*************\n-----END CERTIFICATE-----\n`

Information about the SSL client certificate.



**ClientKey ** <span data-label="purple">String </span>`Example: -----BEGIN RSA PRIVATE KEY-----\nMIIEogIBAAKCAQEAvxLr+6AovkwVm9ZKR7Y7Twq5QxfMmWK8GhYithfDYmg9\n+Urzj7R83zpbOmyJA25x9l2FiIvdS*************=\n-----END RSA PRIVATE KEY-----\n`

Information about the client key.



**OpenVpnClientConfig ** <span data-label="purple">String </span>`Example: client\n# use comp-lzo in openvpn 2.3 or previous versions\n;compress lzo\nexplicit-exit-no******\n`

Configuration of the OpenVPN client.



**CreationTime ** <span data-label="purple">String </span>`Example: 2023-04-18T15:02:37+08:00`

The time when the SSL client certificate is created.



**ExpiredTime ** <span data-label="purple">String </span>`Example: 2023-04-18T15:02:37+08:00`

The time when the SSL client certificate expires.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2023-05-28T18:09:12+08:00`

The time when the SSL client certificate is modified.



**Tags ** <span data-label="purple">Object[] </span>`Example: -`

Information about all tags associated with the SSL client certificate.


**Key ** <span data-label="purple">String </span>`Example: key1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: value1`

The tag value.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeSslVpnClientCertAttributes&Version=2020-04-01&SslVpnClientCertId=vsc-12ads0g2fsmps17q7y2w8**** HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
X-Date: 20251029T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251029/cn-beijing/vpn/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "202307272000497643F762AB49C889****",
        "Action": "DescribeSslVpnClientCertAttributes",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202307272000497643F762AB49C889****",
        "SslVpnClientCertId": "vsc-12ads0g2fsmps17q7y2w8****",
        "SslVpnClientCertName": "test-cicd",
        "Description": "abc",
        "SslVpnServerId": "vss-imwoo6i1dfk08gbssxfj****",
        "Status": "Available",
        "CertificateStatus": "Available",
        "Tags": [
            {
                "Key": "k1",
                "Value": "v1"
            },
            {
                "Key": "k2",
                "Value": "v2"
            }
        ],
        "CreationTime": "2023-07-27T19:55:08+08:00",
        "ExpiredTime": "2026-07-27T19:55:08+08:00",
        "UpdateTime": "2023-07-27T19:57:56+08:00",
        "CaCertificate": "-----BEGIN CERTIFICATE-----\nMIIDXDCCAkSgAwIBAgIEGn5UZjANBgkqhkiG9w0BAQsFADBOMRAwDgYDVQQGEwdC\nZWlqaW5nMRAwDgYDVQQIEwdCZWlqaW5nMQswCQYDVQQHEwJDTjEbMBkGA1UEAxMS\fPNA1qH8gV/j37PnqxEVk2cOpgm2i1gs1c\nnQ222H5r51M9UpvrDi0/9EHeoUeZCwUnHJgn68ZtpJ5pr1Jws2Dv4AKTDxKgUQ6Y\n+6nSFhv51LoibWq4CzJNGQH3BzpO2svgG5H+LWHZ9pEiV3jyzZtc+ecZyzFm1X/2\nzOg/cauPxDlECkLv8Rt901t9ttisVtN4oIG6g8rU4VFqg58tSQENg3y**********\n-----END CERTIFICATE-----\n",
        "ClientCertificate": "-----BEGIN CERTIFICATE-----\nMIIDPTCCAiWgAwIBAgIFAPYCuPgwDQYJKoZIhvcNAQELBQAwTjEQMA4GA1UEBhMH\neZznSRLhkl40QOdOCnFELCjUTouSR1a25TtO1oPgWDNW5wughIO6sEUeQieWcgmB\nu3TOv+YZ4yQlqjJQ+HAYFN5bYkXNMv2cdCg1OqXWo23LAOJFCjxPbzfD5kI4vDC3\naVzrI89PIk0KozvCa9ZtvuHAXAopvK5sRHEiEw9rgL4WQS17EWnsKMSsB2ejF+rk\nY7qmXZ1jAO7VXxnRcttYzkQiMw0XKXNZChYj9uPT8oPzWM1necjcrzvi64lOtY1P\njZGYDO/1NN9iVp0kiLwglC1aYQs/U7HJZNBJWdjTGuqM/wT+N9nHI5Eu99NvKhu4\n0Gq/oDuxo*******=\n-----END CERTIFICATE-----\n",
        "ClientKey": "-----BEGIN RSA PRIVATE KEY-----\nMIIEogIBAAKCAQEAvxLr+6AovkwVm9ZKR7Y7Twq5eZznSRLhkl40QOdOCnFELCjU\no4jOeTD2JVtoftM9znbFrJy2/IaCMD7dfgMQRwIDAQABAoIBAAMfXQnkqSXK+oNs\n/vZnMzwxEL841Jk54CLDfwLjZMJQEM1PB1dMWqL38dg8QxfMmWK8GhYithfDYmg9\n+Urzj7R83zpbOmyJA25x9l2FiIvdSoq5RE3Txlxv******=\n-----END RSA PRIVATE KEY-----\n",
        "OpenVpnClientConfig": "client\n# use comp-lzo in openvpn 2.3 or previous versions\n;compress lzo\nexplicit-exit-no******\n"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|404 |InvalidSslVpnClientCert.NotFound |The specified SSL client certificate does not exist. |The specified SSL client certificate does not exist. |
