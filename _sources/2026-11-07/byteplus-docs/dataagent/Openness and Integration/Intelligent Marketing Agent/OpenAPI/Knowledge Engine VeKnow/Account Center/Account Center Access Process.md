---
title: "Account Center Access Process"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/account-center-access-process"
---

This document describes the authentication method of OpenAPI in the account center, the creation method of Access Key, and the example of multi\-language calls to help the caller quickly complete joint debugging.

# Authentication method

Account Center OpenAPI uses **AWS Sig v4** signature authentication.

Before initiating a request, the caller needs to prepare the following information:

|**Field** |**Description** |
|---|---|
|Access Key |AccessKey ID in API Credentials |
|Secret Key |In "API Credentials", the Secret that matches the AccessKey ID |
|Service |Fixed as `minibasebe` |
|Region |Fixed to `pri` |

# Create Access Key

Go to the console, click the user's avatar in the upper right corner of the page, and then go to "System Configuration \> Access Control \> API Credentials" to create an Access Key.

> **注意**

> Please save the created `AccessKey ID`and `AccessKey Secret`properly to avoid leaking to the code repository or chat history.

# Invocation convention

The destination address used in the request example is as follows:

```Plain
http://your-api-domain.com/{api_path}
```

The public conventions in the example are as follows:

|**Configuration item** |**Value** |
|---|---|
|request method |`POST` |
|Custom Query Parameters |`test_query=test` |
|Custom Header Parameters |`X-Custom-Header: somevalue` |
|Custom Body Request Body |`{"body":"test"}` |

# Python 3 example

Install dependencies first:

```Bash
pip install "botocore~=1.21.64"
```

Code example:

```Python
import json

from botocore.auth import SigV4Auth
from botocore.awsrequest import AWSRequest
from botocore.credentials import Credentials
from botocore.httpsession import URLLib3Session

credential = Credentials("<access_key>", "<secret_key>")
siger = SigV4Auth(credential, "minibasebe", "pri")
session = URLLib3Session()

body = {"body": "test"}
req = AWSRequest(
    method="POST",
    url="http://your-api-domain.com/{api_path}",
    headers={"X-Custom-Header": "somevalue"},
    data=json.dumps(body),
    params={"test_query": "test"},
)

siger.add_auth(req)

resp = session.send(req.prepare())
print(resp.headers)
print(resp.text)
```

# Java example

## **pom.xml**

```XML
<dependencies>
    <dependency>
        <groupId>software.amazon.awssdk</groupId>
        <artifactId>apache-client</artifactId>
        <version>2.16.60</version>
    </dependency>
    <dependency>
        <groupId>software.amazon.awssdk</groupId>
        <artifactId>auth</artifactId>
        <version>2.16.60</version>
    </dependency>
</dependencies>
```

## **Java code**

```Java
import software.amazon.awssdk.auth.credentials.AwsBasicCredentials;
import software.amazon.awssdk.auth.credentials.AwsCredentials;
import software.amazon.awssdk.auth.signer.Aws4Signer;
import software.amazon.awssdk.auth.signer.params.Aws4SignerParams;
import software.amazon.awssdk.http.ContentStreamProvider;
import software.amazon.awssdk.http.ExecutableHttpRequest;
import software.amazon.awssdk.http.HttpExecuteRequest;
import software.amazon.awssdk.http.HttpExecuteResponse;
import software.amazon.awssdk.http.SdkHttpClient;
import software.amazon.awssdk.http.SdkHttpFullRequest;
import software.amazon.awssdk.http.SdkHttpMethod;
import software.amazon.awssdk.http.apache.ApacheHttpClient;
import software.amazon.awssdk.regions.Region;

import java.io.BufferedReader;
import java.io.ByteArrayInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.nio.charset.StandardCharsets;
import java.util.stream.Collectors;

public class Demo {
    public static void main(String[] args) {
        AwsCredentials awsCreds = AwsBasicCredentials.create("<access_key>", "<secret_key>");
        Aws4SignerParams signerParams = Aws4SignerParams.builder()
                .awsCredentials(awsCreds)
                .signingName("minibasebe")
                .signingRegion(Region.of("pri"))
                .build();
        Aws4Signer signer = Aws4Signer.create();
        SdkHttpClient client = ApacheHttpClient.create();

        ContentStreamProvider content = new ContentStreamProviderImpl();

        SdkHttpFullRequest request = SdkHttpFullRequest.builder()
                .method(SdkHttpMethod.POST)
                .protocol("http")
                .host("minibase.tld")
                .port(80)
                .encodedPath({api_path})
                .appendRawQueryParameter("test_query", "test")
                .appendHeader("X-Custom-Header", "somevalue")
                .contentStreamProvider(content)
                .build();
        request = signer.sign(request, signerParams);

        HttpExecuteRequest executeRequest = HttpExecuteRequest.builder()
                .request(request)
                .contentStreamProvider(content)
                .build();
        ExecutableHttpRequest executableRequest = client.prepareRequest(executeRequest);
        try {
            HttpExecuteResponse response = executableRequest.call();
            String result = new BufferedReader(new InputStreamReader(response.responseBody().get()))
                    .lines()
                    .collect(Collectors.joining("\n"));
            System.out.println(result);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

class ContentStreamProviderImpl implements ContentStreamProvider {
    @Override
    public InputStream newStream() {
        return new ByteArrayInputStream("{\"body\":\"test\"}".getBytes(StandardCharsets.UTF_8));
    }
}
```

