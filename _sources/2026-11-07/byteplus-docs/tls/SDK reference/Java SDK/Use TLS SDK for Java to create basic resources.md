---
title: "Use TLS SDK for Java to create basic resources"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/tls_sdk_for_java_to_create_basic_resources"
---

In Torch Log Service (TLS), basic resources include projects and topics. This topic offers sample code that demonstrates how to use an SDK to create projects, topics, and indexes.

<span id="bc193ab9"></span>
## Before you begin


* Install TLS SDK for Java. For more information, refer to [Install TLS SDK for Java](https://docs.byteplus.com/docs/tls/install_tls_sdk_for_java).

* Add environment variables such as `VOLCENGINE_ACCESS_KEY_ID`. For information on how to configure environment variables, refer to [Configure identity authentication](https://docs.byteplus.com/docs/tls/configuring_identity_authentication).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">We recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard\-coded AccessKey information leads to data security risks.   </div>
   

<span id="a5315eaa"></span>
## Creating basic resources

<span id="1b0f5656"></span>
### Scenario description

This topic offers sample code that demonstrates how to use the SDK to create a project, topic, and index in a specific Region. The Region where the project is located must be consistent with that you specified when initializing the client. When you create a topic, we recommend that you enable automatic sharding to prevent data read and write speeds from being affected by the limited number of shards in case of a traffic surge. In the following example, both full\-text indexing and key\-value indexing are enabled. You can configure indexes based on log fields and query and analysis requirements. For information on how to configure indexes, refer to [Configure indexes](https://docs.byteplus.com/docs/tls/getting_started_configure_indexes).

<span id="d32ccc20"></span>
### Sample code

The following sample code demonstrates how to create a project, topic, and index.

```Java
package com.volcengine.example.tls.demo;

import com.volcengine.model.tls.*;
import com.volcengine.model.tls.exception.LogException;
import com.volcengine.model.tls.request.*;
import com.volcengine.model.tls.response.*;
import com.volcengine.service.tls.TLSLogClient;

import java.util.ArrayList;
import java.util.List;


public class Demo {
    public static void main(String[] args) throws LogException {
        // When you initialize the client, we recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard-coded AccessKey information leads to data security risks. 
        // If you use Security Token Service (STS), use a temporary AccessKey ID and AccessKey secret, and set VOLCENGINE_TOKEN. If you do not use STS, leave VOLCENGINE_TOKEN empty.
        ClientConfig clientConfig = new ClientConfig(System.getenv("VOLCENGINE_ENDPOINT"), System.getenv("VOLCENGINE_REGION"),
            System.getenv("VOLCENGINE_ACCESS_KEY_ID"), System.getenv("VOLCENGINE_ACCESS_KEY_SECRET"), System.getenv("VOLCENGINE_TOKEN"));
        TLSLogClient client = ClientBuilder.newClient(clientConfig);

        // Create a project.
        // Specify ProjectName and the optional Description as needed. Specify the same Region as that when you initialize the client.        
        CreateProjectRequest createProjectRequest = new CreateProjectRequest("project-name", "region", "description");
        CreateProjectResponse createProjectResponse = client.createProject(createProjectRequest);
        String projectID = createProjectResponse.getProjectId();

        // Create a topic.
        // Specify parameters such as ProjectId, TopicName, Ttl, Description, ShardCount, AutoSplit, MaxSplitShard, and EnableTracking as needed.
        CreateTopicRequest createTopicRequest = new CreateTopicRequest();
        createTopicRequest.setProjectId(projectID);
        createTopicRequest.setTopicName("topic-name");
        createTopicRequest.setTtl(30);
        createTopicRequest.setDescription("description");
        createTopicRequest.setShardCount(2);
        createTopicRequest.setAutoSplit(true);
        createTopicRequest.setMaxSplitShard(10);
        createTopicRequest.setEnableTracking(true);
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
        keyValue.add(new KeyValueInfo("key1", textValueInfo));
        CreateIndexRequest createIndexRequest = new CreateIndexRequest(topicID, fullText, keyValue);
        CreateIndexResponse createIndexResponse = client.createIndex(createIndexRequest);
    }
}
```


<span id="c8b91ade"></span>
## Related documents


* After you use the SDK to send an API request, the server returns a response. If the response contains a non\-200 status code, the API call fails. To view the error code and error message, refer to API reference.

* The following table describes the API actions involved in the preceding sample code. To view the details of each API action, refer to API reference.

   
   |API |Description |
   |---|---|
   |[CreateProject](https://docs.byteplus.com/en/docs/tls/api-createproject) |Create a project. |
   |[CreateTopic](https://docs.byteplus.com/en/docs/tls/api-createtopic) |Create a topic. |
   |[CreateIndex](https://docs.byteplus.com/en/docs/tls/api-createindex) |Create indexes. |
   

* To get the complete sample code of managing basic TLS resources, refer to [TLS Java SDK Demo on GitHub](https://github.com/volcengine/volc-sdk-java/blob/main/example/src/main/java/com/volcengine/example/tls/demo/ProjectDemo.java).
