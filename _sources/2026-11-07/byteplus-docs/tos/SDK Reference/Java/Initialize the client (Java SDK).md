---
title: "Initialize the client (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Initialize-client-side-java-sdk"
---

TosClient provides a set of interfaces to interact with TOS services, managing resources such as buckets and objects on TOS. TosClient can be initialized using AccessKey/SecretKey, STS (Security Token Service), and other methods. During initialization, you can set optional parameters such as connection timeout, retry attempts on timeout, and maximum idle connections. This article explains how to initialize the TOS Java SDK.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* [Install the SDK](https://docs.byteplus.com/docs/tos/Install-java-sdk)

* [Obtaining AKSK Information](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey)


<span id=".6YWN572u6ZW_5pyf6K6_6Zeu5Yet6K-B"></span>
## Configure long\-term access credentials

Before initializing the SDK, configure the long\-term access credentials first. This chapter explains the steps to configure long\-term access credentials on different operating systems.

<span id=".5Yib5bu6LXRvc2NsaWVudA=="></span>
## 
<Tabs>
<Tab zoneid="ZQdYVeyhxm" title="macOS">
<TabTitle>macOS</TabTitle>

1. Open the terminal and run the following command to open the file.


```Shell
nano ~/.bash_profile
```



2. Add AKSK information at the end of the file.


```Shell
export TOS_ACCESS_KEY=AKTPYmI1Z****
export TOS_SECRET_KEY=T1dJM01UU****
```



3. Save the file and exit.

4. Run the following command to apply the configuration.


```Shell
source ~/.bash_profile
```



5. Run the following command to verify the configuration.


```Shell
echo $TOS_ACCESS_KEY
echo $TOS_SECRET_KEY
```


If the configuration succeeds, the following example will be returned:

```Shell
AKTPYmI1Z****
T1dJM01UU****
```



</Tab>
<Tab zoneid="H9zjAgmpTu" title="Linux">
<TabTitle>Linux</TabTitle>

1. Open the terminal and run the following command to open the file.


```Shell
sudo vim /etc/profile
```



2. Add the AKSK information at the end of the file.


```Shell
export TOS_ACCESS_KEY=AKTPYmI1Z****
export TOS_SECRET_KEY=T1dJM01UU****
```



3. Save the file and exit.

4. Run the following command to apply the configuration.


```Shell
source /etc/profile
```



5. Run the following command to verify the configuration.


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
<Tab zoneid="rcuNIdxD6Z" title="Windows">
<TabTitle>Windows</TabTitle>

1. Open the command\-line tool and execute the following command to add AKSK information.


```Shell
set TOS_ACCESS_KEY=AKTPYmI1Z****
set TOS_SECRET_KEY=T1dJM01UU****
```



2. Execute the following command to apply the configuration.


```Shell
setx TOS_ACCESS_KEY "%TOS_ACCESS_KEY%"
setx TOS_SECRET_KEY "%TOS_SECRET_KEY%"
```



3. Restart the command\-line tool, then execute the following command to verify the configuration.


```Shell
echo %TOS_ACCESS_KEY%
echo %TOS_SECRET_KEY%
```


If the configuration succeeds, the following example will be returned:

```Shell
AKTPYmI1Z****
T1dJM01UU****
```



</Tab>
</Tabs>
Create TosClient

<span id=".5L2_55So5b-F6YCJ5Y-C5pWw5Yid5aeL5YyW"></span>
### **Initialize with required parameters**

The following code shows how to initialize TosClient using required parameters such as the TOS domain name, including AccessKey, SecretKey, Endpoint, and Region.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Endpoint is the publicly accessible domain name for TOS. For the supported Endpoint information in TOS, see <a href="https://docs.byteplus.com/docs/tos/docs-region-and-endpoint">Access domain Endpoint</a>.</div>


* <div data-tips="true" data-tips-type="tip">AKSK information can be obtained from environment variables. For configuration, see <a href="https://docs.byteplus.com/docs/tos/Initialize-client-side-java-sdk">Configure access credentials</a>.</div>



```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;

public class CreateTOSV2ClientExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);
        // do your operation...
    }
}
```


<span id=".5L2_55So5Y-v6YCJ5Y-C5pWw5Yid5aeL5YyW"></span>
### **Initialize with optional parameters**

The TOS Java SDK provides several optional parameters for custom configuration of TosClient, such as configuring STS, HTTP request timeouts, and retry policies. The following code shows how to customize the HTTP connection timeout for TosClient. For specific configuration scenarios, see [Configure timeout mechanisms](https://docs.byteplus.com/docs/tos/Initialize-client-side-java-sdk#.6YWN572u6LaF5pe25py65Yi2).

```java
import com.volcengine.tos.TOSClientConfiguration;
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.auth.StaticCredentials;
import com.volcengine.tos.transport.TransportConfig;

public class CreateTOSV2ClientWithOptionalParamsExample {
    public static void main(String[]  args)  {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");
        
        int connectTimeoutMills = 10000;

        TransportConfig config = TransportConfig.builder()
                .connectTimeoutMills(connectTimeoutMills)
                .build();
        TOSClientConfiguration configuration = TOSClientConfiguration.builder()
                .transportConfig(config)
                .region(region)
                .endpoint(endpoint)
                .credentials(new StaticCredentials(accessKey, secretKey))
                .build();

        TOSV2 tos = new TOSV2ClientBuilder().build(configuration);
        // do your operation...
    }
}
```


<span id=".5bi46KeB6YWN572u5Zy65pmv"></span>
## Common configuration scenarios

<span id=".6YWN572uLXN0cw=="></span>
### Configure STS

You can issue temporary access credentials to other users via the STS service. During the credential validity period, users can access your TOS resources without exposing your long\-term keys, ensuring the security of your TOS resources.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can obtain temporary access credentials through the AssumeRole interface of the STS service. These credentials include security keys (AccessKeyId, SecretAccessKey) and a security token (SessionToken). You can then use this information to access TOS services. For basic operations on setting up the STS service, refer to <a href="https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service">Using STS temporary AK/SK+Token to access BytePlus TOS</a>.</div>


The following code shows how to initialize TosClient using STS.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;

public class CreateTOSV2ClientWithSTSExample { 
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        // 以下 3 个字段均从 STS 服务中获取
        String accessKeyId = "your access key id";
        String secretAccessKey = "your secret access key";
        String sessionToken = "your secure session token";
    
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKeyId, secretAccessKey, sessionToken);
        // do your operation...
    }
}
```


<span id=".6YWN572u6LaF5pe25py65Yi2"></span>
### Configure timeout mechanisms

You can configure the network request timeout by adding optional parameters when initializing TosClient. The current TOS Java SDK provides the following timeout parameters for configuring HTTP request timeouts:


* readTimeoutMills: HTTP read request timeout in milliseconds, default is 30000, which is 30 seconds.

* writeTimeoutMills: HTTP write request timeout in milliseconds, default is 30000, which equals 30 seconds.

* connectTimeoutMills: HTTP connection timeout in milliseconds, default is 10000, which equals 10 seconds.


The following code demonstrates how to configure timeout settings when initializing TosClient.

```java
import com.volcengine.tos.TOSClientConfiguration;
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.auth.StaticCredentials;
import com.volcengine.tos.transport.TransportConfig;

