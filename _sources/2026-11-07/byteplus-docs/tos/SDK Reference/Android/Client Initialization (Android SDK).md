---
title: "Client Initialization (Android SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Initialize-client-side-android-sdk"
---

The TOS SDK provides a set of interfaces for interacting with TOS services, enabling the management of resources such as buckets and objects. You can initialize TOSV2Client using methods such as AccessKey/SecretKey, STS (Security Token Service), and others. TOS also supports configuring optional parameters such as connection establishment timeout and maximum number of idle connections. You may configure settings in accordance with your business requirements by referring to this document.

<span id=".5Yib5bu6LXRvc2NsaWVudA=="></span>
## Creating a TosClient

<span id=".5L2_55SoLXN0cy3lj4LmlbDliJvlu7rvvIjmjIflrpotc2VjdXJpdHl0b2tlbu-8jOaOqOiNkO-8iQ=="></span>
### Create using STS parameters (specify SecurityToken; recommended)

Android mobile devices constitute an untrusted environment; storing the `accessKey` and `secretKey` directly on the device for request signing carries a high risk. It is strongly recommended to use STS parameters when creating TOSV2Client.

STS (Security Token Service) is a service that grants temporary access to third\-party users. With STS, you can provide token access credentials with customizable expiration times to third\-party applications or sub\-users.

TOS supports temporary authorized access via STS, and the Android SDK provides corresponding access interfaces. Configure the authorized token in the SDK to enable access to the TOS service.

The following code demonstrates how to initialize TOSV2Client using STS.

```java
String endpoint = "your endpoint";
String region = "your region";
String accessKey = "your access key";
String secretKey = "your secret key";
String securityToken = "your security token";

TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);
// do your operation...
```


<span id=".5L2_55So5b-F6YCJ5Y-C5pWw5Yib5bu677yIcmVnaW9uLWVuZHBvaW50LWFjY2Vzc2tleS1zZWNyZXRrZXnvvIzkuI3mjqjojZDvvIk="></span>
### Create using required parameters (Region + Endpoint + AccessKey/SecretKey, not recommended)

