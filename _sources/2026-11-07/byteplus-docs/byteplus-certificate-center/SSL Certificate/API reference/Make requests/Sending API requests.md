---
title: "Sending API requests"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/reference-send-api-requests"
---

This document describes how to call the BytePlus Certificate Center API.

Before sending API requests, you need to understand the following:

* [Request structure](https://docs.byteplus.com/en/docs/29/8616#request-structure)

* [Common parameters](https://docs.byteplus.com/en/docs/29/8616#common-parameters)

* [Request authentication](https://docs.byteplus.com/en/docs/29/8616#request-authentication)

* [Signature calculation method](https://docs.byteplus.com/en/docs/29/8616#signature-calculation-method)

## Request structure

The structure of an API request includes the following:

* API service address.

* Communication protocol.

* Request method.

* Request parameters.

### API service address

The API service address for the BytePlus Certificate Center is `open.byteplusapi.com`.

### Communication protocol

You can use either the `HTTP` or `HTTPS` protocol to send requests. It is recommended to use the `HTTPS` protocol for higher security.

### Request method

Unless otherwise specified, use the `POST` method to send requests. Additionally, you must specify `Content-Type: application/json` in the request header.

### Request parameters

Request parameters include common parameters and parameters specific to each API.

## Common parameters

Common parameters are required for every API request. If a common parameter is missing in an API request, the request will fail.

The following table lists the common parameters that must be included in the request header.

|Parameter name |Data type |Required |Description |
|---|---|---|---|
|Region |String |Yes |Service region. The value of this parameter is `ap-singapore-1`. |
|ServiceName |String |Yes |Service name. The value of this parameter is `certificate_service`. |

The following table lists the common parameters that must be included in the query string.

|Parameter name |Data type |Required |Description |Example |
|---|---|---|---|---|
|Action |string |Yes |Represents the API name. The name follows the regular expression format [a\-zA\-Z]+. |`UploadCertificate` |
|Version |string |Yes |Represents the API version. The value of this parameter is `2024-10-01`. |`2024-10-01` |
|X\-Expires |int |No |Represents the validity period of the signature included in the authentication information, in seconds. The default value is `900`. |`900` |

## Request authentication

Every request must include authentication information to verify the identity of the requester. You can provide authentication information using either of the following methods. Method 1 is recommended.

### (Recommended) Method 1: Include authentication information in the request header

You need to include the following parameters in the request header:

|Parameter name |Data type |Required |Description |Example |
|---|---|---|---|---|
|X\-Date |string |Yes |Represents the time of signature calculation in UTC. The time precision is in seconds. Regarding this parameter, please note the following:<br><br><br>* When the request arrives, BytePlus Certificate Center calculates the difference between the arrival time and X\-Date. If the difference exceeds the time range specified by X\-Expires, BytePlus Certificate Center considers the request invalid. Therefore, it is recommended to calibrate the system time before calculating the signature. |`20210913T081805Z` |
|Authorization |string |Yes |This parameter represents the authentication string. The pseudocode for this parameter is as follows:<br><br>`HMAC-SHA256 Credential = {AccessKey}/{ShortDate}/{Region}/{Service}/{Request}, SignedHeaders={SignedHeaders}, Signature={Signature}`<br><br>The explanation of this pseudocode is as follows:<br><br><br>* The `Signature` parameter in the pseudocode represents a calculated signature. For the calculation method of the signature, refer to [Signature calculation method](https://docs.byteplus.com/en/docs/29/8616#signature-calculation-method).<br><br>* For the explanation of other parameters in the pseudocode, refer to [Pseudo code parameter explanation](https://docs.byteplus.com/en/docs/29/8616#pseudo-code-parameter-explanation). | |

### Method 2: Including authentication information in the query string

You need to include the following query parameters in the query string.

|Parameter name |Data type |Parameter description |Example |
|---|---|---|---|
|X\-Date |string |Represents the time of signature calculation in UTC. The time precision is in seconds. Regarding this parameter, please note the following:<br><br><br>* When the request arrives, BytePlus Certificate Center calculates the time difference between the request arrival time and `X-Date`. If the difference exceeds the time range specified by `X-Expires`, BytePlus Certificate Center considers the request invalid. Therefore, it is recommended to calibrate the system time before calculating the signature. |`20210913T081805Z` |
|X\-Algorithm |string |Represents the algorithm used for signature calculation. The value of this parameter is `HMAC-SHA256`. |`HMAC-SHA256` |
|X\-Credential |string |The pseudocode for the parameter value is as follows:<br><br>`{AccessKey}/{ShortDate}/{Region}/{Service}/{Request}`<br><br>For the explanation of the parameters in the pseudocode of `X-Credential`, refer to [Pseudo code parameter explanation](https://docs.byteplus.com/en/docs/29/8616#pseudo-code-parameter-explanation). |`AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZkYzE/20210913/singapore/certificate_service/request` |
|X\-SignedHeaders |string |The explanation of this parameter is the same as the `SignedHeaders` parameter in the [Pseudo code parameter explanation](https://docs.byteplus.com/en/docs/29/8616#pseudo-code-parameter-explanation). |`host;x-content-sha256;x-date` |
|X\-Signature |string |Represents a calculated signature. For the calculation method of the signature, refer to [Signature calculation method](https://docs.byteplus.com/en/docs/29/8616#signature-calculation-method). | |

## Signature calculation method

This section mainly describes how the signature is calculated. The [Pseudo code parameter explanation](https://docs.byteplus.com/en/docs/29/8616#pseudo-code-parameter-explanation) is provided at the end of the document.

* The `HMAC` method used in the pseudo code in this section uses the HMAC\-SHA256 algorithm.

* The `HexEncode` method used in the pseudo code in this section converts a string to a string in hexadecimal encoding format.

The signature parameter `Signature` is calculated based on the `kSigning` and `StringToSign` parameters. The pseudo code for `Signature` is as follows:

```SQL
Signature = HexEncode(HMAC(kSigning, StringToSign))
```

### kSigning

`kSigning` represents the key used to calculate the signature. To calculate `kSigning`, you must first [obtain the secret access key of your account](https://console.byteplus.com/iam/keymanage), and then use the following pseudo code to generate `kSigning`.

```SQL
kSecret = <Your secret access key>
kDate = HMAC(kSecret, ShortDate)
kRegion = HMAC(kDate, Region)
kService = HMAC(kRegion, Service)
kSigning = HMAC(kService, "request")
```

For the explanation of the parameters in the pseudo code of `kSigning`, see [Pseudo code parameter explanation](https://docs.byteplus.com/en/docs/29/8616#pseudo-code-parameter-explanation).

### StringToSign

`StringToSign` represents the signature string used to calculate the signature. The pseudo code for `StringToSign` is as follows:

```SQL
// The Hash function uses the SHA256 algorithm
StringToSign = Algorithm + '\n' + RequestDate + '\n' + CredentialScope + '\n' + HexEncode(Hash(CanonicalRequest))
```

For the explanation of the `Algorithm` and `RequestDate` parameters in the pseudo code of `StringToSign`, see the explanation of the parameters in the pseudo code. The explanation of other parameters in the pseudo code of `StringToSign` is as follows.

**CredentialScope**

`CredentialScope` represents the scope of the credentials. The pseudo code for `CredentialScope` is as follows:

```SQL
{ShortDate}/{Region}/{Service}/{Request}
```

For the explanation of the parameters in the pseudo code of `CredentialScope`, see [Pseudo code parameter explanation](https://docs.byteplus.com/en/docs/29/8616#pseudo-code-parameter-explanation).

**CanonicalRequest**

`CanonicalRequest` represents the canonical request. The pseudo code for `CanonicalRequest` is as follows:

```SQL
HTTPRequestMethod + '\n' + CanonicalURI + '\n' + CanonicalQueryString + '\n' + CanonicalHeaders + '\n' + SignedHeaders + '\n' + HexEncode(Hash(RequestPayload))
```

The explanation of the parameters in the pseudo code of `CanonicalRequest` is as follows:

* `HTTPRequestMethod`: Represents the request method. For BytePlus Certificate Center, the value of this parameter is `POST`.

* `CanonicalURI`: Represents the URI of the request.

* `CanonicalQueryString`: Represents the canonical query string. The value of `CanonicalQueryString` is generated according to the following rules:

   * Sort the query parameters in ascending order by parameter name.

* `CanonicalHeaders`: Represents the canonical request headers. `CanonicalHeaders` is generated through the following steps:

   * Convert the names of the request header parameters involved in signature calculation to lowercase letters.

   * Sort these names in ascending order at the character level.

   * Concatenate these request header parameters in the key\-value format. The key is the name of the request header parameter, and the value is the value of the request header parameter.

   * Add a line break (`\n`) after each request header parameter.

* `SignedHeaders`: See Pseudo code parameter explanation.

* `HexEncode(Hash(RequestPayload))`: Represents a calculated value. This value is obtained by applying the SHA256 hash algorithm to the value of the `payload` in the request body.

## Pseudo code parameter explanation

The following table contains explanations of the parameters used in the pseudo code in this document.

|Parameter name |Data type |Parameter description |Example |
|---|---|---|---|
|AccessKey |string |Represents the Access Key ID of your account. Refer to [Get Access Key](https://console.byteplus.com/iam/keymanage). |`AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZkYzE` |
|RequestDate |string |This parameter is the same as the definition of `X-Date` in the Request Authentication section. |`20210913T081805Z` |
|ShortDate |string |This parameter is the same as the definition of `RequestDate`, but with a daily time precision. |`20210913` |
|Region |string |Represents the region where BytePlus Certificate Center service is located. The value of this parameter is `ap-singapore-1`. |`ap-singapore-1` |
|Service |string |Represents the service name of BytePlus Certificate Center. The value of this parameter is `certificate_service`. |`certificate_service` |
|SignedHeaders |string |Represents the request header parameters involved in the signature calculation. Multiple request header parameters are separated by semicolons (;). These request header parameters are sorted in ascending order based on the parameter name.<br><br>In general, the value of `SignedHeaders` is `host;x-content-sha256;x-date`. You can also specify any request header parameter as the value of `SignedHeaders`. |`host;x-content-sha256;x-date` |
|Algorithm |string |Represents the algorithm used for the signature calculation. The value of this parameter is `HMAC-SHA256`. |`HMAC-SHA256` |
|Request |string |This parameter is a constant with the value `request`. |`request` |

## Request example

```http
POST https://open.byteplusapi.com/?Action=ImportCertificate&Version=2024-10-01

// Request Headers
X-Date: 20230922T073702Z
Authorization: HMAC-SHA256 Credential=AKLTMjYxYTZmYWU4ZWYzNGI2NDg8NTUxODE1ZGVhNmIxZmQ/20230922/ap-singapore-1/certificate_service/request, SignedHeaders=x-content-sha256;x-date, Signature=5a394ce80456c7cdf989c28bd638807c8ead386eb15dd36e39952f405380aef2
Content-Type: application/json
ServiceName: certificate_service
Region: ap-singapore-1
```
