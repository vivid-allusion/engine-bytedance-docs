---
title: "Client initialization"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/client_initialization_3"
---

The MySQL Go SDK supports initializing clients via sessions. MySQL clients created via sessions reuse underlying HTTP/HTTPS resources (connections or requests). When you need to initialize multiple clients for operations, the performance of the clients can be improved if they are created via session. This topic describes how to initialize clients via session.

<span id="prerequisites"></span>
## **Prerequisites**


* A Volcano Engine account has been registered with real name authentication completed.For detailed instructions, please refer to [How to Register an Account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account) and [Real-name authentication](https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration).

* The Access Key ID (AK) and Secret Access Key (SK) information of the account has been obtained. For specific operations, refer to [Managing Access Keys](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-keys).

* The regions supported by RDS for MySQL have been obtained. Refer to [Endpoints](https://docs.byteplus.com/en/docs/RDS_for_MySQL/request_structure_1#.6YCa5L-h5Y2P6K6u).

* The Go SDK of RDS for MySQL has been downloaded and installed. For specific operation steps, refer to [Download and installation](https://docs.byteplus.com/en/docs/RDS_for_MySQL/client_initialization_3).


<span id="initializing-the-client"></span>
## **Initializing the Client**

Initialize the client with the following code.

```go
package main

import  (
   "fmt"
   "os"
   "github.com/volcengine/volcengine-go-sdk/service/rdsmysqlv2"
   "github.com/volcengine/volcengine-go-sdk/volcengine"
   "github.com/volcengine/volcengine-go-sdk/volcengine/credentials"
   "github.com/volcengine/volcengine-go-sdk/volcengine/session"
)

func main() {
   var (
      ak     string
      sk     string
      region string
      config *volcengine.Config
      sess   *session.Session
      client *rdsmysqlv2.RDSMYSQLV2
      err    error
   )

   ak = "Your AK"
   sk = "Your SK"
   region = "Your Region"
   config = volcengine.NewConfig().WithCredentials(credentials.NewStaticCredentials(ak, sk, "")).WithRegion(region)
   sess, err = session.NewSession(config)
   if err != nil {
      fmt.Printf("Failed to create session, err: %v\n", err)
      os.Exit(1)
   }
   client = rdsmysqlv2.New(sess)
}
```


&nbsp;