public class CreateTOSV2ClientWithHttpTimeoutConfigExample {
    public static void main(String[]  args)  {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");
        
        int readTimeoutMills = 30000;
        int writeTimeoutMills = 30000;
        int connectTimeoutMills = 10000;

        TransportConfig config = TransportConfig.builder()
                .readTimeoutMills(readTimeoutMills)
                .writeTimeoutMills(writeTimeoutMills)
                .connectTimeoutMills(connectTimeoutMills)
                .build();
        TOSClientConfiguration configuration = TOSClientConfiguration.builder()
                .transportConfig(config)
                .region(region)
                .endpoint(endpoint)
                .credentials(new StaticCredentials(accessKey, secretKey))
                .build();

        TOSV2 tos = new TOSV2ClientBuilder().build(configuration);
        // do your operation...
    }
}
```


<span id=".6YWN572u6YeN6K-V562W55Wl"></span>
### Configure retry strategy

Network fluctuations or short\-term TOS service failures (returning HTTP 500 status code) may cause requests to the TOS service to fail. To address this, the Java SDK includes an internal retry mechanism. Idempotent interface operations use an exponential backoff strategy to retry on failure, while non\-idempotent interfaces throw the corresponding exception immediately. You can add optional parameters to configure the number of retries when initializing TosClient.

<span id=".6YeN6K-V5Zy65pmv"></span>
#### Retry scenarios


* The following SDK interfaces retry when the client request times out or the server returns 5xx or 429 errors.

   * All GET/HEAD type interfaces, such as getObject, headObject, headBucket.

   * Some PUT/DELETE type interfaces, such as putObjectACL, deleteObject.

   * For putObject/uploadPart interfaces, if the uploaded content (InputStream type) supports markSupported(), it is considered idempotent. For example, if content is a string, local file, or memory array ByteArrayInputStream.

   * putObjectFromFile/uploadPartFromFile/setObjectMeta interfaces.

* Except for appendObject, all POST type HTTP interfaces retry only when the server returns 5xx or 429 errors; client timeout does not trigger retries.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">getObject does not retry if a read exception occurs after returning the data stream to download, such as java.io.IOException: unexpected end of stream.</div>


<span id=".6YeN6K-V562W55Wl"></span>
#### Retry strategy

The Java SDK performs exponential backoff retries based on the set retry count, with a default of 3 retries.

<span id=".56S65L6L5Luj56CB"></span>
#### Example code

The following code shows how to set the SDK retry count.

```java
import com.volcengine.tos.TOSClientConfiguration;
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.auth.StaticCredentials;
import com.volcengine.tos.transport.TransportConfig;

