---
title: "PostObject"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-postobject"
---

<span id="a9ee7175"></span>
## **Introduction**

This API allows for uploading a local file up to 5 GiB into a specified bucket through an HTML form. Calling this API requires write permission for the bucket.

<span id="05d55805"></span>
## **Notes**


* The total size of the form data and boundaries (excluding the `file` content) cannot exceed 20 KiB.

* A request without the "policy" form field is considered anonymous and can work only on a publicly writable bucket.

* When constructing the request, make sure that `file` is the last field in the form (any subsequent fields will be ignored).

* The uploaded object cannot exceed 5 GiB.


<span id="32a0c679"></span>
## **Request syntax**

```JSON
POST / HTTP/1.1
Host: buketname.tos-ap-southeast-1.bytepluses.com
Accept-Encoding: encoding
Accept-Charset: character_set
Keep-Alive: 300
Connection: keep-alive
Content-Type: multipart/form-data; boundary=9431149156168
Content-Length: length
--9431149156168
Content-Disposition: form-data; name="key"
objectname
--9431149156168
Content-Disposition: form-data; name="success_action_redirect"
success_redirect
--9431149156168
Content-Disposition: form-data; name="x-tos-meta-uuid"
uuid
--9431149156168
Content-Disposition: form-data; name="x-tos-meta-tag"
metadata
--9431149156168
Content-Disposition: form-data; name="Content-Disposition"
attachment;filename=download.jpg
--9431149156168
Content-Disposition: form-data; name="x-tos-algorithm"
TOS4-HMAC-SHA256
--9431149156168
Content-Disposition: form-data; name="x-tos-date"
20220411T000000Z
--9431149156168
Content-Disposition: form-data; name="x-tos-credential"
<your-access-key-id>/<date>/<region>/<service>/request
--9431149156168
Content-Disposition: form-data; name="policy"
encoded_policy
--9431149156168
Content-Disposition: form-data; name="x-tos-signature"
signature
--9431149156168
Content-Disposition: form-data; name="file"; filename="MyFilename.jpg"
Content-Type: image/jpeg
file_content
--9431149156168
Content-Disposition: form-data; name="submit"
Upload to TOS
--9431149156168--
```


<span id="c5737713"></span>
## **Request parameters and headers**

No request parameters are used.

