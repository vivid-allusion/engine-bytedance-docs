---
title: "Browser-based uploads using HTTP POST"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-browser-based-upload-forms-include-signatures"
---

TOS supports browser\-based uploads using HTTP POST, allowing you to upload content directly to TOS. When uploading objects using POST, you need to add signature information to the form.

<span id="a306bd55"></span>
## **Signing procedure**

To derive the signature for the form, do the following.


1. You must include the following fields in the form to provide the signature and relevant information, which can then be used by TOS to verify the signature of the received request.

   
   |**Element** |**Description** |**Required** |
   |---|---|---|
   |policy |A Base64\-encoded security policy that specifies the restrictions for a POST request. For signature calculation, this is the StringToSign. |Yes |
   |x\-tos\-algorithm |The signing algorithm. Currently, only the HMAC\-SHA256 algorithm is supported. |Yes |
   |x\-tos\-credential |Contains the AK, date, region, and service information in the format of <`access-key-id>/<date>/<region>/tos/request`, where follows the yyyyMMdd format. |Yes |
   |x\-tos\-date |The UTC timestamp of the request in the format of yyyyMMddTHHmmssZ. |Yes |
   |x\-tos\-signature |The calculated signature. |Yes |
   |x\-tos\-security\-token |When using the temporary AK/SK for authentication, this field must be present with the SecurityToken as its value. |No |
   

2. You must include the following elements in the policy.

   
   |**Element** |**Description** |
   |---|---|
   |x\-tos\-algorithm |The signing algorithm. Currently, only the HMAC\-SHA256 algorithm is supported. |
   |x\-tos\-credential |Contains the AK, date, region, and service information in the format of `<access-key-id>/<date>/<region>/tos/request`, where follows the yyyyMMdd format. |
   |x\-tos\-date |The UTC timestamp of the request in the format of yyyyMMddTHHmmssZ. |
   

3. Calculate the signature of the form, using the policy as the StringToSign.


<span id="c7fbf772"></span>
## **Calculating the signature**


1. Encode the policy in UTF\-8.

2. Encode the UTF\-8 text in Base64 to obtain the StringToSign.

3. Perform HMAC\-SHA256 calculation on the StringToSign using the SigningKey.

4. Convert the result to hexadecimal encoding.

   ```Plain
   StringToSign = Base64(UTF-8-Encoding-Of(policy))
   Signature = HexEncode(HMAC-SHA256(SigningKey, StringToSign))
   ```
   


<span id="cd245a46"></span>
## **POST policy**

The policy form field of the POST request is a JSON text encoded using UTF\-8 and then Base64. It specifies the conditions that must be met for the request for validity verification. While the policy form field is optional for upload to publicly writable buckets, we strongly recommend that you use it to control the allowed content in the request.

Below is a sample POST policy:

```Plain
{
  "expiration": "2022-01-01T12:00:00.000Z",
  "conditions": [
    {"bucket": "examplebucket" },    
    ["eq", "$acl", "public-read"],
    ["starts-with", "$key", "example"]
  ]
}
```


A POST policy must have `expiration` and `conditions` specified.

<span id="89217987"></span>
### **Expiration**

The `expiration` property specifies the expiration time of the policy, in ISO 8601 GMT time. For example, `2022-01-01T12:00:00.000Z` indicates that the request must be made before 12:00 on 1 January 2022.

<span id="92226040"></span>
### **Conditions**

The `conditions` property in the POST policy is an array of objects, each of which is used to validate the request. You can specify conditions to limit the allowed content in the request. For example, in the above sample policy:


* The request must specify the bucket name `examplebucket`.

* The object key must be prefixed with `example`.

* The object ACL must be set to `public-read`.


Every field specified in the form (except for `x-tos-signature`, `file`, `policy`, and fields with names prefixed with `x-ignore-`) must appear in the condition list.

Below are the "conditions" items supported in the policy.


