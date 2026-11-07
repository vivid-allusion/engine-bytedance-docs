---
title: "Pre-signed URL with the X-Tos-Policy Query Parameter"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-presigned-url-with-the-x-tos-policy-query-parameter"
---

Typically, pre\-signed URLs grant access to individual objects only. If you want a pre\-signed URL that lists all directories in a bucket and enables querying and downloading objects under the directories, pre\-sign the URL with the query parameter `X-Tos-Policy`. This topic describes how to use a pre\-signed URL to grant access to a batch of objects within a validity period, without configuring the bucket or objects themselves.

<span id="9ee53240"></span>
## **Format of pre\-signed URLs in listing scenarios**

```Plain
https://bucketname.tos-ap-southeast-1.bytepluses.com/
?X-Tos-Algorithm=TOS4-HMAC-SHA256
&X-Tos-Credential=<access-key-id>/<YYYYMMDD>/<region>/tos/request
&X-Tos-Date=20220101T000000Z
&X-Tos-Expires=86400
&X-Tos-Policy=<policy>
&X-Tos-Signature=<signature>
&X-Tos-Security-Token=<security-token>
json
```


<span id="e24437c4"></span>
### **Parameters**


|**Parameter** |**Description** |**Required** |
|---|---|---|
|X\-Tos\-Algorithm |The version and algorithm of the signature. Currently, only TOS4\-HMAC\-SHA256 is supported. |Yes |
|X\-Tos\-Credential |Contains the AK, date, region, and service information in the format of `<access-key-id>/<date>/<region>/tos/request`, where date follows the yyyyMMdd format. |Yes |
|X\-Tos\-Date |The UTC timestamp of the request in the format of yyyyMMddTHHmmssZ. |Yes |
|X\-Tos\-Expires |The validity period of the URL in seconds. The value is an integer between 1 and 604,800 (7 days), that is, the maximum validity period for the signature is 7 days. |Yes |
|X\-Tos\-Policy |The access control policy of the pre\-signed URL for objects in the bucket. The value should be a Base64\-encoded policy. |Yes |
|X\-Tos\-Signature |The calculated signature. |Yes |
|X\-Tos\-Security\-Token |When using the temporary AK/SK for authentication, this header must be present with the SecurityToken as its value. |No |


<span id="00c4d24b"></span>
### **Policy**

The value of the query parameter `X-Tos-Policy` is a JSON text encoded using UTF\-8 and then Base64. It specifies the conditions that must be met for the URL request for validity verification.

Below is a sample policy.

```JSON
{
  "conditions": [
    {"bucket": "examplebucket"}, 
    ["starts-with", "$key", "example"]
  ]
}
```


Below are the "conditions" items supported in the policy.


|**Parameter** |**Type** |**Description** |**Restriction** |
|---|---|---|---|
|bucket |string |Specifies the acceptable bucket name.<br><br>Supported match type: Exact Match. |There must be one and only one. |
|key |string |The object name or prefix of the object name.<br><br>Supported match types: Exact Match, Starts With. |There must be one and can be multiple ones. |


<span id="8db7735b"></span>
###  **"Conditions" match types**


|**Match type** |**Description** |
|---|---|
|Exact Match |The bucket name or object name must exactly match the value declared in "conditions".<br><br>For example, to specify that the key must be "a", set a condition {"key": "a"}, which is equivalent to ["eq", "$key", "a"]. |
|Starts With |The object name must start with the specified value. For example, ["starts\-with", "$key", "user/user1/"] indicates that the object name must start with "user/user1". |
|Match Any Content |To apply no restriction to the object name, use "starts\-with" with an empty value (""). For example, ["starts\-with", "$key", ""] indicates not to check the key. |


Note that if multiple key conditions exist, they are in an "OR" relationship, indicating that a request is considered valid when any condition is hit.

<span id="adee91a8"></span>
## **Signature calculation**

This section describes the difference in signature calculation between using pre\-signed URLs with the X\-Tos\-Policy query parameter and the Authorization header. The only difference lies in the construction of the CanonicalRequest.


* CanonicalRequest contains only CanonicalQueryString and HashedPayload.

* CanonicalQueryString contains only X\-Tos\-Algorithm, X\-Tos\-Credential, X\-Tos\-Date, X\-Tos\-Expires, X\-Tos\-Policy, and X\-Tos\-Security\-Token.

* When using the temporary AK/SK for authentication, X\-Tos\-Security\-Token must be included.

* Use UNSIGNED\-PAYLOAD instead of HashedPayload, as the request content is unknown.


