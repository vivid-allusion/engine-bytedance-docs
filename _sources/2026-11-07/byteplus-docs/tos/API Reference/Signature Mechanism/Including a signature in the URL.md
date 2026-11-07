---
title: "Including a signature in the URL"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-including-a-signature-in-the-url"
---

You can add signature information to query parameters in a URL. Such a URL carries information such as the AK, validity period, target resource, operation, and signature. Anyone who uses the URL can perform the indicated operation within the validity period. This method is called presigning.

<span id="21689636"></span>
## **Presigned URL format**

```Plain
https://bucketname.tos-ap-southeast-1.bytepluses.com/object
?X-Tos-Algorithm=TOS4-HMAC-SHA256
&X-Tos-Credential=<access-key-id>/<YYYYMMDD>/<region>/tos/request
&X-Tos-Date=20130721T201207Z
&X-Tos-Expires=86400
&X-Tos-SignedHeaders=host
&X-Tos-Signature=<signature> 
&X-Tos-Security-Token=<security-token>
```


<span id="71b63760"></span>
## **Parameters**


|**Parameter** |**Description** |**Required** |
|---|---|---|
|X\-Tos\-Algorithm |The version and algorithm of the signature. Currently, only TOS4\-HMAC\-SHA256 is supported. |Yes |
|X\-Tos\-Credential |Contains the AK, date, region, and service informationin the format of `<access-key-id>/<date>/<region>/tos/request`, wherefollows the `yyyyMMdd` format. |Yes |
|X\-Tos\-Date |The UTC timestamp of the request in the format of `yyyyMMddTHHmmssZ`. |Yes |
|X\-Tos\-Expires |The validity period of the URL in seconds. The value is an integer between 1 and 604,800 (7 days), that is, the maximum validity period for the signature is 7 days. |Yes |
|X\-Tos\-SignedHeaders |Lists the headers involved in signature calculation, with the following restraints:<br><br><br>* The host header must be included.<br><br>* All `x-tos-\*` headers must be included. |Yes |
|X\-Tos\-Signature |The calculated signature. | |
|X\-Tos\-Security\-Token |When using the temporary AK/SK for authentication, this header must be present with the SecurityToken as its value. |No |


<span id="13bd3f83"></span>
## **Signature calculation**

The calculation of URL signatures and that of header signatures differ only in constructing the CanonicalRequest.


* When creating a presigned URL, you need to use UNSIGNED\-PAYLOAD instead of HashedPayload, as the request content is unknown.

* `X-Tos-Signature` is not included in CanonicalQueryString.

* When using the temporary AK/SK for authentication, `X-Tos-Security-Token` must be included.


<span id="6c96ad57"></span>
## **Sample presigned URL**

In this example, an object is downloaded from TOS. The relevant information is as follows.


|**Parameter** |**Value** |
|---|---|
|Bucket name |examplebucket |
|Object name |exampleobject |
|Region |tos\-ap\-southeast\-1 |
|Time |Sat, 1 Jan 2022 00:00:00 GMT |
|AccessKeyId |testAK |
|SecretAccessKey |testSK |


<span id="0546c3ef"></span>
### **CanonicalRequest**

```Plain
GET
/exampleobject
X-Tos-Algorithm=TOS4-HMAC-SHA256&X-Tos-Credential=testAK%2F20220101%2Fap-southeast-1%2Ftos%2Frequest&X-Tos-Date=20220101T000000Z&X-Tos-Expires=86400&X-Tos-SignedHeaders=host
host:examplebucket.tos-ap-southeast-1.bytepluses.com

host
UNSIGNED-PAYLOAD
```


<span id="64a6fa47"></span>
### **StringToSign**

```Plain
TOS4-HMAC-SHA256
20220101T000000Z
20220101/ap-southeast-1/tos/request
b0cda3030fc2db31d57af22c2a7ab4229434edff63f0982db8a3fb99b190677d
```


<span id="501f6c63"></span>
### **SigningKey**

```Plain
HMAC-SHA256(HMAC-SHA256(HMAC-SHA256(HMAC-SHA256("testSK", "20220101"), "ap-southeast-1"), "tos"), "request")
```


<span id="52f3f87b"></span>
### **Signature**

```Plain
353aa55583eceb222aad4bdcb70d4045a202a4af9a3096f25a656b82c8ec2f56
```


<span id="aa805b59"></span>
### **Presigned URL**

```Plain
https://examplebucket.tos-ap-southeast-1.bytepluses.com/exampleobject?X-Tos-Algorithm=TOS4-HMAC-SHA256&X-Tos-Credential=testAK%2F20220101%2Fap-southeast-1%2Ftos%2Frequest&X-Tos-Date=20220101T000000Z&X-Tos-Expires=86400&X-Tos-SignedHeaders=host&X-Tos-Signature=353aa55583eceb222aad4bdcb70d4045a202a4af9a3096f25a656b82c8ec2f56
```
