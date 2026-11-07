---
title: "Signature authentication and examples"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/Signature_authentication"
---

The Knowledge Base API supports three authentication methods: Knowledge Base API key, BytePlus API key, and AK/SK. Each method has a different credential source, request header format, and API scope. Select the method that matches your use case. This topic explains how to obtain each credential and provides multi\-language examples for AK/SK signature authentication and API requests.


---



<span id="e7164f52"></span>
# Authentication methods overview


|**Authentication method** |**Credential source** |**Request header format** |**Supported APIs** |
|---|---|---|---|
|Knowledge Base API key (`VIKING_API_KEY`) |The **API Key** page in ModelArk Knowledge Center |`Authorization: Bearer <VIKING_API_KEY>` |Data\-plane APIs, plus `service/chat` and `chat/completions` |
|BytePlus API key |API access keys for your BytePlus account |`Authorization: Bearer <API_KEY_SECRET>` |Data\-plane APIs only, such as `search` and `doc/add` |
|AK/SK signature authentication |API access keys for your BytePlus account |Signature V4 (HMAC\-SHA256) |All APIs, including control\-plane and data\-plane APIs |


> A Knowledge Base API key is created in ModelArk Knowledge Center. A BytePlus API key and an AK/SK pair are created on the **API Access Key** page in the BytePlus console. Although the two API key methods use the same request header format, their credential sources and supported APIs are different. Do not mix them.



---



<span id="7ab62b10"></span>
# 1. Knowledge Base API key

A Knowledge Base API key is created in ModelArk Knowledge Center and can be bound to specific knowledge bases or knowledge services as needed. You can create up to 100 API keys in a single project.

Log in to the BytePlus console and open VikingDB.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59f36befedbf43ada8ebcbc2193ebcb8~tplv-goo7wpa0wc-image.image) </span>

On the service landing page locate the Knowledge Base card and click Get started the service landing page locate the Knowledge Base card and click Get started.

In the upper\-right corner of the Knowledge Center page, click **API Key**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7651227e745844b89c4e8294d1d05132~tplv-goo7wpa0wc-image.image) </span>

On the **API Key** page, create an API key and bind it to the required knowledge base or knowledge service.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9cc2338c4d054ed6aa84ad8c8f3a74bc~tplv-goo7wpa0wc-image.image) </span>

When calling an API that supports Knowledge Base API key authentication, include the following header:

```HTTP
Authorization: Bearer <VIKING_API_KEY>
```


> A Knowledge Base API key supports Knowledge Base data\-plane APIs, as well as the `service/chat` and `chat/completions` APIs. Follow the principle of least privilege when configuring its binding scope, and keep the key secure.



---



<span id="c78ff946"></span>
# 2. BytePlus API key

A BytePlus API key and an AK/SK pair are created from the same entry point: the **IAM** page in the BytePlus console.

Log in to the BytePlus console.

In the upper\-right corner of the console, hover over your profile picture, and then click **IAM.** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ab6be387c2c4c6f985f91594f1df016~tplv-goo7wpa0wc-image.image) </span>

On the **IAM** page, locate the **Access key management** section, click **Create API Key**, and complete the creation process as prompted.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36209defcd3841078b09074affab109f~tplv-goo7wpa0wc-image.image) </span>

After the API key is created, obtain its API Key Secret. When calling a supported data\-plane API, include the following header:

```HTTP
Authorization: Bearer <API_KEY_SECRET>
```


> A BytePlus API key supports Knowledge Base data\-plane APIs only. It does not support control\-plane APIs. Keep the API Key Secret secure, and do not commit it to a code repository or expose it in client\-side code.



---



<span id="c60a13de"></span>
# 3. AK/SK signature authentication

AK/SK signature authentication supports all Knowledge Base control\-plane and data\-plane APIs. This section explains how to obtain an AK/SK pair, configure the API host, generate a signature, and call the APIs.

