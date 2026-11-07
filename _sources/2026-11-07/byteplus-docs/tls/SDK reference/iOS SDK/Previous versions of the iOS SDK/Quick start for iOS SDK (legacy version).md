---
title: "Quick start for iOS SDK (legacy version)"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/tls_sdk_for_ios_getting_started"
---

This article describes how to quickly use the TLS iOS SDK to implement a basic log collection workflow, including creating a project, creating a log topic, writing logs, and more.

## Prerequisites

Before using the TLS iOS SDK, ensure that you have completed the following:

* The TLS iOS SDK has been installed. For detailed steps, see .

* The BytePlus API access key has been created and obtained. The access key AccessKey has full permissions for all APIs. We recommend using an IAM user for API operations and routine O&M. Before using an IAM user, the primary account must grant the IAM user permissions for TLS\-related resources and operations.

* Environment variables such as `VOLCENGINE_ACCESS_KEY_ID` have been added. For instructions on configuring environment variables, refer to [Configure identity authentication information](https://docs.byteplus.com/en/docs/tls/configuring_identity_authentication).

## Create related resources

1. Initialize the Client instance.

   You can refer to the following sample code to import the TLS iOS SDK and create a TLS Client. It is recommended to dynamically obtain BytePlus credentials and other authentication information via environment variables during initialization to avoid data security risks caused by hardcoding the AccessKey.

   ```Objective-C
   #import <Foundation/Foundation.h>
   #import <VeTLSiOSSDK/VeTLSiOSSDK.h>
   
   // Initialize the client. It is recommended to dynamically obtain the BytePlus key and other authentication information through environment variables to avoid the data security risks caused by hardcoding the AccessKey. For detailed instructions, please refer to https://docs.byteplus.com/en/docs/6470/1166455
   int main(int argc, char *argv[]) {
       NSProcessInfo *processInfo = [NSProcessInfo processInfo];
       NSDictionary *environment = [processInfo environment];
       TLSClientConfig *config = [TLSClientConfig alloc]; {
           config.endpoint = [environment objectForKey:@"VOLCENGINE_ENDPOINT"];
           config.region = [environment objectForKey:@"VOLCENGINE_REGION"];
           config.accessKeyId = [environment objectForKey:@"VOLCENGINE_ACCESS_KEY_ID"];
           config.accessKeySecret = [environment objectForKey:@"VOLCENGINE_ACCESS_KEY_SECRET"];
       }
       // Make client
       TLSClient *client = [[TLSClient alloc] initWithConfig:config];
       return 0;
   }
   ```

2. Create a project.

   You can manage projects using the TLS Client, such as creating and deleting projects. For corresponding parameter settings, refer to [CreateProject](https://docs.byteplus.com/docs/tls/api-createproject).

   ```objectivec
   #import <VeTLSiOSSDK/VeTLSiOSSDK.h>
   
   int main(int argc, char *argv[]) {
       ......
       {
           CreateProjectRequest *request = [CreateProjectRequest alloc];
           request.description = @"my project";
           request.region = @"cn-guilin-boe";
           request.projectName = @"ios-sdk-test-project";
           CreateProjectResponse *response = [CreateProjectResponse alloc];
           NSLog(@"CreateProjectResponse: %@", [response toJSONString]);
       }
       ......
   }
   ```

   You will receive a response similar to the following:

   ```objectivec
   CreateProjectResponse: {"StatusCode":200,"ProjectId":"XXXX","RequestId":"XXX"}
   ```

3. Create a log topic.

   You can manage log topics using the TLS Client, such as creating and deleting log topics. For corresponding parameter settings, refer to [CreateTopic](https://docs.byteplus.com/docs/tls/api-createtopic).

   ```objectivec
   #import <VeTLSiOSSDK/VeTLSiOSSDK.h>
   
   int main(int argc, char *argv[]) {
       ......
       {
           CreateTopicRequest *request = [CreateTopicRequest alloc]; {
               request.projectId = @"XXXX";
               request.topicName = @"ios-sdk-test-topic";
               request.ttl = [[NSNumber alloc] initWithInt:1];
               request.shardCount = [[NSNumber alloc] initWithInt:1];
           }
           [client CreateTopic:request];
       }
       ......
   }
   ```

   You will receive a response similar to the following:

   ```objectivec
   CreateTopicResponse: {"RequestId":"XXXX","StatusCode":200,"TopicId":"XXXX"}
   ```

## Upload logs via the TLS Client

You can upload logs to a specified log topic using the TLS Client. The relevant sample code is as follows. For parameter settings for uploading logs, refer to [PutLogs](https://docs.byteplus.com/docs/tls/api-putlogs).

After logs are successfully uploaded, you can later view the real\-time logs collected on the server in the console, or query the uploaded log data via the SearchLogs API.

```objectivec
#import <VeTLSiOSSDK/VeTLSiOSSDK.h>

int main(int argc, char *argv[]) {
    ......
    // PutLogs
    {
        LogContent *logContent = [[LogContent alloc] init]; {
            logContent.key = @"testKey";
            logContent.value = @"testValue";
        }
        Log *log = [[Log alloc] init]; {
            log.time = (int64_t)([[NSDate date] timeIntervalSince1970]);
            [log.contentsArray addObject:logContent];
        }
        LogGroup *logGroup = [[LogGroup alloc] init]; {
            logGroup.source = @"ios-sdk-test";
            logGroup.fileName = @"ios-sdk-test";
            [logGroup.logsArray addObject:log];
        }
        PutLogsRequest *request = [[PutLogsRequest alloc] init]; {
            request.topicId = @"XXX"; // ios-sdk-test-topic
            request.logGroupList = [[LogGroupList alloc] init];
            [request.logGroupList.logGroupsArray addObject:logGroup];
        }
        PutLogsResponse *response = [client PutLogs:request];
        NSLog(@"PutLogsResponse: %@", [response toJSONString]);
    }
    ......
}
```

## Upload logs using the PutLogs V2 API

The process of defining log uploads using Protobuf is rather complicated. In scenarios where performance requirements for the log upload service are not high, you can use the PutLogs V2 interface provided by the TLS iOS SDK. This allows you to upload logs without assembling complex log structures, using only the language's native built\-in data structures. Code example:

```objectivec
#import <VeTLSiOSSDK/VeTLSiOSSDK.h>

int main(int argc, char *argv[]) {
    ......
    PutLogsV2Request *request = [[PutLogsV2Request alloc] init]; {
        request.source = @"Your log source";
        request.fileName = @"Your filename";
        request.topicId = @"Your topicId";
        request.logs = @[
            [[PutLogsV2LogItem alloc] initWithKeyValueAndTime:@{@"TestKey": @"TestValue"} timeStamp:0]
        ];
    }
    NSLog(@"Response: %@", [[client PutLogsV2:request] toJSONString]);
    ......
}
```

## Upload logs using asynchronous interfaces

To ensure that PutLogs does not block the current thread, you can use the PutLogsAsync and PutLogsV2Async interfaces provided in the TLS iOS SDK.

> **Tip**

> The asynchronous interface does not return a Response object, but instead returns an asynchronous task object. You can obtain the response by setting a callback function to parse the task object.

### PutLogsAsync sample code

```objectivec
#import <VeTLSiOSSDK/VeTLSiOSSDK.h>

int main(int argc, char *argv[]) {
    ......
    LogContent *logContent = [[LogContent alloc] init]; {
        logContent.key = @"testKey";
        logContent.value = @"testValue";
    }
    Log *log = [[Log alloc] init]; {
        log.time = (int64_t)([[NSDate date] timeIntervalSince1970] * 1000);
        [log.contentsArray addObject:logContent];
    }
    LogGroup * logGroup = [[LogGroup alloc] init]; {
        logGroup.source = @"ios-sdk-test";
        logGroup.fileName = @"ios-sdk-test";
        [logGroup.logsArray addObject:log];
    }
    PutLogsRequest *request = [[PutLogsRequest alloc] init]; {
        request.topicId = @"XXX"; // ios-sdk-test-topic
        request.logGroupList = [[LogGroupList alloc] init];
        [request.logGroupList.logGroupsArray addObject:logGroup];
    }
    VeTask* task = [client PutLogsAsync:request];
    // If you do not care about the result of the call, you can ignore the callback below.
    [task continueWithBlock:^id _Nullable(VeTask * _Nonnull t) {
        if (t.error == nil) {
            if (t.result != nil) {
                GeneralHttpResponse* response = t.result;
                NSLog(@"RequestId: %@, HttpStatus: %@, ResponseBody: %@", response.requestId, response.httpStatusCode, [[NSString alloc] initWithData:response.responseBody encoding:NSUTF8StringEncoding]);
            }
        } else NSLog(@"Encountered error: %@", t.error);
        return nil;
    }];
    ......
}
```

### PutLogsV2Async sample code

```objectivec
#import <VeTLSiOSSDK/VeTLSiOSSDK.h>

int main(int argc, char *argv[]) {
    ......
    PutLogsV2Request *request = [[PutLogsV2Request alloc] init]; {
        request.source = @"My source";
        request.fileName = @"My filename";
        request.topicId = @"XXX";
        request.logs = @[
            [[PutLogsV2LogItem alloc] initWithKeyValueAndTime:@{@"TestKey": @"TestValue"} timeStamp:0]
        ];
    }
    VeTask* task = [client PutLogsV2Async:request];
    // If you do not care about the result of the call, you can ignore the callback below.
    [task continueWithBlock:^id _Nullable(VeTask * _Nonnull t) {
        if (t.error == nil) {
            if (t.result != nil) {
                GeneralHttpResponse* response = t.result;
                NSLog(@"RequestId: %@, HttpStatus: %@, ResponseBody: %@", response.requestId, response.httpStatusCode, [[NSString alloc] initWithData:response.responseBody encoding:NSUTF8StringEncoding]);
            }
        } else NSLog(@"Encountered error: %@", t.error);
        return nil;
    }];
    ......
}
```
