---
title: "Getting started"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/tls_sdk_for_go_getting_started"
---

This topic describes how to use Torch Log Service (TLS) SDK for Go to quickly collect logs, including creating projects, creating topics, writing logs, and querying logs.

<span id="前提条件"></span>
## Before you begin


* Install TLS SDK for Go. For more information, refer to [Install TLS SDK for Go](https://docs.byteplus.com/docs/tls/install_tls_for_go).

* Run the following command to install the proto dependency:

   ```Shell
   go get -u github.com/gogo/protobuf/proto
   ```
   

* Add environment variables such as `VOLCENGINE_ACCESS_KEY_ID`. For information on how to configure environment variables, refer to [Configure identity authentication](https://docs.byteplus.com/docs/tls/configuring_identity_authentication).


<span id="a2d9001e"></span>
## Initializing the client

Initialize the client instance before you can send requests to TLS. When you initialize the client, we recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard\-coded AccessKey information leads to data security risks.

Initialization code:

```go
client := NewClient(os.Getenv("VOLCENGINE_ENDPOINT"), os.Getenv("VOLCENGINE_ACCESS_KEY_ID"),
    os.Getenv("VOLCENGINE_ACCESS_KEY_SECRET"), os.Getenv("VOLCENGINE_TOKEN"), os.Getenv("VOLCENGINE_REGION"))
```


<span id="示例代码"></span>
## Sample code

This section uses the log collection and query processes of TLS as an example to describe how to use TLS SDK for Go to manage basic TLS resources. Create a `TLSQuickStart.go` file, and call API actions to create a project, topic, and index, and write, consume, and query log data.

Sample code:

```go
package tls

import (
    "fmt"
    "os"
    "time"

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
       Region:      os.Getenv("VOLCENGINE_REGION"),
    })
    if err != nil {
       // Handle an error.
       fmt.Println(err.Error())
    }
    projectID := createProjectResp.ProjectID

    // Create a topic.
    // Specify parameters such as ProjectId, TopicName, Ttl, Description, and ShardCount as needed.
    createTopicResp, err := client.CreateTopic(&tls.CreateTopicRequest{
       ProjectID:   projectID,
       TopicName:   "topic-name",
       Ttl:         30,
       Description: "topic-description",
       ShardCount:  2,
    })
    if err != nil {
       // Handle an error.
       fmt.Println(err.Error())
    }
    topicID := createTopicResp.TopicID

    // Create an index.
    // Specify TopicId, and enable full-text indexing or key-value indexing or enable both of them as needed.
    _, err = client.CreateIndex(&tls.CreateIndexRequest{
       TopicID: topicID,
       FullText: &tls.FullTextInfo{
          Delimiter:      ",-;",
          CaseSensitive:  false,
          IncludeChinese: false,
       },
       KeyValue: &[]tls.KeyValueInfo{
          {
             Key: "key",
             Value: tls.Value{
                ValueType:      "text",
                Delimiter:      ", ?",
                CasSensitive:   false,
                IncludeChinese: false,
                SQLFlag:        false,
             },
          },
       },
    })
    if err != nil {
       // Handle an error.
       fmt.Println(err.Error())
    }

    // (Not recommended) This section calls PutLogs to upload logs using a synchronous request.
    // (Recommended) In the actual production environment, use Go Producer to write log data to improve efficiency.
     
    // If you use PutLogs to upload logs, we recommend that you aggregate multiple log entries and call PutLogs once to improve throughput and avoid rate limiting.
    // Specify TopicId, Source, FileName, and Logs as needed. We recommend that you use LZ4.
    _, err = client.PutLogsV2(&tls.PutLogsV2Request{
       TopicID:      topicID,
       CompressType: "lz4",
       Source:       "your-log-source",
       FileName:     "your-log-filename",
       Logs: []tls.Log{
          {
             Contents: []tls.LogContent{
                {
                   Key:   "key1",
                   Value: "value1-1",
                },
                {
                   Key:   "key2",
                   Value: "value2-1",
                },
             },
          },
          {
             Contents: []tls.LogContent{
                {
                   Key:   "key1",
                   Value: "value1-2",
                },
                {
                   Key:   "key2",
                   Value: "value2-2",
                },
             },
          },
       },
    })
    if err != nil {
       // Handle an error.
       fmt.Println(err.Error())
    }
    time.Sleep(30 * time.Second)

    // Query and analyze log data.
    // Specify parameters such as TopicId, Query, StartTime, EndTime, and Limit as needed.
    resp, err := client.SearchLogsV2(&tls.SearchLogsRequest{
       TopicID:   topicID,
       Query:     "*",
       StartTime: 1346457600000,
       EndTime:   1630454400000,
       Limit:     20,
    })
    if err != nil {
       // Handle an error.
       fmt.Println(err.Error())
    }

    // Print some basic information in the return value of the SearchLogs API action.
    // Handle other information in the return value as needed.
    fmt.Println(resp.Status)
    fmt.Println(resp.HitCount)
    fmt.Println(resp.Count)
    fmt.Println(resp.Analysis)
}
```
