---
title: "Client initialization"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Go_SDK_Initialize_the_client"
---

The SQL Server Go SDK supports initializing the client through a session. An SQL Server client created through a session reuses underlying HTTP/HTTPS resources (connections or requests). When you need to initialize multiple clients, creating them through a session can improve client performance. This topic describes how to initialize the client through a session.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**


* A volcengine account has been registered and completed verification. For the detailed method, refer to [Sign Up and Verify volcengine account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* As per the regulations in the Chinese mainland, you must have completed real name registration before you can activate and use cloud services on nodes in the Chinese mainland through volcengine.  For more details, refer to [Real name registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration).

* You have obtained the Access Key ID (AK) and Secret Access Key (SK) for your account. For details, see [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey).

* You have obtained the Regions supported by RDS for SQL Server. For more information, see [Service address](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/request-structure#service-address).

* You have downloaded and installed the Go SDK for RDS for SQL Server. For detailed steps, see [Download and installation](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Download_and_installation).


<span id=".5Yid5aeL5YyW5a6i5oi356uv"></span>
## **Initialize the client**

Use the following code to initialize the client.

```go
package  main
import (
   "fmt"
   "os"
   "github.com/byteplus/byteplus-go-sdk-v2/service/rdsmssql"
   "github.com/byteplus/byteplus-go-sdk-v2/byteplus"
   "github.com/byteplus/byteplus-go-sdk-v2/byteplus/credentials"
   "github.com/byteplus/byteplus-go-sdk-v2/byteplus/session"
)

var (
   Config *byteplus.Config
   Sess   *session.Session
   Client *RDSMSSQL
)

func main() {
    ak = "Your AK"
    sk = "Your SK"
    region = "Your Region"
    config = byteplus.NewConfig().WithCredentials(credentials.NewStaticCredentials(ak, sk, "")).WithRegion(region)
    sess, err = session.NewSession(config)
    if err != nil {
       fmt.Printf("Failed to create session, err: %v\n", err)
       os.Exit(1)
    }
    Client = rdsmssql.New(sess)
}
```
