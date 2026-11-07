---
title: "PutBucketMirrorBack"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Putbucketmirrorback"
---

## Feature description

This interface allows setting the bucket's origin rules. You can configure multiple rules based on different conditions in the rules.

## Notes

* Only the bucket owner can set the origin rules.

* Up to 20 origin rules can be set.

For detailed information, see mirroring back to origin [Notes](https://docs.byteplus.com/docs/tos/docs-setting-back-to-origin-rules#3317ff52) and redirect back to origin [Notes](https://docs.byteplus.com/en/docs/tos/Create-a-redirection-back-to-origin-rule#c3d95658).

## Request syntax

```JSON
PUT /?mirror HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
{
    "Rules":[{
        "ID":"1",
        "Condition":{
            "HttpCode":404,  
            "KeyPrefix":"object-key-prefix",  
            "KeySuffix": "object-key-suffix",
            "AllowHost": [
                    "example.volcengine.com"
                ],
            "HttpMethod": [
                    "GET",
                    "HEAD"
               ]
        },
        "Redirect":{
            "RedirectType": "Mirror",        
            "FetchSourceOnRedirect": false,
            "PublicSource":{      
                "SourceEndpoint":{ 
                    "Primary":["http://abc.123/"],
                    "Follower":["http://abc.456/"]
                }
            },
            "PassQuery": true,     
            "FollowRedirect": true, 
            "MirrorHeader":{       
                "PassAll": true,
                "Pass": ["aaa", "bbb"],
                "Remove": ["xxx", "yyy"]
            },
            "Transform": { 
               "WithKeyPrefix": "addtional-key-prefix", 
               "WithKeySuffix": "addtional-key-suffix",  
               "ReplaceKeyPrefix": { 
                  "KeyPrefix": "key-prefix",
                  "ReplaceWith": "replace-with"
               }
            }
        }
    }]
}
```

## Request parameters and headers

This request uses public request headers, see [public parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|---|
|mirror |Query |String |Yes |\- |Special identifier representing the PutBucketMirrorBack request. |

## Request body elements

**Rules**

|**Name** |**Parameter type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|
|Rules |Array |Yes |\- |Origin fetch policy rule array.<br><br>Root node, no parent node. |
|ID |String |No |1 |Rule ID.<br><br>The unique identifier for the origin rule configured on the current bucket. You can set it yourself to differentiate multiple rules. Restrictions are as follows:<br><br><br>* The characters support letters, numbers,`-`and`_`.<br><br>* Supports up to 32 characters.<br><br><br>Parent node: `Rules` |

**Condition**

|**Name** |**Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|
|Condition |Object |Yes |\- |Condition to trigger back\-to\-origin functionality.<br><br>Parent node: `Rules` |
|HttpCode |int |Yes |404 |Error code that triggers the origin fetch function. When a download request returns this error code, it triggers the origin fetch function.<br><br>Limit: Currently only `404` is supported.<br><br>Parent node: `Condition` |
|KeyPrefix |String |No |object\-key\-prefix |Prefix of the object name matched for the origin object.<br><br>Limit: supports up to 512 characters.<br><br>Parent node: `Condition` |
|KeySuffix |String |No |object\-key\-suffix |The object name suffix that matches the back\-to\-origin target.<br><br>Limit: supports up to 512 characters.<br><br>Parent node: `Condition` |
|AllowHost |Array |Not supported |["example.volcengine.com"] |Only requests with specified domain names will trigger origin fetch. The domain must be able to access the bucket. We recommend using the custom domain associated with the bucket.<br><br>Limit: supports up to 30 domains.<br><br>Parent node: `Condition` |
|HttpMethod |Array |No |["GET","HEAD"] |Request types that trigger back\-to\-origin, with the following values:<br><br><br>* `[\"GET\",\"HEAD\"]`: indicates that both GetObject and HeadObject requests can trigger back\-to\-origin.<br><br>* `[\"GET\"]`: indicates that only GetObject requests can trigger back\-to\-origin.<br><br><br>Defaults to `[\"GET\"]`. |

**Redirect**

|**Name** |**Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|
|Redirect |Object |Yes |\- |Specify the action to perform after matching this rule.<br><br>Parent node: `Rules` |
|RedirectType |String |No |Mirror |Specify the type of redirect. Value range:<br><br><br>* `Mirror`: mirror back to origin.<br><br>* `Async`: redirect back to origin.<br><br><br>Parent node: `Redirect` |
|FetchSourceOnRedirect |Boolean |No |false |Whether to pull data from the configured origin after redirection. The values are described as follows:<br><br><br>* `true`: Pull data from the configured origin after redirection.<br><br>* `false`: Do not pull data from the configured origin after redirection.<br><br><br>Parent node: `Redirect` |
|FetchSourceOnRedirectWithQuery |Boolean |No |false |Whether to carry request parameters when pulling data after redirection; if not configured, inherits PassQuery setting:<br><br><br>* `true`: carry request parameters.<br><br>* `false`: no request parameters carried.<br><br><br>Parent node: `Redirect` |
|PublicSource |Object |No |\- |Backsource address configuration when the origin is a public bucket. For details, please refer to the **PublicSource** below.<br><br>Parent node: `Redirect` |
|PrivateSource |Object |No |\- |Back\-to\-origin address configuration for private buckets as source stations. For details, see the following **PrivateSource**.<br><br>Parent node: `Redirect` |
|PassQuery |Boolean |No |true |Whether to include request parameters when executing redirect or mirror origin rules. The options are as follows:<br><br><br>* `true`: include request parameters.<br><br>* `false`: do not include request parameters.<br><br><br>> **warning**<br><br><br>> Even if set to `true`, Query parameters related to TOS authentication will not be included.<br><br><br>Parent node: `Redirect` |
|FollowRedirect |Boolean |No |true |If the mirror origin response is a 3xx status, whether to continue redirecting to the specified Location to fetch data. The options are as follows:<br><br><br>* `true`: TOS will continue to request the address corresponding to Location.<br><br>* `false`: TOS will return 302.<br><br><br>Parent node: `Redirect` |
|MirrorHeader |Object |No |\- |Header carried when specifying the image origin fallback.<br><br>Parent node: Redirect |
|PassAll |Boolean |No |true |Whether to forward all HTTP headers to the origin server. The options are as follows:<br><br><br>* `true`: forward all HTTP headers to the origin server.<br><br>* `false`: do not forward all HTTP headers to the origin server.<br><br><br>The following HTTP header types do not support forwarding:<br><br><br>* `Host`<br><br>* `Content-Length`<br><br>* `Date`<br><br>* `Authorization`<br><br><br>Parent node: `MirrorHeader` |
|Pass |Array |Not supported |["aaa", "bbb"] |Pass the specified header to the origin server.<br><br>Limit: maximum quantity 64.<br><br>Parent node: `MirrorHeader` |
|Remove |Array |No |["xxx", "yyy"] |Prohibit forwarding specified headers to the origin server.<br><br>Limit: maximum quantity 64.<br><br>Parent node: `MirrorHeader` |
|Transform |Object |No |\- |Defines the transformation of the object name for the origin request.<br><br>Parent node: `Redirect` |
|WithKeyPrefix |String |No |addtional\-key\-prefix |Add a prefix before the object name when requesting the origin server.<br><br>Limit: supports up to 512 characters.<br><br>Parent node: `Transform` |
|WithKeySuffix |String |No |addtional\-key\-suffix |A suffix added after the object name when requesting the origin server.<br><br>Limit: supports up to 512 characters.<br><br>Parent node: `Transform` |
|ReplaceKeyPrefix |Object |No |\- |Replace the object name prefix when requesting the origin server.<br><br>Parent node: `Transform` |
|KeyPrefix |String |No |key\-prefix |When requesting the origin, the object name prefix to be replaced.<br><br>Limit: up to 512 characters supported.<br><br>Parent node: `ReplaceKeyPrefix` |
|ReplaceWith |String |No |replace\-with |The value after replacing the object name prefix when requesting the origin server.<br><br>Limit: supports up to 512 characters.<br><br>Parent node: `ReplaceKeyPrefix` |

**PublicSource**

|**Name** |**Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|
|PublicSource |Object |No |\- |Origin address configuration for public buckets.<br><br>Parent node: `Redirect` |
|SourceEndpoint |Object |No |\- |Publicly accessible source endpoint address.<br><br>Parent node: `PublicSource`<br><br>> **tip**<br><br><br>> Required when the origin is a public bucket.<br> |
|Primary |Array |No |["http://abc.123/"] |Origin site address.<br><br>Limit: maximum length 255, supports up to 5 origin addresses.<br><br>Parent node: `SourceEndpoint`<br><br>The origin will prioritize selecting the source from this configuration. |
|Follower |Array |No |["http://abc.456/"] |Origin server address.<br><br>Limit: maximum length 255, supports up to 5 origin addresses.<br><br>Parent node: `SourceEndpoint`<br><br>Select the origin from this configuration when all origin retrievals in Primary fail. |

**PrivateSource**

|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|PrivateSource |Object |No |\- |Configure the back\-to\-origin address when the origin is a private bucket.<br><br>Parent node: `Redirect` |
|SourceEndpoint |Object |No |\- |Origin server fallback address configuration for private buckets.<br><br>Parent node: `PrivateSource` |
|Primary |Array |No |\- |Requested origin address, supports up to 5 origin addresses.<br><br>Parent node: `SourceEndpoint`<br><br>> **tip**<br><br><br>> Required when the origin is a private bucket.<br> |
|Endpoint |String |No |http://s3.bj.bcebos.com |Access domain name of the origin service provider, excluding bucket name, maximum length 255.<br><br>Parent node: `Primary`<br><br>> **tip**<br><br><br>> Required when the origin is a private bucket.<br> |
|BucketName |String |No |bucket |Name of the origin bucket.<br><br>Parent node: `Primary`<br><br>> **tip**<br><br><br>> Required when the origin is a private bucket.<br> |
|CredentialProvider |Object |No |\- |Private origin authorization method.<br><br>Parent node: `Primary`<br><br>> **tip**<br><br><br>> Required when the origin is a private bucket.<br> |
|Role |String |No |ServiceRoleBackSourceAccessTOS |Name of AssumeRole, used only for authentication when accessing private buckets in TOS using AssumeRole.<br><br>Parent node: `CredentialProvider`<br><br>> **tip**<br><br><br>> Role authentication and AK/SK authentication are mutually exclusive; they cannot be set simultaneously.<br> |
|Region |String |No |cn\-beijing |Region of the origin bucket; required when using AK/SK authentication.<br><br>Parent node: `CredentialProvider` |
|StaticCredential |Object |No |\- |Authenticate using AK/SK method.<br><br>Parent node: `CredentialProvider`<br><br>> **tip**<br><br><br>> Choose either AK/SK authentication or Role authentication; these cannot be set simultaneously.<br> |
|StorageVendor |String |No |S3 |The options for origin service providers are as follows:<br><br><br>* `BOS`: Baidu Cloud.<br><br>* `S3`: Other S3 protocol cloud providers.<br><br><br>Parent node: `StaticCredential` |
|AK |String |No |AKLTNDk3NDMxY2NmNzNhNGNiN\*\*\*\* |The AccessKey ID of the origin bucket, required when using AK/SK authentication.<br><br>Parent node: `StaticCredential` |
|SK |String |No |AADFSDfdsfa3ewdr23==d\*\*\*\* |SecretKey of the origin bucket, required when using AK/SK authentication.<br><br>Parent node: `StaticCredential` |
|SKEncryptType |String |No |AES256 |The encryption method used by SecretKey. Values are as follows:<br><br><br>* Empty: SecretKey is in plain text. After receiving the SecretKey, the server encrypts and stores it.<br><br>* AES256: SecretKey is encrypted with the AES256 algorithm on the server side. After receiving the SecretKey, the server parses it and stores it in encrypted form.<br><br>   > **tip**<br>   <br><br>   > Since the initial creation of the origin rule uses AES256 to encrypt the SecretKey, when modifying the origin rule without changing the `SecretKey` parameter, the SecretKey must first be decrypted before being re\-encrypted and stored.<br>   <br><br>   > Therefore, you can set `SKEncryptType` to `AES256` only when modifying other parameters without changing the `SecretKey` parameter by calling the PutBucketMirrorBack interface to update the origin rule.<br>   <br><br>Parent node: `StaticCredential` |

## Response headers

This request returns public response headers, see [public parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

## Response body elements

This response does not use message elements.

## Sample request

* **Sample request 1: origin is a public bucket**

   ```JSON
   PUT /?mirror HTTP/1.1
   Host: bucketname.tos-ap-southeast-1.bytepluses.com
   Date: Fri, 30 Jul 2021 08:05:36 +0000
   Authorization: authorization string
   {
       "Rules":[{
           "ID":"xxx",
           "Condition":{
               "HttpCode":404,
               "KeyPrefix":"prefix"
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

* **Sample request 2: origin is a TOS private bucket**

   ```JSON
   PUT /?mirror HTTP/1.1
   Host: bucketname.tos-ap-southeast-1.bytepluses.com
   Date: Fri, 30 Jul 2021 08:05:36 +0000
   Authorization: authorization string
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

* **Sample request 3: origin is a private bucket from other S3\-compatible cloud providers**

   ```JSON
   PUT /?mirror HTTP/1.1
   Host: bucketname.tos-ap-southeast-1.bytepluses.com
   Date: Fri, 30 Jul 2021 08:05:36 +0000
   Authorization: authorization string
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
                           "Endpoint": "http://s3.com",
                            "BucketName": "bucket",  
                            "CredentialProvider": {
                                "Region": "cn-beijing",         
                                "StaticCredential": {
                                      "StorageVendor": "S3",
                                       "AK": "AKLTNDk3NDMxY2NmNzNhNGNiN****", 
                                       "SK":"AADFSDfdsfa3ewdr23==d****"
                                }
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

## Sample response

```JSON
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
```