<span id="9f0d4b9d"></span>
### **Sample pre\-signing process**

In bucket "examplebucket", to share all objects with prefixes `abc/` and `aaa/abc/` (under one of the two directories), as well as two specific objects named "exampleobject" and "exampleobject1", create the following policy.

```JSON
{
  "conditions": [
    {"bucket": "examplebucket"}, 
    ["starts-with", "$key", "abc/"]
    ["starts-with", "$key", "aaa/abc/"]
    ["eq", "$key", "exampleobject"]
    ["eq", "$key", "exampleobject1"]
  ]
}
```


Below are the parameters for calculating the signature.


|**Parameter** |**Value** |
|---|---|
|Region |tos\-ap\-southeast\-1 |
|Request time |Sat, 1 Jan 2022 00:00:00 GMT |
|AccessKeyId |testAK |
|SecretAccessKey |testSK |
|Pre\-signed URL validity period |86,400 seconds |


<span id="374894f6"></span>
#### **Policy**

Below is the Base64\- and URL\-encoded JSON policy.

```Plain
eyJjb25kaXRpb25zIjpbeyJidWNrZXQiOiJleGFtcGxlYnVja2V0In0sWyJzdGFydHMtd2l0aCIsIiRrZXkiLCJhYmMvIl0sWyJzdGFydHMtd2l0aCIsIiRrZXkiLCJhYWEvYWJjLyJdLFsiZXEiLCIka2V5IiwiZXhhbXBsZW9iamVjdCJdLFsiZXEiLCIka2V5IiwiZXhhbXBsZW9iamVjdDEi****
```


<span id="d7f9212a"></span>
#### **CanonicalRequest**

```Plain
X-Tos-Algorithm=TOS4-HMAC-SHA256&X-Tos-Credential=testAK%2F20220101%2Fap-southeast-1%2Ftos%2Frequest&X-Tos-Date=20220101T000000Z&X-Tos-Expires=86400&X-Tos-Policy=eyJjb25kaXRpb25zIjpbeyJidWNrZXQiOiJleGFtcGxlYnVja2V0In0sWyJzdGFydHMtd2l0aCIsIiRrZXkiLCJhYmMvIl0sWyJzdGFydHMtd2l0aCIsIiRrZXkiLCJhYWEvYWJjLyJdLFsiZXEiLCIka2V5IiwiZXhhbXBsZW9iamVjdCJdLFsiZXEiLCIka2V5IiwiZXhhbXBsZW9iamVjdDEi****
UNSIGNED-PAYLOAD
```


<span id="65d5a5da"></span>
#### **StringToSign**

```Plain
TOS4-HMAC-SHA256
20220101T000000Z
20220101/ap-southeast-1/tos/request
07f73a178c9313fb228dbac92bef3293cabcb546809e4ae8eefb16c401ba8d60
```


<span id="7f25cde3"></span>
#### **SigningKey**

```Plain
HMAC-SHA256(HMAC-SHA256(HMAC-SHA256(HMAC-SHA256("testSK", "20220101"), "ap-southeast-1"), "tos"), "request")
```


<span id="ff7d270e"></span>
#### **Signature**

```Plain
b9a2a01cdaff37247fcdab58717ab20a35b338138a992b1ba0f04df9dd807ba7
```


<span id="7351001e"></span>
## **Generating the request URL**

<span id="be210530"></span>
### **URL generation method**

Concatenate the signature calculated above with CanonicalQueryString to yield the signature query parameters used to generate the URLs for ListObjects, ListObjectVersions, HeadObject, and GetObject methods. Using the signature query parameters, you can generate the respective URLs. The signature query parameters are as follows.

```Plain
X-Tos-Algorithm=TOS4-HMAC-SHA256&X-Tos-Credential=testAK%2F20220101%2Fap-southeast-1%2Ftos%2Frequest&X-Tos-Date=20220101T000000Z&X-Tos-Expires=86400&X-Tos-Policy=eyJjb25kaXRpb25zIjpbeyJidWNrZXQiOiJleGFtcGxlYnVja2V0In0sWyJzdGFydHMtd2l0aCIsIiRrZXkiLCJhYmMvIl0sWyJzdGFydHMtd2l0aCIsIiRrZXkiLCJhYWEvYWJjLyJdLFsiZXEiLCIka2V5IiwiZXhhbXBsZW9iamVjdCJdLFsiZXEiLCIka2V5IiwiZXhhbXBsZW9iamVjdDEiXV19&X-Tos-Signature=b9a2a01cdaff37247fcdab58717ab20a35b338138a992b1ba0f04df9dd80****
```