public class CreateTOSV2ClientWithRetryConfigExample {
    public static void main(String[]  args)  {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        // 设置最大重试次数为 3 次，可根据实际需要调整
        int maxRetryCount = 3;

        TransportConfig config = TransportConfig.builder()
                .maxRetryCount(maxRetryCount)
                .build();
        TOSClientConfiguration configuration = TOSClientConfiguration.builder()
                .transportConfig(config)
                .region(region)
                .endpoint(endpoint)
                .credentials(new StaticCredentials(accessKey, secretKey))
                .build();

        TOSV2 tos = new TOSV2ClientBuilder().build(configuration);
        // do your operation...
    }
}
```


<span id=".6YWN572u5pWw5o2u5qCh6aqM"></span>
### Configure data validation

During object upload and download, the TOS server returns the object's CRC value. The SDK also calculates the object's CRC value and verifies whether it matches the CRC value returned by the TOS server, thus checking the integrity of the uploaded and downloaded data. To ensure data integrity during upload and download, the SDK enables CRC data validation by default. You can add an optional parameter to disable CRC validation when initializing TosClient.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">It is strongly recommended not to disable CRC data validation. If this feature is disabled, TOS does not guarantee data integrity during upload and download.</div>


```java
import com.volcengine.tos.TOSClientConfiguration;
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.auth.StaticCredentials;

public class CreateTOSV2ClientWithEnableCrcExample {
    public static void main(String[]  args)  {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        boolean enableCrc = true;
        
        TOSClientConfiguration configuration = TOSClientConfiguration.builder()
                .region(region)
                .endpoint(endpoint)
                .enableCrc(enableCrc)
                .credentials(new StaticCredentials(accessKey, secretKey))
                .build();

        TOSV2 tos = new TOSV2ClientBuilder().build(configuration);
        // do your operation...
    }
}
```


<span id=".6YWN572uLWRucy3nvJPlrZg="></span>
### Configure DNS cache

The TOS service domain name may experience delays or unresolvable issues in public network environments. The Java SDK addresses this issue by providing a DNS cache mechanism that caches the IP addresses resolved from domain names within the SDK, avoiding DNS resolution for every request.

The SDK's DNS cache mechanism is disabled by default. The following code demonstrates how to configure DNS cache time, with the default unit in minutes.

```java
import com.volcengine.tos.TOSClientConfiguration;
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.auth.StaticCredentials;
import com.volcengine.tos.transport.TransportConfig;

public class CreateTOSV2ClientWitDNSCacheExample {
    public static void main(String[]  args)  {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        int dnsCacheTimeMinutes = 0;

        TransportConfig config = TransportConfig.builder()
                .dnsCacheTimeMinutes(dnsCacheTimeMinutes)
                .build();
        TOSClientConfiguration configuration = TOSClientConfiguration.builder()
                .transportConfig(config)
                .region(region)
                .endpoint(endpoint)
                .credentials(new StaticCredentials(accessKey, secretKey))
                .build();

        TOSV2 tos = new TOSV2ClientBuilder().build(configuration);
        // do your operation...
    }
}
```


<span id=".6YWN572u5Luj55CG5pyN5Yqh5Zmo"></span>
### Configure proxy server

The TOS Java SDK supports accessing TOS services by configuring a proxy server. You can add optional parameters to configure the proxy server when initializing TosClient.

The following code demonstrates how to configure a proxy server.

```java
import com.volcengine.tos.TOSClientConfiguration;
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.auth.StaticCredentials;
import com.volcengine.tos.transport.TransportConfig;