<span id="7904fdd1"></span>
## **Request body elements**


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|policy |String |Yes in some cases |eyJleHBpcmF0aW9uIjoiMjAyMi0wMS0wNVQwMDowMDowM C4wMDBaIiwiY29uZGl0aW9ucyI6W3siYnVja2V0IjoiZXhhbXB sZWJ1Y2tldCJ9LFsic3RhcnRzLXdpdGgiLCIka2V5IiwiZXhhbX BsZSJdXX0= |Base64\-encoded security policy describing what is allowed in the request.<br><br>Default value: None<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the bucket does not allow public writing, the request must include the "policy" form field, which, in turn, requires including the signature\-related fields.</div><br> |
|x\-tos\-algorithm |String |Yes in some cases |TOS4\-HMAC\-SHA256 |Signing algorithm used. For TOS, the value is `TOS4-HMAC-SHA256`.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This parameter is required if the request contains a security policy.</div><br> |
|x\-tos\-credential |String |Yes in some cases |testAK/20220101/ap\-southeast\-1/tos/request |Scope information used to derive the SigningKey during signature calculation, besides the AK.<br><br>The format is `<your-access-key-id>/<date>/<region>/tos/request`.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This parameter is required if the request contains a security policy.</div><br> |
|x\-tos\-date |String |Yes in some cases |*20220101T000000Z* |Date in ISO 8601 format. For example, 20130728T000000Z. This must be the same as the date used to derive the SigningKey and the `x-tos-date` specified in the policy.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This parameter is required if the request contains a security policy.</div><br> |
|x\-tos\-signature |String |Yes in some cases |94d72cb3bbd094f6d8eaa0b7e56905500029813febc9fee352474f88d093c3e5 |HMAC\-SHA256 result of the policy and SigningKey.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This parameter is required if the request contains a security policy.</div><br> |
|x\-tos\-acl |String |No |public\-read |Specifies the access permission of the object.<br><br><br>* Default value: private<br><br>* Valid value: private |
|x\-tos\-tagging |String |No |{ "TagSet": { "Tags": [{ "Key": "Tag1", "Value": "Tag1" }, { "Key": "Tag2", "Value": "Tag2" }] } } |Collection of tags to add to the object.<br><br>Default value: None |
|key |String |Yes |exampleobject |Key of the object to upload. |
|file |File |Yes |/ |File or text content, with no encoding needed. The browser will automatically set `Content-Type` based on the file type and override your settings. TOS allows uploading only one file at a time.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When constructing the request, make sure that <code>file</code> is the last field in the form (any subsequent fields will be ignored).</div><br> |
|Cache\-Control |String |No |/ |HTTP standard header. For more information, see [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt?spm=a2c4g.11186623.0.0.6d016ac1feoDjC&file=rfc2616.txt).<br><br>Default value: None |
|Content\-Type |String |No |/ |HTTP standard header. For more information, see [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt?spm=a2c4g.11186623.0.0.6d016ac1feoDjC&file=rfc2616.txt).<br><br>Default value: None |
|Content\-Disposition |String |No |/ |HTTP standard header. For more information, see [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt?spm=a2c4g.11186623.0.0.6d016ac1feoDjC&file=rfc2616.txt).<br><br>Default value: None |
|Content\-Encoding |String |No |/ |HTTP standard header. For more information, see [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt?spm=a2c4g.11186623.0.0.6d016ac1feoDjC&file=rfc2616.txt).<br><br>Default value: None |
|Content\-Language |String |No |/ |HTTP standard header. For more information, see [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt?spm=a2c4g.11186623.0.0.6d016ac1feoDjC&file=rfc2616.txt).<br><br>Default value: None |
|Content\-MD5 |String |No |XrY7u+Ae7tCTyyK7j1rNww== |Base64\-encoded MD5 digest of the message body. |
|Expires |String |No |/ |HTTP standard header. For more information, see [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt?spm=a2c4g.11186623.0.0.6d016ac1feoDjC&file=rfc2616.txt).<br><br>Default value: None |
|success_action_redirect |String |No |http://examplebucket.tos\-ap\-southeast\-1.bytepluses.com/successful_upload.html |URL to which the client is redirected upon successful upload. If the form field is not specified, the returned result is defined by the `success_action_status` form field. If the upload fails, an error code is returned and no redirection is performed.<br><br>Default value: None |
|success_action_status |Integer |No |201 |Status code returned to the client upon successful upload, if `success_action_redirect` is not specified.<br><br><br>* Default value: 204<br><br>* Valid values: 200, 201, and 204<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If this field is set to 200 or 204, TOS returns an empty document and the corresponding status code.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If this field is set to 201, TOS returns a JSON document and a 201 status code. If this field is unset or set to an invalid value, TOS returns an empty document and a 204 status code.</div><br> |
|x\-tos\-storage\-class |String |No |STANDARD |Specifies the storage type of the object. The object will inherit the default storage type of the bucket if this field is unset.For detailed information, please refer to [Storage type](https://docs.byteplus.com/docs/tos/docs-storage-type). |
|x\-tos\-meta\-\* |String |No |x\-tos\-meta\-tag:image |`User meta` value you specified.<br><br>Default value: None<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Use form fields prefixed with <code>x-tos-meta-</code> (for example, <code>x-tos-meta-location</code>) in the request to specify <code>user meta</code>.</div><br> |
|x\-tos\-security\-token |String |No |/ |If STS temporary authorization is used, this value must be the same as the SecurityToken value, and a paired AK must be used.<br><br>Default value: None |
|x\-tos\-website\-redirect\-location |String |No |/anotherPage.html |For buckets with a **Website** configuration, requests to this object are redirected to another object in the bucket or an external URL. TOS will extract the value and save it in the object metadata.<br><br>Default value: None |
|x\-tos\-server\-side\-encryption |String |No |AES256 |Specifies the method used for encrypting the object. If this parameter is unset, the object is not encrypted by default. Valid values:<br><br><br>* `AES256`: Use SSE\-TOS. |
|x\-tos\-server\-side\-encryption\-customer\-algorithm |String |No, but YES if SSE\-C is used. |AES256 |Specifies the algorithm used for SSE\-C encrypting the object. Valid value:<br><br><br>* `AES256`: Use the AES\-256 algorithm. |
|x\-tos\-server\-side\-encryption\-customer\-key |String |No, but YES if SSE\-C is used. |Y2NjY2NjY2NjY2NjY2NjY2NjY2NjY2NjY2NjY2NjY2M= |Used with x\-tos\-server\-side\-encryption\-customer\-algorithm to specify the key used for SSE\-C encrypting the object. |
|x\-tos\-server\-side\-encryption\-customer\-key\-MD5 |String |No, but YES if SSE\-C is used. |ACdH+Fu9K3HlXdIUBu8GdA== |Used with x\-tos\-server\-side\-encryption\-customer\-key to specify the MD5 value of the customer\-provided key. The value is derived by Base64\-encoding the 128\-bit MD5 of the key and is used for message integrity check to ensure error\-free transmission of the encryption key. |
|x\-tos\-traffic\-limit |String |No |819200 |TOS supports per\-link rate limiting of file uploads and downloads, ensuring ample bandwidth for other applications. Valid values:<br><br><br>* A value between 819200 and 838860800, in bit/s. |
|x\-tos\-forbid\-overwrite |String |No |false |Is it allowed to overwrite objects with the same name? The values are as follows:<br><br><br>* Not specified or specified as false: Indicates allowing the overwriting of objects with the same name.<br><br>* When set to true: It indicates that overwriting objects with the same name is prohibited.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When the target Bucket is in a versioning state of enabled or suspended, the x\-tos\-forbid\-overwrite parameter setting is invalid, allowing the overwriting of objects with the same name.</div><br> |
|x\-tos\-object\-expires |String |No |3 |Set the expiration time for the object, after which TOS will automatically delete the object. The expiration time is calculated from the object's Last\-Modified time, in days.<br><br>After setting the object's expiration time, TOS will start executing the deletion task at midnight on the day the expiration time is reached. For example, if the object's Last\-Modified time is 2024\-09\-26 12:00 and the expiration time is set to 3 days, the object will expire at 2024\-09\-30 00:00.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The expiration time of an object takes priority over the deletion rule based on its lifecycle. For example, if an object has an expiration time set to 5 days and a lifecycle rule specifies the object should be deleted after 3 days, the object will be deleted based on the expiration time, which means it will be deleted after 5 days.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">TOS supports querying the expiration time of objects via <a href="https://docs.byteplus.com/docs/tos/reference--getobject">GetObject</a> or <a href="https://docs.byteplus.com/docs/tos/reference-headobject">HeadObject</a>.</div><br> |
|x\-tos\-object\-lock\-mode |String |No |COMPLIANCE |The mode of the retention policy is only `COMPLIANCE`, which means compliance mode.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To set a retention policy for an object, you must first enable the retention policy feature. For detailed information, see <a href="https://docs.byteplus.com/docs/tos/Putbucketobjectlockconfiguration">PutBucketObjectLockConfiguration</a>.</div><br> |
|x\-tos\-object\-lock\-retain\-until\-date |String |No |2025\-01\-01T00:00:00Z |The lock expiration date of the object; within this period, the object cannot be deleted or overwritten. Follow the ISO 8601 time format.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>x-tos-object-lock-retain-until-date</code> parameter must be used together with the <code>x-tos-object-lock-mode</code> parameter.</div><br> |


<span id="5ad8ede9"></span>
## **Response headers**

For common response headers, see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Type** |**Description** |
|---|---|---|
|x\-tos\-server\-side\-encryption |String |When SSE\-TOS encryption or SSE\-KMS is used, this header is returned, indicating the server\-side encryption method for the object.Valid values:<br><br><br>* `AES256`: Use the encryption method of SSE\-TOS.<br><br>* `kms`:Use the encryption method of SSE\-KMS. |
|x\-tos\-server\-side\-encryption\-kms\-key\-id |String |When SSE\-KMS encryption is used for the object, this header is returned, indicating the KMS master key ID used for SSE\-KMS encryption. |
|x\-tos\-server\-side\-encryption\-customer\-algorithm |String |Algorithm used for encrypting the object, which is returned if the object is SSE\-C encrypted. |
|x\-tos\-server\-side\-encryption\-customer\-key\-MD5 |String |MD5 value of the encryption key, which is returned if the object is SSE\-C encrypted. |
|x\-tos\-version\-id |String |Version ID of the object. This header will not appear in the response if the object has no version ID. |
|x\-tos\-hash\-crc64ecma |Integer |CRC\-64 value of the object, which is calculated according to the ECMA\-182 standard.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This is the CRC\-64 value of the unencrypted object content when server\-side encryption is enabled for object upload.</div><br> |


<span id="d54b022c"></span>
## **Response body elements**

If `success_action_status` is set to 201, TOS returns a JSON document after a successful upload.


|**Name** |**Type** |**Description** |
|---|---|---|
|Bucket |String |Name of the bucket containing the object. |
|Key |String |Object name. |
|Location |String |URL for the newly created object, including a domain name. |
|ETag |String |A piece of information generated at object creation to uniquely identify its content. |
|HashCrc64ecma |String |CRC64 value of the uploaded file. |


<span id="a8da2e52"></span>
## **Sample request**

```JSON
POST / HTTP/1.1
Host: buketname.tos-ap-southeast-1.bytepluses.com
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


<span id="cdf2bb33"></span>
## **Sample response**

```JSON
HTTP/1.1 204 No Content
x-tos-id-2: 367be10900210004-a444ed0
x-tos-request-id: 367be10900210004-a444ed0
Date: Fri, 1 Jul 2022 01:00:36 GMT
Server: TosServer
Content-Length: 0
ETag: "ab7abb0da4bca5323ab6119bb5dcd296"
Location: http://examplebucket.tos-ap-southeast-1.bytepluses.com/successful_upload.html
HashCrc64ecma: 6186290338114851376
```
