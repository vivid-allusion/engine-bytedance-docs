---
title: "Signature Authentication and Usage Examples"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Signature_Authentication_Usage_Examples"
---

You can perform operations on memory collection through API calls. Before calling the relevant API operations, you must complete the following steps.

<span id="0b6a5b9b"></span>
# Prerequisites

You have registered an account and activated the related service as instructed in [Registering an account and activating the service](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

<span id="f51ca890"></span>
## **Obtain an access key**

Before calling the API operations for managing memory collection, make sure that you have generated an access key. An access key consists of an access key ID and a secret access key. The access key ID is used for user identification, and the secret access key is used for access key authentication. Please keep them safe.

You can perform the following steps to obtain an access key. For more information, refer to [Managing access keys](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey).


1. Click your username in the top\-right corner and select from the drop\-down IAM menu.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71cc6160d2004376b468efcc1fb0fbbd~tplv-goo7wpa0wc-image.image) </span>

2. Click on "Access Key Management" in the right \- hand form to navigate to the Key list page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d43128d6ddf47f6baad86bc37dd4a3c~tplv-goo7wpa0wc-image.image) </span>

3. Click Create Access Key to generate an access key. You can use the access key as credentials for calling API operations.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8bb9aa5cb8354ddf849c7c82f7ec4fda~tplv-goo7wpa0wc-image.image) </span>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For security reasons, we recommend that you create a sub\-account and use the access key generated under the sub\-account.</div>


<span id="7c7c696d"></span>
# **Signature authentication**

A signature is a computed coded string in an API request that is used for authentication and protection against data tampering.

<span id="96bcffdb"></span>
## **Can I use it all the time after I get the signature?** 

Unlike ak and sk, the signature of each request is independent and temporary, and a signature can only be used for a specific request once and cannot be used for a long time.

<span id="8fe536f6"></span>
## **What is the calculation of the signature?** 

The signature is computed by the signature generation function prepare_request based on the following parameters:


|**parameter** |**effect** |
|---|---|
|Method (request method) |Affects signature calculations, such as GET, POST |
|Path (API request path) |For example "/api/memory/collection/create" |
|AK (Access Key) |Identify the API caller |
|SK (Secret Key) |For HMAC\-SHA256 calculation of signatures (confidential) |
|Params (query parameter) |Applicable to GET requests, etc. |
|Data (request body) |Applicable to POST, PUT requests |