# Golang example

```Go
package main

import (
    "bytes"
    "encoding/json"
    "fmt"
    "io"
    "net/http"
    "net/url"
    "time"

    "github.com/aws/aws-sdk-go/aws/credentials"
    v4 "github.com/aws/aws-sdk-go/aws/signer/v4"
)

func main() {
    minibaseURL := url.URL{Scheme: "http", Host: "minibase.tld", Path: {api_path}}
    q := minibaseURL.Query()
    q.Set("test_query", "test")
    minibaseURL.RawQuery = q.Encode()

    reqBodyJson := map[string]string{"body": "test"}
    reqBody, _ := json.Marshal(reqBodyJson)
    reqBodyReader := bytes.NewReader(reqBody)

    req, _ := http.NewRequest(http.MethodPost, minibaseURL.String(), reqBodyReader)
    req.Header.Set("X-Custom-Header", "somevalue")

    signer := v4.NewSigner(credentials.NewStaticCredentials("<access_key>", "<secret_key>", ""))
    signer.Sign(req, reqBodyReader, "minibasebe", "pri", time.Now())

    resp, _ := http.DefaultClient.Do(req)
    respBody, _ := io.ReadAll(resp.Body)
    respBodyJson := new(map[string]any)
    json.Unmarshal(respBody, respBodyJson)
    fmt.Println(respBodyJson)
}
```

# Node.js (ES Modules) example

## package.json

```JSON
{
  "dependencies": {
    "@aws-crypto/sha256-js": "^4.0.0",
    "@aws-sdk/node-http-handler": "^3.329.0",
    "@aws-sdk/protocol-http": "^3.329.0",
    "@aws-sdk/signature-v4": "^3.329.0"
  }
}
```

## TypeScript

```TypeScript
import { Sha256 } from "@aws-crypto/sha256-js";
import { NodeHttpHandler } from "@aws-sdk/node-http-handler";
import { HttpRequest } from "@aws-sdk/protocol-http";
import { SignatureV4 } from "@aws-sdk/signature-v4";
import { IncomingMessage } from "http";

const signerInit = {
  service: "minibasebe",
  region: "pri",
  sha256: Sha256,
  credentials: {
    accessKeyId: "<access_key>",
    secretAccessKey: "<secret_key>",
  },
};
const signer = new SignatureV4(signerInit);

const nodeHttpHandler = new NodeHttpHandler();

const hostname = "minibase.tld";
const port = 80;
const demoRequest = new HttpRequest({
  method: "POST",
  protocol: "http",
  hostname,
  port,
  path: {api_path},
  headers: {
    Host: `${hostname}:${port}`,
    "X-Custom-Header": "somevalue",
  },
  query: {
    test_query: "test",
  },
  body: JSON.stringify({ body: "test" }),
});
const signedRequest = (await signer.sign(demoRequest)) as HttpRequest;

const { response } = await nodeHttpHandler.handle(signedRequest);
const body = await ((body: IncomingMessage) => {
  return new Promise((resolve, reject) => {
    const buffer: Uint8Array[] = [];
    body
      .on("data", (chunk) => {
        buffer.push(chunk);
      })
      .on("end", () => {
        if (!body.complete) {
          reject(new Error("The body failed to stream to the end."));
          return;
        }
        resolve(JSON.parse(Buffer.concat(buffer).toString()));
      });
  });
})(response.body as IncomingMessage);
console.log(body);
```

## JavaScript

```JavaScript
import { Sha256 } from "@aws-crypto/sha256-js";
import { NodeHttpHandler } from "@aws-sdk/node-http-handler";
import { HttpRequest } from "@aws-sdk/protocol-http";
import { SignatureV4 } from "@aws-sdk/signature-v4";

const signerInit = {
  service: "minibasebe",
  region: "pri",
  sha256: Sha256,
  credentials: {
    accessKeyId: "<access_key>",
    secretAccessKey: "<secret_key>",
  },
};
const signer = new SignatureV4(signerInit);

const nodeHttpHandler = new NodeHttpHandler();

const hostname = "minibase.tld";
const port = 80;
const demoRequest = new HttpRequest({
  method: "GET",
  protocol: "http",
  hostname,
  port,
  path: {api_path},
  headers: {
    Host: `${hostname}:${port}`,
    "X-Custom-Header": "somevalue",
  },
  query: {
    test_query: "test",
  },
  body: JSON.stringify({ body: "test" }),
});
const signedRequest = await signer.sign(demoRequest);

const { response } = await nodeHttpHandler.handle(signedRequest);
const body = await ((body) => {
  return new Promise((resolve, reject) => {
    const buffer = [];
    body
      .on("data", (chunk) => {
        buffer.push(chunk);
      })
      .on("end", () => {
        if (!body.complete) {
          reject(new Error("The body failed to stream to the end."));
          return;
        }
        resolve(JSON.parse(Buffer.concat(buffer).toString()));
      });
  });
})(response.body);
console.log(body);
```

# Suggestions for use

* Priority is given to using HTTPS addresses to initiate requests to avoid clear text transmission risks.

* Keep `access_key`and `secret_key`in a secure key management system.

* Do not hardcode credentials to front\-end code or public repositories.

* When the signature fails, the time skew, request path, Query parameters, and headers are checked first.
