---
title: "Log Configuration (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Log-configuration-go-sdk"
---

The TOS Go SDK provides logging functionality. You can view request\-related information by enabling logs.

<span id=".5pel5b-X6K-05piO"></span>
## Log Description

The SDK records relevant logs separately in each of the following scenarios.


|Scenario |Log Level |
|---|---|
|When requesting the server, the elapsed time, returned HTTP code, and request ID are recorded. |INFO |
|Record the original signature value of the request |DEBUG |
|HTTP Stage Timing for This Interface Invocation |DEBUG |


<span id=".5byA5ZCv5pel5b-X5pa55byP"></span>
## Log Activation Methods

In the Go SDK, logging functionality can be injected by implementing the tos.Logger interface. This interface is currently compatible with the [logrus](https://github.com/sirupsen/logrus) logging library.

```go
package main

import (
   "fmt"
   "os"

   "github.com/sirupsen/logrus"
   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

func main() {
   var (
      accessKey = os.Getenv("TOS_ACCESS_KEY")
      secretKey = os.Getenv("TOS_SECRET_KEY")
     
      endpoint = "*** Provide your endpoint ***"
      region   = "*** Provide your region ***"
   )
  
   logger := logrus.New()
   credential := tos.NewStaticCredentials(ak, sk)
   client, err := tos.NewClientV2(endpoint, tos.WithCredentials(credential), tos.WithRegion(region), tos.WithLogger(logger))
   if err != nil {
      fmt.Println("Error:", err)
      panic(err)
   }

   
   client.Close()
}
```


<span id=".5pel5b-X5YaF5a6556S65L6L"></span>
## Log Content Example

When the default log format is used, the log content is as follows.

```go
time=2022-12-05T10:19:32+08:00 level=info msg=[tos] Response StatusCode:200, RequestId:950b488d553465ee638d5534-ac16898b, Cost:241 ms
time=2022-12-05T10:19:32+08:00 level=info msg=[tos] Response StatusCode:200, RequestId:950b488d553465ef638d5534-ac16898b, Cost:72 ms
time=2022-12-05T10:19:32+08:00 level=info msg=[tos] Response StatusCode:200, RequestId:950b488d553465f1638d5534-ac16898b, Cost:101 ms
```
