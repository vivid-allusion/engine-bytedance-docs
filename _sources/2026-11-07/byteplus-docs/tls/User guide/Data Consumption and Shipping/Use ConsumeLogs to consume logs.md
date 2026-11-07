---
title: "Use ConsumeLogs to consume logs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/use_consumelogs_to_consume_logs"
---

Torch Log Service (TLS) offers the ConsumeLogs API to consume log data collected to the server in real time. This topic describes how to use a TLS SDK to call the ConsumeLogs API to read and write full log data in order.

<span id="背景信息"></span>
## Background

TLS offers a log data transfer feature similar to Kafka. By using the ConsumeLogs API and a multi\-language SDK of TLS, you can use an application developed in Go or other languages as a consumer to consume TLS data in real time. For more information on the server\-side API for consuming logs, refer to [ConsumeLogs](https://docs.byteplus.com/docs/tls/api-consumelogs). For more information on the multi\-language SDK offered by TLS, refer to [SDK Overview](https://docs.byteplus.com/docs/tls/sdk_overview).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">TLS offers the consumer group feature through the SDK, so you can use consumer groups to consume log data. When you use consumer groups to consume data, TLS automatically allocates shards to balance the consumption capability and progress of each consumer group. For more information，please refer to <a href="https://docs.byteplus.com/docs/tls/using_consumer_groups_to_consume_logs">Use consumer groups to consume logs</a>.</div>


<span id="示例代码"></span>
## Sample code

The following sample code creates a `ConsumeLogs.go` file, calls the `ConsumeLogs` API to read log data, and consumes the log data in real time.

```go
import (
        "fmt"
        "time"
        . "github.com/volcengine/volc-sdk-golang/service/tls"
        "github.com/volcengine/volc-sdk-golang/service/tls/pb"
)
func consumeLogs(topicID string, shardID int) {
        client := NewClient(os.Getenv("LOG_TEST_ENDPOINT"), os.Getenv("LOG_TEST_ACCESS_KEY_ID"),
        //LOG_TEST_SECURITY_TOKEN is a temporary security token obtained through the security token service (STS) of Identity and Access Management (IAM). If you use the temporary token, pass in the temporary AccessKey ID and AccessKey secret. If you do not use the temporary token, pass an empty value for LOG_TEST_SECURITY_TOKEN.
                os.Getenv("LOG_TEST_ACCESS_KEY_SECRET"), os.Getenv("LOG_TEST_SECURITY_TOKEN"),
                os.Getenv("LOG_TEST_REGION"))
        // Get the start cursor.
        beginCursorResp, err := client.DescribeCursor(&DescribeCursorRequest{
                TopicID: topicID,
                ShardID: shardID,
                From:    "begin",
        })
        if err != nil {
                panic(err.Error())
        }
        // Get the last cursor.
        endCursorResp, err := client.DescribeCursor(&DescribeCursorRequest{
                TopicID: topicID,
                ShardID: shardID,
                From:    "end",
        })
        if err != nil {
                panic(err.Error())
        }
        // Get the cursor at a point in time.
        timestampCursorResp, err := client.DescribeCursor(&DescribeCursorRequest{
                TopicID: topicID,
                ShardID: shardID,
                From:    "1661418000",
        })
        if err != nil {
                panic(err.Error())
        }
        var logGroupCount = 10
        // Consume 10 groups of logs.
        consumedLogs, err := client.ConsumeLogs(&ConsumeLogsRequest{
                TopicID:       topicID,
                ShardID:       shardID,
                Cursor:        timestampCursorResp.Cursor,
                LogGroupCount: &logGroupCount,
        })
        if err != nil {
                panic(err.Error())
        }
        fmt.Println(consumedLogs)
        // Consume 10 groups of logs and set the compression type to lz4. Currently, LZ4 is supported.
        var compressionType = "lz4"
        consumedLogs, err = client.ConsumeLogs(&ConsumeLogsRequest{
                TopicID:       topicID,
                ShardID:       shardID,
                Cursor:        timestampCursorResp.Cursor,
                LogGroupCount: &logGroupCount,
                Compression:   &compressionType,
        })
        if err != nil {
                panic(err.Error())
        }
        // Specify the start and end of logs to be consumed.
        consumedLogs, err = client.ConsumeLogs(&ConsumeLogsRequest{
                TopicID:       topicID,
                ShardID:       shardID,
                Cursor:        beginCursorResp.Cursor,
                EndCursor:     &endCursorResp.Cursor,
                LogGroupCount: &logGroupCount,
                Compression:   &compressionType,
        })
        if err != nil {
                panic(err.Error())
        }
}
```
