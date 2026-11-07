---
title: "Initializing client"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/client-initialization-go"
---

The Redis Go SDK supports initializing the client through a session. A Redis client created through a session reuses underlying HTTP/HTTPS resources (connections or requests). When you need to initialize multiple clients for operations, creating them through a session can improve client performance. This topic describes how to initialize the client through a session.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Downloaded and installed the Redis Go SDK. For specific procedures, refer to [Downloading and installing SDK](https://docs.byteplus.com/en/docs/redis/download-install-go-sdk).

* Before initializing the client, ensure that you have obtained the following information:

   * Access Key ID (AK) and Secret Access Key (SK) for your account. For methods to obtain AKSK information, refer to [Access Key](https://docs.byteplus.com/en/docs/byteplus-platform/reference-access-key).

   * Region information. For the regions supported by Redis, refer to [Service endpoints](https://docs.byteplus.com/en/docs/redis/request-structure#.5pyN5Yqh5Zyw5Z2A).


<span id=".5Yid5aeL5YyW5a6i5oi356uv"></span>
## Initializing client

Use the following code to initialize the client.

```Go
package main

import (
   "fmt"
   "os"

   "github.com/byteplus-sdk/byteplus-go-sdk-v2/service/redis"
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
      client *redis.REDIS
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

   // Create a Redis SDK client, which can be used to call the API to perform task requests later.
   client = redis.New(sess)
}
```
