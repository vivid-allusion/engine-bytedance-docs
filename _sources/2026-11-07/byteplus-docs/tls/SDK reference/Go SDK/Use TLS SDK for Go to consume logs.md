---
title: "Use TLS SDK for Go to consume logs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/use_tls_sdk_for_go_to_consume_logs"
---

Torch Log Service (TLS) allows you to use an SDK to consume log data collected to the server. This topic offers sample code that demonstrates how to use TLS SDK for Go to consume logs.

<span id="97842ffd"></span>
## Before you begin


* Install TLS SDK for Go. For more information, refer to [Install TLS SDK for Go](https://docs.byteplus.com/docs/tls/install_tls_for_go).

* Run the following command to install the proto dependency:

   ```Shell
   go get -u github.com/gogo/protobuf/proto
   ```
   

* Add environment variables such as `VOLCENGINE_ACCESS_KEY_ID`. For information on how to configure environment variables, refer to [Configure identity authentication](https://docs.byteplus.com/docs/tls/configuring_identity_authentication).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">We recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard\-coded AccessKey information leads to data security risks.   </div>
   

<span id="219833ee"></span>
## Consuming logs

<span id="98a429f6"></span>
### Scenario description

This topic offers sample code that demonstrates how to use TLS SDK for Go to consume log data. TLS SDK for Go supports the following methods to write log data:


|Method |Description |
|---|---|
|Consumer |Recommended.<br><br>In the actual production environment, use Go Consumer to consume log data to improve efficiency. Go Consumer consumes the data of all shards in a topic in a balanced way. Go Consumer features asynchronous consumption, high performance, retry on failure, and graceful shutdown. To get the sample code, refer to [Using Go Consumer to consume logs](https://docs.byteplus.com/docs/tls/use_tls_sdk_for_go_to_consume_logs#e68335ba). For information on how to use consumer groups to consume logs, refer to [Use ConsumeLogs to consume logs](https://docs.byteplus.com/docs/tls/use_consumelogs_to_consume_logs) and [Use TLS SDK for Go consumer groups to consume logs](https://docs.byteplus.com/docs/tls/go_sdk_consumer_groups_to_consume_logs). |
|ConsumeLogs |Not recommended.<br><br>TLS allows you to call ConsumeLogs to consume logs using synchronous requests. The progress of consuming logs is limited by the read and write performance of a single shard and must be maintained manually. In addition, the consumption logic and process are cumbersome in automatic sharding scenarios.<br><br>If you use the HashKey Routing Shard mode when you call PutLogs, log data is written to the specified shard in sequence. In this case, you can call ConsumeLogs to consume the log data in a specific shard. To get the sample code, refer to [Using the synchronous ConsumeLogs API action to consume logs](https://docs.byteplus.com/docs/tls/use_tls_sdk_for_go_to_consume_logs#c2e84e4b). |


<span id="e68335ba"></span>
### Use Go Consumer to consume logs

The following sample code demonstrates how to use Go Consumer to consume log data.

```Go
package tls

import (
    "context"
    "fmt"
    "os"
    "time"

    "github.com/pkg/errors"
    log_consumer "github.com/volcengine/volc-sdk-golang/service/tls/consumer"
    "github.com/volcengine/volc-sdk-golang/service/tls/pb"
)

func launchConsumer() error {
    // Get the default configurations of a consumer group.
    consumerCfg := log_consumer.GetDefaultConsumerConfig()
    // Specify basic information such as Endpoint, Region, AccessKeyID, and AccessKeySecret.
    consumerCfg.Endpoint = os.Getenv("VOLCENGINE_ENDPOINT")
    consumerCfg.Region = os.Getenv("VOLCENGINE_REGION")
    consumerCfg.AccessKeyID = os.Getenv("VOLCENGINE_ACCESS_KEY_ID")
    consumerCfg.AccessKeySecret = os.Getenv("VOLCENGINE_ACCESS_KEY_SECRET")
    // Specify your project ID and topic ID list.
    consumerCfg.ProjectID = "<YOUR-PROJECT-ID>"
    consumerCfg.TopicIDList = []string{"<YOUR-TOPIC-ID>"}
    // Specify the name of the consumer group. If you did not create a consumer group, the SDK creates a consumer group with the specified name by default.
    consumerCfg.ConsumerGroupName = "<CONSUMER-GROUP-NAME>"
    // Specify the name of the consumer. The name must be unique in the consumer group.
    consumerCfg.ConsumerName = "<CONSUMER_NAME>"

    // Implement a log consumption function to handle LogGroupList as needed.
    // The following sample code prints the key-value pair of each log entry that is consumed.
    var handleLogs = func(topicID string, shardID int, l *pb.LogGroupList) {
       fmt.Printf("received new logs from topic: %s, shard: %d\n", topicID, shardID)
       for _, logGroup := range l.LogGroups {
          for _, log := range logGroup.Logs {
             for _, content := range log.Contents {
                fmt.Printf("%s: %s\n", content.Key, content.Value)
             }
          }
       }
    }
    
    // Create a consumer.
    consumer, err := log_consumer.NewConsumer(context.TODO(), consumerCfg, handleLogs)
    if err != nil {
       return errors.Wrap(err, "get new consumer failed: ")
    }

    // Start the consumer.
    if err := consumer.Start(); err != nil {
       return errors.Wrap(err, "start consumer failed: ")
    }

    // Wait for log data to be consumed.
    <-time.After(time.Second * 60)

    // Stop the consumer.
    consumer.Stop()

    return nil
}

func main() {
    if err := launchConsumer(); err != nil {
       fmt.Println(err.Error())
    }
}
```


<span id="c2e84e4b"></span>
### Use the synchronous ConsumeLogs API action to consume logs

The following sample code demonstrates how to use the synchronous ConsumeLogs API action to consume log data.

```Go
package tls

import (
    "fmt"
    "github.com/volcengine/volc-sdk-golang/service/tls"
    "github.com/volcengine/volc-sdk-golang/service/tls/pb"
)

func main() {
    // When you initialize the client, we recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard-coded AccessKey information leads to data security risks. 
    // If you use Security Token Service (STS), use a temporary AccessKey ID and AccessKey secret, and set VOLCENGINE_TOKEN. If you do not use STS, leave VOLCENGINE_TOKEN empty.
    client := tls.NewClient(os.Getenv("VOLCENGINE_ENDPOINT"), os.Getenv("VOLCENGINE_ACCESS_KEY_ID"),
        os.Getenv("VOLCENGINE_ACCESS_KEY_SECRET"), os.Getenv("VOLCENGINE_TOKEN"), os.Getenv("VOLCENGINE_REGION"))

    // Specify TopicID and shardID from which you want to consume logs.
    topicID := "TopicId"
    shardID := 0

    // Get the start cursor of log consumption.
    describeCursorResp, err := client.DescribeCursor(&tls.DescribeCursorRequest{
       TopicID: topicID,
       ShardID: shardID,
       From:    "begin",
    })
    if err != nil {
       // Handle an error.
       fmt.Println(err.Error())
    }
    beginCursor := describeCursorResp.Cursor

    // Consume log data.
    // Specify parameters such as TopicId, ShardId, Cursor, LogGroupCount, and Compression as needed. We recommend that you use LZ4 for compression.
    // Call DescribeCursor again to get the end cursor of log consumption as the value of EndCursor in the ConsumeLogs API request.
    logGroupCount := 1000
    compression := "lz4"
    resp, err := client.ConsumeLogs(&tls.ConsumeLogsRequest{
       TopicID:       topicID,
       ShardID:       shardID,
       Cursor:        beginCursor,
       LogGroupCount: &logGroupCount,
       Compression:   &compression,
    })
    if err != nil {
       // Handle an error.
       fmt.Println(err.Error())
    }

    handleLogs(topicID, shardID, resp.Logs)
}

// Implement a log consumption function to handle LogGroupList as needed.
// The following sample code prints the key-value pair of each log entry that is consumed.
func handleLogs(topicID string, shardID int, l *pb.LogGroupList) {
    fmt.Printf("received new logs from topic: %s, shard: %d\n", topicID, shardID)
    for _, logGroup := range l.LogGroups {
       for _, log := range logGroup.Logs {
          for _, content := range log.Contents {
             fmt.Printf("%s: %s\n", content.Key, content.Value)
          }
       }
    }
}
```


<span id="8c7cd6d3"></span>
## Related documents


* After you use the SDK to send an API request, the server returns a response. If the response contains a non\-200 status code, the API call fails. To view the error code and error message, refer to API reference.

* For more information on Go Consumer, refer to [Go Consumer](https://github.com/volcengine/volc-sdk-golang/tree/main/service/tls/consumer).

* To get the complete sample code of consuming logs using Go Consumer, refer to [TLS Go SDK Demo on GitHub](https://github.com/volcengine/volc-sdk-golang/blob/main/example/tls/demo_consumer.go).
