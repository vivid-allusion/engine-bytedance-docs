---
title: "SDK Installation and Initialization"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/sdk_installation_and_initialization"
---

VikingDB vector database supports database operations through Go SDK. Before using the Go SDK, you need to complete the SDK installation and initialization steps.

<span id="prerequisites"></span>
# Prerequisites


1. You have completed account registration and service activation through [Register Account and Activate Service](https://www.volcengine.com/docs/84313/1254444).

2. Obtain security credentials. An Access Key is a security credential for accessing Volcengine services, consisting of an Access Key ID (AK for short) and a Secret Access Key (SK for short). You can log in to the Volcengine Console and go to [Key Management] to view the AK/SK of your current account. For more details, please refer to [Access Key Management](https://www.volcengine.com/docs/6291/65568).


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5ef0f716976d0e2060797391b516a839.png) </span>

<span id="install-sdk"></span>
# Install SDK

To optimize the permission system, the vector database SDK is divided into **control plane** and **data plane**: the control plane is used to manage collections, indexes, and offline tasks; the data plane is used for data writing, retrieval, and vectorization. The control plane also supports operations from the console page, please configure dependencies according to your needs.

<span id="_1-control-plane-and-data-plane-dependency-configuration"></span>
## 1. Control Plane and Data Plane Dependency Configuration

```bash
# Data plane SDK
go get -u github.com/volcengine/vikingdb-go-sdk

# Control plane SDK
go get -u github.com/volcengine/volcengine-go-sdk
```


<span id="initialize-sdk"></span>
# Initialize SDK

For private network connection, refer to [Private Network Connection Method](https://docs.byteplus.com/docs/84313/1254445) for configuration and domain name acquisition. Currently, only http is supported for private network connection request protocol.

The sample code reads AK/SK from environment variables `VIKINGDB_AK` and `VIKINGDB_SK` by default; please replace `endpoint` and `region` with the actual domain name and region you use.


1. **Data Plane (Data / Search / Embedding)** 



|**Region Name** |**Region ID** |Internet Domain (Public Network) |Private Network Connection Endpoint Service (**NOT a domain name**, please refer to the [Private Network Connection](https://docs.byteplus.com/en/docs/VikingDB/APIV2Upgrade) documentation) |
|---|---|---|---|
|Asia Pacific (Johor) |ap\-southeast\-1 |[api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com](http://api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com/) |[com.bytepluses.privatelink.ap-southeast-1.vikingdb-ann](https://docs.byteplus.com/en/docs/198/com.bytepluses.privatelink.ap-southeast-1.vikingdb-ann) |


```go
package main

import (
    "fmt"
    "github.com/volcengine/vikingdb-go-sdk/vector"
    "os"
    "time"
)

func main() {
    var (
       accessKey = os.Getenv("VIKINGDB_AK")
       secretKey = os.Getenv("VIKINGDB_SK")
       //apiKey    = os.Getenv("VIKINGDB_APIKEY")
       endpoint  = "https://api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com"
       region    = "ap-southeast-1"
    )

    client, err := vector.New(
       vector.AuthIAM(accessKey, secretKey), // IAM auth
       // vector.AuthAPIKey(apiKey),            // APIKey auth
       vector.WithEndpoint(endpoint),
       vector.WithRegion(region),
       vector.WithTimeout(time.Second*30),
       vector.WithMaxRetries(3),
    )
    if err != nil {
       fmt.Println("New client failed, err: ", err)
       panic(err)
    }
}
```



2. **Control Plane (Collection / Index / Task)** 



|**Region Name** |**Region ID** |Internet Domain (Public Network) |Private Network Connection Endpoint Service (**NOT a domain name**, please refer to the [Private Network Connection](https://docs.byteplus.com/en/docs/VikingDB/APIV2Upgrade) documentation) |
|---|---|---|---|
|Asia Pacific (Johor) |ap\-southeast\-1 |[vikingdb.ap-southeast-1.byteplusapi.com](http://vikingdb.ap-southeast-1.byteplusapi.com/) |com.bytepluses.privatelink.ap\-southeast\-1.api.vikingdb |


```go
package main

import (
    "fmt"
    "os"

    "github.com/volcengine/volcengine-go-sdk/service/vikingdb"
    "github.com/volcengine/volcengine-go-sdk/volcengine"
    "github.com/volcengine/volcengine-go-sdk/volcengine/credentials"
    "github.com/volcengine/volcengine-go-sdk/volcengine/session"
)

func main() {
    var (
       accessKey = os.Getenv("VIKINGDB_AK")
       secretKey = os.Getenv("VIKINGDB_SK")
       region    = "ap-southeast-1"
    )
    config := volcengine.NewConfig().
       WithRegion(region).
       WithCredentials(credentials.NewStaticCredentials(accessKey, secretKey, ""))

    sess, err := session.NewSession(config)
    if err != nil {
       panic(err)
    }
    svc := vikingdb.New(sess)

    fmt.Printf("APIVersion: %s\n", svc.APIVersion)
}
```
