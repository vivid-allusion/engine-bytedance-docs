---
title: "Use TLS SDK for Java to consume logs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/tls_sdk_for_java_to_consume_logs"
---

Torch Log Service (TLS) allows you to use an SDK to consume log data collected to the server. This topic offers sample code that demonstrates how to use TLS SDK for Java to consume logs.

<span id="42302ef5"></span>
## Before you begin


* Install TLS SDK for Java. For more information, refer to [Install TLS SDK for Java](https://docs.byteplus.com/docs/tls/install_tls_sdk_for_java).

* Add environment variables such as `VOLCENGINE_ACCESS_KEY_ID`. For information on how to configure environment variables, refer to [Configure identity authentication](https://docs.byteplus.com/docs/tls/configuring_identity_authentication).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">We recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard\-coded AccessKey information leads to data security risks.   </div>
   

<span id="808857bb"></span>
## Consuming logs

<span id="34aff17e"></span>
### Scenario description

This topic offers sample code that demonstrates how to use TLS SDK for Java to consume log data. TLS SDK for Java supports the following methods to write logs:


|Method |Description |
|---|---|
|Consumer |Recommended.<br><br>In the actual production environment, use Java Consumer to consume log data to improve efficiency. Java Consumer consumes the data of all shards in a topic in a balanced way. Go Consumer features asynchronous consumption, high performance, retry on failure, and graceful shutdown. To get the sample code, refer to [Using Java Consumer to consume logs](https://docs.byteplus.com/docs/tls/tls_sdk_for_java_to_consume_logs#f0d3b108). For information on how to use consumer groups to consume logs, refer to [Use ConsumeLogs to consume logs](https://docs.byteplus.com/docs/tls/use_consumelogs_to_consume_logs) and [Use TLS SDK for Java consumer groups to consume logs](https://docs.byteplus.com/docs/tls/tls_sdk_for_java_consumer_groups_to_consume_logs). |
|ConsumeLogs |Not recommended.<br><br>TLS allows you to call ConsumeLogs to consume logs using synchronous requests. The progress of consuming logs is limited by the read and write performance of a single shard and must be maintained manually. In addition, the consumption logic and process are cumbersome in automatic sharding scenarios.<br><br>If you use the HashKey Routing Shard mode when you call PutLogs, log data is written to the specified shard in sequence. In this case, you can call ConsumeLogs to consume the log data in a specific shard. To get the sample code, refer to [Using the synchronous ConsumeLogs API action to consume logs](https://docs.byteplus.com/docs/tls/tls_sdk_for_java_to_consume_logs#c2e84e4b). |


<span id="f0d3b108"></span>
### Using Java Consumer to consume logs

The following sample code demonstrates how to use Java Consumer to consume log data.

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


<span id="c2e84e4b"></span>
### Using the synchronous ConsumeLogs API action to consume logs

The following sample code demonstrates how to use the synchronous ConsumeLogs API action to consume log data.

```Go
package com.volcengine.example.tls.demo;

import com.volcengine.model.tls.*;
import com.volcengine.model.tls.exception.LogException;
import com.volcengine.model.tls.pb.PutLogRequest;
import com.volcengine.model.tls.request.*;
import com.volcengine.model.tls.response.*;
import com.volcengine.service.tls.TLSLogClient;

import java.util.ArrayList;
import java.util.List;


public class Demo {
    public static void main(String[] args) throws LogException {
        // Initialize the SDK. Specify the endpoint, Region, AcccessKey ID, AccessKey secret, and token based on your account and service information. Note that the token can be null.
        ClientConfig clientConfig = new ClientConfig(System.getenv("VOLCENGINE_ENDPOINT"), System.getenv("VOLCENGINE_REGION"),
            System.getenv("VOLCENGINE_ACCESS_KEY_ID"), System.getenv("VOLCENGINE_ACCESS_KEY_SECRET"), System.getenv("VOLCENGINE_TOKEN"));
        TLSLogClient client = ClientBuilder.newClient(clientConfig);

        // Specify TopicID and shardID from which you want to consume logs.
        String topicID = "your-topic-id";
        int shardID = 0;

        // Get the start cursor of log consumption.
        DescribeCursorRequest describeCursorRequest = new DescribeCursorRequest(topicID, shardID, "begin");
        DescribeCursorResponse describeCursorResponse = client.describeCursor(describeCursorRequest);
        String beginCursor = describeCursorResponse.getCursor();

        // Consume log data.
        // Specify parameters such as TopicId, ShardId, Cursor, LogGroupCount, and Compression as needed. We recommend that you use LZ4 for compression.
        // Call DescribeCursor again to get the end cursor of log consumption as the value of EndCursor in the ConsumeLogs API request.
        ConsumeLogsRequest consumeLogsRequest = new ConsumeLogsRequest();
        consumeLogsRequest.setTopicId(topicID);
        consumeLogsRequest.setShardId(shardID);
        consumeLogsRequest.setCursor(beginCursor);
        consumeLogsRequest.setLogGroupCount(1000);
        consumeLogsRequest.setCompression("lz4");
        ConsumeLogsResponse consumeLogsResponse = client.consumeLogs(consumeLogsRequest);
        PutLogRequest.LogGroupList logGroupList = consumeLogsResponse.getLogGroupList();
    }
}
```


<span id="7e501ac6"></span>
## Related documents


* After you use the SDK to send an API request, the server returns a response. If the response contains a non\-200 status code, the API call fails. To view the error code and error message, refer to API reference.

* For more information on Java Consumer, refer to [Java Consumer](https://github.com/volcengine/volc-sdk-java/tree/main/volc-sdk-java/src/main/java/com/volcengine/model/tls/consumer).

* To get the complete sample code of consuming logs using Java Consumer, refer to [TLS Java SDK Demo on GitHub](https://github.com/volcengine/volc-sdk-java/blob/main/example/src/main/java/com/volcengine/example/tls/demo/ConsumerDemo.java).