|**Name** |**Type** |**Description** |
|---|---|---|
|x\-tos\-acl |String |Specifies the ACL value that must be used in the submitted form.<br><br>Supported match types: Exact Match, Starts With. |
|x\-tos\-tagging |String |Specifies the collection of tags to be added to the object.<br><br>Supported match types: Exact Match, Starts With. |
|bucket |String |Specifies the acceptable bucket name.<br><br>Supported match type: Exact Match. |
|content\-length\-range |Integer Array |Specifies the minimum and maximum sizes of the uploaded content.<br><br>Supported match type: Specifying Ranges. |
|Cache\-Control<br><br>Content\-Type<br><br>Content\-Disposition<br><br>Content\-Encoding<br><br>Expires |String |Standard HTTP headers.<br><br>Supported match types: Exact Match, Starts With. |
|key |String |The object name or prefix of the object name.<br><br>Supported match types: Exact Match, Starts With. |
|success_action_redirect |String |The URL to which the client is redirected upon successful upload.<br><br>Supported match types: Exact Match, Starts With. |
|success_action_status |Integer |The status code returned to the client upon successful upload, if `success_action_redirect` is not specified.<br><br>Supported match type: Exact Match. |
|x\-tos\-algorithm |String |The algorithm that must be used for signature calculation. For TOS V4 signatures, the value is TOS4\-HMAC\-SHA256.<br><br>Supported match type: Exact Match. |
|x\-tos\-credential |String |The scope information used to derive the SigningKey during signature calculation, besides the AK.<br><br>Supported match type: Exact Match. |
|x\-tos\-date |String |The date in ISO 8601 format. For example, 20130728T000000Z.<br><br>This must be the same as the SigningKey creation date. It must also be the same value as the `x-tos-date` specified in the form field<br><br>Supported match type: Exact Match. |
|x\-tos\-security\-token |String |If STS temporary authorization is used, this value must be the same as the `SecurityToken` value, and a paired AK must be used.<br><br>Supported match type: Exact Match. |
|x\-tos\-meta\-\* |String |User\-defined metadata.<br><br>Supported match types: Exact Match, Starts With. |
|x\-tos\-\* |String |Supported match types: Exact Match, Starts With. |
|Content\-MD5 |String |The MD5 hash of the uploaded file.<br><br>Supported match types: Exact Match, Starts With. |


If your toolkit adds more form fields (for example, Flash adds `filename`), you must add them to the POST policy. If you can control this feature, prefix this field with `x-ignore-`.

<span id="a4216b8e"></span>
###  **"Conditions" match types**


| **"Conditions" match types** ||
|---|---|
|Exact Match |The value of a form field must exactly match the value specified in "conditions". For example, to specify that the "key" must be "a", set a condition {"key": "a"}, which is equivalent to ["eq", "$key", "a"]. |
|Starts With |The value must start with the specified value. For example, ["starts\-with", "$key", "user/user1/"] indicates that the object name must start with `user/user1`. |
|Match Any Content |To configure the policy to allow any content in a field, use `starts-with` with an empty value (""). The following example allows any content in `success_action_redirect`:<br><br>["starts\-with", "$success_action_redirect", ""] |
|Specifying Range |For fields with a value range, separate the upper and lower limits with a comma (,). The following example allows a file size from 1 to 10 MiB:<br><br>```Plain```<br>```["content-length-range", 1048576, 10485760]```<br> |


<span id="5ae54cc0"></span>
## **Sample case**

This section describes how to upload object `exampleobject` to bucket `examplebucket` and set the object ACL to public\-read. Below are the parameters.


|**Parameter** |**Value** |
|---|---|
|Bucket name |examplebucket |
|Object name |exampleobject |
|Region |ap\-southeast\-1 |
|Time |Sat, 1 Jan 2022 00:00:00 GMT |
|AccessKeyId |testAK |
|SecretAccessKey |testSK |


<span id="00812e59"></span>
### **Creating the policy**

