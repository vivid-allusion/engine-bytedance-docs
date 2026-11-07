---
title: "Client initialization"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Go_Client_initialization"
---

The Cloud Search Service Go SDK supports initializing a client through a session. A Cloud Search client created through a session reuses underlying HTTP/HTTPS resources (connections or requests). When you need to initialize multiple clients for operations, creating them through a session can improve client performance. This topic describes how to initialize a client through a session.

<span id="ZlMMo2NI"></span>
## **Prerequisites**


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* You have obtained the Access Key ID (AK) and Secret Access Key (SK) for your account. For details, refer to [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey).

* You have obtained the regions supported by Cloud Search. For details, refer to [Service endpoints](https://docs.byteplus.com/en/docs/cloudsearch/request-structure#request-method).

* You have downloaded and installed the Cloud Search Go SDK. For details, refer to [Download and installation](https://docs.byteplus.com/en/docs/cloudsearch/Go_Download_and_installation).


<span id="Eu8kqD17"></span>
## **Initialize the client**

Use the following code to initialize the client.

```go
package main

import (
        "fmt"
        "github.com/byteplus/byteplus-go-sdk-v2/service/escloud"
        "github.com/byteplus/byteplus-go-sdk-v2/byteplus"
        "github.com/byteplus/byteplus-go-sdk-v2/byteplus/credentials"
        "github.com/byteplus/byteplus-go-sdk-v2/byteplus/session"
        "net/http"
        "time"
)

func main() {
        //Create an instance
        var (
                ak     string
                sk     string
                region string
                config *byteplus.Config
                sess   *session.Session
                client *escloud.ESCLOUD
                err    error
        )

        ak = "Your AK"
        sk = "Your SK"
        region = "cn-beijing"
        config = volcengine.NewConfig().
                WithRegion(region).
                WithCredentials(credentials.NewStaticCredentials(ak, sk, "")).
                WithHTTPClient(&http.Client{Timeout: 3 * time.Second}).
                WithEndpoint("escloud.cn-beijing.byteplusapi.com")

        sess, err = session.NewSession(config)
        if err != nil {
                panic(err)
        }
        client = escloud.New(sess)
```
