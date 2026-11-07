---
title: "Upload callbacks"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Upload-callback"
---

Upload callbacks refer to the client carrying a callback parameter during the request. After the server completes the upload, it sends a synchronous POST callback request to the third\-party application server specified in CallBack. Only after the server confirms acceptance and returns the result will all results be returned to the client. Because the callback request and waiting for a response are added, the waiting time is longer compared to a normal upload.

<span id=".5LiK5Lyg5Zue6LCD6K-05piO"></span>
## Upload callback description

The following interfaces currently support upload callbacks:


* [PutObject](https://docs.byteplus.com/docs/tos/reference-putobject)

* [PostObject](https://docs.byteplus.com/docs/tos/reference-postobject)

* [CompleteMultipartUpload](https://docs.byteplus.com/docs/tos/reference-completemultipartupload)


The upload callback process is as follows:

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_b90026c5176d28872d06dd3d7051bd6e.png) </span>

&nbsp;

<span id="zqJ237cN"></span>
## Step 1: Construct callback parameters

Using upload callbacks depends on the client carrying callback parameters and callback parameter variables during the request.

<span id=".5Zue6LCD5Y-C5pWw"></span>
### Callback parameters

Callback parameters are a Base64\-encoded JSON string. Example:

```json
//  Example 1, passing a message body of type application/json.
{
    "callbackUrl" : "http://domainname.com/callback", 
    "callbackHost" : "alternative-domainname.com",               
    "callbackBody" : "{\"bucket\" : ${bucket}, \"object\" : ${object}, \"key1\" : ${x:key1}, \"key2\" : ${x:key2}}", 
    "callbackBodyType" : "application/json"                
}

//  Example 2, passing a message body of type application/x-www-form-urlencoded.
{
    "callbackUrl" : "http://domain-name/callback", 
    "callbackHost" : "alternative-domain-name",               
    "callbackBody" : "bucket=${bucket}&object=${object}&key1=${x:key1}&key2=${x:key2}", 
    "callbackBodyType" : "application/x-www-form-urlencoded"               
}
```


The callback parameters are explained as follows:


|**Field** |**Function description** |**Restrictions** |
|---|---|---|
|callbackUrl |Callback request URL specifies the address of the third\-party application service for the callback request. After a successful upload, TOS service sends an HTTP/HTTPS request to this address. |* The callback parameter can be empty; if empty, it means no upload callback parameter was set for this request.<br><br>* The URL format must be an HTTP/HTTPS protocol address. If the protocol type is not specified, the default is `https://`.<br><br>* The path and query parts of the URL must be URL\-encoded.<br><br>* Supports up to 5 URLs, separated by semicolons`;`as separators. TOS server requests each URL in order during the callback, stopping at the first URL that returns successfully.<br><br>* Callback parameter variables are not supported. |
|callbackHost |Host header sent with the callback request, used to replace the host parsed from the callbackUrl. |* Can be empty; if not empty, it must comply with the format rules for domains or IP addresses.<br><br>* Callback parameter variables are not supported. |
|callbackBody |The callback request message body must match the format specified by callbackBodyType. |* Cannot be empty and must be in a valid format. The TOS server will strictly validate this field.<br><br>* Supports callback parameter variables. |
|callbackBodyType |Callback request message body type (Content\-Type), used with callbackBody. |* can be empty; defaults to application/x\-www\-form\-urlencoded when empty.<br><br>* only supports values of application/x\-www\-form\-urlencoded and application/json; other values are considered invalid.<br><br>* callback parameter variables are not supported. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When callbackUrl is empty, it means no upload callback parameters are set for this request, and other parameters become invalid.</div>


* <div data-tips="true" data-tips-type="warning">The domain name or IP included in callbackUrl and callbackHost must not be special domain names or IPs, such as 127.0.0.1, 0.0.0.0, 0:0:0:0:0:0:0:1, 0:0:0:0:0:0:0:0, or localhost.</div>



<span id=".5Zue6LCD5Y-C5pWw5Y-Y6YeP"></span>
### Callback parameter variables

CallbackBody in callback parameters supports callback parameter variables, divided into system built\-in variables and custom variables (callback\-var). The former can be used directly in callbackBody; the latter must be carried together by the client during the request. TOS server parses the custom variables from the JSON format and merges them with system built\-in variables into a set of usable key\-value pairs for replacing variables in the callbackBody in the form of  **${variable_name} and ${x:variable_name}** .

<span id=".57O757uf5YaF572u5Y-Y6YeP"></span>
#### System built\-in variables

The system built\-in variables available for setting in callbackBody are listed below.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When using system built\-in variables in callbackBody, you must add the <code>${}</code> operator, for example, ${bucket} represents the uploaded bucket name.</div>


* <div data-tips="true" data-tips-type="warning">When callbackBodyType is application/json, as a <strong>field value</strong> in JSON format, the value will be filled according to the variable type. For example, if bucket is the string bucket\-test and size is the integer 1024, then {\"bucket\": ${bucket}, \"size\" : ${size}} will be parsed as {\"bucket\" : \"bucket\-test\", \"size\" : 1024}.</div>




|**variable name** |**Variable description** |**Variable type** |
|---|---|---|
|bucket |The uploaded bucket name. |string |
|key |Name of the uploaded object. |string |
|object |Name of the uploaded object. |string |
|size |The size of the uploaded object. |int64 |
|etag |ETag of the uploaded object. |string |
|crc64ecma |CRC64 of the object after upload. |string |
|versionId |The version ID of the object after upload is present only if the bucket has multi\-versioning enabled. |string |
|filename |original file name uploaded via PostObject. |string |
|fname |The original file name uploaded by PostObject. |string |
|mimeType |The Content\-Type specified by the client when uploading the object; if not specified, defaults to binary/octet\-stream. |string |
|requestId |Request ID of this request. |string |


<span id=".6Ieq5a6a5LmJ5Y-Y6YeP"></span>
#### Custom variables

The client can carry custom variable key\-value pairs in JSON format during the request. The TOS server will parse the custom variables from the JSON format for variable replacement in callbackBody. As shown below, four custom variables are defined:

```json
{
    "x:key1" : "value1",                 // Define a field of type string.
    "x:key2" : 123,                      // Define a field of type number.
    "x:key3" : ["value2", "value3"],     // Define a field of array type.
    "x:key4" : true                      // Define a boolean type field.
}
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Custom variables must begin with <code>x:</code>, otherwise they will be considered invalid.</div>


* <div data-tips="true" data-tips-type="warning">When using custom variables in callbackBody, you must add the <strong>${} operator</strong>, for example, ${x:key1} represents getting the variable x:key1.</div>


* <div data-tips="true" data-tips-type="warning">When callbackBodyType is application/json, the TOS server fills data using the same rules as with built\-in system variables.</div>


* <div data-tips="true" data-tips-type="warning">When callbackBodyType is application/x\-www\-form\-urlencoded, the system variables (key, object, fname, filename) in callbackBody are url_encoded during filling.</div>



<span id=".5p6E6YCg5LiK5Lyg5Zue6LCD6K-35rGC"></span>
## Step two: construct the callback request

<span id="4727bf55"></span>
### Construction method

The upload callback supports interfaces including PutObject, PostObject, and CompleteMultipartUpload. Among these, PutObject and CompleteMultipartUpload can carry callback parameters and custom variables via URL or Header; PostObject carries callback parameters and custom variables through form fields. The client constructs the upload callback request as shown below.


|**Upload callback support interface** |**Supported parameter carrying methods** |**parameter definitions** |**Signature method** |**restrictions** |
|---|---|---|---|---|
|PutObject, CompleteMultipartUpload |Parameters carried in Header |Header usage:<br><br><br>* x\-tos\-callback<br><br>* x\-tos\-callback\-var |Calculate according to the [signature mechanism](https://docs.byteplus.com/docs/6349/74839) including CanonicalHeaders and SignedHeaders. |* Both variables must be Base64\-encoded JSON formats.<br><br>* Callback parameters and custom variables cannot appear repeatedly in both Header and Query, but each can contain one combination. |
||Parameters included in the URL |Query usage:<br><br><br>* x\-tos\-callback<br><br>* x\-tos\-callback\-var |Calculate into CanonicalQueryString according to the [signature mechanism](https://docs.byteplus.com/docs/6349/74839). ||
|PostObject |Use POST form fields |* Use x\-tos\-callback for form fields<br><br>* Use x\-tos\-callback\-var or pass each custom variable field through form fields. |Add x\-tos\-callback, x\-tos\-callback\-var, and custom variables as conditions into the form upload policy according to the [POST object upload signature mechanism](https://docs.byteplus.com/docs/tos/reference-browser-based-upload-forms-include-signatures). |* x\-tos\-callback and x\-tos\-callback\-var must be Base64\-encoded JSON format.<br><br>* Prioritize using x\-tos\-callback\-var. If x\-tos\-callback\-var is not provided, each custom variable field is passed via form fields. |


**Parameter description**


* **Carry parameters in the URL**: carry callback parameters via `x-tos-callback`; carry custom variables of callback parameter variables via `x-tos-callback-var`.

* **Carry parameters in the Header**: carry callback parameters via `x-tos-callback`; carry custom variables of callback parameter variables via `x-tos-callback-var`.

* **Carry parameters in the body of the POST request through form fields, carrying callback parameters via x\-tos\-callback**: custom variables in callback parameter variables are carried via `x-tos-callback-var`. If `x-tos-callback-var` is not carried, each field of the custom variables is individually passed through form fields. For example:

   ```Plain
   --9431149156168
   Content-Disposition: form-data; name="x:key1"
   value1
   --9431149156168
   Content-Disposition: form-data; name="x:key2"
   123
   ```
   


<span id=".5a6i5oi356uv5LiK5Lyg5Zue6LCD5p6E6YCg56S65L6L"></span>
### Construct example

This article uses the third\-party application server's callback response {\"Status\":\"OK\"} to TOS as an example to demonstrate how to construct a callback request.


1. Construct callback parameters:

   ```json
   // Callback parameter: 
   {
       "callbackUrl" : "http://domainname.com/callback", 
       "callbackHost" : "alternative-domainname.com",               
       "callbackBody" : "{\"bucket\" : ${bucket}, \"object\" : ${object}, \"key1\" : ${x:key1}, \"key2\" : ${x:key2}}", 
       "callbackBodyType" : "application/json"                
   }
   
   // Callback parameter variable:
   {
       "x:key1" : "value1",
       "x:key2" : 123,
   }
   
   // Results returned by third-party application services.：
   {"Status":"OK"}
   ```
   

2. Encode the callback parameters and callback parameter variables using Base64.

   ```json
   // Encode the callback parameter in Base64 to get x-tos-callback:
   Cgl7CgkJImNhbGxiYWNrVXJsIiA6ICJodHRwOi8vZG9tYWlubmFtZS5jb20vY2FsbGJhY2siLCAKCQkiY2FsbGJhY2tIb3N0IiA6ICJhbHRlcm5hdGl2ZS1kb21haW5uYW1lLmNvbSIsICAgICAgICAgICAgICAgCgkJImNhbGxiYWNrQm9keSIgOiAie1wiYnVja2V0XCIgOiAke2J1Y2tldH0sIFwib2JqZWN0XCIgOiAke29iamVjdH0sIFwia2V5MVwiIDogJHt4OmtleTF9LCBcImtleTJcIiA6ICR7eDprZXkyfX0iLCAKCQkiY2FsbGJhY2tCb2R5VHlwZSIgOiAiYXBwbGljYXRpb24vanNvbiIgICAgICAgICAgICAgICAgCgl9
   // Base64 encode the callback parameter variable to get x-tos-callback-var:
   ewogICAgIng6a2V5MSIgOiAidmFsdWUxIiwKICAgICJ4OmtleTIiIDogMTIzLAp9
   ```
   

3. Construct the upload callback request.

   
   <Tabs>
   <Tab zoneid="qhMc2qjHwg" title="PutObject request">
   <TabTitle>PutObject request</TabTitle>
   
   Construct a PutObject request and include callback parameters and custom variables in the Header as follows:
   
   ```Plain
   PUT /objectName HTTP/1.1
   Host: bucketname.tos-cn-beijing.bytepluses.com.cn
   Date: Fri, 30 Jul 2021 08:05:36 +0000
   x-tos-callback-var: ewogICAgIng6a2V5MSIgOiAidmFsdWUxIiwKICAgICJ4OmtleTIiIDogMTIzLAp9
   x-tos-callback: Cgl7CgkJImNhbGxiYWNrVXJsIiA6ICJodHRwOi8vZG9tYWlubmFtZS5jb20vY2FsbGJhY2siLCAKCQkiY2FsbGJhY2tIb3N0IiA6ICJhbHRlcm5hdGl2ZS1kb21haW5uYW1lLmNvbSIsICAgICAgICAgICAgICAgCgkJImNhbGxiYWNrQm9keSIgOiAie1wiYnVja2V0XCIgOiAke2J1Y2tldH0sIFwib2JqZWN0XCIgOiAke29iamVjdH0sIFwia2V5MVwiIDogJHt4OmtleTF9LCBcImtleTJcIiA6ICR7eDprZXkyfX0iLCAKCQkiY2FsbGJhY2tCb2R5VHlwZSIgOiAiYXBwbGljYXRpb24vanNvbiIgICAgICAgICAgICAgICAgCgl9
   Authorization: authorization_string
   Content-Type: text/plain
   Content-Length: 0
   ```
   
   
   
   </Tab>
   <Tab zoneid="gnzUB1d68P" title="CompleteMultipartUpload request">
   <TabTitle>CompleteMultipartUpload request</TabTitle>
   
   Construct a CompleteMultipartUpload request with callback parameters and custom variables carried in the URL, as follows:
   
   ```Plain
   POST /objectName?uploadId=UploadId&x-tos-callback=Cgl7CgkJImNhbGxiYWNrVXJsIiA6ICJodHRwOi8vZG9tYWlubmFtZS5jb20vY2FsbGJhY2siLCAKCQkiY2FsbGJhY2tIb3N0IiA6ICJhbHRlcm5hdGl2ZS1kb21haW5uYW1lLmNvbSIsICAgICAgICAgICAgICAgCgkJImNhbGxiYWNrQm9keSIgOiAie1wiYnVja2V0XCIgOiAke2J1Y2tldH0sIFwib2JqZWN0XCIgOiAke29iamVjdH0sIFwia2V5MVwiIDogJHt4OmtleTF9LCBcImtleTJcIiA6ICR7eDprZXkyfX0iLCAKCQkiY2FsbGJhY2tCb2R5VHlwZSIgOiAiYXBwbGljYXRpb24vanNvbiIgICAgICAgICAgICAgICAgCgl9&x-tos-callback-var=ewogICAgIng6a2V5MSIgOiAidmFsdWUxIiwKICAgICJ4OmtleTIiIDogMTIzLAp9 HTTP/1.1
   Host: bucketname.tos-cn-beijing.bytepluses.com.cn
   Date: Fri, 30 Jul 2021 08:05:36 +0000
   Authorization: authorization_string
   
   {
       "Parts":[{
           "PartNumber":1, 
           "ETag":"7de47c292287f7965357c1ddd724b2b7"
       }]
   }
   ```
   
   
   
   </Tab>
   <Tab zoneid="t2KsaZ7DJJ" title="PostObject request">
   <TabTitle>PostObject request</TabTitle>
   
   Construct a PostObject request and include callback parameters and custom variables in the form fields as follows:
   
   ```Plain
   POST / HTTP/1.1
   Host: buketname.tos-cn-beijing.bytepluses.com.cn
   Content-Type: multipart/form-data; boundary=9431149156168
   Content-Length: length
   --9431149156168
   Content-Disposition: form-data; name="key"
   objectname
   --9431149156168
   Content-Disposition: form-data; name="x-tos-callback"
   Cgl7CgkJImNhbGxiYWNrVXJsIiA6ICJodHRwOi8vZG9tYWlubmFtZS5jb20vY2FsbGJhY2siLCAKCQkiY2FsbGJhY2tIb3N0IiA6ICJhbHRlcm5hdGl2ZS1kb21haW5uYW1lLmNvbSIsICAgICAgICAgICAgICAgCgkJImNhbGxiYWNrQm9keSIgOiAie1wiYnVja2V0XCIgOiAke2J1Y2tldH0sIFwib2JqZWN0XCIgOiAke29iamVjdH0sIFwia2V5MVwiIDogJHt4OmtleTF9LCBcImtleTJcIiA6ICR7eDprZXkyfX0iLCAKCQkiY2FsbGJhY2tCb2R5VHlwZSIgOiAiYXBwbGljYXRpb24vanNvbiIgICAgICAgICAgICAgICAgCgl9
   --9431149156168
   Content-Disposition: form-data; name="x:key1"
   value1
   --9431149156168
   Content-Disposition: form-data; name="x:key2"
   123
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
   base64encoded_policy
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
   
   
   
   </Tab>
   </Tabs>
   


<span id=".5Y-R6LW35Zue6LCD6K-35rGC"></span>
## Step 3: Initiate the callback request

After the TOS server finishes uploading the object, it sends a Post request to the third\-party application service according to the callback parameter configuration in the upload request. The callback interface implemented by the third\-party application server must meet the following requirements.


|**Constraints** |**Requirement** |
|---|---|
|interface protocol |HTTP and HTTPS. When using HTTPS protocol, third\-party application services must have valid certificates. |
|Supported methods |POST |
|request message body format |application/x\-www\-form\-urlencoded、application/json |
|response status code |200 |
|Response message body format |application/json |
|Response message body size |Must not exceed 3MB. |


TOS calls the third\-party server using a Post request based on the callback parameters and callback parameter variables in the user's request. Example:

```http
POST /callback HTTP/1.1
Host: alternative-domainname.com
Content-Length: 71
Content-Type: application/json

{"bucket":"bucket-test","object":"key-test","key1":"value1","key2":123}
```


<span id="87551489"></span>
## (Optional) Step 4: Callback signature

After receiving the callback request, the third\-party application server can verify whether the request comes from TOS by checking the signature in the callback.


<Tabs>
<Tab zoneid="X0NixULjJi" title="The TOS server generates the signature">
<TabTitle>The TOS server generates the signature</TabTitle>

The TOS server uses RSA asymmetric encryption to automatically calculate the signature and sends it to the third\-party application server. The following describes the process of signature generation on the TOS server.


1. Create the string to be signed (StringToSign).

   ```Plain
   url_decode(path) + '?' + url_decode(sorted(query)) + '\\n' + body
   ```
   

2. Calculate the hash value of the string to be signed using the MD5 hash function.

   ```Plain
   md5(StringToSign)
   ```
   

3. Encrypt the hash value of the string to be signed with the private key to generate the signature.

   ```Plain
   rsa_sign(private_key, url_decode(path) + '?' + url_decode(sorted(query)) + '\\n' + body, md5)
   ```
   

4. Encode the signature with Base64, then add the encoded signature to the Authorization header of the callback request and send it to the third\-party application server.

   ```Plain
   Authorization = base64_encode(rsa_sign(private_key, url_decode(path) + '?' + url_decode(sorted(query)) + '\\n' + body, md5))
   ```
   


</Tab>
<Tab zoneid="yNWP7ZWfU2" title="Third-party application server signature verification">
<TabTitle>Third-party application server signature verification</TabTitle>

The following introduces the signature verification process for third\-party servers.


1. The value of the callback request header `x-tos-pub-key-url` is the download URL of the Base64\-encoded public key used for signature verification. Decode the value of `x-tos-pub-key-url` using Base64, then download the public key locally.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To ensure this public key is issued by TOS, verify that the download URL of the public key starts with <code>http://sf-tos-public.bytepluscdn.com</code> or <code>https://sf-tos-public.bytepluscdn.com</code>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The public key is long\-term and unchanged. It is recommended to store the public key in local cache for future use.   </div>
   

2. Base64\-decode the value of the callback request header `Authorization` to obtain the signature.

3. Create the string to sign (StringToSign) using the request path, request parameters, and request body obtained from the request.

   ```Plain
   url_decode(path) + '?' + url_decode(sorted(query)) + '\\n' + body
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When creating a string to be signed, the <code>query</code> must be sorted in dictionary order.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the <code>query</code> contains only keys, create the string to be signed in the format of <code>"key="</code>.   </div>
   

4. Calculate the hash value of the string to be signed using the MD5 hash function.

   ```Plain
   md5(StringToSign)
   ```
   

5. Verify the signature using the public key, signature, and hash value of the string to be signed.

   ```Plain
   result = rsa_verify(public_key, md5(StringToSign), signature)
   ```
   

   Using Go as an example, demonstrate how a third\-party application server verifies the signature.

   ```Go
   package callback
   import (
       "bytes"
       "crypto"
       "crypto/md5"
       "crypto/rsa"
       "crypto/x509"
       "encoding/base64"
       "encoding/json"
       "encoding/pem"
       "errors"
       log "github.com/sirupsen/logrus"
       "io/ioutil"
       "net/http"
       "sort"
       jsoniter "github.com/json-iterator/go"
   )
   const XTosPublicKeyUrl = "x-tos-pub-key-url"
   const Authorization = "Authorization"
   type CallbackAPI struct {
   }
   type ErrResp struct {
       Err    string `json:"Err"`
       RetMsg string `json:"RetMsg"`
   }
   func (api *CallbackAPI) CallbackHandler(w http.ResponseWriter, r *http.Request) {
       sign, err := getSignature(r)
       if err != nil {
          log.Warn("authorization: %s is not base64 encoding", r.Header.Get(Authorization))
          JsonResponse(w, 401, ErrResp{Err: "[Callback] invalid Authorization, err:" + err.Error()})
          return
       }
       publicKey, err := getPublicKey(r)
       if err != nil {
          JsonResponse(w, 401, ErrResp{Err: "[Callback] invalid public key, err:" + err.Error()})
          return
       }
       signMd5, body, err := getContentAndSignMD5(r)
       if err != nil {
          JsonResponse(w, 401, ErrResp{Err: "[Callback] invalid public key, err:" + err.Error()})
          return
       }
       if err = verifySignature(publicKey, signMd5, sign); err != nil {
          JsonResponse(w, 401, ErrResp{Err: "[Callback] verify signature failed, err:" + err.Error()})
          return
       }
       log.Info("[Callback] handle callback request")
       bodyType := r.Header.Get("Content-Type")
       switch bodyType {
       case "application/json":
          if !jsoniter.Valid(body) {
             JsonResponse(w, 500, ErrResp{Err: "[Callback] the body is not a valid json"})
             return
          }
          JsonResponse(w, 200, body)
       default: // application/x-www-form-urlencoded
          JsonResponse(w, 200, struct {
             EncodedBody string `json:"encoded_body"`
          }{
             EncodedBody: base64.StdEncoding.EncodeToString(body),
          })
       }
   }
   func verifySignature(publicKey []byte, signMd5 []byte, sign []byte) error {
       pubBlock, _ := pem.Decode(publicKey)
       if pubBlock == nil {
          log.Warn("Failed to parse PEM block containing the public key")
          return errors.New("invalid public key pem")
       }
       pubInterface, err := x509.ParsePKIXPublicKey(pubBlock.Bytes)
       if err != nil || pubInterface == nil {
          log.Warn("x509.ParsePKIXPublicKey(publicKey) failed, err:%v", err)
          return errors.New("invalid public key pem")
       }
       pub := pubInterface.(*rsa.PublicKey)
       err = rsa.VerifyPKCS1v15(pub, crypto.MD5, signMd5, sign)
       if err != nil {
          log.Warn("verify signature failed, err:%v", err)
          return err
       }
       return nil
   }
   func getContentAndSignMD5(r *http.Request) ([]byte, []byte, error) {
       bodyContent, err := ioutil.ReadAll(r.Body)
       _ = r.Body.Close()
       if err != nil {
          log.Warn("read request body failed, err:%v", err)
          return nil, nil, err
       }
       stringToSign := calcStringToSign(r, bodyContent)
       log.Info("stringToSign: %s", stringToSign)
       authMd5 := md5.New()
       authMd5.Write(stringToSign)
       signMd5 := authMd5.Sum(nil)
       return signMd5, bodyContent, nil
   }
   func getPublicKey(r *http.Request) ([]byte, error) {
       var bytePublicKey []byte
       publicKeyURLBase64 := r.Header.Get(XTosPublicKeyUrl)
       if publicKeyURLBase64 == "" {
          log.Warn("GetPublicKey from Request header failed :  No x-tos-pub-key-url field. ")
          return bytePublicKey, errors.New("no x-tos-pub-key-url field in Request header ")
       }
       publicKeyURL, _ := base64.StdEncoding.DecodeString(publicKeyURLBase64)
       resp, err := http.Get(string(publicKeyURL)) // ignore_security_alert
       if err != nil {
          log.Warn("Get PublicKey Content from URL failed : %s", err.Error())
          return bytePublicKey, err
       }
       bytePublicKey, err = ioutil.ReadAll(resp.Body)
       defer resp.Body.Close()
       if err != nil {
          log.Warn("Read PublicKey Content from URL failed : %s", err.Error())
          return bytePublicKey, err
       }
       if resp.StatusCode >= http.StatusBadRequest {
          log.Warn("get public key failed, res:%s", string(bytePublicKey))
          return nil, errors.New("get public key failed")
       }
       return bytePublicKey, nil
   }
   func getSignature(r *http.Request) ([]byte, error) {
       authorization := r.Header.Get(Authorization)
       if authorization == "" {
          return nil, nil
       }
       return base64.StdEncoding.DecodeString(authorization)
   }
   // url_decode(path) + '?' + url_decode(sorted(query)) + '\n' + body
   func calcStringToSign(req *http.Request, body []byte) []byte {
       buf := bytes.NewBuffer(nil)
       buf.WriteString(req.URL.Path)
       query := req.URL.Query()
       if len(query) > 0 {
          buf.WriteByte('?')
          keys := make([]string, 0, len(query))
          for key := range query {
             keys = append(keys, key)
          }
          sort.Strings(keys)
          for _, key := range keys {
             values := query[key]
             for _, value := range values {
                buf.WriteString(key)
                buf.WriteByte('=')
                buf.WriteString(value)
                buf.WriteByte('&')
             }
          }
          buf.Truncate(buf.Len() - 1)
       }
       buf.WriteByte('\n')
       buf.Write(body)
       return buf.Bytes()
   }
   func JsonResponse(w http.ResponseWriter, status int, entity interface{}) {
       // content-type must be set before WriteHeader, or it will not take effect
       if entity != nil {
          w.Header().Set("Content-Type", "application/json")
       }
       w.WriteHeader(status)
       if entity != nil {
          if body, ok := entity.([]byte); ok {
             _, _ = w.Write(body)
             return
          }
          body, _ := json.Marshal(entity)
          _, _ = w.Write(body)
       }
   }
   ```
   


</Tab>
</Tabs>


<span id=".6L-U5Zue5Zue6LCD57uT5p6c"></span>
## **Step 5: Return the callback result**

The third\-party application server returns a response to TOS, as shown below:

```http
HTTP/1.1 200 OK
Date: Fri, 1 Jul 2022 01:00:36 GMT
Content-Length: 15
Content-Type: application/json

{"Status":"OK"}
```


<span id=".6L-U5Zue5LiK5Lyg5Zue6LCD57uT5p6c"></span>
## **Step 6: Return the upload result**

TOS returns the content from the third\-party application server to the user.


<Tabs>
<Tab zoneid="a5DmNqAuX7" title="PutObject request response result">
<TabTitle>PutObject request response result</TabTitle>

```Plain
HTTP/1.1 200 OK
x-tos-id-2: 367be10900210004-a444ed0
x-tos-request-id: 367be10900210004-a444ed0
Date: Fri, 30 Jul 2021 08:05:36 GMT
server: TosServer
Content-Length: 15
Content-Type: application/json
ETag: 1c06e540e11d65a51aeb724e72fa641a

{"Status":"OK"}
```



</Tab>
<Tab zoneid="tUmJOKDXUt" title="CompleteMultipartUpload request response">
<TabTitle>CompleteMultipartUpload request response</TabTitle>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The CompleteMultipartUpload result contains a message body. When using the upload callback function, it will overwrite the original message body. The client must handle this case appropriately.</div>


* <div data-tips="true" data-tips-type="warning">When using the upload callback function, a Location header is added to return the domain\-prefixed URL of the new object, and an ETag header is added to return the ETag value.</div>



```Plain
HTTP/1.1 200 OK
x-tos-id-2: 9b84750a5bbc0029-a444ed0
x-tos-request-id: 9b84750a5bbc0029-a444ed0
Date: Fri, 30 Jul 2021 13:59:38 GMT
server: TosServer
Content-Length: 15
Content-Type: application/json
Location: http://bucketname.tos-cn-beijing.bytepluses.com.cn/objectname
ETag: 7de47c292287f7965357c1ddd724b2b7-1

{"Status":"OK"}
```



</Tab>
<Tab zoneid="gIK7QyFw10" title="PostObject request response">
<TabTitle>PostObject request response</TabTitle>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">After using the upload callback feature with PostObject, the response body is returned, changing the HTTP status code from 204 to 200. The client needs to handle this accordingly.</div>


* <div data-tips="true" data-tips-type="warning">When the CallbackFailed error code appears, the corresponding HTTP status code is 203. The client needs to handle this situation properly. For other status codes and details, refer to <a href="https://docs.byteplus.com/docs/6349/74874">response codes</a>.</div>



```Plain
HTTP/1.1 200  OK
x-tos-id-2: 367be10900210004-a444ed0
x-tos-request-id: 367be10900210004-a444ed0
Date: Fri, 1 Jul 2022 01:00:36 GMT
Server: TosServer
Content-Length: 15
Content-Type: application/json
ETag: ab7abb0da4bca5323ab6119bb5dcd296
Location: http://bucketname.tos-cn-beijing.bytepluses.com.cn/objectname

{"Status":"OK"}
```



</Tab>
</Tabs>


<span id=".cHV0b2JqZWN0Leivt-axgui_lOWbnue7k-aenA=="></span>
## Error Code


|**HTTP status code** |**Error Code** |**Error Message** |
|---|---|---|
|203 |CallbackFailed |Object uploaded successfully, but the callback request to the third\-party application service failed, such as domain name resolution error, request timeout, or invalid response content. |
|400 |InvalidCallbackArgument |* The field validation in the callback parameter is invalid<br><br>* Custom variable (callback\-var) format is invalid<br><br>* Header or Query contains duplicate custom parameters or custom variables. |
|403 |AccessDenied |PostObject's policy validation for callback parameters and custom variables failed. |
