---
title: "Use TLS SDK for Go to create basic resources"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/use_tls_for_go_to_create_basic_resources"
---

In Torch Log Service (TLS), basic resources include projects and topics. This topic offers sample code that demonstrates how to use an SDK to create projects, topics, and indexes.

<span id="0a03ef83"></span>
## Before you begin


* Install TLS SDK for Go. For more information, refer to [Install TLS SDK for Go](https://docs.byteplus.com/docs/tls/install_tls_for_go).

* Run the following command to install the proto dependency:

   ```Shell
   go get -u github.com/gogo/protobuf/proto
   ```
   

* Add environment variables such as `VOLCENGINE_ACCESS_KEY_ID`. For information on how to configure environment variables, refer to [Configure identity authentication](https://docs.byteplus.com/docs/tls/configuring_identity_authentication).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">We recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard\-coded AccessKey information leads to data security risks.   </div>
   

<span id="1c816eeb"></span>
## Creat basic resources

<span id="5fded6cf"></span>
### Scenario description

This topic offers sample code that demonstrates how to use the SDK to create a project, topic, and index in a specific Region. The Region of the project is your\-service\-region. The Region is consistent with that you specified when initializing the client. When you create a topic, we recommend that you enable automatic sharding to prevent data read and write speeds from being affected by the limited number of shards in case of a traffic surge. In the following example, both full\-text indexes and key\-value indexes are enabled. You can configure indexes based on log fields and query and analysis requirements. For information on how to configure indexes, refer to [Configure indexes](https://docs.byteplus.com/docs/tls/getting_started_configure_indexes).

<span id="4d97c4b6"></span>
### Sample code

The following sample code demonstrates how to create a project, topic, and index.

```Go
package tls

import (
    "fmt"
    "github.com/volcengine/volc-sdk-golang/service/tls"
)

func main() {
    // When you initialize the client, we recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard-coded AccessKey information leads to data security risks. 
    // If you use Security Token Service (STS), use a temporary AccessKey ID and AccessKey secret, and set VOLCENGINE_TOKEN. If you do not use STS, leave VOLCENGINE_TOKEN empty.
    client := tls.NewClient(os.Getenv("VOLCENGINE_ENDPOINT"), os.Getenv("VOLCENGINE_ACCESS_KEY_ID"), 
        os.Getenv("VOLCENGINE_ACCESS_KEY_SECRET"), os.Getenv("VOLCENGINE_TOKEN"), os.Getenv("VOLCENGINE_REGION"))

    // Create a project.
    // Specify ProjectName and the optional Description as needed. Specify the same Region as that when you initialize the client.
    createProjectResp, err := client.CreateProject(&tls.CreateProjectRequest{
       ProjectName: "project-name",
       Description: "project-description",
       Region:      "your-service-region",
    })
    if err != nil {
       // Handle an error.
       fmt.Println(err.Error())
    }
    projectID := createProjectResp.ProjectID

    // Create a topic.
    // Specify parameters such as ProjectId, TopicName, Ttl, Description, ShardCount, AutoSplit, MaxSplitShard, and EnableTracking as needed.
    maxSplitShard := int32(10)
    enableTracking := true
    createTopicResp, err := client.CreateTopic(&tls.CreateTopicRequest{
       ProjectID:      projectID,
       TopicName:      "topic-name",
       Ttl:            30,
       Description:    "topic-description",
       ShardCount:     2,
       AutoSplit:      true,
       MaxSplitShard:  &maxSplitShard,
       EnableTracking: &enableTracking,
    })
    if err != nil {
       // Handle an error.
       fmt.Println(err.Error())
    }
    topicID := createTopicResp.TopicID

    // Create an index.
    // Specify TopicId, and enable full-text indexes or key-value indexes or enable both of them as needed.
    _, err = client.CreateIndex(&tls.CreateIndexRequest{
       TopicID: topicID,
       FullText: &tls.FullTextInfo{
          Delimiter:      ",-;",
          CaseSensitive:  false,
          IncludeChinese: false,
       },
       KeyValue: &[]tls.KeyValueInfo{
          {
             Key: "key1",
             Value: tls.Value{
                ValueType:      "text",
                Delimiter:      ", ?",
                CasSensitive:   false,
                IncludeChinese: false,
                SQLFlag:        false,
             },
          },
          {
             Key: "key2",
             Value: tls.Value{
                ValueType:      "long",
                Delimiter:      "",
                CasSensitive:   false,
                IncludeChinese: false,
                SQLFlag:        true,
             },
          },
       },
    })
    if err != nil {
       // Handle an error.
       fmt.Println(err.Error())
    }
}
```


<span id="dfd4713a"></span>
## Related documents


* After you use the SDK to send an API request, the server returns a response. If the response contains a non\-200 status code, the API call fails. To view the error code and error message, refer to API reference.

* The following table describes the API actions involved in the preceding sample code. To view the details of each API action, refer to API reference.

   
   |API |Description |
   |---|---|
   |[CreateProject](https://docs.byteplus.com/en/docs/tls/api-createproject) |Create a project. |
   |[CreateTopic](https://docs.byteplus.com/en/docs/tls/api-createtopic) |Create a topic. |
   |[CreateIndex](https://docs.byteplus.com/en/docs/tls/api-createindex) |Create indexes. |
   

* To get the complete sample code of managing basic TLS resources, refer to [TLS Go SDK Demo on GitHub](https://github.com/volcengine/volc-sdk-golang/blob/main/example/tls/demo_project.go).
