---
title: "Preparation"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Preparation"
---

<span id="preparation"></span>
# Preparation

Before you can interact with the Vector Database API, you must complete a few essential authentication prerequisites. This guide provides step\-by\-step instructions for registering an account and obtaining an access key. It also includes ready\-to\-use signature generation functions for Python, Go, Java, and Node.js, enabling you to quickly authenticate your API requests and begin development.

<span id="09a84148"></span>
# 1. Register an account and enable the service

Register an account and enable the related service as instructed in [Account registration and service activation](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

<span id="61ac89a5"></span>
# 2. Obtain an access key

Before using the capabilities of Vector Database, make sure that you have generated an access key.

An access key consists of an access key ID and a secret access key. The access key ID is used for user identification and the secret access key is used for access key authentication. Please keep them safe.

You can perform the following steps to obtain an access key.


1. Click your username in the top\-right corner and select Account Management from the drop\-down menu.

2. Click your username in the top\-right corner and select [UI_ELEMENT_NAME] from the drop\-down IAM menu.

3. Click Create Access Key to generate an access key. You can use the access key as credentials for calling API operations.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a14ed356a46744fbbb836a2384740e9c~tplv-goo7wpa0wc-image.image) </span>

<span id="dffb879c"></span>
# 3. Construct and save a signature generation function (in Python)

<span id="9a77efdd"></span>
## **What is a signature?** 

A signature is an encoded string calculated in an API request. Signatures are used to authenticate identities and prevent data tampering.

<span id="43b8a1a2"></span>
## **Are signatures permanently valid?** 

Unlike access keys, the signature in each request is independent and temporary. A signature is valid only for the specific request in which it is included.

<span id="6a70cf76"></span>
## **How is a signature calculated?** 

A signature is calculated using the prepare_request signature generation function based on the following parameters.


|**Parameter** |**Description** |
|---|---|
|method |The method to be used for signature calculation, such as GET and POST. |
|path |The API request path. Example: /api/collection/create. |
|ak |The access key ID, which identifies the user who initiates the API call. |
|sk |The secret access key, which is to be used for HMAC\-SHA256 signature calculation. |
|params |The parameters you want to query; suitable for GET requests. |
|data |The request body; suitable for POST and PUT requests. |
|doseq |A flag that determines how list\-type query parameters are serialized. |


For information about how to construct the prepare_request signature generation function in multiple programming languages, refer to the sample code in the "4. Construct the prepare_request function in multiple programming languages" section.

<span id="ca66736c"></span>
## How do I generate a signature to perform operations in Vector Database?

The "4. Construct the prepare_request function in multiple programming languages" section provides sample code for this function in several languages. The following code describes how to use the prepare_request function to generate a signature and create a collection in Python, as an example.


1. **Save the function**: Save the following code to a local file named volc_auth.py. This file is used to generate a signature for an API request. It is intended to be imported into code rather than run directly, and requires no changes.

2. **Install the BytePlus SDK for Python**: On your terminal, enter `pip install volcengine` to install the BytePlus SDK for Python.


```Python
# volc_auth.py 

import json 
import sys 

from volcengine.auth.SignerV4 import SignerV4 
from volcengine.base.Request import Request 
from volcengine.Credentials import Credentials 


def prepare_request(method, path, ak, sk, params=None, data=None, doseq=0): 
    if params: 
        for key in params: 
            if ( 
                type(params[key]) == int 
                or type(params[key]) == float 
                or type(params[key]) == bool 
            ): 
                params[key] = str(params[key]) 
            elif sys.version_info[0] != 3: 
                if type(params[key]) == unicode: 
                    params[key] = params[key].encode("utf-8") 
            elif type(params[key]) == list: 
                if not doseq: 
                    params[key] = ",".join(params[key]) 
    r = Request() 
    r.set_shema("https") 
    r.set_method(method) 
    r.set_connection_timeout(10) 
    r.set_socket_timeout(10) 
    mheaders = { 
        "Accept": "application/json", 
        "Content-Type": "application/json", 
        "Host": "api-vikingdb.mlp.ap-mya.byteplus.com", 
    } 
    r.set_headers(mheaders) 
    if params: 
        r.set_query(params) 
    r.set_host("api-vikingdb.mlp.ap-mya.byteplus.com") 
    r.set_path(path) 
    if data is not None: 
        r.set_body(json.dumps(data)) 
    # Generate a signature. 
    credentials = Credentials(ak, sk, "air", "ap-southeast-1") 
    SignerV4.sign(r, credentials) 
    return r
```



