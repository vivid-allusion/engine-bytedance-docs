---
title: "Use TLS SDK for Go consumer groups to consume logs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/go_sdk_consumer_groups_to_consume_logs"
---

Torch Log Service (TLS) SDKs offer the ConsumerGroup feature that allows you to consume log data using consumer groups. This topic describes how to use TLS SDK for Go consumer groups to consume logs.

<span id="749e52ee"></span>
## Before you begin


* Install TLS SDK for Go. For more information, refer to [Install TLS SDK for Go](https://docs.byteplus.com/docs/tls/install_tls_for_go).

* Run the following command to install the proto dependency:

   ```Shell
   go get -u github.com/gogo/protobuf/proto
   ```
   

* Add environment variables such as `VOLCENGINE_ACCESS_KEY_ID`. For information on how to configure environment variables, refer to [Configure identity authentication](https://docs.byteplus.com/docs/tls/configuring_identity_authentication).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">We recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard\-coded AccessKey information leads to data security risks.   </div>
   

<span id="5eaf4254"></span>
## Configuration description

When you use consumer groups to consume data, TLS automatically allocates shards to balance the consumption capability and progress of each consumer group. Therefore, you do not need to consider internal scheduling, load balancing among consumers, or failovers that may occur. Just focus on your business logic.

For information on the relevant terms, refer to [Use ConsumeLogs to consume logs](https://docs.byteplus.com/docs/tls/use_consumelogs_to_consume_logs).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">TLS SDK consumer groups support automatically retrying failed requests and reporting the checkpoints. Therefore, you only need to focus on the business logic of handling LogGroupList generated after log data is consumed each time.</div>


In TLS SDK for Go, the `log_consumer.GetDefaultConsumerConfig()` function returns the default consumerCfg of a consumer group. You can specify basic information such as Endpoint, Region, AccessKeyID, and AccessKeySecret, as well as the project ID, topic ID list, consumer group name, and consumer name. In addition, you can set other consumerCfg parameters as needed.

The following table describes the consumerCfg parameters:


|Parameter |Type |Example |Description |
|---|---|---|---|
|MaxFetchLogGroupCount |Integer |100 |The maximum number of log groups when the consumer consumes log data each time. Default value: 100. Maximum value: 1000. |
|HeartbeatIntervalInSecond |Integer |20 |The interval at which the consumer reports a heartbeat. Unit: seconds. |
|DataFetchIntervalInMillisecond |Integer |200 |The interval at which the consumer consumes log data. Unit: milliseconds. |
|FlushCheckpointIntervalSecond |Integer |5 |The interval at which the consumer uploads the consumption progress. Unit: seconds. |
|ConsumeFrom |String |begin |The default consumer offset when the consumption starts. The value is consistent with that of From in the DescribeCursor API action. The parameter takes effect only when the consumer has not uploaded consumer offsets. |
|OrderedConsume |Boolean |false |Whether to enable consumption in sequence. If enabled, the consumer consumes log data based on the parent\-child relationship of shard splitting.<br><br>For example, Shard 0 is split into Shard 1 and Shard 2, while Shard 1 is then split into Shard 3 and Shard 4. If the feature is enabled, log data is consumed in the sequence of (Shard 0) \> (Shard 1, Shard 2) \> (Shard 2, Shard 3, Shard 4). |
|LoggerConfig |LoggerConfig |/ |For information on log configurations, refer to the following table. |


LoggerConfig configurations


|Parameter |Type |Example |Description |
|---|---|---|---|
|LogLevel |String |info |The log output level. Default value: info. For consumers, four log output levels exist: debug, info, warn, and error. |
|LogFileName |String |50 |The output path of the log file. If not specified, the log file is output to stdout by default. |
|IsJsonType |Boolean |false |Whether to format the file output. Default value: false. |
|LogMaxSize |Integer |10 |The maximum size of a single log file. Default value: 10 MiB. |
|LogCompress |Boolean |false |Whether to enable log compression. |


<span id="ad7d0d71"></span>
## Sample code

The following sample code demonstrates how to use TLS SDK for Go to create a consumer group and consumers to consume logs.

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
    // We recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard-coded AccessKey information leads to data security risks. 
    // If you use Security Token Service (STS), use a temporary AccessKey ID and AccessKey secret, and set VOLCENGINE_TOKEN. If you do not use STS, leave VOLCENGINE_TOKEN empty.
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
