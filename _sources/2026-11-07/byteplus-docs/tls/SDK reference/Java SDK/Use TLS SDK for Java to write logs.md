---
title: "Use TLS SDK for Java to write logs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/tls_sdk_for_java_to_write_logs"
---

Java Producer sends log data quickly in massive data scenarios. This topic offers sample code that demonstrates how to use Java Producer to collect log data.

<span id="d42d6a18"></span>
## Before you begin


* Install TLS SDK for Java. For more information, refer to [Install TLS SDK for Java](https://docs.byteplus.com/docs/tls/install_tls_sdk_for_java).

* Add environment variables such as `VOLCENGINE_ACCESS_KEY_ID`. For information on how to configure environment variables, refer to [Configure identity authentication](https://docs.byteplus.com/docs/tls/configuring_identity_authentication).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">We recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard\-coded AccessKey information leads to data security risks.   </div>
   

<span id="a40187db"></span>
## Writing log data

<span id="5dcc65e8"></span>
### Scenario description

This topic offers sample code that demonstrates how to write log data to TLS using the SDK. TLS SDK for Java supports the following methods to write logs:


|Method |Description |
|---|---|
|PutLogs |Not recommended.<br><br>TLS allows you to call PutLogs to upload logs using synchronous requests. If you use PutLogs to upload logs, we recommend that you aggregate multiple log entries and call PutLogs once. Compared with uploading log entries one by one, log aggregation can improve throughput and avoid rate limiting. |
|Producer |Recommended.<br><br>In the actual production environment, use Java Producer to write log data to improve efficiency. Java Producer sends log data quickly in massive data and high\-concurrency scenarios. Go Producer features asynchronous sending, high performance, retry on failure, and graceful shutdown. |


<span id="c9902b81"></span>
### Sample code

The following sample code demonstrates how to use Java Producer to collect log data.

```Java
package com.volcengine.example.tls.demo;

import com.volcengine.model.tls.LogItem;
import com.volcengine.model.tls.exception.LogException;
import com.volcengine.model.tls.producer.CallBack;
import com.volcengine.model.tls.producer.ProducerConfig;
import com.volcengine.model.tls.producer.Result;
import com.volcengine.service.tls.Producer;
import com.volcengine.service.tls.ProducerImpl;

import java.util.ArrayList;
import java.util.List;


public class Demo {
    public static void main(String[] args) throws LogException, InterruptedException {
        // When you initialize the client, we recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard-coded AccessKey information leads to data security risks. 
        // If you use Security Token Service (STS), use a temporary AccessKey ID and AccessKey secret, and set VOLCENGINE_TOKEN. If you do not use STS, leave VOLCENGINE_TOKEN empty.
        ProducerConfig producerConfig = new ProducerConfig(System.getenv("VOLCENGINE_ENDPOINT"), System.getenv("VOLCENGINE_REGION"),
            System.getenv("VOLCENGINE_ACCESS_KEY_ID"), System.getenv("VOLCENGINE_ACCESS_KEY_SECRET"), System.getenv("VOLCENGINE_TOKEN"));
        // Instantiate and start the producer.
        Producer producer = new ProducerImpl(producerConfig);
        producer.start();

        // Specify topicId, source, and filename as needed.
        String topicID = "your-topic-id";
        String source = "your-log-source";
        String filename = "your-log-filename";
        // If a callback is not required, pass null for the callback in sendLogV2 and sendLogsV2 offered by Java Producer.
        CallBack callBack = new CallBack() {
            @Override
            public void onComplete(Result result) {
                System.out.println("producer result:" + result);
            }
        };

        LogItem item;

        // Call sendLogV2 offered by Java Producer to submit one log entry at a time.
        item = new LogItem();
        item.setTime(System.currentTimeMillis());
        item.addContent("key1", "value1");
        item.addContent("key2", "value2");
        producer.sendLogV2("", topicID, source, filename, item, callBack);

        // Call sendLogsV2 offered by Java Producer to submit multiple log entries at a time.
        List<LogItem> items = new ArrayList<>();
        for (int i = 1; i <= 1000; i++) {
            item = new LogItem();
            item.setTime(System.currentTimeMillis());
            item.addContent("key1", "value1-" + i);
            item.addContent("key2", "value2-" + i);
            items.add(item);
        }
        producer.sendLogsV2("", topicID, source, filename, items, callBack);

        // Close the producer.
        producer.close();
    }
}
```


<span id="e48c042a"></span>
## Related documents


* After you use the SDK to send an API request, the server returns a response. If the response contains a non\-200 status code, the API call fails. To view the error code and error message, refer to API reference.

* For more information on Java Producer, refer to [Java Producer](https://github.com/volcengine/volc-sdk-java/tree/main/volc-sdk-java/src/main/java/com/volcengine/model/tls/producer).

* To get the complete sample code of uploading logs using Java Producer, refer to [TLS Java SDK Demo on GitHub](https://github.com/volcengine/volc-sdk-java/blob/main/example/src/main/java/com/volcengine/example/tls/demo/ProducerDemo.java).