```Plain
{
        "expiration": "2022-01-05T00:00:00.000Z",
        "conditions": [
        {"bucket": "examplebucket"},
        ["starts-with", "$key", "example"], 
        {"acl": "public-read"}, 
        {"success_action_redirect": "http://examplebucket.tos-ap-southeast-1.bytepluses.com/successful_upload.html"},
        ["starts-with", "$Content-Type", "image/"], 
        ["starts-with", "$x-tos-meta-tag", ""], 
        
        {"x-tos-server-side-encryption": "AES256"}, 
        {"x-tos-credential": "testAK/20220101/ap-southeast-1/tos/request"}, 
        {"x-tos-algorithm": "TOS4-HMAC-SHA256"}, 
        {"x-tos-date": "20220101T000000Z"}
        ]
}
```


This POST policy sets the following conditions on the request:


* Upload must take place before 00:00 on 5 January 2022.

* The object can only be uploaded to bucket `examplebucket`, which must be within the region you specified in the credential scope (the `x-tos-credential` form parameter), as the signature you provided is valid only within this scope.

* Any object with a name starting with `example` (like `exampleobject`) can be uploaded.

* The ACL must be set to `public-read`.

* If the upload is successful, the browser will be redirected to `http://examplebucket.tos-ap-southeast-1.bytepluses.com/successful_upload.html`.

* The uploaded object must be an `image` file.

* `x-tos-meta-tag` can contain any value.

* `x-tos-server-side-encryption` must be set to `AES256`.


Below is the Base64\-encoded version of this POST policy, which is used as the StringToSign in signature calculation.

```Plain
ewogICAgICAgICJleHBpcmF0aW9uIjogIjIwMjItMDEtMDVUMDA6MDA6MDAuMDAwWiIsCiAgICAgICAgImNvbmRpdGlvbnMiOiBbCiAgICAgICAgeyJidWNrZXQiOiAiZXhhbXBsZWJ1Y2tldCJ9LAogICAgICAgIFsic3RhcnRzLXdpdGgiLCAiJGtleSIsICJleGFtcGxlIl0sIAogICAgICAgIHsiYWNsIjogInB1YmxpYy1yZWFkIn0sIAogICAgICAgIHsic3VjY2Vzc19hY3Rpb25fcmVkaXJlY3QiOiAiaHR0cDovL2V4YW1wbGVidWNrZXQudG9zLWNuLWJlaWppbmcudm9sY2VzLmNvbS9zdWNjZXNzZnVsX3VwbG9hZC5odG1sIn0sCiAgICAgICAgWyJzdGFydHMtd2l0aCIsICIkQ29udGVudC1UeXBlIiwgImltYWdlLyJdLCAKICAgICAgICBbInN0YXJ0cy13aXRoIiwgIiR4LXRvcy1tZXRhLXRhZyIsICIiXSwgCiAgICAgICAgCiAgICAgICAgeyJ4LXRvcy1zZXJ2ZXItc2lkZS1lbmNyeXB0aW9uIjogIkFFUzI1NiJ9LCAKICAgICAgICB7IngtdG9zLWNyZWRlbnRpYWwiOiAidGVzdEFLLzIwMjIwMTAxL2NuLWJlaWppbmcvdG9zL3JlcXVlc3QifSwgCiAgICAgICAgeyJ4LXRvcy1hbGdvcml0aG0iOiAiVE9TNC1ITUFDLVNIQTI1NiJ9LCAKICAgICAgICB7IngtdG9zLWRhdGUiOiAiMjAyMjAxMDFUMDAwMDAwWiJ9CiAgICAgICAgXQp9
```


<span id="6693651e"></span>
### **SigningKey**

```Plain
HMAC-SHA256(HMAC-SHA256(HMAC-SHA256(HMAC-SHA256("testSK", "20220101"), "ap-southeast-1"), "tos"), "request")
```


