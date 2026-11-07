---
title: "Initialize Client (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Initializing-the-client-side-go-sdk"
---

This article presents example code for client initialization and introduces common configuration scenarios.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* [Install SDK](https://docs.byteplus.com/docs/tos/Install-the-go-sdk)

* [Obtaining AKSK Information](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey)


<span id=".6YWN572u6ZW_5pyf6K6_6Zeu5Yet6K-B"></span>
## Configuring Long\-Term Access Credentials

Before initializing the SDK, you must first configure long\-term access credentials. This section outlines the procedures for configuring long\-term access credentials across different operating systems.


<Tabs>
<Tab zoneid="qKzhY4Sm" title="macOS">
<TabTitle>macOS</TabTitle>

1. Open the terminal and execute the following command to open the file.


```Go
nano ~/.bash_profile
```



2. Add the AKSK information at the end of the file.


```Go
export TOS_ACCESS_KEY=AKTPYmI1Z****
export TOS_SECRET_KEY=T1dJM01UU****
```



3. Save the file and exit.

4. Execute the following command to apply the configuration.


```Go
source ~/.bash_profile
```



5. Execute the following command to verify the configuration.


```Go
echo $TOS_ACCESS_KEY
echo $TOS_SECRET_KEY
```


If the configuration succeeds, the following example will be returned:

```Go
AKTPYmI1Z****
T1dJM01UU****
```





</Tab>
<Tab zoneid="G79GHKi4" title="Linux">
<TabTitle>Linux</TabTitle>

1. Open the terminal and run the following command to open the file.


```Go
sudo vim /etc/profile
```



2. Add AKSK information at the end of the file.


```Go
export TOS_ACCESS_KEY=AKTPYmI1Z****
export TOS_SECRET_KEY=T1dJM01UU****
```



3. Save the file and exit.

4. Run the following command to apply the configuration.


```Go
source /etc/profile
```



5. Run the following command to verify the configuration.


```Go
echo $TOS_ACCESS_KEY
echo $TOS_SECRET_KEY
```


If the configuration is successful, the following example is returned:

```Go
AKTPYmI1Z****
T1dJM01UU****
```





</Tab>
<Tab zoneid="Z8XISXjs" title="Windows">
<TabTitle>Windows</TabTitle>

1. open the command line tool and run the following command to add AKSK information.


```Go
set TOS_ACCESS_KEY=AKTPYmI1Z****
set TOS_SECRET_KEY=T1dJM01UU****
```



2. run the following command to apply the configuration.


```Go
setx TOS_ACCESS_KEY "%TOS_ACCESS_KEY%"
setx TOS_SECRET_KEY "%TOS_SECRET_KEY%"
```



3. restart the command line tool, then run the following command to verify the configuration.


```Go
echo %TOS_ACCESS_KEY%
echo %TOS_SECRET_KEY%
```


if the configuration is successful, the following example will be returned:

```Go
AKTPYmI1Z****
T1dJM01UU****
```





</Tab>
</Tabs>


<span id="5twqpvS6"></span>
## Create TosClient

After initializing the TOSClient instance, you can send HTTP or HTTPS requests to the TOS service.

TOSClient provides a set of interfaces for interacting with TOS services, enabling the management of resources such as storage buckets and objects within the TOS service. When initializing TOSClient, you must provide the AccessKey, SecretKey, Endpoint, and Region.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The Endpoint is the domain name used to access TOS's external services. For information on Endpoints supported by TOS, please refer to <a href="https://docs.byteplus.com/docs/tos/docs-region-and-endpoint">Access Domain Endpoint</a>.</div>


* <div data-tips="true" data-tips-type="tip">AKSK information can be obtained from environment variables. For configuration method, please refer to <a href="https://docs.byteplus.com/docs/tos/Initializing-the-client-side-go-sdk">Access Credentials Configuration</a>.</div>



```go
package main

import (
   "fmt"
   "os"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

func main() {
   var (
      ak       = os.Getenv("TOS_ACCESS_KEY")
      sk       = os.Getenv("TOS_SECRET_KEY")
      
      endpoint = "*** Provide your endpoint ***"
      region   = "*** Provide your region ***"
   )
   credential := tos.NewStaticCredentials(ak, sk)
   client, err := tos.NewClientV2(endpoint, tos.WithCredentials(credential), tos.WithRegion(region))
   if err != nil {
      fmt.Println("Error:", err)
      panic(err)
   }
   
   client.Close()
}
```


**Configuring Client Optional Parameters via Option**

During Client initialization, optional parameters can be configured to meet the needs of different business scenarios by invoking functions that return ClientOption.

The following example uses `WithConnectionTimeout` and `WithSocketTimeout` to set the connection establishment timeout and the read/write timeout.

```go
package main

import (
   "fmt"
   "os"
   "time"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

func main() {
   var (
      ak       = os.Getenv("TOS_ACCESS_KEY")
      sk       = os.Getenv("TOS_SECRET_KEY")
    
      endpoint = "*** Provide your endpoint ***"
      region   = "*** Provide your region ***"
   )
   credential := tos.NewStaticCredentials(ak, sk)
  
 
   client, err := tos.NewClientV2(endpoint, tos.WithCredentials(credential), tos.WithRegion(region), tos.WithConnectionTimeout(10*time.Second), tos.WithSocketTimeout(30*time.Second, 30*time.Second))
   if err != nil {
      fmt.Println("Error:", err)
      panic(err)
   }

  
   client.Close()
}
```


<span id=".5bi46KeB6YWN572u5Zy65pmv"></span>
## Common Configuration Scenarios

<span id=".6YWN572uLXN0cw=="></span>
### Configuring STS

If you prefer not to disclose long\-term key information, you can use the STS service to create a temporary access credential. This allows users to access TOS resources within the credential’s validity period; once expired, the credential becomes invalid, thereby effectively safeguarding the security of your resources.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can obtain temporary access credentials through the AssumeRole API of the STS service. These temporary credentials include security keys (AccessKeyId and SecretAccessKey) and a security token (SessionToken). Subsequently, you can use this information to access the TOS service. For basic operations on setting up the STS service, please refer to <a href="https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service">Using STS Temporary AK/SK+Token to Access Volcengine TOS</a>.</div>


After obtaining the STS Token, you can initialize the TOS SDK using the following sample code.

```go
package main

import (
   "fmt"
   "os"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

func main() {
   var (
      ak       = "*** Provide your access key ***"
      sk       = "*** Provide your secret key ***"
      endpoint = "*** Provide your endpoint ***"
      region   = "*** Provide your region ***"
      stsToken = "*** Provide your sts token ***"
   )
   credential := tos.NewStaticCredentials(ak, sk)
  
   credential.WithSecurityToken(stsToken)
   client, err := tos.NewClientV2(endpoint, tos.WithCredentials(credential), tos.WithRegion(region))
   if err != nil {
      fmt.Println("Error:", err)
      panic(err)
   }
   client.Close()
}
```


<span id=".6YWN572u6LaF5pe25py65Yi2"></span>
### Configure Timeout Mechanism

In the SDK, the timeout duration can be adjusted using optional parameters. The following parameters are available for configuring the timeout:


* WithConnectionTimeout

   By using `WithConnectionTimeout`, you can set the connection timeout, which specifies the maximum waiting time during the connection establishment phase. The SDK's default timeout is 10 seconds.

* WithSocketTimeout

   The `WithSocketTimeout` function allows you to configure the timeout for reading and writing network streams, specifying the maximum wait time for a single read or write operation. The SDK default timeout is 30 seconds.


In the SDK, the default configuration for ConnectionTimeout is 10 seconds, while the default read/write timeout for SocketTimeout is set to 30 seconds.

```go
package main

import (
   "fmt"
   "os"
   "time"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

func main() {
   var (
      ak       = os.Getenv("TOS_ACCESS_KEY")
      sk       = os.Getenv("TOS_SECRET_KEY")
      
      endpoint = "*** Provide your endpoint ***"
      region   = "*** Provide your region ***"
   )
   credential := tos.NewStaticCredentials(ak, sk)
  
  
   client, err := tos.NewClientV2(endpoint, tos.WithCredentials(credential), tos.WithRegion(region), tos.WithConnectionTimeout(10*time.Second), tos.WithSocketTimeout(30*time.Second, 30*time.Second))
   if err != nil {
      fmt.Println("Error:", err)
      panic(err)
   }

   
   client.Close()
}
```


<span id=".6YWN572u6YeN6K-V562W55Wl"></span>
### Configuring Retry Strategies

In the TOS SDK, the number of retries after a request failure can be configured through the initialization parameter `WithMaxRetryCount`. This helps address request failures caused by network fluctuations and reduces the probability of encountering such errors again. Due to the fact that retry attempts may still fail in certain scenarios, this can even result in unpredictable outcomes. Retries are only performed in scenarios where idempotent semantics can be ensured. These scenarios include cases such as request timeouts, or when the server returns a 5XX error or a 429 error. The retry strategy of the TOS SDK is as follows:


* All HTTP interfaces of the GET/HEAD type, such as GetObjectV2 and HeadObject.

* Certain HTTP interfaces of the PUT/DELETE type, such as PutObjectACL and DeleteObjectV2.

* The PutObjectV2/UploadPartV2 interfaces can be considered to provide idempotent semantics when the Content field in the request body can be reset.


During TOS retries, exponential backoff is applied starting from a base interval of 100 ms until the maximum number of retries is reached. For example, when the maximum number of retries is 3, the retry intervals are 100 ms, 200 ms, and 400 ms, respectively.

In the default implementation of the SDK, the number of retry attempts is set to zero, indicating that no retries will be performed.

```go
package main

import (
   "fmt"
   "os"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

func main() {
   var (
      ak       = os.Getenv("TOS_ACCESS_KEY")
      sk       = os.Getenv("TOS_SECRET_KEY")
      endpoint = "*** Provide your endpoint ***"
      region   = "*** Provide your region ***"
   )
   credential := tos.NewStaticCredentials(ak, sk)
 
   client, err := tos.NewClientV2(endpoint, tos.WithCredentials(credential), tos.WithRegion(region), tos.WithMaxRetryCount(3))
   if err != nil {
      fmt.Println("Error:", err)
      panic(err)
   }

  
   client.Close()
}
```


<span id=".6YWN572u5pWw5o2u5qCh6aqM"></span>
### Configuration Data Validation

The TOS SDK **by default** enables CRC data validation when uploading or downloading objects, ensuring data integrity during transmission.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">It is strongly recommended that you do not disable the CRC data verification function. If this feature is disabled, TOS does not guarantee data integrity during upload and download processes.</div>


You can use the following code to enable CRC data verification.

```go
package main

import (
   "fmt"
   "os"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

func main() {
   var (
      ak       = os.Getenv("TOS_ACCESS_KEY")
      sk       = os.Getenv("TOS_SECRET_KEY")
      endpoint = "*** Provide your endpoint ***"
      region   = "*** Provide your region ***"
   )
   credential := tos.NewStaticCredentials(ak, sk)
   
   client, err := tos.NewClientV2(endpoint, tos.WithCredentials(credential), tos.WithRegion(region), tos.WithEnableCRC(true))
   if err != nil {
      fmt.Println("Error:", err)
      panic(err)
   }
   
   client.Close()
}
```


<span id=".6YWN572uLWRucy3nvJPlrZg="></span>
### Configure DNS Cache

In public network environments, domain name resolution may be time\-consuming or may be unavailable for a period of time. The TOS SDK allows you to configure the validity period of the domain name cache by setting `WithDNSCacheTime`, with a default value of`0`, indicates that the domain name cache feature is disabled.

```go
package main

import (
   "fmt"
   "os"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

func main() {
   var (
      ak       = os.Getenv("TOS_ACCESS_KEY")
      sk       = os.Getenv("TOS_SECRET_KEY")
      endpoint = "*** Provide your endpoint ***"
      region   = "*** Provide your region ***"
   )
   credential := tos.NewStaticCredentials(ak, sk)
   
   client, err := tos.NewClientV2(endpoint, tos.WithCredentials(credential), tos.WithRegion(region), tos.WithDNSCacheTime(60))
   if err != nil {
      fmt.Println("Error:", err)
      panic(err)
   }
   
   client.Close()
}
```


<span id=".6YWN572u5Luj55CG5pyN5Yqh5Zmo"></span>
### Configuring a Proxy Server

The TOS Go SDK supports configuring HTTP protocol proxy services. You can create a new HTTP proxy using the NewProxy method. If authentication is required, you may set the account and password via the Proxy's WithAuth method. After obtaining the Proxy instance, you can configure it using WithProxy.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, only HTTP protocol proxy is supported.</div>


```go
package main

import (
   "fmt"
   "os"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

func checkErr(err error) {
   if err != nil {
      if serverErr, ok := err.(*tos.TosServerError); ok {
         fmt.Println("Error:", serverErr.Error())
         fmt.Println("Request ID:", serverErr.RequestID)
         fmt.Println("Response Status Code:", serverErr.StatusCode)
         fmt.Println("Response Header:", serverErr.Header)
         fmt.Println("Response Err Code:", serverErr.Code)
         fmt.Println("Response Err Msg:", serverErr.Message)
      } else if clientErr, ok := err.(*tos.TosClientError); ok {
         fmt.Println("Error:", clientErr.Error())
         fmt.Println("Client Cause Err:", clientErr.Cause.Error())
      } else {
         fmt.Println("Error:", err)
      }
      panic(err)
   }
}

func main() {
   var (
      ak        = os.Getenv("TOS_ACCESS_KEY")
      sk        = os.Getenv("TOS_SECRET_KEY")
      endpoint  = "*** Provide your endpoint ***"
      region    = "*** Provide your region ***"
      proxyHost = "*** Provide your proxy host ***"
      proxyPort = 8080 /* Provide your proxy port */
   )
   proxy, err := tos.NewProxy(proxyHost, proxyPort)
   checkErr(err)
   credential := tos.NewStaticCredentials(ak, sk)
  
   client, err := tos.NewClientV2(endpoint, tos.WithCredentials(credential), tos.WithRegion(region), tos.WithProxy(proxy))
   checkErr(err)

   client.Close()
}
```


<span id=".6YWN572u6L-e5o6l5rGg"></span>
### Configure Connection Pool

The TOS Go SDK supports connection pool configuration. When initializing the TosClient, you can specify optional parameters to set the connection pool size. The parameters for connection pool configuration are described as follows.


|**Parameters** |**Description** |Default Value |
|---|---|---|
|MaxIdleConns |Configure the size of the idle connection pool. |1024 |
|MaxIdleConnsPerHost |Configure the cache size for a single Host in the idle connection pool. |1024 |
|MaxConnsPerHost |Configure the maximum number of available connections for a single Host. |1024 |


In the SDK, connection pool parameters can be configured using `WithMaxConnections`.

```go
package main

import (
   "fmt"
   "os"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

func main() {
   var (
      ak       = os.Getenv("TOS_ACCESS_KEY")
      sk       = os.Getenv("TOS_SECRET_KEY")
      endpoint = "*** Provide your endpoint ***"
      region   = "*** Provide your region ***"
   )
   credential := tos.NewStaticCredentials(ak, sk)
  
   op := tos.WithMaxConnections(1024)
   client, err := tos.NewClientV2(endpoint, tos.WithCredentials(credential), tos.WithRegion(region), op)
   if err != nil {
      fmt.Println("Error:", err)
      os.Exit(-1)
   }

   client.Close()
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>WithMaxConnections</code> will, by default, set all three parameters to the same value. If you need to configure them separately, you can do so via <code>Transport</code>.</div>


<span id="daef6a8c"></span>
### Setting Up a Custom Domain Name

The TOS Go SDK supports configuring a custom domain name. You can specify a custom domain name as the Host parameter when initializing TosClient. After specifying a custom domain name, it is not necessary to provide the Bucket parameter when using the SDK interface.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before using a custom domain, you must configure the custom domain on the server. For details, please refer to <a href="https://docs.byteplus.com/docs/tos/Set-up-a-custom-domain-name">Setting Up a Custom Domain</a>.</div>


In the SDK, the `WithCustomDomain` identifier can be used to designate the current domain as a custom domain.

```Go
package main

import (
    "fmt"
    "os"

    "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

func main() {
    var (
       ak           = os.Getenv("TOS_ACCESS_KEY")
       sk           = os.Getenv("TOS_SECRET_KEY")
       customDomain = "*** Provide your custom domain ***"
       region       = "*** Provide your region ***"
    )
    credential := tos.NewStaticCredentials(ak, sk)



    op := tos.WithCustomDomain(true)
    client, err := tos.NewClientV2(customDomain, tos.WithCredentials(credential), tos.WithRegion(region), op)
    if err != nil {
       fmt.Println("Error:", err)
       os.Exit(-1)
    }

    client.Close()
}
```


<span id=".5Yid5aeL5YyW5Y-C5pWw5YiX6KGo"></span>
## Initialization Parameter List

The following parameters are supported for initializing TosClient.


|**Parameters** |**Parameter Type** |**Mandatory** |**Sample Value** |**Description** |
|---|---|---|---|---|
|AccessKeyID |string |Mandatory |AKTPYmI1ZGQwMDA0NjlhNGFkMzhjNzM0N2Q0OTQ3ZTV\*\*\*\* |Access Key ID, also known as Key ID. |
|AccessKeySecret |string |Mandatory |T1dJM01UUXpOak0wTVdWak5EUmtOR0poWldJNU1HWmxaV1V5TkdReVl6\*\*\*\* |SecretAccess Key, that is, the private access key. |
|Endpoint |string |Mandatory |tos\-ap\-southeast\-1.bytepluses.com |Access the domain name. |
|Region |string |Mandatory |ap\-southeast\-1 |Region where the TOS server is located. |
|SecurityToken |string |Optional |STSeyJBY2NvdW50SWQiOjIxMDAwMDUyMjQsIklkZW50aXR5VHlwZSI6NCwiSWRlbnRpdHlJZCI6MTE3MjI5NiwiQ2hhbm5lbCI6IlVzZXIiLCJBY2Nlc3NLZXlJZCI6IkFLVFBZbUkxWkdRd01EQTBOamxoTkdGa016aGpOek0wTjJRME9UUTNaVFZqTXpFIiwiU2l\*\*\*\*\*\*\*\*\*\*\*\* |The security token contained in the temporary access credential. |
|EnableVerifySSL |bool |Optional |True |Configure whether to enable SSL certificate verification; the default value is False. |
|Transport |struct |Optional |Refer to the configuration of DefaultTransportConfig. |Set a custom Transport; for default values, refer to tos.DefaultTransportConfig(). |
|AutoRecognizeContentType |bool |Optional |True |Automatic MIME type detection is enabled by default. |
|SocketTimeout |time.Duration |Optional |30\*time.Second |Socket read/write timeout period, with a default value of 30 seconds. |
|ConnectionTimeout |time.Duration |Optional |10\*time.Second |Set the connection establishment timeout; the default value is 10 seconds. |
|MaxConnections |int |Optional |1024 |Set the maximum number of connections; the default value is 1024. |
|IdleConnTimeout |time.Duration |Optional |60\*time.Second |Configure the maximum connection idle time; if this duration is exceeded, the connection will be terminated. The default value for the SDK is 60 seconds. |
|Logger |struct |Optional |logrus.New() |Configure a custom Logger; by default, no logs are output. |
|MaxRetryCount |int |Optional |5 |Set the maximum number of retry attempts; the default value is 0 times. |
|EnableCRC |bool |Optional |True |Setting to enable CRC verification; default value is True. |
|DNSCacheTime |int |Optional |30 |Set the domain name cache duration; the time unit is minutes. The default value is 0 minutes, which means domain name caching is not enabled. |
|Proxy |struct |Optional | |Configure an HTTP forward proxy. The default value is empty; no connection proxy is used. |
|IsCustomDomain |bool |Optional |False |Indicates whether to prepend the bucket name to the Endpoint in order to access TOS using the virtual host domain name method. The value description is as follows:<br><br><br>* `true`: Do not concatenate.<br><br>* `false`: Concatenation.<br><br><br>The default value is false.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When accessing TOS via a custom domain, you must set <code>isCustomDomain</code> to <code>true</code>.</div><br> |
