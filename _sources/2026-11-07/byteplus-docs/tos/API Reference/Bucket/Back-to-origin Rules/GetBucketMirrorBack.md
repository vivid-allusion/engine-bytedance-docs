---
title: "GetBucketMirrorBack"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Getbucketmirrorback"
---

<span id="0TMyZbcK"></span>
## Feature description

This interface retrieves the Bucket’s origin fetch rules.

<span id=".6K-35rGC5raI5oGv5qC35byP"></span>
## Request syntax

```JSON
GET /?mirror HTTP/1.1
Host: bucketname.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id=".6K-35rGC5Y-C5pWw5ZKM5raI5oGv5aS0"></span>
## Request parameters and headers

This request uses common request headers. See [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|---|
|mirror |Query |String |Yes |\- |Represents a special identifier for the GetBucketMirrorBack request. |


<span id=".6K-35rGC5YWD57Sg"></span>
## Request body elements

No elements are used.

<span id=".5ZON5bqU5raI5oGv5aS0"></span>
## Response headers

The public response message header returned by this request; see [public parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id=".5ZON5bqU5YWD57Sg"></span>
## Response body elements

**Rules**


|**Name** |**Type** |**Sample value** |**Note** |
|---|---|---|---|
|Rules |Array |\- |Array of origin request policy rules.<br><br>Root node, no parent node. |
|ID |String |1 |Rule ID. The unique identifier for the origin pull rule configured on the current bucket.<br><br>Parent node: Rules. |


**Condition**


|**Name** |**Type** |**Sample value** |**Note** |
|---|---|---|---|
|Condition |Object |\- |Conditions that trigger the origin fetch function.<br><br>Parent node: Rules. |
|HttpCode |int |404 |Error codes that trigger origin retrieval. Origin retrieval triggers when a download request returns this error code.<br><br>Limit: Currently only `404` is supported.<br><br>Parent node: Condition |
|Condition/KeyPrefix |String |object\-key\-prefix |Prefix of the object name matching the origin request.<br><br>Limit: supports up to 512 characters.<br><br>Parent node: Condition |
|KeySuffix |String |object\-key\-suffix |Suffix of the target name that matches the origin object.<br><br>Limit: supports up to 512 characters.<br><br>Parent node: Condition |
|AllowHost |Array |["example.volcengine.com"] |Trigger origin fetch only for specified domain names. The domain names must be accessible to the bucket. We recommend using the custom domain associated with the bucket.<br><br>Limit: supports up to 30 domain names.<br><br>Parent node: Condition |
|HttpMethod |Array |["GET","HEAD"] |Types of requests that trigger origin retrieval are explained as follows:<br><br><br>* `["GET","HEAD"]`: Both GetObject and HeadObject requests can trigger origin retrieval.<br><br>* `["GET"]`: Only GetObject requests can trigger origin retrieval. |


**Redirect**


|**Name** |**Type** |**Sample value** |**Note** |
|---|---|---|---|
|Redirect |Object |\- |Specify the action executed after this rule matches.<br><br>Parent node: Rules |
|RedirectType |String |Mirror |Specify the type of redirect. Valid values:<br><br><br>* `Mirror`: mirror origin fetch.<br><br>* `Async`: redirect to origin.<br><br><br>Parent node: Redirect |
|FetchSourceOnRedirect |Boolean |false |Whether to pull data from the configured origin after redirection. The value descriptions are as follows:<br><br><br>* `true`: Pull data from the configured origin after redirection.<br><br>* `false`: Do not pull data from the configured origin after redirection.<br><br><br>Parent node: Redirect |
|FetchSourceOnRedirectWithQuery |Boolean |false |Whether to carry request parameters when fetching data after redirection. If not configured, it inherits the PassQuery setting:<br><br><br>* `true`: carry request parameters.<br><br>* `false`: no request parameters included<br><br><br>Parent node: Redirect |
|PublicSource |Object |\- |Configuration of origin addresses for public buckets. See the following **PublicSource** for details.<br><br>Parent node: Redirect |
|PrivateSource |Object |\- |Configuration for the back\-to\-origin address when the origin is a private bucket. For details, see the **PrivateSource** below.<br><br>Parent node: Redirect |
|PassQuery |Boolean |true |Whether to carry request parameters when executing redirect or origin mirror rules. The options are as follows:<br><br><br>* `true`: carry request parameters.<br><br>* `false`: do not carry request parameters.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Even if <code>true</code> is set, Query parameters related to TOS authentication in the request will not be carried.</div><br><br><br>Parent node: Redirect |
|FollowRedirect |Boolean |true |If the mirror origin fetch result is 3xx, should it continue to redirect to the specified Location to retrieve data? The options are as follows:<br><br><br>* `true`: TOS will continue to request the address corresponding to Location.<br><br>* `false`: TOS will return 302.<br><br><br>Parent node: Redirect |
|MirrorHeader |Object |\- |Header carried when specifying image origin retrieval.<br><br>Parent node: Redirect |
|PassAll |Boolean |true |Whether to pass all HTTP headers to the source endpoint. The options are as follows:<br><br><br>* `true`: All HTTP headers will be passed to the source endpoint.<br><br>* `false`: All HTTP headers will not be passed to the source endpoint.<br><br><br>The following HTTP header types are not supported for passing through:<br><br><br>* `Host`<br><br>* `Content-Length`<br><br>* `Date`<br><br>* `Authorization`<br><br><br>Parent node: MirrorHeader |
|Pass |Array |["aaa", "bbb"] |Pass through the specified header to the origin station.<br><br>Limit: maximum quantity 64.<br><br>Parent node: MirrorHeader |
|Remove |Array |["xxx", "yyy"] |Prohibit forwarding specified headers to the origin server.<br><br>Limit: maximum quantity 64.<br><br>Parent node: MirrorHeader |
|Transform |Object |\- |Define the transformation for the requested origin object's name.<br><br>Parent node: MirrorHeader |
|WithKeyPrefix |String |addtional\-key\-prefix |Prefix added before the object name when requesting the origin server.<br><br>Limit: Maximum length of 512 characters.<br><br>Parent node: Transform |
|WithKeySuffix |String |addtional\-key\-suffix |A suffix appended to the object name when requesting the origin server.<br><br>Limitation: maximum length is 512 characters.<br><br>Parent node: Transform |
|ReplaceKeyPrefix |Object |\- |Replace the prefix of the target name when requesting the origin server.<br><br>Parent node: Transform |
|ReplaceKeyPrefix/KeyPrefix |String |key\-prefix |When requesting the origin server, the object name prefix to be replaced.<br><br>Limit: maximum length 512.<br><br>Parent node: ReplaceKeyPrefix |
|ReplaceWith |String |replace\-with |The value after replacing the object name prefix when requesting the origin site.<br><br>Limit: maximum length 512<br><br>Parent node: ReplaceKeyPrefix |


**PublicSource**


|**Name** |**Type** |**Sample value** |**Note** |
|---|---|---|---|
|PublicSource |Object |\- |Configure the origin address when the source site is a public bucket.<br><br>Parent node: Redirect |
|SourceEndpoint |Object |\- |Publicly accessible source address.<br><br>Parent node: PublicSource |
|Primary |Array |["http://abc.123/"] |Source address to request.<br><br>Limit: maximum length 255, supports up to 5 origin addresses.<br><br>Parent node: SourceEndpoint |


**PrivateSource**


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|PrivateSource |Object |\- |Back\-to\-origin address configuration for private bucket origin.<br><br>Parent node: Redirect |
|SourceEndpoint |Object |\- |Origin fetch address configuration when the source is a private bucket.<br><br>Parent node: PrivateSource |
|Primary |Array |\- |Source addresses requested, supporting up to 5 origin addresses.<br><br>Parent node: SourceEndpoint |
|Endpoint |String |http://s3.bj.bcebos.com |The access domain name of the origin service provider, without the bucket name, maximum length 255.<br><br>Parent node: Primary |
|BucketName |String |bucket |Name of the origin bucket.<br><br>Parent node: Primary |
|CredentialProvider |Object |\- |Private origin authentication method.<br><br>Parent node: Primary |
|Role |String |ServiceRoleBackSourceAccessTOS |Name of AssumeRole. This can be used for authentication only when pulling origin from a private bucket in TOS and is mutually exclusive with AK/SK authentication.<br><br>Parent node: CredentialProvider |
|Region |String |cn\-beijing |Region of the origin bucket.<br><br>Parent node: CredentialProvider |
|StaticCredential |Object |\- |Authenticate using AK/SK method.<br><br>Parent node: CredentialProvider |
|StorageVendor |String |S3 |Origin service provider, value description as follows:<br><br><br>* `BOS`: Baidu Cloud<br><br>* `S3`: other cloud providers using S3 storage protocol<br><br><br>Parent node: StaticCredential |
|AK |String |AKLTNDk3NDMxY2NmNzNhNGNiN\*\*\*\* |AccessKey ID of the origin bucket.<br><br>Parent node: StaticCredential |
|SK |String |AADFSDfdsfa3ewdr23==d\*\*\*\* |Encrypted SecretKey information of the origin bucket.<br><br>Parent node: StaticCredential |
|SKEncryptType |String |AES256 |Encryption method used by SecretKey.<br><br>Parent node: StaticCredential |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
GET /?mirror HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 13:53:55 +0000
Authorization: authorization string
```


