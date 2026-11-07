---
title: "Quick start .NET SDK"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Quick_start_NET_SDK"
---

This article describes how to quickly use the TLS .NET SDK to implement a basic log collection workflow, including creating a project, creating a log topic, writing logs, querying logs, and more. 

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* TLS .NET SDK has been installed. For detailed steps, please refer to [Install .NET SDK](https://docs.byteplus.com/docs/tls/Install_NET_SDK).

* Windows only; requires .NET Framework 4.6.2 or later.

* The `VOLCENGINE_ACCESS_KEY_ID` and other environment variables have been added. For information on configuring environment variables, please refer to [Configure authentication information](https://docs.byteplus.com/docs/tls/configuring_identity_authentication).


<span id="4de651bb"></span>
## Initialize the client

You can send requests to the TLS service only after initializing the Client instance. It is recommended to dynamically obtain authentication information such as the BytePlus key through environment variables during initialization, in order to avoid hardcoding the AccessKey and thereby prevent data security risks.

Initialization code is as follows:

```SQL
VOLCENGINE_ACCESS_KEY_ID="your accessKeyId" VOLCENGINE_ACCESS_KEY_SECRET="your secretKey" VOLCENGINE_ENDPOINT="your host" VOLCENGINE_REGION="your region"
```


<span id="22468c26"></span>
## Example code

The following sample code demonstrates how to configure Volcengine Cloud permissions, start consumers, send single or multiple messages, simulate task processing, and other information.

Detailed example code is as follows:

```JavaScript
using System; 
using System.Threading; 
using VolcengineTls.Producer; 

namespace VolcengineTls.Examples 
{ 
    public class DefaultCallBackImp : ICallBack 
    { 
        public void Fail(ProducerResult result) 
        { 
            Console.WriteLine("put log to tls failed"); 
        } 

        public void Success(ProducerResult result) 
        { 
            Console.WriteLine("put log to tls success"); 
        } 
    } 

    public class ProducerExample 
    { 
        public void Run() 
        { 
// Set Volcengine permission configuration 
            var vc = new VolcengineConfig( 
                region: Environment.GetEnvironmentVariable("VOLCENGINE_REGION"), 
                endpoint: Environment.GetEnvironmentVariable("VOLCENGINE_ENDPOINT"), 
                accessKeyId: Environment.GetEnvironmentVariable("VOLCENGINE_ACCESS_KEY_ID"), 
                accessKeySecret: Environment.GetEnvironmentVariable("VOLCENGINE_ACCESS_KEY_SECRET"), 
                securityToken: Environment.GetEnvironmentVariable("VOLCENGINE_SECURITY_TOKEN") 
            ); 

            // Set Volcano Cloud configuration; currently retrieving the default configuration 
            var config = new ProducerConfig(vc); 
// Instantiate 
            var producer = new ProducerImp(config); 
// Start the consumer 
            producer.Start(); 

/// Send a single item 
            // Construct log 
            var keyNum = 2; 
            var log = new Pb.Log 
            { 
                Time = DateTimeOffset.UtcNow.ToUnixTimeMilliseconds(), 
            }; 

            for (var i = 0; i < keyNum; i++) 
            { 
                var logContent = new Pb.LogContent 
                { 
                    Key = $"key{i}", 
                    Value = $"c#-value-test-{i}", 
                }; 

                log.Contents.Add(logContent); 
            } 

            // Send a single entry or use SendLogV2 
            producer.SendLog( 
                topicId: Environment.GetEnvironmentVariable("TOPIC_ID"), 
                log: log, 
                source: "your log source", 
                filename: "your log filename", 
                shardHash: null, 
                callback: new DefaultCallBackImp() // If not needed, you can pass null 
            ); 

Send multiple messages 
            var logNum = 1000; 
            var logGroup = new Pb.LogGroup(); 

            for (var j = 0; j < logNum; j++) 
            { 
                log = new Pb.Log 
                { 
                    Time = DateTimeOffset.Now.ToUnixTimeSeconds(), 
                }; 

                for (var i = 0; i < keyNum; i++) 
                { 
                    var logContent = new Pb.LogContent 
                    { 
                        Key = $"no-{j}-key{i}", 
                        Value = $"no-{j}-c#-value-test-{i}", 
                    }; 

                    log.Contents.Add(logContent); 
                } 

                logGroup.Logs.Add(log); 
            } 

            producer.SendLogs( 
                topicId: Environment.GetEnvironmentVariable("TOPIC_ID"), 
                logs: logGroup, 
                source: "your log source", 
                filename: "your log filename", 
                shardHash: null, 
                callback: new DefaultCallBackImp() // If not needed, you can pass null 
            ); 

// Simulate other task processing 
            Thread.Sleep(TimeSpan.FromSeconds(20)); 

            // Producer shutdown 
            producer.Close(); 
        } 
    } 
}
```