public class CreateTOSV2ClientWithProxyExample {
    public static void main(String[]  args)  {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");
        
        // 代理服务器地址
        String proxyHost = "your proxy host";
        // 代理服务器端口，请填写您的代理服务器端口，此处仅为示例
        int proxyPort = 8080;
        // 代理服务器用户名
        String proxyUserName = "your proxy user name";
        // 代理服务器密码
        String proxyPassword = "your proxy password";
        
        TransportConfig config = TransportConfig.builder()
                .proxyHost(proxyHost)
                .proxyPort(proxyPort)
                .proxyUserName(proxyUserName)
                .proxyPassword(proxyPassword)
                .build();
        TOSClientConfiguration configuration = TOSClientConfiguration.builder()
                .transportConfig(config)
                .region(region)
                .endpoint(endpoint)
                .credentials(new StaticCredentials(accessKey, secretKey))
                .build();

        TOSV2 tos = new TOSV2ClientBuilder().build(configuration);
        // do your operation...
    }
}
```


<span id=".6YWN572u6L-e5o6l5rGg"></span>
### Configure connection pool

The Java SDK provides the following parameters for configuring the SDK HTTP connection pool.


* idleConnectionTimeMills: the idle time for connections in the HTTP connection pool. Connections exceeding this time are closed. The unit is milliseconds, with a default value of 60000, which equals 60 seconds.

* maxConnections: the maximum number of connections in the HTTP connection pool. The default value is 1024.


The following code demonstrates how to set the above parameters.

```java
import com.volcengine.tos.TOSClientConfiguration;
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.auth.StaticCredentials;
import com.volcengine.tos.transport.TransportConfig;

public class CreateTOSV2ClientWithIdlegExample {
    public static void main(String[]  args)  {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        int idleConnectionTimeMills = 60000;
        int maxConnections = 1024;

        TransportConfig config = TransportConfig.builder()
                .idleConnectionTimeMills(idleConnectionTimeMills)
                .maxConnections(maxConnections)
                .build();
        TOSClientConfiguration configuration = TOSClientConfiguration.builder()
                .transportConfig(config)
                .region(region)
                .endpoint(endpoint)
                .credentials(new StaticCredentials(accessKey, secretKey))
                .build();

        TOSV2 tos = new TOSV2ClientBuilder().build(configuration);
        // do your operation...
    }
}
```


<span id="811ef377"></span>
### Configure User\-Agent Extension Information (V2.8.1)

TOS Java SDK supports customers configuring custom business information into the User\-Agent. You can add optional parameters to configure User\-Agent extension information when initializing TosClient.

User\-Agent extension information specifications are as follows:

```Go
// 扩展模版
ve-tos-{sdk_type}-sdk/{sdk_version} ({os_type}/{cpu_arch};{language_version}) -- {product_name}/{soft_name}/{soft_version} ({custom_key1}/{custom_value1};{custom_key2}/{custom_value2};{custom_key3}/{custom_value3})

// 扩展后示例
ve-tos-java-sdk/v2.8.1 (linux/amd64;11.0.19) -- EMR/Hadoop/v3.0.0 (cloud_type/volc;cloud_region/cn-beijing)
```


The following code shows how to configure User\-Agent extension information.

```java
import com.volcengine.tos.TOSClientConfiguration;
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.auth.StaticCredentials;
import com.volcengine.tos.transport.TransportConfig;
import java.util.HashMap;
import java.util.Map;

