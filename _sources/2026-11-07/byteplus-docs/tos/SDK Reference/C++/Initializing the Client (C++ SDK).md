---
title: "Initializing the Client (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Initialize-client-side-c-sdk"
---

TOSClient provides a set of interfaces for interacting with the TOS service, enabling the management of resources such as buckets and objects. You can initialize TOSClient using methods such as AccessKey/SecretKey, STS (Security Token Service), and other similar approaches. When initializing TOSClient, TOS also supports configuring optional parameters such as connection establishment timeout. You may refer to this document to configure these parameters according to your business requirements.

When initializing TosClient, you must provide the AccessKey, SecretKey, and Region.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* [Installing the SDK](https://docs.byteplus.com/docs/tos/Install-c-sdk)

* [Obtaining AKSK Information](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey)


<span id=".6YWN572u6ZW_5pyf6K6_6Zeu5Yet6K-B"></span>
## Configuring Long\-Term Access Credentials

Before initializing the SDK, you must first configure long\-term access credentials. This chapter outlines the procedures for configuring long\-term access credentials across different operating systems.


<Tabs>
<Tab zoneid="Fy80xopKJU" title="macOS">
<TabTitle>macOS</TabTitle>

1. Open the terminal and execute the following command to open the file.


```Shell
nano ~/.bash_profile
```



2. Add AKSK information at the end of the document.


```Shell
export TOS_ACCESS_KEY=AKTPYmI1Z****
export TOS_SECRET_KEY=T1dJM01UU****
```



3. Save the file and exit.

4. Execute the following commands to make the configuration information take effect.


```Shell
source ~/.bash_profile
```



5. Execute the following command to verify the configuration information.


```Shell
echo $TOS_ACCESS_KEY
echo $TOS_SECRET_KEY
```


If the configuration is successful, the following example will be returned:

```Shell
AKTPYmI1Z****
T1dJM01UU****
```



</Tab>
<Tab zoneid="J1hsSAXdtd" title="Linux">
<TabTitle>Linux</TabTitle>

1. Open the terminal and execute the following command to open the file.


```Shell
sudo vim /etc/profile
```



2. Add AKSK information at the end of the document.


```Shell
export TOS_ACCESS_KEY=AKTPYmI1Z****
export TOS_SECRET_KEY=T1dJM01UU****
```



3. Save the file and exit.

4. Execute the following command to make the configuration information take effect.


```Shell
source /etc/profile
```



5. Execute the following command to verify the configuration information.


```Shell
echo $TOS_ACCESS_KEY
echo $TOS_SECRET_KEY
```


If the configuration is successful, the following example will be returned:

```Shell
AKTPYmI1Z****
T1dJM01UU****
```



</Tab>
<Tab zoneid="jeuxJTtG5t" title="Windows">
<TabTitle>Windows</TabTitle>

1. Open the command\-line tool and execute the following command to add AKSK information.


```Shell
set TOS_ACCESS_KEY=AKTPYmI1Z****
set TOS_SECRET_KEY=T1dJM01UU****
```



2. Execute the following command for the configuration settings to take effect.


```Shell
setx TOS_ACCESS_KEY "%TOS_ACCESS_KEY%"
setx TOS_SECRET_KEY "%TOS_SECRET_KEY%"
```



3. Restart the command\-line tool, then execute the following command to verify the configuration information.


```Shell
echo %TOS_ACCESS_KEY%
echo %TOS_SECRET_KEY%
```


If the configuration is successful, the following example will be returned:

```Shell
AKTPYmI1Z****
T1dJM01UU****
```



</Tab>
</Tabs>


<span id=".5Yib5bu6LXRvc2NsaWVudA=="></span>
## Creating TosClient

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The TosClient instance is thread\-safe and supports concurrent access by multiple threads. You may create a single TosClient instance for multi\-threaded invocation, or create multiple TosClient instances for separate use.</div>


* <div data-tips="true" data-tips-type="warning">InitializeClient() and CloseClient() are global interfaces that should be invoked only once during the program's lifecycle.</div>



<span id=".6K6-572u5b-F6YCJ5Y-C5pWw"></span>
### **Configure mandatory parameters**

TosClient is used to manage TOS resources such as storage buckets (Bucket) and files (Object). The following sample code demonstrates how to initialize TosClient using only the required parameters: AccessKey, SecretKey, and Region.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Endpoint is the access domain name for TOS external services. For information on the endpoints supported by TOS, please refer to <a href="https://docs.byteplus.com/docs/tos/docs-region-and-endpoint">Access Domain Name Endpoint</a>.</div>


* <div data-tips="true" data-tips-type="tip">AKSK information can be obtained from environment variables. For configuration instructions, please refer to <a href="https://docs.byteplus.com/docs/tos/Initialize-client-side-c-sdk">Configuring Access Credentials</a>.</div>



```C++
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
   
    std::string region = "Your Region";
    
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    
    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey);
    
    CloseClient();
    return 0;
}
```


<span id=".5bi46KeB6YWN572u5Zy65pmv"></span>
## Common Configuration Scenarios

ClientConfig is the configuration class for TOSClient, allowing the specification of parameters such as endpoint, timeout duration, and whether to perform CRC data validation. When initiating a request using the C++ SDK, you need to initialize a TosClient instance and modify the default configuration options in ClientConfig as needed.

<span id=".6YWN572uLXN0cw=="></span>
### Configuring STS

If you do not wish to disclose long\-term key information, you can use the STS service to generate temporary access credentials. This allows users to access TOS resources within a specified time frame; once expired, the credentials become invalid, effectively safeguarding your resources.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can obtain temporary access credentials by calling the STS service's <a href="https://docs.byteplus.com/en/docs/6257/86374">AssumeRole</a> API. Temporary access credentials consist of temporary access keys (AccessKeyId and AccessKeySecret) and a security token (SecurityToken). You may subsequently use this information to access the TOS service. For specific steps on setting up the STS service, please refer to <a href="https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service">Using STS Temporary AK/SK+Token to Access BytePlus TOS</a>.</div>


The following code example demonstrates how to configure the initialization of the TOS C++ SDK using an STS Token.

```C++
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
    
    
    std::string region = "Your Region";
    std::string accessKey = "Your Access Key";
    std::string secretKey = "Your Secret Key";
    
    std::string securityToken = "Your Security Token";
    
    
    InitializeClient();
    
    TosClientV2 client(region, accessKey,secretKey, securityToken);
    
    
    // ClientConfig conf;
    // conf.xxx = xxx
    // TosClientV2 client(region, accessKey,secretKey, securityToken, conf);
    
    
    CloseClient();
    return 0;
}
```


<span id=".6YWN572u6LaF5pe25py65Yi2"></span>
### Configure Timeout Mechanism

When initializing TosClient, you can configure the network request timeout by adding optional parameters. The TOS C++ SDK currently supports setting the connection timeout (connectionTimeout) and the read/write request timeout (socketTimeout). The following code example is used to configure a timeout mechanism:

```C++
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
   
    std::string region = "Your Region";
   
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
   
    ClientConfig conf;
    
    conf.connectionTimeout = 10000;
   
    conf.socketTimeout = 30000;
    
   
    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey,conf);
   
    CloseClient();
    return 0;
}
```


<span id=".6YWN572u6YeN6K-V562W55Wl"></span>
### Configuring Retry Strategies

The TOS C++ SDK configures the number of retry attempts after a request failure through the initialization parameter maxRetryCount, helping to address request failures caused by issues such as network jitter and reducing the probability of users encountering intermittent errors. In cases of request timeout, or when the server returns 5xx errors or 429 errors, retries are performed for scenarios with idempotent semantics using an exponential backoff strategy based on the number of retry attempts.

During TOS retries, exponential backoff is applied with a base interval of 100 ms until the maximum retry count is reached. For example, if the maximum retry count is three, the retry intervals are 100 ms, 200 ms, and 400 ms, respectively.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To disable the retry mechanism, set maxRetryCount to a value less than or equal to zero.</div>


The following code example is used to configure a retry strategy.

```C++
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
    
    
    std::string region = "Your Region";
    
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    ClientConfig conf;
    
    conf.maxRetryCount = 3;
   
    InitializeClient();
   
    TosClientV2 client(region, accessKey, secretKey,conf);
  
    CloseClient();
    return 0;
}
```


<span id=".6YWN572u5pWw5o2u5qCh6aqM"></span>
### Configuration Data Validation

During object upload and download, the TOS server returns the object's Crc64 value. The SDK verifies whether the locally computed Crc64 matches the Crc64 returned by TOS, thereby ensuring the integrity of uploaded and downloaded data. To ensure data integrity during upload and download processes, the SDK enables Crc64 data verification by default. You may disable the Crc64 verification feature by specifying an optional parameter when initializing TosClient.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">It is strongly recommended that you do not disable the Crc64 data verification feature. If this feature is disabled, TOS does not guarantee data integrity during upload and download operations.</div>


The following code example demonstrates how to configure CRC verification.

```C++
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
 
   
    std::string region = "Your Region";
   
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
  
    ClientConfig conf;
  
    conf.enableCRC = true;
 
    InitializeClient();

    TosClientV2 client(region, accessKey, secretKey,conf);

    CloseClient();
    return 0;
}
```


<span id=".6YWN572uLWRucy3nvJPlrZg="></span>
### Configure DNS Cache

In public network environments, there may be scenarios where domain name resolution for TOS services is time\-consuming or unavailable for a period of time. To address this, the TOS C++ SDK supports configuring the DNS cache validity period through the initialization parameter dnsCacheTime. The default value is 0, which indicates that the domain name caching feature is disabled. The following code example is used to set up the DNS cache.

```C++
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){

    std::string region = "Your Region";
      
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    
    ClientConfig conf;
    
    conf.dnsCacheTime = 3;
    
   
    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey,conf);
    
    CloseClient();
    return 0;
}
```


<span id=".6YWN572u5Luj55CG5pyN5Yqh5Zmo"></span>
### Configure Proxy Server

The TOS C++ SDK supports accessing TOS services via a proxy server. You can configure the proxy server by adding an optional parameter when initializing TosClient.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, only HTTP protocol proxies are supported.</div>


The following code is used to configure the proxy server.

```C++
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
     
    std::string region = "Your Region";
      
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    
    ClientConfig conf;
    
    conf.proxyHost = http::SchemeHTTP;
    
    conf.proxyPort = 80;
 
    conf.proxyUsername = "Your Proxy UserName";
    
    conf.proxyPassword = "your Proxy Password";
    
    
    InitializeClient();
   
    TosClientV2 client(region, accessKey, secretKey,conf);
    
    CloseClient();
    return 0;
}
```


<span id=".6YWN572u6L-e5o6l5rGg"></span>
### Configure Connection Pool

The TOS C++ SDK supports connection pool configuration. When initializing the TosClient, you can specify optional parameters to configure the connection pool size.

The following code is used to configure the connection pool.

```C++
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
    
    
    std::string region = "Your Region";
      
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    // Clien
    ClientConfig conf;
   
    conf.maxConnections = 64;
    
   
    InitializeClient();
   
    TosClientV2 client(region, accessKey, secretKey,conf);
   
    CloseClient();
    return 0;
}
```


<span id="f0da13ed"></span>
### Configure Custom Domain Name

The TOS C++ SDK supports the configuration of custom domain names. When initializing TosClient, you can specify a custom domain name as the Host. After specifying a custom domain name, it is not necessary to provide the Bucket parameter when using the SDK interface.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before using a custom domain name, you must configure the custom domain name on the server. For detailed instructions, please refer to <a href="https://docs.byteplus.com/docs/tos/Set-up-a-custom-domain-name">Setting Up a Custom Domain Name</a>.</div>


In the SDK, the `isCustomDomain` identifier can be used to indicate that the current domain name is a custom domain.

```C++
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
    
    std::string region = "Your Region";
    
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    
    ClientConfig conf;
    
    conf.endPoint = "your custom endpoint";
    conf.isCustomDomain = true;

    
    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey, conf);
    
    CloseClient();
    return 0;
}
```


<span id=".5Yid5aeL5YyW5Y-C5pWw5YiX6KGo"></span>
## Initialization Parameter List

The following parameters are optional when initializing TOSClient.


|**Parameters** |**Parameter Type** |**Mandatory** |**Sample Value** |**Description** |
|---|---|---|---|---|
|ak |string |Mandatory |AKTPYmI1Z\*\*\*\* |Access Key ID, that is, Key ID. |
|sk |string |Mandatory |T1dJM01UU\*\*\*\* |SecretAccess Key, that is, a private access key. |
|region |string |Mandatory |cn\-beijing |TOS server region. |
|securityToken |string |Optional |STSkeyJBY2NvdW50SW\*\*\*\*\*\*\*\*\*\*\*\* |The security token in the temporary access credential. |
|endPoint |string |Optional |tos\-ap\-southeast\-1.bytepluses.com |TOS server\-side domain name. The default value is empty. If no protocol is specified, the HTTPS protocol is used by default, with the complete format being https://{host}:{port}. |
|enableVerifySSL |bool |Optional |true |Configure whether to enable SSL certificate verification; enabled by default. |
|autoRecognizeContentType |bool |Optional |true |Automatic MIME type recognition is enabled by default. |
|requestTimeout |int |Optional |120000 |Set the timeout duration for a single HTTP request in milliseconds; the default value is 120,000 milliseconds. |
|connectionTimeout |int |Optional |10000 |Set the connection establishment timeout period in milliseconds; the default value is 10,000 milliseconds. |
|enableCRC |bool |Optional |true |Whether to enable CRC data verification; enabled by default. |
|dnsCacheTime |int |Optional |3 |Validity period of DNS cache (unit: minutes). A value less than or equal to 0 disables DNS cache. The default value is 0. |
|proxyHost |string |Optional |localhost |Host address of the proxy server; currently, only the HTTP protocol is supported. |
|proxyPort |int |Optional |8080 |Port number of the proxy server. |
|proxyUsername |string |Optional |Alice |Username used for connecting to the proxy server. |
|proxyPassword |string |Optional |pwd123 |The user password used when connecting to the proxy server. |
|maxRetryCount |int |Optional |3 |Maximum number of retries allowed after a request failure. Default: three times. |
|maxConnections |int |Optional |25 |Maximum number of connections in the connection pool. Default: 25. |
|socketTimeout |int |Optional |30000 |Request timeout duration. If no data is received within the request timeout period, the connection will be closed. The default timeout is 30,000 milliseconds. |
|isCustomDomain |bool |Optional |false |Whether to prepend the bucket name to the Endpoint to access TOS using the virtual host domain name method; the value descriptions are as follows:<br><br><br>* true: Do not concatenate.<br><br>* false: Concatenation.<br><br><br>The default value is false.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When accessing TOS via a custom domain, you must set <code>isCustomDomain</code> to <code>true</code>.</div><br> |
