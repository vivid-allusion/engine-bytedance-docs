---
title: "Getting started"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/tls_sdk_for_java_getting_started"
---

This topic describes how to use Torch Log Service (TLS) SDK for Java to quickly collect logs, including creating projects, creating topics, writing logs, and querying logs.

<span id="前提条件"></span>
## Before you begin


* Install TLS SDK for Java. For more information, refer to [Install TLS SDK for Java](https://docs.byteplus.com/docs/tls/install_tls_sdk_for_java).

* Add environment variables such as `VOLCENGINE_ACCESS_KEY_ID`. For information on how to configure environment variables, refer to [Configure identity authentication](https://docs.byteplus.com/docs/tls/configuring_identity_authentication).


<span id="9075d484"></span>
## Initializing the client

Initialize the client instance before you can send requests to TLS. When you initialize the client, we recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard\-coded AccessKey information leads to data security risks.

Initialization code:

```java
ClientConfig clientConfig = new ClientConfig(System.getenv("VOLCENGINE_ENDPOINT"), System.getenv("VOLCENGINE_REGION"),
        System.getenv("VOLCENGINE_ACCESS_KEY_ID"), System.getenv("VOLCENGINE_ACCESS_KEY_SECRET"), System.getenv("VOLCENGINE_TOKEN"));
TLSLogClient client = ClientBuilder.newClient(clientConfig);
```


<span id="示例代码"></span>
## Sample code

This section uses the log collection and retrieval processes of TLS as an example to describe how to use TLS SDK for Java to manage basic TLS resources. Create a `test.java` file, and call API actions to create a project, topic, and index, and write, consume, and query log data.

Sample code:

```java
package com.volcengine.example.tls.demo;

import com.volcengine.model.tls.*;
import com.volcengine.model.tls.exception.LogException;
import com.volcengine.model.tls.request.*;
import com.volcengine.model.tls.response.*;
import com.volcengine.service.tls.TLSLogClient;

import java.util.ArrayList;
import java.util.List;

import static com.volcengine.model.tls.Const.LZ4;


public class Demo {
    public static void main(String[] args) throws LogException, InterruptedException {
        // When you initialize the client, we recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard-coded AccessKey information leads to data security risks.
        // If you use Security Token Service (STS), use a temporary AccessKey ID and AccessKey secret, and set VOLCENGINE_TOKEN. If you do not use STS, leave VOLCENGINE_TOKEN empty.
        ClientConfig clientConfig = new ClientConfig(System.getenv("VOLCENGINE_ENDPOINT"), System.getenv("VOLCENGINE_REGION"),
                System.getenv("VOLCENGINE_ACCESS_KEY_ID"), System.getenv("VOLCENGINE_ACCESS_KEY_SECRET"), System.getenv("VOLCENGINE_TOKEN"));
        TLSLogClient client = ClientBuilder.newClient(clientConfig);

        // Create a project.
        // Specify ProjectName and the optional Description as needed. Specify the same Region as that when you initialize the client.
        CreateProjectRequest createProjectRequest = new CreateProjectRequest("project-name", System.getenv("VOLCENGINE_REGION"), "description");
        CreateProjectResponse createProjectResponse = client.createProject(createProjectRequest);
        String projectID = createProjectResponse.getProjectId();

        // Create a topic.
        // Specify parameters such as ProjectId, TopicName, Ttl, Description, and ShardCount as needed.
        CreateTopicRequest createTopicRequest = new CreateTopicRequest();
        createTopicRequest.setProjectId(projectID);
        createTopicRequest.setTopicName("topic-name");
        createTopicRequest.setTtl(30);
        createTopicRequest.setDescription("description");
        createTopicRequest.setShardCount(2);
        CreateTopicResponse createTopicResponse = client.createTopic(createTopicRequest);
        String topicID = createTopicResponse.getTopicId();

        // Create an index.
        // Specify TopicId, and enable full-text indexing or key-value indexing or enable both of them as needed.
        FullTextInfo fullText = new FullTextInfo(false, ",-;", false);
        ValueInfo textValueInfo = new ValueInfo();
        textValueInfo.setValueType("text");
        textValueInfo.setDelimiter(",");
        textValueInfo.setCaseSensitive(false);
        textValueInfo.setIncludeChinese(false);
        textValueInfo.setSqlFlag(false);
        List<KeyValueInfo> keyValue = new ArrayList<>();
        keyValue.add(new KeyValueInfo("test-key", textValueInfo));
        CreateIndexRequest createIndexRequest = new CreateIndexRequest(topicID, fullText, keyValue);
        CreateIndexResponse createIndexResponse = client.createIndex(createIndexRequest);

        // (Not recommended) This section calls PutLogs to upload logs using a synchronous request.
        // (Recommended) In the actual production environment, use Java Producer to write log data to improve efficiency.
        // If you use PutLogs to upload logs, we recommend that you aggregate multiple log entries and call PutLogs once to improve throughput and avoid rate limiting.
        // Specify TopicId, Source, FileName, and Logs as needed. We recommend that you use LZ4.
        List<LogItem> logs = new ArrayList<>();
        for (int i = 0; i < 100; i++) {
            LogItem item = new LogItem(System.currentTimeMillis());
            item.addContent("index", String.valueOf(i));
            item.addContent("test-key", "test-value");
            logs.add(item);
        }
        PutLogsRequestV2 request = new PutLogsRequestV2(logs, topicID, null, LZ4, "log-path", "127.0.0.1");
        PutLogsResponse putLogsResponse = client.putLogsV2(request);
        Thread.sleep(30000);

        // Query and analyze log data.
        // Specify parameters such as TopicId, Query, StartTime, EndTime, and Limit as needed.
        SearchLogsRequest searchLogsRequest = new SearchLogsRequest();
        searchLogsRequest.setTopicId("TopicId");
        searchLogsRequest.setQuery("*");
        searchLogsRequest.setStartTime(1346457600);
        searchLogsRequest.setEndTime(1630454400);
        searchLogsRequest.setLimit(20);
        SearchLogsResponseV2 searchLogsResponse = client.searchLogsV2(searchLogsRequest);

        // Print some basic information in the return value of the SearchLogs API action.
        // Handle other information in the return value as needed.
        System.out.println(searchLogsResponse.getResultStatus());
        System.out.println(searchLogsResponse.getHitCount());
        System.out.println(searchLogsResponse.getCount());
        System.out.println(searchLogsResponse.isAnalysis());
    }
}
```