<span id=".5ZON5bqU56S65L6L"></span>
## Sample response


* **Sample response 1: origin pull rule for public bucket source**

   ```JSON
   HTTP/1.1 200 OK
   Date: Fri, 30 Jul 2021 13:53:55 GMT
   Server: TosServer
   x-tos-id-2: 1e89f203jld00006-a444fd0
   x-tos-request-id: 1e89f203b2d00006-a444ed0
   Content-Length: 643
   {
       "Rules":[{
           "ID":"xxx",
           "Condition":{
               "HttpCode":204,
               "ObjectKeyPrefix":"prefix"
           },
           "Redirect":{
               "PublicSource":{
                   "SourceEndpoint":{
                       "Primary":["http://abc.123/"]
                   }
               },
               "PassQuery":true,
               "FollowRedirect":true,
               "MirrorHeader":{"PassAll":true}
           }
       }]
   }
   ```
   

* **Response example 2: origin pull rule for TOS private bucket**

   ```JSON
   HTTP/1.1 200 OK
   Date: Fri, 30 Jul 2021 13:53:55 GMT
   Server: TosServer
   x-tos-id-2: 1e89f203jld00006-a444fd0
   x-tos-request-id: 1e89f203b2d00006-a444ed0
   Content-Length: 643
   {
       "Rules":[{
           "ID":"xxx",
           "Condition":{
               "HttpCode":404,
               "KeyPrefix":"prefix"
           },
           "Redirect":{
               "PrivateSource":{
                   "SourceEndpoint":{
                       "Primary": [{
                           "Endpoint": "http://tos-cn-beijing.volces.com",
                            "BucketName": "bucket",  
                            "CredentialProvider": {
                                "Role": "ServiceRoleBackSourceAccessTOS"          
                            }              
                       }]
                   }
               },
               "PassQuery":true,
               "FollowRedirect":true,
               "MirrorHeader":{"PassAll":true}
           }
       }]
   }
   ```
   