3. Run the code: Save the following code to a local file in the same directory as the volc_auth.py file. Specify your access key ID and secret access key at the beginning of the code. After you run the code, a collection named "your_collection" is created in Vector Database. Now, you have generated a signature and performed an operation in Vector Database. The following code contains a more detailed explanation of how it works.


```Python
import requests 
from volc_auth import prepare_request 
# The prepare_request signature generation function in the volc_auth.py file is imported. 

AK = "Specify your access key ID here (do not delete the quotation marks)" 
SK = "Specify your secret access key here (do not delete the quotation marks)" 

DOMAIN = "api-vikingdb.mlp.ap-mya.byteplus.com" 

# Create a collection. 
request_params = { 
    "collection_name": "your_collection", 
    "description": "This is a use case that describes how to use the prepare_request function to generate a signature and create a collection in Vector Databese." 
    # Set a primary key. 
    "primary_key": "id", 
    # Specify fields. 
    "fields": [ 
        { 
            "field_name": "id", 
            "field_type": "int64", 
            "default_val": 0, 
        }, 
        {"field_name": "vector_field", "field_type": "vector", "dim": 64} 
        # Specify other fields as you need. 
    ], 
} 

# Call the prepare_request function to generate a request and add a signature. 
info_collection_req = prepare_request( 
    method="POST", 
    path="/api/collection/create", 
    ak=AK, 
    sk=SK, 
    data=request_params, 
) 
# Complete the request. 
r = requests.request( 
    method=info_collection_req.method, 
    url="https://{}{}".format(DOMAIN, info_collection_req.path), 
    headers=info_collection_req.headers, 
    params=info_collection_req.query, 
    data=info_collection_req.body, 
) 

# Print the response. 
print(r.text)
```



4. Code explanation: At the beginning of the preceding code, the "from volc_auth import prepare_request" command imports the prepare_request function from the volc_auth.py file for generating a signature. The `info_collection_req` object contains the generated signature in its headers. The signature is passed in through "headers=info_collection_req.headers".

5. More operations: After you generate a signature by using the prepare_request function, you can perform more operations. For more information, refer to Core process. You can also learn how to construct the prepare_request function in other programming languages.


<span id="89945eb3"></span>
# 4. Construct the prepare_request function in multiple programming languages

Sample code for constructing the signature generation function in several programming languages (including Python, Go, Java, and Node.js) is provided below for your reference.

<span id="86f1288f"></span>
## Signature generation by using the BytePlus SDK for Python


1. Install the BytePlus SDK for Python.

   `pip install volcengine`

2. Generate a signature.

   ```Python
   # volc_auth.py 
   
   import json 
   import sys 
   
   from volcengine.auth.SignerV4 import SignerV4 
   from volcengine.base.Request import Request 
   from volcengine.Credentials import Credentials 
   
   
   def prepare_request(method, path, ak, sk, params=None, data=None, doseq=0): 
       if params: 
           for key in params: 
               if ( 
                   type(params[key]) == int 
                   or type(params[key]) == float 
                   or type(params[key]) == bool 
               ): 
                   params[key] = str(params[key]) 
               elif sys.version_info[0] != 3: 
                   if type(params[key]) == unicode: 
                       params[key] = params[key].encode("utf-8") 
               elif type(params[key]) == list: 
                   if not doseq: 
                       params[key] = ",".join(params[key]) 
       r = Request() 
       r.set_shema("https") 
       r.set_method(method) 
       r.set_connection_timeout(10) 
       r.set_socket_timeout(10) 
       mheaders = { 
           "Accept": "application/json", 
           "Content-Type": "application/json", 
           "Host": "api-vikingdb.mlp.ap-mya.byteplus.com", 
       } 
       r.set_headers(mheaders) 
       if params: 
           r.set_query(params) 
       r.set_host("api-vikingdb.mlp.ap-mya.byteplus.com") 
       r.set_path(path) 
       if data is not None: 
           r.set_body(json.dumps(data)) 
       # Generate a signature. 
       credentials = Credentials(ak, sk, "air", "ap-southeast-1") 
       SignerV4.sign(r, credentials) 
       return r
   ```
   


<span id="3b6baa93"></span>
## Signature generation by using the BytePlus SDK for Go