<span id="515752ef"></span>
## Obtain an AK/SK pair

An AK/SK pair consists of:

**Access Key ID (AK):**  Identifies the API caller.

**Secret Access Key (SK):**  Authenticates the API caller and must be kept confidential.

To create an AK/SK pair:

Log in to the BytePlus console.

In the upper\-right corner of the console, hover over your profile picture, and then click **IAM.** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa15464f61ee4df79b3a03692aa3494e~tplv-goo7wpa0wc-image.image) </span>

On the **IAM** page, locate the **Access key management** section and click **Create Access Key**. After creation, use the Access Key ID as the AK and the Secret Access Key as the SK.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/91901bc13f744476939cf1675c455d96~tplv-goo7wpa0wc-image.image) </span>

To protect your data and account, keep the AK/SK pair secure and do not disclose it. Because a primary account has broad permissions, we recommend creating a sub\-account and using an AK/SK pair generated for that sub\-account. For more information, see [Managing access keys](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey).

<span id="5d5fdfee"></span>
## Host configuration

The Knowledge Base API is available in multiple regions. When making API requests, you need to use the correct host domain based on your region.

<span id="fea4c570"></span>
### Available regions


|Region |Host Domain |
|---|---|
|Hong Kong |[api-knowledgebase.mlp.cn-hongkong.bytepluses.com](http://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/) |
|Johor |[api-knowledgebase.mlp.ap-southeast-1.bytepluses.com](http://api-knowledgebase.mlp.ap-southeast-1.bytepluses.com/) |


<span id="80813a9d"></span>
### Usage notes

**Important:**  All code examples in the subsequent API documentation use the Hong Kong (HK) host by default. If you are using the Johor region, please replace the host domain accordingly in the example code.

A signature is a computed string included in an API request for authentication and protection against data tampering.

<span id="b0485d46"></span>
## Signature principles

<span id="a2184053"></span>
### Signature validity period

Unlike AK/SK, the signature for each request is independent and temporary. A signature can only be used for one specific request and cannot be used for long\-term use.

<span id="771ab11a"></span>
### Signature calculation method

The signature is calculated by the `prepare_request` function based on the following parameters:


|**Parameter** |**Description** |
|---|---|
|Method (request method) |Affects signature calculations, such as GET, POST |
|Path (API request path) |For example "/api/collection/create" |
|AK (Access Key) |Identifies the API caller |
|SK (Secret Key) |Used for HMAC\-SHA256 signature calculation (confidential) |
|Params (query parameter) |Applicable to GET requests, etc. |
|Data (request body) |Applicable to POST, PUT requests |
|Doseq (format control of query parameters) |Controls the format of query parameters |


<span id="e8df2a99"></span>
## Signature generation function example code

The signature generation function is shown below in several languages.

For details on generating signatures through source code, please refer to [Signature Authentication Methods](https://docs.byteplus.com/en/docs/ModelArk/1298459).

**Note on Host Configuration:**  The examples below use Hong Kong (HK) as the host. If you are using the Johor region, please replace the host accordingly:

Hong Kong: `api-knowledgebase.mlp.cn-hongkong.bytepluses.com`

Johor: `api-knowledgebase.mlp.ap-southeast-1.bytepluses.com`

<span id="4728472a"></span>
### Python

Install the BytePlus SDK package.

```Python
pip install volcengine
```


Generate the signature.

```Python
import json
import sys
import requests
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
            # elif sys.version_info[0] != 3: # In Python 3.x, this part of the code is not needed
            #     if type(params[key]) == unicode:
            #         params[key] = params[key].encode("utf-8")
            elif type(params[key]) == list:
                if not doseq:
                    params[key] = ",".join(params[key])
    r = Request()
    r.set_schema("https")
    r.set_method(method)
    r.set_connection_timeout(10)
    r.set_socket_timeout(10)
    mheaders = {
        "Accept": "application/json",
        "Content-Type": "application/json",
    }
    r.set_headers(mheaders)
    if params:
        r.set_query(params)
    r.set_path(path)
    if data is not None:
        r.set_body(json.dumps(data))
    # Generate signature
    credentials = Credentials(ak, sk, "air", "cn-hongkong")
    SignerV4.sign(r, credentials)
    return r
```


<span id="48818427"></span>
### Java

Install the BytePlus SDK package.

```Java
<dependency>
    <groupId>com.volcengine</groupId>
    <artifactId>volc-sdk-java</artifactId>
    <version>Latest version</version>
</dependency> 
```


Generate the signature.

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

    Credentials credentials = new Credentials("cn-hongkong", "air");
    credentials.setAccessKeyID(ak);
    credentials.setSecretAccessKey(sk);

    ISignerV4 ISigner = new SignerV4Impl();
    ISigner.sign(request, credentials);

    return request;
  }
```


<span id="31e3fa3f"></span>
### Go

Install the BytePlus SDK package.

```Go
go get -u github.com/volcengine/volc-sdk-golang
```


Generate the signature.

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
                Path:     "/api/knowledge/collection/search",
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
                Region:          "cn-hongkong",
        }
        req = credential.Sign(req)
        return req
}
```


<span id="8a6415a4"></span>
### Node.js

Install the BytePlus SDK package.

```JavaScript
pnpm add @volcengine/openapi
```


Generate the signature.

After calling the `signer` function to generate the request body header, inject the generated header into the user request function.

```JavaScript
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


<span id="ea7aa843"></span>
### C# / PHP

Currently, SDK signature generation methods for C# and PHP languages are not provided. You can refer to the corresponding source code to generate signatures. See the following examples for details.

<span id="8739e3f8"></span>
## AK/SK API request examples

<span id="3f35d65b"></span>
### Python

The following Python sample code integrates the signature generation logic and the knowledge base creation API. The sample code below provides a complete example of calling the knowledge base API, including signature generation, retrieval, generation, and parsing of streaming/non\-streaming results.

Please replace `ak` and `sk` in the main function with your own AK and SK, respectively.

```Python
import json
import requests
from volcengine.auth.SignerV4 import SignerV4
from volcengine.base.Request import Request
from volcengine.Credentials import Credentials

# Signature generation logic. 
def prepare_request(method, path, params=None, data=None, doseq=0): 
    # Create a request. 
    if params:
        for key in params:
            if (
                    isinstance(params[key], int)
                    or isinstance(params[key], float)
                    or isinstance(params[key], bool)
            ):
                params[key] = str(params[key])
            elif isinstance(params[key], list):
                if not doseq:
                    params[key] = ",".join(params[key])
    r = Request()
    r.set_schema("http")
    r.set_method(method)
    r.set_connection_timeout(10)
    r.set_socket_timeout(10)
    mheaders = {
        "Accept": "application/json",
        "Content-Type": "application/json",
        "Host": g_knowledge_base_domain,
        "V-Account-Id": account_id,
    }
    r.set_headers(mheaders)
    if params:
        r.set_query(params)
    r.set_host(g_knowledge_base_domain)
    r.set_path(path)
    if data is not None:
        r.set_body(json.dumps(data))
    # Generate a signature. 
    credentials = Credentials(ak, sk, "air", "cn-hongkong") 
    SignerV4.sign(r, credentials) 
    return r 

# Knowledge base creation logic. 
def create(): 
    # Request method for creating a knowledge base. 
    method = "POST" 
    # Request path for creating a knowledge base. 
    path = "/api/knowledge/collection/create" 
    # Parameters required for creating a knowledge base. 
    request_params = { 
        "name": "test", 
        "data_type": "unstructured_data", 
        "preprocessing": { 
            "chunking_strategy":"custom_balance", 
            "multi_modal":["image_ocr"] 
        }, 
        "index": { 
            "cpu_quota": 1, 
            "embedding_model": "bge-large-zh-and-m3", 
            "embedding_dimension": 2048, 
            "quant": "int8", 
            "index_type": "hnsw_hybrid" 
        }, 
    } 
    info_req = prepare_request(method=method, path=path, data=request_params)
    rsp = requests.request(
        method=info_req.method,
        url="https://{}{}".format(g_knowledge_base_domain, info_req.path),
        headers=info_req.headers,
        data=info_req.body
    )
    print(rsp.text)

if __name__ == "__main__": 
    ak = 'Your access key ID' 
    sk = 'Your secret access key' 
    g_knowledge_base_domain = "api-knowledgebase.mlp.cn-hongkong.bytepluses.com" 
    account_id = "Your BytePlus account ID" 
    # Call the function to create a knowledge base. 
    create()
```


<span id="8aa82e0e"></span>
### Java

The sample code below provides a complete example of calling the knowledge base API, including signature generation, retrieval, generation, and parsing of streaming/non\-streaming results.

Main.java

Unknown size

`your ak`: Your AK.

`your sk`: Your SK.

`your query`: Your query.

`your collection`: The name of the knowledge base, which you can find in the UI.

`default`: The project that the knowledge base belongs to, which you can find in the UI.

`your resource_id`: The ID of the knowledge base, which you can find in the UI.

`your model name`: Model name.

`your model version`: Model version.

<span id="18745156"></span>
### Go

The sample code below provides a complete example of calling the knowledge base API, including signature generation, retrieval, generation, and parsing of streaming/non\-streaming results.

main.go

Unknown size

`your ak`: Your AK.

`your sk`: Your SK.

`your query`: Your query.

`your collection`: The name of the knowledge base, which you can find in the UI.

`default`: The project that the knowledge base belongs to, which you can find in the UI.

`your resource ID`: Knowledge base ID, which can be obtained from the frontend interface.

`your model name`: Model name.

<span id="255c8d71"></span>
### C#

The sample code below provides an example of calling the knowledge base search interface, including signature generation and retrieval.

To run this example, replace the placeholders in the sample code with your knowledge base parameters.

`_ak`: Your AK.

`_sk`: Your SK.

`_path`: Interface path.

```C#
using System;
using System.Collections.Generic;
using System.Collections.Immutable;
using System.Collections.Specialized;
using System.IO;
using System.Linq;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Security.Cryptography;
using System.Text;
using System.Text.Json;
using System.Web;

class GitHubSign
{
    private readonly string _region;
    private readonly string _service;
    private readonly string _schema;
    private readonly string _host;
    private readonly string _path;
    private readonly string _ak;
    private readonly string _sk;

    private static readonly Encoding Utf8 = Encoding.UTF8;

    private readonly HttpClient _httpClient;

    public GitHubSign(string region, string service, string schema, string host, string path, string ak, string sk)
    {
        _region = region;
        _service = service;
        _schema = schema;
        _host = host;
        _path = path;
        _ak = ak;
        _sk = sk;
        _httpClient = new HttpClient();
    }

    public HttpResponseMessage Request(HttpMethod method, List<KeyValuePair<string, string>> queryList,
        byte[]? body, string contentType,
        DateTimeOffset date, string action, string version)
    {
        body ??= Array.Empty<byte>();
        if (string.IsNullOrWhiteSpace(contentType))
        {
            contentType = "application/x-www-form-urlencoded";
        }

        string xContentSha256 = ToHexString(HashSha256(body));
        string xDate = date.UtcDateTime.ToString("yyyyMMdd'T'HHmmss'Z'");
        string shortXDate = xDate[..8];
        string signHeader = "host;x-date;x-content-sha256;content-type";

        var realQueryList = new NameValueCollection();
        queryList.ForEach(s => realQueryList.Add(s.Key, s.Value));
        realQueryList.Add("Action", action);
        realQueryList.Add("Version", version);

        var query = string.Join("&", realQueryList.AllKeys.ToImmutableSortedSet().Select(key =>
        {
            var values = realQueryList.GetValues(key)?.ToImmutableSortedSet() ?? ImmutableSortedSet<string>.Empty;
            return string.Join("&",
                values.Select(value => $"{HttpUtility.UrlEncode(key)}={HttpUtility.UrlEncode(value)}"));
        }));
        string canonicalStringBuilder =
            $"{method}
" +
            $"{_path}
" +
            $"{query}
" +
            $"host:{_host}
" +
            $"x-date:{xDate}
" +
            $"x-content-sha256:{xContentSha256}
" +
            $"content-type:{contentType}
" +
            $"
" +
            $"{signHeader}
" +
            $"{xContentSha256}";

        string hashCanonicalString = ToHexString(HashSha256(Utf8.GetBytes(canonicalStringBuilder)));
        string credentialScope = $"{shortXDate}/{_region}/{_service}/request";
        string signString = $"HMAC-SHA256
{xDate}
{credentialScope}
{hashCanonicalString}";

        byte[] signKey = GenSigningSecretKeyV4(_sk, shortXDate, _region, _service);
        string signature = ToHexString(HmacSha256(signKey, signString));

        Uri url = new Uri($"{_schema}://{_host}{_path}?{query}");
        var request = new HttpRequestMessage();
        request.Method = method;
        request.RequestUri = url;
        request.Headers.TryAddWithoutValidation("Host", _host);
        request.Headers.Add("X-Date", xDate);
        request.Headers.Add("X-Content-Sha256", xContentSha256);
        request.Headers.TryAddWithoutValidation("Authorization",
            $"HMAC-SHA256 Credential={_ak}/{credentialScope}, SignedHeaders={signHeader}, Signature={signature}");
        HttpContent content = new ByteArrayContent(body);
        content.Headers.ContentType = new MediaTypeHeaderValue(contentType);
        request.Content = content;

        return _httpClient.Send(request);
    }

    private byte[] GenSigningSecretKeyV4(string secretKey, string date, string region, string service)
    {
        byte[] kDate = HmacSha256(Utf8.GetBytes(secretKey), date);
        byte[] kRegion = HmacSha256(kDate, region);
        byte[] kService = HmacSha256(kRegion, service);
        return HmacSha256(kService, "request");
    }

    private static byte[] HmacSha256(byte[] secret, string text)
    {
        using HMACSHA256 mac = new HMACSHA256(secret);
        var hash = mac.ComputeHash(Encoding.UTF8.GetBytes(text));
        return hash;
    }

    private static byte[] HashSha256(byte[] data)
    {
        using SHA256 sha = SHA256.Create();
        var hash = sha.ComputeHash(data);
        return hash;
    }

    private static string ToHexString(byte[]? bytes)
    {
        if (bytes == null)
        {
            return "";
        }

        StringBuilder sb = new StringBuilder();
        foreach (var t in bytes)
        {
            sb.Append(t.ToString("X2"));
        }

        return sb.ToString().ToLower();
    }
}
```


<span id="d9949c17"></span>
### PHP

The sample code below provides a generic PHP request example, including interface signature and request sending logic.

You only need to replace `ak`, `sk`, `Path`, `body`, and `method` in the sample code with the actual relevant parameters of the knowledge base. The remaining parameters (such as `Service`, `Region`, `Host`, `Content-Type`, and so on) are filled in according to the default service configuration and generally do not need to be modified.

```PHP
<?php
/**
 * Copyright (year) BytePlus Pte. Ltd.
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 * http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */
require 'vendor/autoload.php';
// You need to install Composer (see https://getcomposer.org/doc/00-intro.md) and the GuzzleHttp dependency: composer require guzzlehttp/guzzle:^7.0
use GuzzleHttpClient;
use GuzzleHttpExceptionGuzzleException;
$Service = "air";
$Version = "2018-01-01";
$Region = "cn-hongkong";
$Host = "api-knowledgebase.mlp.cn-hongkong.bytepluses.com";
$ContentType = "application/json";
$Path = ""; // Request path
/**
 * @throws GuzzleException
 */
// Step 1: Create an API request function. The signature calculation process is included in this function.
function request($method, $header, $ak, $sk, $body)
{
// Step 2: Create credentials. The Service and Region fields are fixed. `ak` and `sk` represent
// your AccessKeyID and SecretAccessKey, respectively. You also need to initialize the signature struct and handle some properties required for signature calculation here.
// Initialize the credential struct
 global $Service, $Region, $Host, $Version, $ContentType, $Path;
 $credential = [
 'accessKeyId' => $ak,
 'secretKeyId' => $sk,
 'service' => $Service,
 'region' => $Region,
 ];
 $requestParam = [
// `body` is the raw body required for the HTTP request
 'body' => $body,
 'host' => $Host,
 'path' => $Path,
 'method' => $method,
 'contentType' => $ContentType,
 'date' => gmdate('YmdTHisZ'),
 ];
// Step 3: Calculate the signature. Before calculation, prepare the `signResult` variable to receive the result and set some parameters.
// Initialize the signature result struct
 $xDate = $requestParam['date'];
 $shortXDate = substr($xDate, 0, 8);
 $xContentSha256 = hash('sha256', $requestParam['body']);
 $signResult = [
 'Host' => $requestParam['host'],
 'X-Content-Sha256' => $xContentSha256,
 'X-Date' => $xDate,
 'Content-Type' => $requestParam['contentType']
 ];
// Step 4: Calculate the Signature.
 $signedHeaderStr = join(';', ['content-type', 'host', 'x-content-sha256', 'x-date']);
 $canonicalRequestStr = join("
", [
 $requestParam['method'],
 $requestParam['path'],
 '',
 join("
", ['content-type:' . $requestParam['contentType'], 'host:' . $requestParam['host'], 'x-content-sha256:' . $xContentSha256, 'x-date:' . $xDate]),
 '',
 $signedHeaderStr,
 $xContentSha256
 ]);
 $hashedCanonicalRequest = hash("sha256", $canonicalRequestStr);
 $credentialScope = join('/', [$shortXDate, $credential['region'], $credential['service'], 'request']);
 $stringToSign = join("
", ['HMAC-SHA256', $xDate, $credentialScope, $hashedCanonicalRequest]);
 $kDate = hash_hmac("sha256", $shortXDate, $credential['secretKeyId'], true);
 $kRegion = hash_hmac("sha256", $credential['region'], $kDate, true);
 $kService = hash_hmac("sha256", $credential['service'], $kRegion, true);
 $kSigning = hash_hmac("sha256", 'request', $kService, true);
 $signature = hash_hmac("sha256", $stringToSign, $kSigning);
 $signResult['Authorization'] = sprintf("HMAC-SHA256 Credential=%s, SignedHeaders=%s, Signature=%s", $credential['accessKeyId'] . '/' . $credentialScope, $signedHeaderStr, $signature);
 $header = array_merge($header, $signResult);
// Step 5: Write the signature into the HTTP header and send the HTTP request.
 $client = new Client([
 'base_uri' => 'https://' . $requestParam['host'],
 'timeout' => 120.0,
 ]);
 return $client->request($method, 'https://' . $requestParam['host'] . $requestParam['path'], [
 'headers' => $header,
 'body' => $requestParam['body']
 ]);
}
$now = time();
$body = [
// Request body
$requestBody =json_encode($body);
$AK = '';
$SK = '';
try {
 $response = request("POST",[], $AK, $SK, $requestBody);
 print_r($response->getBody()->getContents());
} catch (GuzzleException $e) {
 print_r($e->getMessage());
}
```
