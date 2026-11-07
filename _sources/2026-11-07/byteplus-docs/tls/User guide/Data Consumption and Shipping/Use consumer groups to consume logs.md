---
title: "Use consumer groups to consume logs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/using_consumer_groups_to_consume_logs"
---

Torch Log Service (TLS) allows you to consume data using consumer groups and offers a series of SDKs to manage consumer groups. This topic describes how to use consumer groups to consume data.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

TLS offers the [ConsumeLogs](https://docs.byteplus.com/en/docs/tls/api-consumelogs) API to consume log data collected to the server in real time. When you use the ConsumeLogs API, you must specify the topic ID, shard ID, start cursor, and end cursor to consume shard\-level log data. The progress of consuming logs is limited by the read and write capacity of a single shard and must be maintained manually. In addition, the consumption logic and process are cumbersome in automatic sharding scenarios.

TLS offers the consumer group feature through the SDK, so you can use consumer groups to consume log data. When you use consumer groups to consume data, TLS automatically allocates shards to balance the consumption capability and progress of each consumer group. Therefore, you do not need to consider internal scheduling, load balancing among consumers, or failovers that may occur. Just focus on your business logic.

<span id=".5Z-65pys5qaC5b-1"></span>
## Terms


|Term |Description |
|---|---|
|Consumer group |A virtual collection of multiple consumers. When you consume log data using a consumer group, all consumers in the consumer group subscribe to the same topic and consume data in that topic. Each consumer consumes data in one or more shards of a topic. Consumers do not repeatedly consume data. |
|Consumer |A client to consume data from TLS. It is part of a consumer group.<br><br><br>* The consumer name in a consumer group must be unique.<br><br>* A shard of a topic is assigned to a specific consumer in a consumer group. One consumer can consume data from multiple shards. During the running process of a consumer group, the relationship between consumers and shards may change. |
|Checkpoint |When a shard is being consumed by a consumer, the current checkpoint of the shard is recorded and reported to the server. The checkpoint is the start cursor when the application restarts to ensure that data is not consumed repeatedly. |


<span id=".6ZmQ5Yi26K-05piO"></span>
## Limits


* Up to 150 consumer groups can be configured for each project.

* One consumer group can consume multiple topics in the same project, but cannot consume data across projects.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Before you begin


* Create and get a BytePlus AccessKey pair.

* The AccessKey pair of a BytePlus account has the permissions to access all API actions. We recommend that you use an IAM user to call API actions or perform routine O&M. Before you use an IAM user, use a BytePlus account to grant the IAM user the permissions to operate consumer groups. For the sample code of authorization, refer to [Permissions policy template](https://docs.byteplus.com/docs/tls/Permissions_policy_template).

* Install TLS SDK for Go. Currently, TLS SDKs that support consumer groups include [SDK for Go overview](https://docs.byteplus.com/docs/tls/go_sdk_overview), [SDK for Java overview](https://docs.byteplus.com/docs/tls/tls_sdk_for_java_overview) and [SDK for Python overview](https://docs.byteplus.com/docs/tls/tls_sdk_for_python_overview).


<span id=".6YCa6L-H5raI6LS557uE5raI6LS55pWw5o2u"></span>
## Use consumer groups to consume logs

TLS offers an asynchronous log consumption library that allows consumers to consume multiple topics in the same project. It features asynchronous consumption, high performance, retry upon failure, and graceful shutdown. You can use TLS SDK for Go, TLS SDK for Java, or TLS SDK for Python to manage consumer groups and consume log data.

<span id=".56S65L6L5Luj56CB"></span>
### Sample code

The following sample code demonstrates how to use TLS SDK for Go to create a consumer group and consumers to consume logs.

```go
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
    consumerCfg.Endpoint = os.Getenv("LOG_SERVICE_ENDPOINT")
    consumerCfg.Region = os.Getenv("LOG_SERVICE_REGION")
    consumerCfg.AccessKeyID = os.Getenv("LOG_SERVICE_AK")
    consumerCfg.AccessKeySecret = os.Getenv("LOG_SERVICE_SK")
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


<span id=".6YWN572u6K-05piO"></span>
### Configuration description

TLS SDKs allow you to configure the details of a consumer group through parameters to manage the consumption logic. For example, specify whether to enable consumption in order, and specify the interval at which a consumer reports a heartbeat.

For example, in the preceding sample code of TLS SDK for Go, the `log_consumer.GetDefaultConsumerConfig()` function returns the default consumerCfg of the consumer group. The sample code demonstrates how to specify basic information such as Endpoint, Region, AccessKeyID, and AccessKeySecret, as well as the project ID, topic ID list, consumer group name, and consumer name. In addition, you can set other consumerCfg parameters as needed. The following table describes the consumerCfg parameters:


|Parameter |Type |Example |Description |
|---|---|---|---|
|MaxFetchLogGroupCount |Integer |100 |The maximum number of log groups when the consumer consumes log data each time. Default value: 100. Maximum value: 1000. |
|HeartbeatIntervalInSecond |Integer |20 |The interval at which the consumer reports a heartbeat. Unit: seconds. |
|DataFetchIntervalInMillisecond |Integer |200 |The interval at which the consumer consumes log data. Unit: milliseconds. |
|FlushCheckpointIntervalSecond |Integer |5 |The interval at which the consumer uploads the consumption progress. Unit: seconds. |
|ConsumeFrom |String |begin |The default consumer offset when the consumption starts. The value is consistent with that of From in the DescribeCursor API action. The parameter takes effect only when the consumer has not uploaded consumer offsets. |
|OrderedConsume |Boolean |FALSE |Whether to enable consumption in sequence. If enabled, the consumer consumes log data based on the parent\-child relationship of shard splitting.<br><br>For example, Shard 0 is split into Shard 1 and Shard 2, while Shard 1 is then split into Shard 3 and Shard 4. If the feature is enabled, log data is consumed in the sequence of (Shard 0) \> (Shard 1, Shard 2) \> (Shard 2, Shard 3, Shard 4). |
|LoggerConfig |LoggerConfig |/ |For information on log configurations, refer to the following table. |


LoggerConfig configurations


|Parameter |Type |Example |Description |
|---|---|---|---|
|LogLevel |String |info |The log output level. Default value: info. For consumers, four log output levels exist: debug, info, warn, and error. |
|LogFileName |String |50 |The output path of the log file. If not specified, the log file is output to stdout by default. |
|IsJsonType |Boolean |true |Whether to format the file output. Default value: false. |
|LogMaxSize |Integer |10 |The maximum size of a single log file. Default value: 10 MiB. |
|LogCompress |Boolean |true |Whether to enable compression. The default value is false. |


<span id=".5byC5bi45aSE55CG"></span>
### Exception handling

TLS SDK consumer groups support automatically retrying failed requests and reporting the checkpoints. Therefore, you only need to focus on the business logic of handling LogGroupList generated after log data is consumed each time.

<span id=".5p-l55yL5oiW6YeN572u5raI6LS56L-b5bqm"></span>
## View or resetting the consumption progress

When you use consumers to consume log data, you can view the consumption progress at any time. To consume log data in a historical time period or from a specific position in offline data processing scenarios, reset the checkpoint for the consumer group. The checkpoint indicates the position where data consumption starts.

In the TLS console, you can view the consumption progress or reset all checkpoints in a topic subscribed by the consumer group. You can also use an API to reset the checkpoint of a specific shard.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you reset a checkpoint, close the consumption progress. If you reset all checkpoints for a consumer group, close all consumption processes. Otherwise, resetting checkpoints fails.</div>


In the console, perform the following operations:


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Data processing** \> **Log consumption**.

   * View a checkpoint.

      In the list of consumer groups on the left side, click the name of a consumer group to view the latest consumption time of each consumer in each shard.

   * Reset a checkpoint.

      1. In the list of consumer groups on the left side, click the name of a consumer group.

      2. On the upper\-right corner of the page, click **Reset check point**.

      3. Select reset location.

         
         |reset location |Description |
         |---|---|
         |Earliest location |Consume data from the earliest data record in a topic. |
         |Latest location |Skip all historical data, and consume data from the latest data record written to a topic. |
         |Specify the time |Consume data from a specific point in time. The time depends on the data retention period of a topic. When you specify a point in time to reset the checkpoint, you cannot specify a historical or future point in time that is not within the data retention period. |
         

3. Click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[CreateConsumerGroup](https://docs.byteplus.com/en/docs/tls/api-createconsumergroup) |Call the CreateConsumerGroup API to create a consumer group in TLS. |
|[DeleteConsumerGroup](https://docs.byteplus.com/en/docs/tls/api-deleteconsumergroup) |Call the DeleteConsumerGroup API to delete a consumer group in TLS. |
|[DescribeConsumerGroups](https://docs.byteplus.com/en/docs/tls/api-describeconsumergroups) |Call the DescribeConsumerGroups API to get all consumer groups in a project. |
|[ModifyConsumerGroup](https://docs.byteplus.com/en/docs/tls/api-modifyconsumergroup) |Call the ModifyConsumerGroup API to modify the configuration of a consumer group. |
|[ConsumerHeartbeat](https://docs.byteplus.com/en/docs/tls/api-consumerheartbeat) |Call the ConsumerHeartbeat API to send the heartbeat of a consumer in a consumer group to TLS. |
|[DescribeCheckPoint](https://docs.byteplus.com/en/docs/tls/api-describecheckpoint) |Call the DescribeCheckPoint API to view the current checkpoint of a specific shard for a consumer group. |
|[ModifyCheckpoint](https://docs.byteplus.com/en/docs/tls/api-modifycheckpoint) |Call the ModifyCheckPoint API to reset the checkpoint of a specific shard for a consumer group. |
|[ResetCheckPoint](https://docs.byteplus.com/en/docs/tls/api-resetcheckpoint) |Call the ResetCheckPoint API to reset all checkpoints for a consumer group. |