* **Response example 3: origin pull rule for other S3 storage protocol cloud providers' private buckets**

   ```JSON
   HTTP/1.1 200 OK
   Date: Fri, 30 Jul 2021 13:53:55 GMT
   Server: TosServer
   x-tos-id-2: 1e89f203jld00006-a444fd0
   x-tos-request-id: 1e89f203b2d00006-a444ed0
   Content-Length: 643
   {
       "Rules":[{
           "ID":"xxx",
           "Condition":{
               "HttpCode":404,
               "KeyPrefix":"prefix"
           },
           "Redirect":{
               "PrivateSource":{
                   "SourceEndpoint":{
                       "Primary": {
                           "Endpoint": "http://s3.com",
                            "BucketName": "bucket",  
                            "CredentialProvider": {
                                "Region": "cn-beijing"，           
                                "StaticCredential": {
                                      "StorageVendor": "S3",
                                       "AK": "AKLTNDk3NDMxY2NmNzNhNGNiN****", 
                                       "SK":"AADFSDfdsfa3ewdr23==d****",
                                       "SKEncryptType": "AES256"
                                }
                            }      
                       }
                   }
               },
               "PassQuery":true,
               "FollowRedirect":true,
               "MirrorHeader":{"PassAll":true}
           }
       }]
   }
   ```