<span id="ff1bba08"></span>
### **Signature**

```Plain
94d72cb3bbd094f6d8eaa0b7e56905500029813febc9fee352474f88d093c3e5
```


<span id="64285e9f"></span>
### **POST request**

```Plain
POST / HTTP/1.1
Host: examplebucket.tos-ap-southeast-1.bytepluses.com
Accept-Encoding: encoding
Accept-Charset: character_set
Keep-Alive: 300
Connection: keep-alive
Content-Type: multipart/form-data; boundary=9431149156168
Content-Length: length

--9431149156168
Content-Disposition: form-data; name="key"

exampleobject
--9431149156168
Content-Disposition: form-data; name="success_action_redirect"

http://examplebucket.tos-ap-southeast-1.bytepluses.com/successful_upload.html
--9431149156168
Content-Disposition: form-data; name="x-tos-meta-tag"

metadata
--9431149156168
Content-Disposition: form-data; name="Content-Type"

image/jpg
--9431149156168
Content-Disposition: form-data; name="x-tos-server-side-encryption"

AES256
--9431149156168
Content-Disposition: form-data; name="x-tos-algorithm"

TOS4-HMAC-SHA256
--9431149156168
Content-Disposition: form-data; name="x-tos-date"

20220101T000000Z
--9431149156168
Content-Disposition: form-data; name="x-tos-credential"

testAK/20220101/ap-southeast-1/tos/request
--9431149156168
Content-Disposition: form-data; name="policy"

ewogICAgICAgICJleHBpcmF0aW9uIjogIjIwMjItMDEtMDVUMDA6MDA6MDAuMDAwWiIsCiAgICAgICAgImNvbmRpdGlvbnMiOiBbCiAgICAgICAgeyJidWNrZXQiOiAiZXhhbXBsZWJ1Y2tldCJ9LAogICAgICAgIFsic3RhcnRzLXdpdGgiLCAiJGtleSIsICJleGFtcGxlIl0sIAogICAgICAgIHsiYWNsIjogInB1YmxpYy1yZWFkIn0sIAogICAgICAgIHsic3VjY2Vzc19hY3Rpb25fcmVkaXJlY3QiOiAiaHR0cDovL2V4YW1wbGVidWNrZXQudG9zLWNuLWJlaWppbmcudm9sY2VzLmNvbS9zdWNjZXNzZnVsX3VwbG9hZC5odG1sIn0sCiAgICAgICAgWyJzdGFydHMtd2l0aCIsICIkQ29udGVudC1UeXBlIiwgImltYWdlLyJdLCAKICAgICAgICBbInN0YXJ0cy13aXRoIiwgIiR4LXRvcy1tZXRhLXRhZyIsICIiXSwgCiAgICAgICAgCiAgICAgICAgeyJ4LXRvcy1zZXJ2ZXItc2lkZS1lbmNyeXB0aW9uIjogIkFFUzI1NiJ9LCAKICAgICAgICB7IngtdG9zLWNyZWRlbnRpYWwiOiAidGVzdEFLLzIwMjIwMTAxL2NuLWJlaWppbmcvdG9zL3JlcXVlc3QifSwgCiAgICAgICAgeyJ4LXRvcy1hbGdvcml0aG0iOiAiVE9TNC1ITUFDLVNIQTI1NiJ9LCAKICAgICAgICB7IngtdG9zLWRhdGUiOiAiMjAyMjAxMDFUMDAwMDAwWiJ9CiAgICAgICAgXQp9
--9431149156168
Content-Disposition: form-data;f name="x-tos-signature"

94d72cb3bbd094f6d8eaa0b7e56905500029813febc9fee352474f88d093c3e5
--9431149156168
Content-Disposition: form-data; name="file"; filename="MyFile.jpg"
Content-Type: image/jpeg

file_content
--9431149156168
Content-Disposition: form-data; name="submit"

Upload to TOS
--9431149156168--
```
