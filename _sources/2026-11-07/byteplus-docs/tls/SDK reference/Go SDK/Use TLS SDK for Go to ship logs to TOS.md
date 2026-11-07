---
title: "Use TLS SDK for Go to ship logs to TOS"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Use-tls-sdk-for-go-to-ship-logs-to-tos"
---

Torch Log Service (TLS) supports shipping logs to TOS by using SDK. This topic demonstrates through sample code how to ship logs to TOS using the Go SDK.

<span id="a837ea25"></span>
## Before you begin


* Install TLS SDK for Go. For more information, refer to [Install TLS SDK for Go](https://docs.byteplus.com/docs/tls/install_tls_for_go).

* Run the following command to install the proto dependency:

   ```Shell
   go get -u github.com/gogo/protobuf/proto
   ```
   

* Add environment variables such as `VOLCENGINE_ACCESS_KEY_ID`. For information on how to configure environment variables, refer to [Configure identity authentication](https://docs.byteplus.com/docs/tls/configuring_identity_authentication).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">We recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard\-coded AccessKey information leads to data security risks.   </div>
   

<span id="0d2007b1"></span>
## Configuration description

This document demonstrates how to create a configuration for shipping logs to TOS in a specific project using the GO SDK through sample code. For relevant precautions and fee descriptions, please refer to [Overview](https://docs.byteplus.com/docs/tls/Ship_logs_to_tos_overview1).

<span id="7cacaaff"></span>
## Sample code

```Go
package demo

import (
    "github.com/volcengine/volc-sdk-golang/service/tls"
    "os"
    "time"
)

func CreateShipperTosDemo() (*tls.CreateShipperResponse, error) {
    // When you initialize the client, we recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard-coded AccessKey information leads to data security risks.
    // If you use Security Token Service (STS), use a temporary AccessKey ID and AccessKey secret, and set VOLCENGINE_TOKEN. If you do not use STS, leave VOLCENGINE_TOKEN empty.
    client := tls.NewClient(os.Getenv("VOLCENGINE_ENDPOINT"), os.Getenv("VOLCENGINE_ACCESS_KEY_ID"), os.Getenv("VOLCENGINE_ACCESS_KEY_SECRET"), os.Getenv("VOLCENGINE_TOKEN"), os.Getenv("VOLCENGINE_REGION"))
    //create a shipping configuration.
    createShipperRes, err := client.CreateShipper(&tls.CreateShipperRequest{
       TopicId:          "c7****",
       ShipperName:      "tosship",
       ShipperType:      "tos",
       ShipperStartTime: int(time.Now().UnixMilli()),
       ShipperEndTime:   int(time.Now().UnixMilli()) + 3600*1000,
       TosShipperInfo: &tls.TosShipperInfo{
          Bucket:          "mytos",
          Prefix:          "testprefix",
          MaxSize:         10,
          Compress:        "none",
          Interval:        900,
          PartitionFormat: "%Y/%m/%d/%H",
       },
       ContentInfo: &tls.ContentInfo{
          Format: "json",
          JsonInfo: &tls.JsonInfo{
             Keys:   []string{"__content__", "__source__", "__path__"},
             Enable: true,
             Escape: true,
          },
       },
    })

    if err != nil {
       return nil, err
    }

    return createShipperRes, nil
}
```


<span id="f3279d51"></span>
## Related documents


* After you use the SDK to send an API request, the server returns a response. If the response contains a non\-200 status code, the API call fails. To view the error code and error message, refer to API reference.

* The following table describes the API actions involved in the preceding sample code. To view the details of each API action, refer to API reference.

   
   |API |说明 |
   |---|---|
   |[CreateShipper](https://docs.byteplus.com/en/docs/tls/CreateShipper) |Create a shipping configuration. |
   |[DeleteShipper](https://docs.byteplus.com/en/docs/tls/DeleteShipper) |Delete the specified shipping configuration. |
   |[ModifyShipper](https://docs.byteplus.com/en/docs/tls/ModifyShipper) |Modify the specified shipping configuration. |
   |[DescribeShipper](https://docs.byteplus.com/en/docs/tls/DescribeShipper) |Obtain detailed information about the shipping configuration. |
   |[DescribeShippers](https://docs.byteplus.com/en/docs/tls/DescribeShippers) |Obtain the list of shipping configurations. |