1. Install the BytePlus SDK for Go.

   `go get -u github.com/volcengine/volc-sdk-golang`

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
                   Host:     "api-vikingdb.mlp.ap-mya.byteplus.com", 
                   Path:     path, 
           } 
           if query != nil { 
                   u.RawQuery = query.Encode() 
           } 
           req, _ := http.NewRequest(strings.ToUpper(method), u.String(), bytes.NewReader(body)) 
           req.Header.Add("Accept", "application/json") 
           req.Header.Add("Content-Type", "application/json") 
           req.Header.Add("Host", "api-vikingdb.mlp.ap-mya.byteplus.com") 
           credential := base.Credentials{ 
                   AccessKeyID:     ak, 
                   SecretAccessKey: sk, 
                   Service:         "air", 
                   Region:          "ap-southeast-1", 
           } 
           req = credential.Sign(req) 
           return req 
   } 
   
   func main() { 
           body := []byte(`{"collection_name":"test_no_vector_collection"}`) 
           req := PrepareRequest("GET", "/api/collection/info", testAk, testSk, nil, body) 
           fmt.Printf("%+v\n", req) 
           // Send a request 
           client := &http.Client{} 
           resp, err := client.Do(req) 
           if err != nil { 
                   fmt.Println("Error sending request:", err) 
                   return 
           } 
           defer resp.Body.Close() 
   
           rb, _ := ioutil.ReadAll(resp.Body) 
           fmt.Println(string(rb)) 
   }
   ```
   


<span id="20ed680a"></span>
## Signature generation by using the BytePlus SDK for Java


1. Install the BytePlus SDK for Java.

   ```Java
    <dependency> 
       <groupId>com.volcengine</groupId> 
       <artifactId>volc-sdk-java</artifactId> 
       <version>Latest version</version> 
   </dependency>
   ```
   


You can find the latest version number in the ["Obtain and install the SDK" section in the README file at GitHub](https://github.com/volcengine/volc-sdk-java?tab=readme-ov-file), as shown in the figure on the right.

You can directly copy the latest version number from this section, such as 1.0.206, to your code.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6bd75930b6c84134b5c14fd9c9843cdb~tplv-goo7wpa0wc-image.image) </span>


2. Generate a signature.

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
       request.setHeader("Host", host); 
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
   
       Credentials credentials = new Credentials("ap-southeast-1", "air"); 
       credentials.setAccessKeyID(ak); 
       credentials.setSecretAccessKey(sk); 
   
       // Generate a signature. 
       ISignerV4 ISigner = new SignerV4Impl(); 
       ISigner.sign(request, credentials); 
   
       return request; 
     } 
   
     public static void main(String[] args) throws Exception { 
       String host = "api-vikingdb.mlp.ap-mya.byteplus.com"; 
       String path = "/api/collection/info"; 
       String method = "GET"; 
       String query = "collection_name = test_collection"; 
       String body = null; 
       String ak = "your_ak_on_volcengine"; // Replace with your own access key ID. 
       String sk ="your_sk_on_volcengine"; // Replace with your own secret access key. 
       
       SignableRequest request = prepareRequest(host, path, method, null, body, ak, sk); 
       System.out.println(request.getURI()); 
   
       HttpClient client = HttpClients.createDefault(); 
       HttpResponse response = client.execute(request); 
   
       int statusCode = response.getStatusLine().getStatusCode(); 
       String content = EntityUtils.toString(response.getEntity()); 
   
       System.out.println(statusCode); 
       System.out.println(content); 
     } 
   }
   ```
   


<span id="16c897fc"></span>
## Signature generation by using the BytePlus SDK for Node.js


1. Install the BytePlus SDK for Node.js.


```TypeScript
pnpm add @volcengine/openapi
```



2. Generate a signature.


```TypeScript
import { Signer } from '@volcengine/openapi'; 
import type { RequestObj } from '@volcengine/openapi/lib/base/types'; 

interface Options { 
  pathname: string 
  method: 'GET' | 'POST' 
  body?: string // Specify a JSON string (required only for a POST request). 
  region: 'cn-beijing'
  params?: Record<string, any> // Required only for a GET request. 
} 

function signer({ pathname, method, body, region, params }: Options) { 
  const requestObj: RequestObj = { 
   region, 
   headers: { 
     Accept: 'application/json', 
     'Content-Type': 'application/json' 
   }, 
   method, 
   body, 
   pathname, 
   params, 
 } 

  const signer = new Signer(requestObj, 'air') 
    signer.addAuthorization({ 
      accessKeyId: 'ak', // Replace with your own access key ID. 
      secretKey: 'sk', // Replace with your own secret access key. 
 }) 
 return requestObj.headers 
}
```


After the signer function is called to generate the request headers, the generated header is injected into the request function.
