---
title: "Initializing client"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/client-initialization-go"
---

The MongoDB Go SDK supports initializing clients via sessions. MongoDB clients created via sessions reuse underlying HTTP/HTTPS resources (connections or requests). When you need to initialize multiple clients for operations, the performance of the clients can be improved if they are created via session. This topic describes how to initialize clients via session.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisite


* The MongoDB Go SDK has been downloaded and installed. For the specific procedure, refer to [Downloading and installing SDK](https://docs.byteplus.com/en/docs/mongodb/download-install-go-sdk).

* Before initializing the client, make sure you have obtained the following information:

   * The Access Key ID (AK) and Secret Access Key (SK) of the account. For methods to obtain AKSK information, refer to [Access Key](https://docs.byteplus.com/en/docs/byteplus-platform/reference-access-key).

   * Region information. For regions supported by MongoDB, refer to [Service endpoints](https://docs.byteplus.com/en/docs/mongodb/request-structure#9TeFSOVO).


<span id=".5Yid5aeL5YyW5a6i5oi356uv"></span>
### Initializing the client

Initialize the client with the following code.

```Go
package main

import (
   "fmt"
   "os"

   "github.com/byteplus-sdk/byteplus-go-sdk-v2/service/mongodb"
   "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus"
   "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus/credentials"
   "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus/session"
)

func main() {
   var (
      ak     string
      sk     string
      region string
      config *byteplus.Config
      sess   *session.Session
      client *mongodb.MONGODB
      err    error
   )

   // Set access key and secret key verification information and region.
   ak = "Your AK"
   sk = "Your SK"
   region = "Your Region"
   config = byteplus.NewConfig().WithCredentials(credentials.NewStaticCredentials(ak, sk, "")).
      WithRegion(region)

   // All clients require sessions, which provide settings shared by them, such as access key and secret key verification information and region information.
   sess, err = session.NewSession(config)
   if err != nil {
      fmt.Printf("Failed to create session, err: %v\n", err)
      os.Exit(1)
   }

   // Create a MongoDB SDK client, which can be used to call the API to perform task requests later.
   client = mongodb.New(sess)
}
```