For information on the Regions and Endpoints supported by TOS, please refer to [Regions and Endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

AKSK information can be obtained from environment variables. You may refer to the following steps to configure AKSK information in environment variables.


<Tabs>
<Tab zoneid="OQMjbGMMpo" title="macOS">
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

4. Execute the following command to make the configuration information take effect.


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
<Tab zoneid="HHglzxEU8c" title="Linux">
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
<Tab zoneid="M9Za5OhgVe" title="Windows">
<TabTitle>Windows</TabTitle>

1. Open the command\-line tool, execute the following command, and add the AKSK information.


```Shell
set TOS_ACCESS_KEY=AKTPYmI1Z****
set TOS_SECRET_KEY=T1dJM01UU****
```



2. Execute the following commands to apply the configuration settings.


```Shell
setx TOS_ACCESS_KEY "%TOS_ACCESS_KEY%"
setx TOS_SECRET_KEY "%TOS_SECRET_KEY%"
```



3. Restart the command\-line tool, and then execute the following command to verify the configuration information.


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


The following is sample code for initializing TOSV2Client.

```java
String endpoint = "your endpoint";
String region = "your region";
String accessKey = System.getenv("TOS_ACCESS_KEY");
String secretKey = System.getenv("TOS_SECRET_KEY");

TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);
// do your operation...
```


<span id=".5bi46KeB6YWN572u5Zy65pmv"></span>
## Common Configuration Scenarios

<span id=".6YWN572u6LaF5pe25py65Yi2"></span>
### Configure Timeout Mechanism

The Android SDK provides the following timeout parameters for configuring HTTP request timeouts.


* readTimeoutMills: HTTP read request timeout period, measured in milliseconds. The default value is 30000, which corresponds to 30 seconds.

* writeTimeoutMills: Specifies the HTTP write request timeout in milliseconds. The default value is 30000 (30 seconds).

* connectTimeoutMills: The timeout period for establishing an HTTP connection, measured in milliseconds. The default value is 10000, which corresponds to 10 seconds.


The following code demonstrates how to configure the aforementioned timeout parameters.

```java
String endpoint = "your endpoint";
String region = "your region";
String accessKey = "your access key";
String secretKey = "your secret key";
String securityToken = "your security token";

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
    .credentials(new StaticCredentials(accessKey, secretKey).withSecurityToken(securityToken))
    .build();

TOSV2 tos = new TOSV2ClientBuilder().build(configuration);
// do your operation...
```


<span id=".6YWN572u6YeN6K-V562W55Wl"></span>
### Configuring Retry Strategies

Beginning with version 2.2.0, a retry mechanism was added to the underlying layer of the Android SDK. When a client request times out, or the server returns a 5xx error or a 429 error, the SDK will perform backoff and retry for requests to interfaces that support idempotent semantics.

<span id=".6YeN6K-V5Zy65pmv"></span>
#### Retry Scenarios

The following interfaces will retry when a client request times out, or when the server returns a 5xx error or a 429 error.


* All GET/HEAD\-type interfaces, such as GetObject, HeadObject, and HeadBucket.

* Some interfaces are of the PUT/DELETE type, such as PutObjectACL and DeleteObject.

* For the PutObject/UploadPart interfaces, if the uploaded content (of InputStream type) supports markSupported(), the operation can be considered to have idempotent semantics. For example, content may be a string, a local file, a memory array, a ByteArrayInputStream, etc.

* PutObjectFromFile, UploadPartFromFile, and SetObjectMeta interfaces.


Except for AppendObject, all POST\-type HTTP interfaces will only retry when the server returns a 5xx error or a 429 error; retries will not be attempted in the event of a client timeout.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If a read exception occurs after GetObject returns the data stream to be downloaded, such as java.io.IOException: unexpected end of stream, no retry will be performed.</div>


<span id=".6YeN6K-V562W55Wl"></span>
#### Retry Strategy

The Android SDK performs exponential backoff retries according to the configured number of attempts, with the default set to three attempts.

<span id=".56S65L6L5Luj56CB"></span>
#### Sample Code

The following code demonstrates how to configure the retry count for the SDK.

```java
String endpoint = "your endpoint";
String region = "your region";
String accessKey = "your access key";
String secretKey = "your secret key";
String securityToken = "your security token";


int maxRetryCount = 3;

TransportConfig config = TransportConfig.builder()
    .maxRetryCount(maxRetryCount)
    .build();
TOSClientConfiguration configuration = TOSClientConfiguration.builder()
    .transportConfig(config)
    .region(region)
    .endpoint(endpoint)
    .credentials(new StaticCredentials(accessKey, secretKey).withSecurityToken(securityToken))
    .build();

TOSV2 tos = new TOSV2ClientBuilder().build(configuration);
// do your operation...
```


To disable the retry strategy, set maxRetryCount in the above code to a value **less than 0**, such as maxRetryCount = \-1.

<span id=".6YWN572u5pWw5o2u5qCh6aqM"></span>
### Configuration Data Validation

The TOS Android SDK supports verifying the integrity of uploaded and downloaded data through CRC calculation. For upload interfaces, including PutObject, AppendObject, UploadPart, PutObjectFromFile, and UploadFile, the server returns the Crc64 value of the uploaded data upon completion of the request. The SDK compares this value with the locally computed Crc64 value, and if they do not match, a TosClientException is thrown.

For the GetObject, GetObjectToFile, and DownloadFile interfaces, the Crc64 value is calculated during the download process. After the download is complete, the SDK compares the CRC64 value returned by the server with the CRC64 value calculated locally. If the values do not match, a TosClientException is thrown.

By default, CRC verification is enabled in the Android SDK. The following code demonstrates how to enable or disable CRC verification.

```java
String endpoint = "your endpoint";
String region = "your region";
String accessKey = "your access key";
String secretKey = "your secret key";
String securityToken = "your security token";


boolean enableCrc = true;

TOSClientConfiguration configuration = TOSClientConfiguration.builder()
    .enableCrc(enableCrc)
    .region(region)
    .endpoint(endpoint)
    .credentials(new StaticCredentials(accessKey, secretKey).withSecurityToken(securityToken))
    .build();

TOSV2 tos = new TOSV2ClientBuilder().build(configuration);
// do your operation...
```


<span id=".6YWN572uLWRucy3nvJPlrZg="></span>
### Configure DNS Cache

In public network environments, TOS service domain names may experience delays in domain name resolution or be unable to resolve for a period of time. To address this, the Android SDK implements a DNS caching mechanism that stores the IP addresses resolved from domain names within the SDK, eliminating the need to perform domain name resolution for every request.

The DNS caching mechanism of the SDK is disabled by default. The following code demonstrates how to configure the DNS cache duration. The default unit is minutes.

```java
String endpoint = "your endpoint";
String region = "your region";
String accessKey = "your access key";
String secretKey = "your secret key";
String securityToken = "your security token";


int dnsCacheTimeMinutes = 10;

TransportConfig config = TransportConfig.builder()
    .dnsCacheTimeMinutes(dnsCacheTimeMinutes)
    .build();
TOSClientConfiguration configuration = TOSClientConfiguration.builder()
    .transportConfig(config)
    .region(region)
    .endpoint(endpoint)
    .credentials(new StaticCredentials(accessKey, secretKey).withSecurityToken(securityToken))
    .build();

TOSV2 tos = new TOSV2ClientBuilder().build(configuration);
// do your operation...
```


<span id=".6YWN572u5Luj55CG5pyN5Yqh5Zmo"></span>
### Configure Proxy Server

Beginning with version 2.3.0, the Android SDK supports configuring access to proxy servers; currently, only HTTP protocol proxies are supported.

The following code demonstrates how to configure a proxy server.

```java
String endpoint = "your endpoint";
String region = "your region";
String accessKey = "your access key";
String secretKey = "your secret key";
String securityToken = "your security token";


String proxyHost = "your proxy host";

int proxyPort = 8080;

String proxyUserName = "your proxy user name";

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
    .credentials(new StaticCredentials(accessKey, secretKey).withSecurityToken(securityToken))
    .build();

TOSV2 tos = new TOSV2ClientBuilder().build(configuration);
// do your operation...
```


<span id=".6YWN572u6L-e5o6l5rGg"></span>
### Configure Connection Pool

The Android SDK provides the following parameters for configuring the underlying HTTP connection pool.


* idleConnectionTimeMills: Specifies the maximum idle time for a connection in the HTTP connection pool. If this threshold is exceeded, the connection will be closed. The unit is milliseconds. The default value is 60000 (60 seconds).

* maxConnections: Specifies the maximum number of connections in the HTTP connection pool; the default value is 1024.


The following code demonstrates how to configure the above parameters.

```java
String endpoint = "your endpoint";
String region = "your region";
String accessKey = "your access key";
String secretKey = "your secret key";
String securityToken = "your security token";

int idleConnectionTimeMills = 10000;
int maxConnections = 1024;

TransportConfig config = TransportConfig.builder()
    .idleConnectionTimeMills(idleConnectionTimeMills)
    .maxConnections(maxConnections)
    .build();
TOSClientConfiguration configuration = TOSClientConfiguration.builder()
    .transportConfig(config)
    .region(region)
    .endpoint(endpoint)
    .credentials(new StaticCredentials(accessKey, secretKey).withSecurityToken(securityToken))
    .build();

TOSV2 tos = new TOSV2ClientBuilder().build(configuration);
// do your operation...
```


<span id=".5Yid5aeL5YyW5Y-C5pWw5YiX6KGo"></span>
## Initialization Parameter List


|**Parameters** |**Description** |Parameter Type |**Default Value** |Sample Value |
|---|---|---|---|---|
|accessKey |Access Key ID (密钥ID). |String |null |AKTPYmI1Z\*\*\*\* |
|secretKey |SecretAccess Key: a private access key. |String |null |T1dJM01UU\*\*\*\*== |
|endpoint |Access the domain name. |String |null |tos\-ap\-southeast\-1.bytepluses.com |
|region |The region where the TOS server is located. |String |null |cn\-beijing |
|securityToken |The security token in the temporary access credential. |String |null |STSeyJBY2NvdW50SW\*\*\*\*\*\*\*\*\*\*\*\* |
|writeTimeoutMills |HTTP write request timeout duration, in milliseconds. |int |30000 |30000 |
|connectTimeoutMills |Timeout period for establishing a connection, in milliseconds. |int |10000 |10000 |
|idleConnectionTimeMills |If the idle time of an HTTP connection in the connection pool exceeds the value specified by this parameter, the HTTP connection will be closed. Unit: milliseconds. |int |60000 |60000 |
|maxConnections |Maximum number of connections in the HTTP connection pool. |int |1024 |1024 |
|maxRetryCount |The maximum number of retry attempts after a request failure. |int |3 |3 |
|dnsCacheTimeMinutes |DNS cache validity period, in minutes; a value less than or equal to 0 indicates that DNS caching is disabled. |int |0 |0 |
|proxyHost |Host address of the proxy server; currently, only the HTTP protocol is supported. |String |null |"localhost" |
|proxyPort |Proxy server port number. |int |0 |8080 |
|proxyUserName |Username for connecting to the proxy server. |String |null |"Alice" |
|proxyPassword |The password used to connect to the proxy server. |String |null |"pwd123" |
|enableVerifySSL |Whether to enable SSL certificate verification. |boolean |true |true |
|enableCrc |Enable CRC verification? |boolean |true |true |
|clientAutoRecognizeContentType |Enable Content\-Type recognition based on object name suffix? |boolean |true |true |
