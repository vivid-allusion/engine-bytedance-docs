---
title: "API Authentication"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/API_Authentication"
---

***Viking AI Search*** * is an enterprise\-grade AI search product powered by generative AI. It uses multimodal semantic representation and large model understanding, combined with ByteDance's best practices in information retrieval, to provide an out\-of\-the\-box AI search platform. This service helps customers build and integrate end\-to\-end multimodal search and recommendation capabilities for images and text. To experience more of Viking AI Search's capabilities, visit: * [Viking AI Search Engine, an integrated intelligent engine for enterprise search, recommendation, and Q&A](https://www.volcengine.com/product/AI-Search-Rec) *.* 


---



<span id="02121831"></span>
# Authentication Mechanism

AI Search Data Plane APIs — including APIs for search, conversation, and recommendation, and for uploading, deleting, and querying data — support two authentication methods:


1. **API Key authentication:**  A simple method that you can configure and use directly from the AI Search console.

2. **Access Key authentication:**  The standard method for authenticating cloud resource access in the Volcano Engine product system, designed for enterprises that require fine\-grained resource and permission management.


&nbsp;

<span id="8f210132"></span>
# Method 1: API Key Authentication

<span id="a6b8af0a"></span>
## Create and get an API Key


1. Log in to the AI Search Engine console and go to the [API Key Management](https://console.volcengine.com/aisearch/platform/home/api-key) page. You can view existing API Keys or create a new one.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/b5b54e3940584100874d4de08cb7ee37) </span>


&nbsp;

2. View and copy the API Key from the API Key list.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/036d1f36336e482ea9776dd96f85f9ef) </span>

&nbsp;

<span id="2c6d9ce7"></span>
## Construct Signature

API Key signature authentication requires adding an `Authorization` header to the HTTP request header as follows:

```Bash
Authorization: Bearer <API_KEY>
```


<span id="852735d4"></span>
## API Call Example

```Shell
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/${application_id}/search/{scene_id}' \ 
  -H 'Content-Type: application/json' \ 
  -H 'Authorization:Bearer <API_KEY>' \ 
  -d '{ 
    "query": { 
        "text": "Sci-fi" 
    }, 
    "page_number": 1, 
    "page_size": 5, 
    "user": { 
        "_user_id": "user_123" 
    }, 
    "filter": {
        "op": "must",
        "field": "director",
        "conds": ["Mr X"]
    },
    "dataset_id": "106265704" 
}' 
```


&nbsp;

<span id="5e6cd7f0"></span>
# Method 2: Authenticate with a Volcano Access Key

<span id="eaa5b427"></span>
## Get an Access Key

An Access Key includes an Access Key ID (AK) and an Access Key Secret (SK). The Access Key ID identifies the user, and the Access Key Secret verifies the user's identity. Keep both values secure.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">If you are using a sub\-account, confirm with your enterprise administrator that it has permission to create and read Access Keys.</div>


Obtain your AK/SK as follows. For more details, refer to [Access Key Management](https://www.volcengine.com/docs/6291/65568).


1. Click **API Access Key** in the account dropdown menu in the top\-right corner to go to the corresponding page.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/65a9afd5a726464585e6c8b5425a8d47" width="600px" /></div>



&nbsp;

2. Click **New Key** to get an AK/SK. Use these as credentials to call the APIs of your integrated applications.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/5aa7e99ed2c34f6d8af9e6894615712d" width="600px" /></div>


**Note:**  For security reasons, create a sub\-account and use its AK/SK.

<span id="00a1d784"></span>
## Create a signature


1. Use the Access Key to create a signature. For details on the signature method and creation mechanism, see [Signature Method](https://www.volcengine.com/docs/6369/67269). Use the multi\-language [official SDK](https://www.volcengine.com/docs/6369/156029) provided by Volcano Engine to create the signature.

   **AI Search Platform parameters for signatures**

   ```Plain Text
   Service：aisearch
   Region：cn-beijing
   ```
   

2. Add the created signature string to the HTTP request header as `Authorization`.

   ```Bash
   curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/{api action}'
     -H 'Content-Type: application/json' \
     -H 'Authorization: HMAC-SHA256 Credential={AccessKeyId}/{CredentialScope}, SignedHeaders={SignedHeaders}, Signature={Signature}' \
     -d '{
     "key": "value"
   }'
   ```
   


<span id="23610564"></span>
## API Call Example

<span id="e80940a9"></span>
### Install the Volcano Engine Package


<Tabs>
<Tab zoneid="vKue1XTqhX" title="Python">
<TabTitle>Python</TabTitle>

&nbsp;

```Python
pip install volcengine
```





</Tab>
<Tab zoneid="lM4CQLMOcl" title="Java">
<TabTitle>Java</TabTitle>

&nbsp;

```Java
<dependency>
    <groupId>com.volcengine</groupId>
    <artifactId>volc-sdk-java</artifactId>
    <version>最新版本</version>
</dependency> 
```



</Tab>
<Tab zoneid="EXcjFb0vdz" title="Go">
<TabTitle>Go</TabTitle>

&nbsp;

```Go
go get -u github.com/volcengine/volc-sdk-golang
```



</Tab>
</Tabs>


<span id="4a0f4675"></span>
### Generate a Signature and Test the Call


<Tabs>
<Tab zoneid="pQ0oKnA8Jc" title="Python">
<TabTitle>Python</TabTitle>

&nbsp;

```Python
import json
import sys
import requests

from volcengine.auth.SignerV4 import SignerV4
from volcengine.base.Request import Request
from volcengine.Credentials import Credentials

Host = "aisearch.cn-beijing.volces.com"
Schema = "https"
Service = "aisearch"
Region = "cn-beijing"

# 用户的AK/SK
AK = "xxx"
SK = "xxx"


def prepare_request(method, path, ak, sk, params=None, data=None, doseq=0):
    if params:
        for key in params:
            if (
                    type(params[key]) == int
                    or type(params[key]) == float
                    or type(params[key]) == bool
            ):
                params[key] = str(params[key])
            # elif sys.version_info[0] != 3: # 在 Python 3.x 中，不需要这部分代码
            #     if type(params[key]) == unicode:
            #         params[key] = params[key].encode("utf-8")
            elif type(params[key]) == list:
                if not doseq:
                    params[key] = ",".join(params[key])
    r = Request()
    r.set_shema(Schema)
    r.set_method(method)
    r.set_connection_timeout(10)
    r.set_socket_timeout(10)
    mheaders = {
        "Accept": "application/json",
        "Content-Type": "application/json",
        "Host": Host
    }
    r.set_headers(mheaders)
    if params:
        r.set_query(params)
    r.set_path(path)
    if data is not None:
        r.set_body(json.dumps(data))
    # 生成签名
    credentials = Credentials(ak, sk, Service, Region)
    SignerV4.sign(r, credentials)
    return r


def search_demo():
    path = "/api/v1/application/{}/search".format("应用id")
    url_param = None
    body_data = {
        "query": {
            "text": "测试"
        },
        "user": {
            "_user_id": "mock_user_id",
        },
        "dataset_id": "106621109",
        "page_number": 1,
        "page_size": 10
    }

    sign_req = prepare_request("POST", path, AK, SK, url_param, body_data)

    resp = requests.request(
        method=sign_req.method,
        url="{}://{}{}".format(Schema, Host, path),
        headers=sign_req.headers,
        data=sign_req.body
    )
    resp.raise_for_status()

    print(resp.text)


def chat_search_demo():
    path = "/api/v1/application/{}/chat_search".format("APP id")
    url_param = None
    body_data = {
        "input_message": {
            "content": [
                {
                    "type": "text",
                    "text": "Show me some comedy shows."
                }
            ]
        },
        "user": {
            "_user_id": "mock_user_id",
        },
        "session_id": "mock_session_id",
    }

    sign_req = prepare_request("POST", path, AK, SK, url_param, body_data)

    resp = requests.request(
        method=sign_req.method,
        url="{}://{}{}".format(Schema, Host, path),
        headers=sign_req.headers,
        data=sign_req.body,
        stream=True,  # make sure streaming mode enabled.
    )
    resp.raise_for_status()
    process_stream_response(resp)


def process_stream_response(response):
    for line in response.iter_lines(decode_unicode=True):
        if line:
            print(line)


if __name__ == "__main__":
    search_demo()
    chat_search_demo()
```





</Tab>
<Tab zoneid="KiNVBHR3Ua" title="Java">
<TabTitle>Java</TabTitle>

&nbsp;

```Java
package javaTest;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.URI;
import java.nio.charset.StandardCharsets;
import java.util.*;

import com.google.gson.Gson;
import org.apache.http.Header;
import org.apache.http.HttpEntity;
import org.apache.http.HttpResponse;
import org.apache.http.NameValuePair;
import org.apache.http.client.HttpClient;
import org.apache.http.client.config.RequestConfig;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.client.utils.URIBuilder;
import org.apache.http.entity.StringEntity;
import org.apache.http.impl.client.HttpClients;
import org.apache.http.util.EntityUtils;

import com.volcengine.auth.ISignerV4;
import com.volcengine.auth.impl.SignerV4Impl;
import com.volcengine.model.Credentials;
import com.volcengine.service.SignableRequest;

public class Example {
    private static final String AK = "xxx";
    private static final String SK = "xxx";
    private static final String HOST = "aisearch.cn-beijing.volces.com";
    private static final String SERVICE = "aisearch";
    private static final String REGION = "cn-beijing";
    private static final String SCHEMA = "https";


    public static SignableRequest prepareRequest(String host, String path, String method, List<NameValuePair> params, String body, String ak, String sk) throws Exception {
        SignableRequest request = new SignableRequest();
        request.setMethod(method);
        request.setHeader("Accept", "application/json");
        request.setHeader("Content-Type", "application/json");
        request.setHeader("Host", HOST);
        request.setEntity(new StringEntity(body, "utf-8"));

        URIBuilder builder = request.getUriBuilder();
        builder.setScheme(SCHEMA);
        builder.setHost(host);
        builder.setPath(path);
        if (params != null) {
            builder.setParameters(params);
        }

        RequestConfig requestConfig = RequestConfig.custom().setSocketTimeout(5000).setConnectTimeout(2000).build();
        request.setConfig(requestConfig);

        Credentials credentials = new Credentials(REGION, SERVICE);
        credentials.setAccessKeyID(ak);
        credentials.setSecretAccessKey(sk);

        // Signature
        ISignerV4 ISigner = new SignerV4Impl();
        ISigner.sign(request, credentials);

        return request;
    }

    public static void search_demo() {
        try {
            String path = String.format("/api/v1/application/%s/search", "应用id");

            Map<String, Object> bodyData = new HashMap<>();
            bodyData.put("dataset_id", "实际数据集id");
            bodyData.put("page_number", 1);
            bodyData.put("page_size", 10);
            
            Map<String, String> query = new HashMap<>();
            query.put("text", "测试");
            bodyData.put("query", query);
            
            Map<String, String> user = new HashMap<>();
            user.put("_user_id", "mock_user_id");
            bodyData.put("user", user);

            Gson gson = new Gson();
            String body = gson.toJson(bodyData);

            SignableRequest signableRequest = prepareRequest(HOST, path, "POST", null, body, AK, SK);
            URI uri = new URIBuilder().setScheme(SCHEMA).setHost(HOST).setPath(path).build();

            HttpPost httpPost = new HttpPost(uri);
            httpPost.setConfig(signableRequest.getConfig());
            httpPost.setEntity(signableRequest.getEntity());
            for (Header header : signableRequest.getAllHeaders()) {
                httpPost.setHeader(header.getName(), header.getValue());
            }
            HttpClient httpClient = HttpClients.createDefault();
            HttpResponse response = httpClient.execute(httpPost);
            int statusCode = response.getStatusLine().getStatusCode();
            String responseBody = EntityUtils.toString(response.getEntity());

            System.out.println(statusCode);
            System.out.println(responseBody);

        } catch (IOException e) {
            System.out.println("请求出错: " + e.getMessage());
        } catch (Exception e) {
            throw new RuntimeException(e);
        }
    }

    public static void chat_search_demo() {
        // Note that chat_search is a streaming API.
        try {
            String path = String.format("/api/v1/application/%s/chat_search", "应用id");

            Map<String, Object> bodyData = new HashMap<>();
            bodyData.put("session_id", "mock_session_id");

            Map<String, Object> inputMessage = new HashMap<>();
            Map<String, String> content = new HashMap<>();
            content.put("type", "text");
            content.put("text", "帮我推荐几部喜剧?");
            inputMessage.put("content", Collections.singletonList(content));
            bodyData.put("input_message", inputMessage);

            Map<String, String> user = new HashMap<>();
            user.put("_user_id", "mock_user_id");
            bodyData.put("user", user);

            Gson gson = new Gson();
            String body = gson.toJson(bodyData);

            SignableRequest signableRequest = prepareRequest(HOST, path, "POST", null, body, AK, SK);
            URI uri = new URIBuilder().setScheme(SCHEMA).setHost(HOST).setPath(path).build();

            HttpPost httpPost = new HttpPost(uri);
            httpPost.setConfig(signableRequest.getConfig());
            httpPost.setEntity(signableRequest.getEntity());
            for (Header header : signableRequest.getAllHeaders()) {
                httpPost.setHeader(header.getName(), header.getValue());
            }
            HttpClient httpClient = HttpClients.createDefault();
            HttpResponse response = httpClient.execute(httpPost);
            int statusCode = response.getStatusLine().getStatusCode();
            if (statusCode == 200) {
                // Note: Streaming processing is required.
                processStreamResponse(response.getEntity());
            } else {
                System.err.println("HTTP请求失败，状态码: " + statusCode);
                String responseBody = EntityUtils.toString(response.getEntity(), StandardCharsets.UTF_8);
                System.err.println("响应内容: " + responseBody);
            }
        } catch (IOException e) {
            System.out.println("请求出错: " + e.getMessage());
        } catch (Exception e) {
            throw new RuntimeException(e);
        }
    }

    private static void processStreamResponse(HttpEntity entity) throws IOException {
        try (InputStream inputStream = entity.getContent();
             BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream, StandardCharsets.UTF_8), 128)) {

            String line;
            // Read and print the response content line by line
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } finally {
            EntityUtils.consumeQuietly(entity);
        }
    }

    public static void main(String[] args) {
        search_demo();
        chat_search_demo();
    }
}
```





</Tab>
<Tab zoneid="TzYOWVzyLW" title="Go">
<TabTitle>Go</TabTitle>

&nbsp;

```Go
package main

import (
    "bufio"
    "bytes"
    "encoding/json"
    "errors"
    "fmt"
    "io"
    "net/http"
    "net/url"
    "strings"

    "github.com/volcengine/volc-sdk-golang/base"
)

const (
    Service = "aisearch"
    Host    = "aisearch.cn-beijing.volces.com"
    Schema  = "https"
    Region  = "cn-beijing"

    // User's AK/SK
    AK = "xxx"
    SK = "xxx"
)

func PrepareRequest(method string, path string, ak string, sk string, query url.Values, body []byte) *http.Request {
    u := url.URL{
       Scheme: Schema,
       Host:   Host,
       Path:   path,
    }
    if query != nil {
       u.RawQuery = query.Encode()
    }
    req, _ := http.NewRequest(strings.ToUpper(method), u.String(), bytes.NewReader(body))
    req.Header.Set("Accept", "application/json")
    req.Header.Set("Content-Type", "application/json")
    req.Header.Set("Host", Host)
    credential := base.Credentials{
       AccessKeyID:     ak,
       SecretAccessKey: sk,
       Service:         Service,
       Region:          Region,
    }
    req = credential.Sign(req)
    return req
}

func searchDemo() {
    path := fmt.Sprintf("/api/v1/application/%s/search", "应用id")
    urlParam := url.Values{}
    bodyData := map[string]interface{}{
       "query": map[string]string{
          "text": "测试",
       },
       "user": map[string]interface{}{
          "_user_id": "mock_user_id",
       },
       "dataset_id":  "实际数据集id",
       "page_number": 1,
       "page_size":   10,
    }
    body, _ := json.Marshal(bodyData)
    req := PrepareRequest("POST", path, AK, SK, urlParam, body)

    // send request
    resp, err := http.DefaultClient.Do(req)
    if err != nil {
       fmt.Printf("读取响应内容出错: %v\n", err)
       return
    }
    defer resp.Body.Close()

    respBody, err := io.ReadAll(resp.Body)
    if err != nil {
       fmt.Printf("读取响应内容出错: %v\n", err)
       return
    }
    fmt.Printf("响应状态码: %d\n", resp.StatusCode)
    fmt.Printf("响应内容: %s\n", respBody)
}

func chatSearchDemo() {
    path := fmt.Sprintf("/api/v1/application/%s/chat_search", "应用id")
    urlParam := url.Values{}
    bodyData := map[string]interface{}{
       "input_message": map[string]interface{}{
          "content": []map[string]interface{}{
             {
                "type": "text",
                "text": "帮我推荐几部喜剧?",
             },
          },
       },
       "user": map[string]interface{}{
          "_user_id": "mock_user_id",
       },
       "session_id": "mock_session_id",
    }
    body, _ := json.Marshal(bodyData)
    req := PrepareRequest("POST", path, AK, SK, urlParam, body)

    // send request
    resp, err := http.DefaultClient.Do(req)
    if err != nil {
       fmt.Printf("读取响应内容出错: %v", err)
       return
    }
    if resp.StatusCode != http.StatusOK {
       fmt.Printf("响应状态码异常: %v", resp.StatusCode)
       return
    }
    processStreamResponse(resp)
}

func processStreamResponse(resp *http.Response) {
    defer func() {
       _ = resp.Body.Close()
    }()

    reader := bufio.NewReader(resp.Body)
    for {
       line, _, err := reader.ReadLine()
       if err != nil {
          if errors.Is(err, io.EOF) {
             break
          }
          fmt.Printf("读取流式响应内容出错: %v", err)
       }
       fmt.Println(string(line))
    }
}

func main() {
    searchDemo()
    chatSearchDemo()
}
```



</Tab>
</Tabs>


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To explore more Viking AI search capabilities, visit: <a href="https://www.volcengine.com/product/AI-Search-Rec">Viking AI Search Engine, the all\-in\-one intelligent engine for enterprise search, recommendations, and Q&A</a></div>