Concatenate the BucketName, EndPoint, Path, signature query parameters, and additional query parameters in the following manner to generate the request URL. For object listing, leave ObjectKey empty. For object querying and acquisition, ObjectKey is the object name. Additional query parameters are used to control the behavior of the method and explained in the next section.

```Plain
https://{BucketName}.{Endpoint}/{ObjectKey}?{ signature query parameters}&{Additional query parameter}
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">During URL generation, there is no strict requirement for the order of query parameters. In the above example, the signature query parameters are placed before additional query parameters for illustrative purposes only.</div>


<span id="8d5ea82b"></span>
### **Sample URL generation**

Note:


* examplebucket is the bucket name in the policy.

* tos\-ap\-southeast\-1.bytepluses.com is the endpoint and corresponds to the ap\-southeast\-1 region involved in signature calculation.


<span id="a9900a30"></span>
#### **Listing objects**

Using signature query parameters, you can list all objects with the prefix `abc/abc/` among the shared objects. Specifically, add the query parameter `prefix=abc/abc/` to obtain the URL below, and then send a GET request to the URL.

```Plain
https://examplebucket.tos-ap-southeast-1.bytepluses.com/?X-Tos-Algorithm=TOS4-HMAC-SHA256&X-Tos-Credential=testAK%2F20220101%2Fap-southeast-1%2Ftos%2Frequest&X-Tos-Date=20220101T000000Z&X-Tos-Expires=86400&X-Tos-Policy=eyJjb25kaXRpb25zIjpbeyJidWNrZXQiOiJleGFtcGxlYnVja2V0In0sWyJzdGFydHMtd2l0aCIsIiRrZXkiLCJhYmMvIl0sWyJzdGFydHMtd2l0aCIsIiRrZXkiLCJhYWEvYWJjLyJdLFsiZXEiLCIka2V5IiwiZXhhbXBsZW9iamVjdCJdLFsiZXEiLCIka2V5IiwiZXhhbXBsZW9iamVjdDEiXV19&X-Tos-Signature=b9a2a01cdaff37247fcdab58717ab20a35b338138a992b1ba0f04df9dd807ba7&prefix=abc
```


**Additional query parameters**

Additional query parameters can be used to control the behavior of the request. For example, a request carrying the "prefix=abc/abc/" query parameter lists objects with the prefix "abc/abc/"; a request carrying the "versions" parameter lists multiversion objects. For more parameters, see the **Request parameters and headers** section in [ListObjects](https://docs.byteplus.com/en/tos/reference/listobjects) and [ListObjectsVersions](https://docs.byteplus.com/en/tos/reference/listobjectversions).

<span id="0a700b43"></span>
#### **Querying/Getting an object**

The URL for querying and getting an object is the same. Sending a HEAD request to the URL queries the information about that object, while sending a GET request gets the object.

The following URL queries/gets version 123 of object "exampleobject" in bucket "examplebucket":

```Plain
https://examplebucket.tos-ap-southeast-1.bytepluses.com/exampleobject?X-Tos-Algorithm=TOS4-HMAC-SHA256&X-Tos-Credential=testAK%2F20220101%2Fap-southeast-1%2Ftos%2Frequest&X-Tos-Date=20220101T000000Z&X-Tos-Expires=86400&X-Tos-Policy=eyJjb25kaXRpb25zIjpbeyJidWNrZXQiOiJleGFtcGxlYnVja2V0In0sWyJzdGFydHMtd2l0aCIsIiRrZXkiLCJhYmMvIl0sWyJzdGFydHMtd2l0aCIsIiRrZXkiLCJhYWEvYWJjLyJdLFsiZXEiLCIka2V5IiwiZXhhbXBsZW9iamVjdCJdLFsiZXEiLCIka2V5IiwiZXhhbXBsZW9iamVjdDEiXV19&X-Tos-Signature=b9a2a01cdaff37247fcdab58717ab20a35b338138a992b1ba0f04df9dd807ba7&versionId=123
```


Here, "examplebucket" is the bucket name in the policy, and "exampleobject" is the name of the object to query/get.

**Additional query parameters**

They can be used to control the behavior of the request. For more information, see the **Request parameters and headers** section in [HeadObject](https://docs.byteplus.com/en/tos/reference/headobject) and [GetObject](https://docs.byteplus.com/en/docs/tos/reference--getobject).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You can control the behavior of a HeadObject or GetObject request by carrying relevant headers in the request URL.</div>


TOS supports uploading objects to TOS through POST requests directly from a browser. To do so, you need to include signature information in the form.
