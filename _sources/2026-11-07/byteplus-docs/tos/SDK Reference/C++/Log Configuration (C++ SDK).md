---
title: "Log Configuration (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/log-configuration-c-sdk"
---

The logging feature of the C++ SDK can collect logs of various operations performed on TOS and store these logs locally as files.

<span id=".5pel5b-X5omT5Y2w5pe25py6"></span>
## **Log Output Timing**

For each API call, the SDK will print logs at the following locations:


* Before initiating the request, print the original signature values for this API call at the DEBUG level, including CanonicalRequest and StringToSign.

* At the DEBUG level, logs are printed detailing the HTTP connection information and the duration of each stage for the current API call, including Method, Host, Request URI, DNS resolution time, TCP connection time, TLS handshake time, data transmission time, and total HTTP request duration.

* After a request is made, the execution details are logged at the INFO level. If the request fails, failure information is recorded; upon completion of the request, the HTTP status code, RequestID, and total interface invocation time are logged.


<span id=".5byA5ZCv5pel5b-X5pa55byP"></span>
## Method for Enabling Logging

The following code demonstrates how to enable the logging functionality in the C++ SDK.

```cpp
#include "TosClientV2.h"
#include "../src/utils/LogUtils.h"
using namespace VolcengineTos;

int main(void){
    
    std::string logFilePath = "Your Log File Path";
    
    LogUtils::SetLogger(logFilePath, "tos-cpp-sdk", LogLevel::LogDebug);
    
    

    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    
    InitializeClient();
   
    TosClientV2 client(region, accessKey, secretKey);
   
    LogUtils::SetLoggerLevel(LogLevel::LogOff);
 
    CloseClient();
    return 0;
}
```


Additionally, the following statements must be added to the CMakelist file.

```cpp

target_include_directories(${PROJECT_NAME} PRIVATE ${CMAKE_SOURCE_DIR}/sdk/src/external)
```


<span id=".5pel5b-X5YaF5a6556S65L6L"></span>
## Sample Log Content

```cpp
[2022-12-07 22:59:31.811] [tos-cpp-sdk] [debug] canonicalRequest: PUT
/

date:20221207T145931Z
host:sdktest-bucket-1670425171810.tos-cn-chongqing-sdv.volces.com
x-tos-acl:private
x-tos-date:20221207T145931Z
x-tos-storage-class:STANDARD

date;host;x-tos-acl;x-tos-date;x-tos-storage-class
e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
[2022-12-07 22:59:31.812] [tos-cpp-sdk] [debug] string to sign: TOS4-HMAC-SHA256
20221207T145931Z
20221207/cn-chongqing-sdv/tos/request
d67b2d6fc6aa98c269bf4ecaa963605fda4bc3286f550764b79dd61b32c9da74
[2022-12-07 22:59:31.998] [tos-cpp-sdk] [debug] Method:PUT, Host:sdktest-bucket-1670425171810.tos-cn-chongqing-sdv.volces.com, request uri:/, DNS resolution time:59 ms, TCP establish connection time:100 ms, TLS handshake time:0 ms, start transfer time:100 ms, Data sending time:85 ms, Total HTTP request time:185 ms
[2022-12-07 22:59:31.998] [tos-cpp-sdk] [info] Response StatusCode:200, RequestId:703f4890aa5428476390aa54-ac101de5-1p2vtU-CB-ccs-front-mtaz-c, Cost:186.078084 ms
```
