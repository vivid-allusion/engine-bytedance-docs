---
title: "Getting started"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/tls_sdk_for_nodejs_getting_started"
---

This topic describes how to use Torch Log Service (TLS) SDK for Node.js to quickly collect logs, including creating projects, creating topics, writing logs, and querying logs.

<span id="前提条件"></span>
## Before you begin


* Install TLS SDK for Node.js. For more information, refer to [Install TLS SDK for Node.js](https://docs.byteplus.com/docs/tls/install_tls_sdk_for_nodejs).

* We recommend that you use the latest version of TLS SDK for Node.js. You can view the SDK version in the `@volcengine/openapi` field of the `package.json` file.


<span id="示例代码"></span>
## Sample code

This section uses the log collection and query processes of TLS as an example. Create a `TLSQuickStart.js` file, and call API actions to create a project, topic, and index, and write and query log data.

Sample code:

```JavaScript
const { tlsOpenapi } = require('@volcengine/openapi');
async function main() {
    const tlsOpenapiService = tlsOpenapi.defaultService;
    tlsOpenapiService.setHost('your host');
    tlsOpenapiService.setSecretKey('your secret key');
    tlsOpenapiService.setAccessKeyId('your access key id');
    
    const project = await tlsOpenapiService.CreateProject({
        ProjectName: 'your project name',
        Region: 'project belong to which region',
    });
    
    const topic = await tlsOpenapiService.CreateTopic({
        ProjectId: 'your project id',
        ShardCount: 'your shard count',
        TopicName: 'your topic name',
        Ttl: 'your ttl time',
    });
    
    const index = await tlsOpenapiService.CreateIndex({
        TopicId: 'your topic id',
        FullText: 'your full-text config',
        KeyValue: 'your kv config',
    });
    
    // Use the objToProtoBuffer method to convert structured log data to Protobuf log data.
    const logBuffer = await tlsOpenapi.TlsService.objToProtoBuffer({
        LogGroups: [
            {
                Logs: [
                    {
                        Time: 'log time',
                        Contents: [{ Key: 'content key', Value: 'key value' }]
                    }
                ],
                Source: 'log source',
                LogTags: [{ Key: 'tag key', Value: 'key value' }],
                FileName: 'file name',
                ContextFlow: 'context flow',
            }
        ]
    });
    
    // The PutLogs API action accepts TopicId, CompressType, and LogGroupList as input parameters to upload log data to TLS. Note that LogGroupList specifies logs in Protobuf format.
    const putLogsResult = await tlsOpenapiService.PutLogs({
        TopicId: 'your topic id',
        CompressType: 'log compress type',
        LogGroupList: logBuffer,
    });
    
    const searchLogsResult = await tlsOpenapiService.SearchLogs({
        StartTime: 'log start time',
        EndTime: 'log end time',
        Limit: 'page size',
        Query: 'query phrases',
        TopicId: 'your topic id',
    });

}
```
