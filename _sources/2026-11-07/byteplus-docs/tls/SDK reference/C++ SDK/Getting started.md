---
title: "Getting started"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/tls_sdk_for_c_getting_started"
---

This topic describes how to use Torch Log Service (TLS) SDK for C++ to quickly collect logs, including creating projects, creating topics, and writing logs.

<span id="前提条件"></span>
## Before you begin

Before you use TLS SDK for C++:


* Install TLS SDK for C++. For more information, refer to [Install TLS SDK for C++](https://docs.byteplus.com/docs/tls/install_tls_sdk_for_c)

* Create and get a BytePlus AccessKey pair. The AccessKey pair has the permissions to access all API actions. We recommend that you use an IAM user to call API actions or perform routine O&M. Before you use an IAM user, use a BytePlus account to grant the IAM user the permissions to operate TLS resources.

* Add environment variables such as `VOLCENGINE_ACCESS_KEY_ID`. For information on how to configure environment variables, refer to [Configure identity authentication](https://docs.byteplus.com/docs/tls/configuring_identity_authentication).


<span id="创建相关资源"></span>
## Creating related resources


1. Initialize a client instance.

   Refer to the following sample code to load TLS SDK for C++ and create a TLS client. When you initialize the client, we recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard\-coded AccessKey information leads to data security risks.

   ```C++
   include <cstdlib>
   #include <ve-tls-cpp-sdk/TlsClient.h>
   #include <ve-tls-cpp-sdk/TlsClientConfig.h>
   #include <ve-tls-cpp-sdk/TlsRequest.h>
   #include <ve-tls-cpp-sdk/TlsJsonConversion.h>
   #include <ve-tls-cpp-sdk/TlsResponse.h>
   
   int main(int argc, char **argv) {
       // Create a client.
       TlsClientConfig cfg; {
           // Set the protocol type to https://.
           cfg.scheme = "https://";
           // When you initialize the client, we recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard-coded AccessKey information leads to data security risks. 
           if (std::getenv("VOLCENGINE_ENDPOINT") != nullptr) {
               cfg.endpoint = std::getenv("VOLCENGINE_ENDPOINT");
           }
           if (std::getenv("VOLCENGINE_ACCESS_KEY_ID") != nullptr) {
               cfg.access_key_id = std::getenv("VOLCENGINE_ACCESS_KEY_ID");
           }
           if (std::getenv("VOLCENGINE_ACCESS_KEY_SECRET") != nullptr) {
               cfg.access_key_secret = std::getenv("VOLCENGINE_ACCESS_KEY_SECRET");
           }
           if (std::getenv("VOLCENGINE_REGION") != nullptr) {
               cfg.region = std::getenv("VOLCENGINE_REGION");
           }
       }
       TlsClient cli = TlsClient(cfg);
   }
   ```
   

2. Create a project.

   Use the TLS client to manage projects, such as creating and deleting projects. For information on how to set the parameters, refer to [API overview](https://docs.byteplus.com/docs/tls/API-overview).

   ```C++
   #include <ve-tls-cpp-sdk/TlsClient.h>
   #include <ve-tls-cpp-sdk/TlsClientConfig.h>
   #include <ve-tls-cpp-sdk/TlsRequest.h>
   #include <ve-tls-cpp-sdk/TlsJsonConversion.h>
   #include <ve-tls-cpp-sdk/TlsResponse.h>
   
   int main(int argc, char **argv) {
       ......
       {
           CreateProjectRequest request; {
               request.region = std::make_shared<std::string>("cn-guilin-boe");
               request.description = std::make_shared<std::string>("eren test cpp sdk");
               request.project_name = std::make_shared<std::string>("cppsdkunittest");
           }
           auto resp = client.CreateProject(request);
       }
       ......
   }
   ```
   

   The following response is returned:

   ```C++
   CreateProjectResponse: {"StatusCode":200,"ProjectId":"XXXX","RequestId":"XXX"}
   ```
   

3. Create a topic.

   Use the TLS client to manage topics, such as creating and deleting topics. For information on how to set the parameters, refer to [API overview](https://docs.byteplus.com/docs/tls/API-overview).

   ```C++
   #include <ve-tls-cpp-sdk/TlsClient.h>
   #include <ve-tls-cpp-sdk/TlsClientConfig.h>
   #include <ve-tls-cpp-sdk/TlsRequest.h>
   #include <ve-tls-cpp-sdk/TlsJsonConversion.h>
   #include <ve-tls-cpp-sdk/TlsResponse.h>
   
   int main(int argc, char **argv) {
       ......
       {
           CreateTopicRequest request; {
               request.topic_name = std::make_shared<std::string>("cpptesttopic");
               request.project_id = std::make_shared<std::string>("XXX");
               request.ttl = std::make_shared<int>(7);
               request.shard_count = std::make_shared<int>(2);
               request.auto_split = std::make_shared<bool>(true);
               request.max_split_shard = std::make_shared<int>(10);
           }
           auto resp = client.CreateTopic(request);
       }
       ......
   }
   ```
   

   The following response is returned:

   ```C++
   CreateTopicResponse: {"RequestId":"XXXX","StatusCode":200,"TopicId":"XXXX"}
   ```
   


<span id="通过-tls-client-上传日志"></span>
## Using the TLS client to upload logs

Use the TLS client to upload logs to a specific topic. The sample code is as follows. For information on how to set the parameters, refer to [API overview](https://docs.byteplus.com/docs/tls/API-overview).

After you upload logs, view the log data collected to the server in the console. Alternatively, call [SearchLogs](https://docs.byteplus.com/en/docs/tls/api-searchlogs) to query the log data you uploaded.

```C++
#include <ve-tls-cpp-sdk/TlsClient.h>
#include <ve-tls-cpp-sdk/TlsClientConfig.h>
#include <ve-tls-cpp-sdk/TlsRequest.h>
#include <ve-tls-cpp-sdk/TlsJsonConversion.h>
#include <ve-tls-cpp-sdk/TlsResponse.h>

int main(int argc, char **argv) {
    ......
    // PutLogs
    {
        auto pb = std::make_shared<pb::LogGroupList>();
        auto log_group = pb->add_loggroups();
        auto log = log_group->add_logs();
        log->set_time(time(nullptr));
        auto log_content = log->add_contents();
        log_content->set_key("cpptestkey");
        log_content->set_value("cpptestvalue");
        PutLogsRequest request; {
            request.topic_id = std::make_shared<std::string>("XXX");
            request.log_group_list = pb;
        }
        auto resp = client.PutLogs(request);
    }
    ......
}
```


<span id="使用-putlogs-v2接口上传日志"></span>
## Using PutLogs V2 to upload logs

Defining Protobuf to upload logs is troublesome. If high performance is not required for uploading logs, consider using PutLogs V2 in TLS SDK for C++. It allows you to use the built\-in data structure of the language to upload logs without building a complex log structure. Sample code:

```C++
#include <ve-tls-cpp-sdk/TlsClient.h>
#include <ve-tls-cpp-sdk/TlsClientConfig.h>
#include <ve-tls-cpp-sdk/TlsRequest.h>
#include <ve-tls-cpp-sdk/TlsJsonConversion.h>
#include <ve-tls-cpp-sdk/TlsResponse.h>

int main(int argc, char **argv) {
    ......
    PutLogsV2Request request; {
        request.topic_id = std::make_shared<std::string>("XXX");
        request.source = std::make_shared<std::string>("sdkut");
        request.filename = std::make_shared<std::string>("utstdout");
        request.logs = std::make_shared<std::vector<LogItem>>();
        request.logs->push_back(LogItem());
        (*request.logs)[0].log_content["cpptestkey"] = "cpptestvalue";
    }
    client.PutLogsV2(request);
    ......
}
```
