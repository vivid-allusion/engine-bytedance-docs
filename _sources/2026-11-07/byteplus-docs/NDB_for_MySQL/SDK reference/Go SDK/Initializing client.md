---
title: "Initializing client"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Initializing_client_go"
---

NDB for MySQL Go SDK supports initializing the client through Session. The NDB for MySQL clients created through the Session method will implement the reuse of HTTP/HTTPS resources (connections or requests) at the bottom layer. When multiple clients need to be initialized for operation, creating them in Session mode can improve client performance. This article describes how to initialize the client through the Session method.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A BytePlus account has been registered. For account registration, refer to [How to Register an Account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* The Access Key ID (AK) and Secret Access Key (SK) information of the account have been obtained. 

* The Regions supported by NDB for MySQL have been obtained. For more information, refer to [Service endpoints](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Request_structure#.5pyN5Yqh5Zyw5Z2A).

* The NDB for MySQL Go SDK has been downloaded and installed. For the specific procedure, refer to [Downloading and installing SDK](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Downloading_and_installing_SDK_go).


<span id=".5Yid5aeL5YyW5a6i5oi356uv"></span>
## Initializing client

Initialize the client with the following code.

```go
import (
    "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus"
    "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus/credentials"
    "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus/session"
    "github.com/byteplus-sdk/byteplus-go-sdk-v2/service/vedbm"
)
var (
    region      string
    ak          string
    sk          string
    config      *byteplus.Config
    sess        *session.Session
    VeDBMClient *VEDBM
)
func InitClient() {
    region = "your region"
    ak = "your ak"
    sk = "your sk"
    config = byteplus.NewConfig().
       WithCredentials(credentials.NewStaticCredentials(ak, sk, "")).
       WithRegion(region).
       WithEndpoint("service host")
    sess, _ = session.NewSession(config)
    VeDBMClient = New(sess)
}
```