public class CreateTOSV2ClientWithProxyExample {
    public static void main(String[]  args)  {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");
        
        Map<String, String> customInfo = new HashMap<>();
        customInfo.put("cloud_type", "volc");
        customInfo.put("cloud_region", "cn-beijing");
        TOSClientConfiguration configuration = TOSClientConfiguration.builder()
        .region(region)
        .endpoint(endpoint)
        .credentials(new StaticCredentials(accessKey, secretKey))
        .userAgentProductName("EMR")
        .userAgentSoftName("Spark")
        .userAgentSoftVersion("v3.1.2")
        .userAgentCustomizedKeyValues(customInfo)
        .build();
        
        TOSV2 tos = new TOSV2ClientBuilder().build(configuration);
        // do your operation...
    }
}
```


&nbsp;

<span id="9aa3d42e"></span>
### Associating a custom domain

TOS Java SDK supports setting custom domains. You can pass a custom domain as the Host when initializing TosClient. After specifying a custom domain, there is no need to pass Bucket in SDK interfaces.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You need to configure the custom domain on the server before using a custom domain. For details, see <a href="https://docs.byteplus.com/docs/tos/Set-up-a-custom-domain-name">Associating a custom domain</a>.</div>


In the SDK, you can use `isCustomDomain` to mark the current domain as a custom domain.

```Java
import com.volcengine.tos.TOSClientConfiguration;
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.auth.StaticCredentials;
import com.volcengine.tos.transport.TransportConfig;

public class CreateTOSV2ClientWithCustomDomainExample {
    public static void main(String[] args) {
        // endpoint填写自定义域名
        String endpoint = "your custom domain";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        TOSClientConfiguration configuration = TOSClientConfiguration.builder()
                .region(region)
                .endpoint(endpoint)
                .isCustomDomain(true)   // 标识当前域名为自定义域名
                .credentials(new StaticCredentials(accessKey, secretKey))
                .build();

        TOSV2 tos = new TOSV2ClientBuilder().build(configuration);
        // do your operation...
    }
}
```


<span id=".5Yid5aeL5YyW5Y-C5pWw5YiX6KGo"></span>
## initialize parameter list


|**Parameter** |**Type** |**Required** |**Example value** |**Note** |
|---|---|---|---|---|
|accessKey |String |Yes |AKTPYmI1Z\*\*\*\* |Access Key ID, the key ID, default is null. |
|secretKey |String |Yes |T1dJM01UU\*\*\*\* |SecretAccess Key, the private access key, default is null. |
|endpoint |String |No, defaults to region parameter when empty |tos\-ap\-southeast\-1.bytepluses.com |access domain name, default is null. |
|region |String |Yes |cn\-beijing |TOS server region, default is null. |
|securityToken |String |No |STSkeyJBY2NvdW50SW\*\*\*\*\*\*\*\*\*\*\*\* |security token in temporary access credentials, default is null. |
|writeTimeoutMills |int |No |30000 |HTTP write request timeout, in milliseconds, default value is 30000. |
|connectTimeoutMills |int |No |10000 |connection timeout in milliseconds, default is 10000. |
|idleConnectionTimeMills |int |No |60000 |If idle HTTP connection time in the connection pool exceeds this value, the HTTP connection will be closed. Unit: milliseconds. Default value is 60000. |
|maxConnections |int |No |1024 |maximum number of HTTP connection pool connections, default is 1024. |
|maxRetryCount |int |No |3 |maximum retry attempts on request failure, default is 3. |
|dnsCacheTimeMinutes |int |No |0 |DNS cache validity period in minutes. A value less than or equal to 0 disables DNS caching. The default value is 0. |
|proxyHost |String |no |"localhost" |Host address of the proxy server; only HTTP protocol is supported currently, default value is null. |
|proxyPort |int |No |8080 |Proxy server port number, default value is 0. |
|proxyUserName |String |No |"Alice" |Username for connecting to the proxy server, default value is null. |
|proxyPassword |String |No |"pwd123" |User password for connecting to the proxy server, default is null. |
|enableVerifySSL |boolean |no |true |Enable SSL certificate verification, default is true. |
|enableCrc |boolean |No |true |Enable CRC check, default is true. |
|clientAutoRecognizeContentType |boolean |No |true |Enable Content\-Type recognition based on object name extension; the default value is true. |
|isCustomDomain |boolean |No |false |Whether to append the bucket name before the Endpoint to access TOS via virtual host domain. The options are as follows:<br><br><br>* `true`: do not concatenate.<br><br>* `false`: concatenate.<br><br><br>The default value is false.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When accessing TOS via a custom domain, set <code>isCustomDomain</code> to <code>true</code>.</div><br> |
