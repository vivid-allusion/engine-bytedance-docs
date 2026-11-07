---
title: "Use TLS SDK for Java consumer groups to consume logs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/tls_sdk_for_java_consumer_groups_to_consume_logs"
---

Torch Log Service (TLS) SDKs offer the ConsumerGroup feature that allows you to consume log data using consumer groups. This topic describes how to use TLS SDK for Java consumer groups to consume logs.

<span id="749e52ee"></span>
## Before you begin


* Install TLS SDK for Java. For more information, refer to [Install TLS SDK for Java](https://docs.byteplus.com/docs/tls/install_tls_sdk_for_java).

* Add environment variables such as `VOLCENGINE_ACCESS_KEY_ID`. For information on how to configure environment variables, refer to [Configure identity authentication](https://docs.byteplus.com/docs/tls/configuring_identity_authentication).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">We recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard\-coded AccessKey information leads to data security risks.   </div>
   

<span id="5eaf4254"></span>
## Configuration description

When you use consumer groups to consume data, TLS automatically allocates shards to balance the consumption capability and progress of each consumer group. Therefore, you do not need to consider internal scheduling, load balancing among consumers, or failovers that may occur. Just focus on your business logic.

For information on the relevant terms, refer to [Use ConsumeLogs to consume logs](https://docs.byteplus.com/docs/tls/use_consumelogs_to_consume_logs).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">TLS SDK consumer groups support automatically retrying failed requests and reporting the checkpoints. Therefore, you only need to focus on the business logic of handling LogGroupList generated after log data is consumed each time.</div>


In TLS SDK for Java, the ConsumerConfig constructor returns the default config of a consumer group. In the config, specify basic information such as the endpoint, Region, AccessKey ID, and AccessKey secret, as well as the project ID, topic ID list, consumer group name, and consumer name.

In addition, you can use the setter method to set other ConsumerConfig parameters as needed. The following table describes the ConsumerConfig parameters:


|Parameter |Type |Example |Description |
|---|---|---|---|
|maxFetchLogGroupCount |int |100 |The maximum number of log groups when the consumer consumes log data each time. Default value: 100. Maximum value: 1000. |
|heartbeatIntervalInSecond |int |20 |The interval at which the consumer reports a heartbeat. Unit: seconds. |
|dataFetchIntervalInMillisecond |int |200 |The interval at which the consumer consumes log data. Unit: milliseconds. |
|flushCheckpointIntervalInSecond |int |5 |The interval at which the consumer uploads the consumption progress. Unit: seconds. |
|consumeFrom |String |begin |The default consumer offset when the consumption starts. The value is consistent with that of From in the DescribeCursor API action. The parameter takes effect only when the consumer has not uploaded consumer offsets. |
|orderedConsume |boolean |false |Whether to enable consumption in sequence. If enabled, the consumer consumes log data based on the parent\-child relationship of shard splitting.<br><br>For example, Shard 0 is split into Shard 1 and Shard 2, while Shard 1 is then split into Shard 3 and Shard 4. If the feature is enabled, log data is consumed in the sequence of (Shard 0) \> (Shard 1, Shard 2) \> (Shard 2, Shard 3, Shard 4). |


<span id="8df13ef6"></span>
## Sample code

The following sample code demonstrates how to use TLS SDK for Java to create a consumer group and consumers to consume logs.

```Java
package com.volcengine.example.tls.demo;

import java.util.ArrayList;
import java.util.List;

import com.volcengine.model.tls.consumer.ConsumerConfig;
import com.volcengine.model.tls.exception.LogException;
import com.volcengine.model.tls.pb.PutLogRequest;
import com.volcengine.service.tls.consumer.Consumer;
import com.volcengine.service.tls.consumer.ConsumerImpl;
import com.volcengine.service.tls.consumer.LogProcessor;


// Define a class to implement LogProcessor.
public class ConsumerDemo implements LogProcessor {
    public static void main(String[] args) throws LogException, InterruptedException {
        // When you initialize the client, we recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard-coded AccessKey information leads to data security risks. 
        // If you use Security Token Service (STS), use a temporary AccessKey ID and AccessKey secret, and set VOLCENGINE_TOKEN. If you do not use STS, leave VOLCENGINE_TOKEN empty. 
        ConsumerConfig config = new ConsumerConfig(System.getenv("VOLCENGINE_ENDPOINT"), System.getenv("VOLCENGINE_REGION"),
                System.getenv("VOLCENGINE_ACCESS_KEY_ID"), System.getenv("VOLCENGINE_ACCESS_KEY_SECRET"), System.getenv("VOLCENGINE_TOKEN"));
        // Specify your project ID.
        config.setProjectID("your-project-id");
        // Specify the topic ID list for consumption.
        config.setTopicIDList(new ArrayList<String>(){{
            add("your-topic-id");
        }});
        // Specify the name of the consumer group.
        config.setConsumerGroupName("java-consumer-group");
        // Specify the name of the consumer.
        config.setConsumerName("java-consumer");

        // Instantiate ConsumerImpl, and call consumer.start() to continuously consume log data.
        Consumer consumer = new ConsumerImpl(config, new ConsumerDemo());
        consumer.start();

        // Call consumer.stop() to end consumption by the consumer group.
        Thread.sleep(10000);
        consumer.stop();
    }

    /**
     Implement a process method to handle LogGroupList generated after log data is consumed each time as needed.
     The following sample code prints each log entry that is consumed.
     */
    @Override
    public void process(String topicID, int shardID, PutLogRequest.LogGroupList logGroupList) {
        System.out.println(topicID + " --- " + shardID);
        System.out.println(logGroupList.getLogGroupsCount());

        int count = 0;

        List<PutLogRequest.LogGroup> logGroups = logGroupList.getLogGroupsList();
        for (PutLogRequest.LogGroup logGroup: logGroups) {
            List<PutLogRequest.Log> logs = logGroup.getLogsList();
            for (PutLogRequest.Log log: logs) {
                count++;
                System.out.println("*** Count = " + count + " ***");
                List<PutLogRequest.LogContent> logContents = log.getContentsList();
                for (PutLogRequest.LogContent logContent: logContents) {
                    System.out.println(logContent.getKey() + ": " + logContent.getValue());
                }
                System.out.println();
            }
        }
    }
}
```