The specific code of each language of the signature generation function is described below. (For details on generating signatures through source code, please refer to [Signature Authentication Methods](https://www.volcengine.com/docs/6369/185600). For details on generating signatures through the SDK, please refer to [SDK Overview](https://www.volcengine.com/docs/6369/156029).)

<span id="66665e08"></span>
## Python language SDK generates signature


1. Install the Volcano Engine package.

   ```Python
   pip install --upgrade volcengine
   ```
   

2. Generate a signature.

   ```Python
   import json
   import requests
   from volcengine.base.Request import Request
   from volcengine.Credentials import Credentials
   from volcengine.auth.SignerV4 import SignerV4
   
   
   AK = "xxxxx" 
   SK = "xxxxx" 
   Domain = "api-knowledgebase.mlp.cn-hongkong.bytepluses.com"
   
   
   def prepare_request(method, path, ak, sk, data=None):
     r = Request()
     r.set_shema("http")
     r.set_method(method)
     r.set_host(Domain)
     r.set_path(path)
   
   
     if data is not None:
       r.set_body(json.dumps(data))
     credentials = Credentials(ak, sk, 'air', 'cn-north-1')
     SignerV4.sign(r, credentials)
     return r
   
   
   def internal_request(method, api, payload, params=None):
   
   
     req = prepare_request(
                           method = method,
                           path = api,
                           ak = AK,
                           sk = SK,
                           data = payload)
   
   
     r = requests.request(method=req.method,
             url="{}://{}{}".format(req.schema, req.host, req.path),
             headers=req.headers,
             data=req.body,
             params=params,
         )
     return r
   ```
   


<span id="2c697384"></span>
## GO language SDK generates signature


1. Install the Volcano Engine package.

   ```Go
   go get -u github.com/volcengine/volc-sdk-golang
   ```
   

2. Generate a signature.

   ```Go
   package main
   
   import (
           "bytes"
           "fmt"
           "net/http"
           "net/url"
           "strings"
           "io/ioutil"
           "github.com/volcengine/volc-sdk-golang/base"
   )
   
   const (
           testAk = "***"
           testSk = "***"
   )
   
   func PrepareRequest(method string, path string, ak string, sk string, query url.Values, body []byte) *http.Request {
           u := url.URL{
                   Scheme:   "https",
                   Host:     "api-knowledgebase.mlp.cn-hongkong.bytepluses.com",
                   Path:     "/api/memory/search",
           }
           if query != nil {
                   u.RawQuery = query.Encode()
           }
           req, _ := http.NewRequest(strings.ToUpper(method), u.String(), bytes.NewReader(body))
           req.Header.Add("Accept", "application/json")
           req.Header.Add("Content-Type", "application/json")
           req.Header.Add("Host", "api-knowledgebase.mlp.cn-hongkong.bytepluses.com")
           credential := base.Credentials{
                   AccessKeyID:     ak,
                   SecretAccessKey: sk,
                   Service:         "air",
                   Region:          "cn-north-1",
           }
           req = credential.Sign(req)
           return req
   }
   ```
   


<span id="befeda84"></span>
## Java Language SDK Generate Signature


1. Install the Volcano Engine package.

   ```Java
    <dependency>
       <groupId>com.volcengine</groupId>
       <artifactId>volc-sdk-java</artifactId>
       <version>Latest version</version>
   </dependency> 
   ```
   

2. Generate signature

   ```Java
   package javaTest;
   
   import java.util.List;
   
   import org.apache.http.HttpResponse;
   import org.apache.http.NameValuePair;
   import org.apache.http.client.HttpClient;
   import org.apache.http.client.config.RequestConfig;
   import org.apache.http.client.utils.URIBuilder;
   import org.apache.http.entity.StringEntity;
   import org.apache.http.impl.client.HttpClients;
   import org.apache.http.util.EntityUtils;
   
   import com.volcengine.auth.ISignerV4;
   import com.volcengine.auth.impl.SignerV4Impl;
   import com.volcengine.model.Credentials;
   import com.volcengine.service.SignableRequest;
   
   public class sign {
     public static SignableRequest prepareRequest(String host, String path, String method, List<NameValuePair> params, String body, String ak, String sk) throws Exception {
       SignableRequest request = new SignableRequest();
       request.setMethod(method);
       request.setHeader("Accept", "application/json");
       request.setHeader("Content-Type", "application/json");
       request.setHeader("Host", "api-knowledgebase.mlp.cn-hongkong.bytepluses.com");
       request.setEntity(new StringEntity(body, "utf-8"));
   
       URIBuilder builder = request.getUriBuilder();
       builder.setScheme("https");
       builder.setHost(host);
       builder.setPath(path);
       if (params != null) {
         builder.setParameters(params);
       }
   
       RequestConfig requestConfig = RequestConfig.custom().setSocketTimeout(5000).setConnectTimeout(2000).build();
       request.setConfig(requestConfig);
   
       Credentials credentials = new Credentials("cn-north-1", "air");
       credentials.setAccessKeyID(ak);
       credentials.setSecretAccessKey(sk);
   
       ISignerV4 ISigner = new SignerV4Impl();
       ISigner.sign(request, credentials);
   
       return request;
     }
   ```
   


<span id="b8eecd67"></span>
## Node.js language SDK generates signature


1. Install the Volcano Engine package.


```TypeScript
pnpm add @volcengine/openapi
```



2. Generate signature


Note: Call function `signer` After generating the request body header, inject the generated header into the user request function.

```TypeScript
import { Signer } from '@volcengine/openapi';
import type { RequestObj } from '@volcengine/openapi/lib/base/types';

interface Options { 
      pathname: string 
      method: 'GET' | 'POST' 
      body?: string // Specify a JSON string (required only for a POST request). 
      region: 'cn-hongkong' 
      params?: Record<string, any> // Required only for a GET request. 
    } 

function signer({ pathname, method, body, region, params }: Options) {
  const requestObj: RequestObj = {
   region, 
   headers: {
     Accept: 'application/json',
     'Content-type': 'application/json'
   },
   method,
   body,
   pathname,
   params,
 }

  const signer = new Signer(requestObj, 'air')
    signer.addAuthorization({
      accessKeyId: 'ak', // Replace it with your own access key ID. 
      secretKey: 'sk', // Replace it with your own secret access key. 
  })
  return requestObj.headers
}
```


<span id="9cde7a44"></span>
## C #language/PHP language, through the source code, generate the signature

C #and PHP languages do not currently provide a way for the SDK to generate signatures. You can refer to the corresponding source code to generate signatures:

C #: https://github.com/volcengine/volc\-openapi\-demos/blob/main/signature/csharp/Program.cs

PHP: https://github.com/volcengine/volc\-openapi\-demos/blob/main/signature/php/sign.php

<span id="3c2ae242"></span>
# Viking Memory API Call Example

<span id="7bb3bb49"></span>
## Python language call example

After obtaining the AK/SK key, you can **signature generation function** and **specific interface call.**  Write it into the same script file. Here is the practical process of docking the signature generation logic with the creation of the memory collection. Take Python code as an example:

Note: The'ak/sk 'parameter in the main function is the ak/sk you just applied for.

```Python
import json
import requests
from volcengine.base.Request import Request
from volcengine.Credentials import Credentials
from volcengine.auth.SignerV4 import SignerV4


AK = "xxxxx" 
SK = "xxxxx" 
Domain = "api-knowledgebase.mlp.cn-hongkong.bytepluses.com"


def prepare_request(method, path, ak, sk, data=None):
  r = Request()
  r.set_shema("http")
  r.set_method(method)
  r.set_host(Domain)
  r.set_path(path)


  if data is not None:
    r.set_body(json.dumps(data))
  credentials = Credentials(ak, sk, 'air', 'cn-north-1')
  SignerV4.sign(r, credentials)
  return r


def internal_request(method, api, payload, params=None):


  req = prepare_request(
                        method = method,
                        path = api,
                        ak = AK,
                        sk = SK,
                        data = payload)


  r = requests.request(method=req.method,
          url="{}://{}{}".format(req.schema, req.host, req.path),
          headers=req.headers,
          data=req.body,
          params=params,
      )
  return r
  
path = '/api/memory/collection/create'
playload = {
    'CollectionName': "my_first_memory_collectionaaa",
    'Description': "test description",
    'BuiltinEventTypes': ["sys_event_v1"],
    'BuiltinProfileTypes': ["sys_profile_v1"],
}
rsp = internal_request('POST', path, playload)
print(rsp.json())
```
