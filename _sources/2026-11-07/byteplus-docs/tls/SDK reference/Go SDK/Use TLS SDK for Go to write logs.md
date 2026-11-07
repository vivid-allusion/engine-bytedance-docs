---
title: "Use TLS SDK for Go to write logs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/use_tls_sdk_for_go_to_write_logs"
---

Go Producer sends log data quickly in massive data scenarios. This topic offers sample code that demonstrates how to use Go Producer to collect log data.

<span id="10a7159b"></span>
## Before you begin


* Install TLS SDK for Go. For more information, refer to [Install TLS SDK for Go](https://docs.byteplus.com/docs/tls/install_tls_for_go).

* Run the following command to install the proto dependency:

   ```Shell
   go get -u github.com/gogo/protobuf/proto
   ```
   

* Add environment variables such as `VOLCENGINE_ACCESS_KEY_ID`. For information on how to configure environment variables, refer to [Configure identity authentication](https://docs.byteplus.com/docs/tls/configuring_identity_authentication).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">We recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard\-coded AccessKey information leads to data security risks.   </div>
   

<span id="02c67a70"></span>
## Writing log data

<span id="20199ae7"></span>
### Scenario description

This topic offers sample code that demonstrates how to write log data to TLS using the SDK. TLS SDK for Go supports the following methods to write log data:


|Method |Description |
|---|---|
|PutLogs |Not recommended.<br><br>TLS allows you to call PutLogs to upload logs using synchronous requests. If you use PutLogs to upload logs, we recommend that you aggregate multiple log entries and call PutLogs once. Compared with uploading log entries one by one, log aggregation can improve throughput and avoid rate limiting. |
|Producer |Recommended.<br><br>In the actual production environment, use Go Producer to write log data to improve efficiency. Go Producer sends log data quickly in massive data and high\-concurrency scenarios. Go Producer features asynchronous sending, high performance, retry on failure, and graceful shutdown. |


<span id="2f282a39"></span>
### Sample code

The following sample code demonstrates how to use Go Producer to collect log data.

```Go
package tls

import (
    "fmt"
    "os"
    "time"

    "github.com/volcengine/volc-sdk-golang/service/tls"
    "github.com/volcengine/volc-sdk-golang/service/tls/pb"
    "github.com/volcengine/volc-sdk-golang/service/tls/producer"
)

func main() {
    // When you initialize the client, we recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard-coded AccessKey information leads to data security risks.
    // If you use Security Token Service (STS), use a temporary AccessKey ID and AccessKey secret, and set VOLCENGINE_TOKEN. If you do not use STS, leave VOLCENGINE_TOKEN empty.
    tlsProducerCfg := producer.GetDefaultProducerConfig()
    tlsProducerCfg.Endpoint = os.Getenv("VOLCENGINE_ENDPOINT")
    tlsProducerCfg.Region = os.Getenv("VOLCENGINE_REGION")
    tlsProducerCfg.AccessKeyID = os.Getenv("VOLCENGINE_ACCESS_KEY_ID")
    tlsProducerCfg.AccessKeySecret = os.Getenv("VOLCENGINE_ACCESS_KEY_SECRET")

    // Initialize and start the producer.
    tlsProducer := producer.NewProducer(tlsProducerCfg)
    tlsProducer.Start()

    // Specify topicId, source, and filename as needed.
    topicID := "your-topic-id"
    source := "your-log-source"
    filename := "your-log-filename"

    // Call SendLog offered by Go Producer to submit one log entry at a time.
    // Customize a callback to handle business in the SendLog API request as needed.
    err := tlsProducer.SendLog("", topicID, source, filename, &pb.Log{
       Contents: []*pb.LogContent{
          {
             Key:   "key1",
             Value: "value1",
          },
          {
             Key:   "key2",
             Value: "value2",
          },
       },
       Time: time.Now().Unix(),
    }, nil)
    if err != nil {
       // Handle an error.
       fmt.Println(err.Error())
    }

    // Call SendLogs offered by Go Producer to submit multiple log entries at a time.
    // Customize a callback to handle business in the SendLogs API request as needed.
    err = tlsProducer.SendLogs("", topicID, source, filename, &pb.LogGroup{
       Source:   source,
       FileName: filename,
       Logs: []*pb.Log{
          {
             Contents: []*pb.LogContent{
                {
                   Key:   "key1",
                   Value: "value1-1",
                },
                {
                   Key:   "key2",
                   Value: "value2-1",
                },
             },
             Time: time.Now().Unix(),
          },
          {
             Contents: []*pb.LogContent{
                {
                   Key:   "key1",
                   Value: "value1-2",
                },
                {
                   Key:   "key2",
                   Value: "value2-2",
                },
             },
             Time: time.Now().Unix(),
          },
       },
    }, nil)
    if err != nil {
       // Handle an error.
       fmt.Println(err.Error())
    }

    // Close the producer.
    tlsProducer.Close()
}
```


<span id="9132f7da"></span>
## Related documents


* After you use the SDK to send an API request, the server returns a response. If the response contains a non\-200 status code, the API call fails. To view the error code and error message, refer to API reference.

* For more information on Go Producer, refer to [Go Producer](https://github.com/volcengine/volc-sdk-golang/tree/main/service/tls/producer).

* To get the complete sample code of uploading logs using Go Producer, refer to [TLS Go SDK Demo on GitHub](https://github.com/volcengine/volc-sdk-golang/blob/main/example/tls/demo_producer.go).
