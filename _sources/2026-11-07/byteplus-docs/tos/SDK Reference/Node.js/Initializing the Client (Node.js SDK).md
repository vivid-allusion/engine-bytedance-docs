---
title: "Initializing the Client (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Initializing-the-client-side-node-js-sdk"
---

You can send HTTP/HTTPS requests to the TOS service only after initializing a TOSClient instance. This article presents the initialization methods for the Node.js SDK.

The TOS Node.js client provides a series of interfaces for interacting with the TOS service, enabling management of resources such as buckets and objects on TOS. When initializing the client, you must provide the AccessKey ID, AccessKey Secret, Region, and other related information. During initialization, you can configure optional parameters such as connection establishment timeout, timeout retry count, and the maximum number of idle connections.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* [Install SDK](https://docs.byteplus.com/docs/tos/Install-the-node-js-sdk)

* [Obtaining AKSK Information](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey)


<span id=".6YWN572u6ZW_5pyf6K6_6Zeu5Yet6K-B"></span>
## Configuring Long\-Term Access Credentials

Before initializing the SDK, you must first configure long\-term access credentials. This chapter introduces the procedures for configuring long\-term access credentials on different operating systems.


<Tabs>
<Tab zoneid="ELBeTLrwZy" title="macOS">
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

4. Execute the following command to make the configuration take effect.


```Shell
source ~/.bash_profile
```



5. Run the following command(s) to verify the configuration information.


```Shell
echo $TOS_ACCESS_KEY
echo $TOS_SECRET_KEY
```


If the configuration is successful, the following example is returned:

```Shell
AKTPYmI1Z****
T1dJM01UU****
```



</Tab>
<Tab zoneid="dO0QdY47Lm" title="Linux">
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

4. Execute the following command(s) to make the configuration take effect.


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
<Tab zoneid="UrKaOHUeEI" title="Windows">
<TabTitle>Windows</TabTitle>

1. Open the command\-line tool, execute the following command, and add the AKSK information.


```Shell
set TOS_ACCESS_KEY=AKTPYmI1Z****
set TOS_SECRET_KEY=T1dJM01UU****
```



2. Execute the following commands to make the configuration information take effect.


```Shell
setx TOS_ACCESS_KEY "%TOS_ACCESS_KEY%"
setx TOS_SECRET_KEY "%TOS_SECRET_KEY%"
```



3. Restart the command\-line tool, and then execute the following commands to verify the configuration information.


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
## Creating a TosClient

<span id=".5L2_55So5b-F6YCJ5Y-C5pWw5Yid5aeL5YyW"></span>
### Initialize using required parameters

The following code demonstrates how to initialize TosClient using required parameters such as the TOS domain name, AccessKey ID, AccessKey Secret, Endpoint, and Region.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For more information on TOS regions and endpoints, see <a href="https://docs.byteplus.com/docs/tos/docs-region-and-endpoint">Regions and Endpoints</a>.</div>


* <div data-tips="true" data-tips-type="tip">AKSK information can be obtained from environment variables. For configuration instructions, please refer to <a href="https://docs.byteplus.com/docs/tos/Initializing-the-client-side-node-js-sdk">Configuring Access Credentials</a>.</div>



```javascript
import { TosClient } from '@volcengine/tos-sdk';

const client = new TosClient({
  accessKeyId: process.env['TOS_ACCESS_KEY'], 
  accessKeySecret: process.env['TOS_SECRET_KEY'], 
  region: "Provide your region", 
  endpoint: "Provide your endpoint", 
});
```


<span id=".5L2_55So5Y-v6YCJ5Y-C5pWw5Yid5aeL5YyW"></span>
### Initialize with optional parameters

The TOS Node.js SDK provides multiple optional parameters for customizing the configuration of TosClient, such as configuring STS, setting HTTP request timeouts, and specifying request retry policies.

The following code demonstrates how to customize the HTTP connection timeout for TosClient. For specific configuration scenarios, refer to the timeout mechanism section below.

```javascript
import { TosClient } from '@volcengine/tos-sdk';

const connectionTimeout = 10000;

const client = new TosClient({
  accessKeyId: process.env['TOS_ACCESS_KEY'], 
  accessKeySecret: process.env['TOS_SECRET_KEY'], 
  region: "Provide your region", 
  endpoint: "Provide your endpoint", 
  connectionTimeout,
});

console.log(client);
```


<span id=".5bi46KeB6YWN572u5Zy65pmv"></span>
## Common Configuration Scenarios

<span id=".6YWN572u6LaF5pe25py65Yi2"></span>
### Configure Timeout Mechanism

You can configure the network request timeout by specifying optional parameters during TosClient initialization. Currently, the TOS Node.js SDK provides the following timeout parameters for configuring HTTP request timeouts:


* `requestTimeout`: The HTTP request timeout duration, measured in milliseconds. The default value is 120,000, which is equivalent to 120 seconds.

* `connectionTimeout`: The timeout period for establishing an HTTP connection, measured in milliseconds. The default value is 10000, which corresponds to 10 seconds.

   The following code demonstrates how to configure the timeout setting during TosClient initialization.


```javascript
import { TosClient } from '@volcengine/tos-sdk';

const connectionTimeout = 10000;
const requestTimeout = 120000;

const client = new TosClient({
  accessKeyId: process.env['TOS_ACCESS_KEY'], 
  accessKeySecret: process.env['TOS_SECRET_KEY'], 
  region: "Provide your region", 
  endpoint: "Provide your endpoint", 
  connectionTimeout,
  requestTimeout,
});

console.log(client);
```


<span id=".6YWN572u6YeN6K-V562W55Wl"></span>
### Configuring Retry Strategies

Network fluctuations or short\-term TOS service anomalies (such as returning a 500 HTTP status code) may result in failed requests to the TOS service. To address this issue, the SDK incorporates an internal retry mechanism that performs exponential backoff retries according to the configured number of attempts, with the default set to three.

Interfaces supporting idempotent operations will retry upon failure using an exponential backoff strategy, whereas non\-idempotent interfaces will directly throw the corresponding exception. You can configure the number of retry attempts by adding an optional parameter during TosClient initialization.

The following code demonstrates how to set the retry count for the SDK.

```javascript
import { TosClient } from '@volcengine/tos-sdk';
const maxRetryCount = 3;

const client = new TOS({
  accessKeyId: process.env['TOS_ACCESS_KEY'], 
  accessKeySecret: process.env['TOS_SECRET_KEY'], 
  region: "Provide your region", 
  endpoint: "Provide your endpoint", 
  maxRetryCount,
});
```


<span id=".6YWN572u5pWw5o2u5qCh6aqM"></span>
### Configuration Data Validation

When uploading or downloading objects, CRC data validation is **disabled by default** in the TOS SDK, which may affect data integrity during transmission.

You can use the following code to enable CRC data verification.

```javascript
import { TosClient } from '@volcengine/tos-sdk';

const enableCRC = true;

const client = new TosClient({
  accessKeyId: process.env['TOS_ACCESS_KEY'], 
  accessKeySecret: process.env['TOS_SECRET_KEY'], 
  region: "Provide your region", 
  endpoint: "Provide your endpoint", 
  enableCRC,
});
```


<span id=".5Yid5aeL5YyW5Y-C5pWw5YiX6KGo"></span>
## Initialization Parameter List


|Parameter |  |  |Example value |Description |
|---|---|---|---|---|
|accessKeyId |String |Yes |AKTPYmI1Z\*\*\*\* |Access Key ID, Secret Key ID, default value: null. |
|accessKeySecret |String |Yes |T1dJM01UU\*\*\*\*== |AccessKey Secret: a private access key with a default value of null. |
|region |String |Yes |cn\-beijing |The region where the TOS server is located; the default value is null. |
|endpoint |String |Optional; if left empty, the value is determined by the region parameter. |tos\-ap\-southeast\-1.bytepluses.com |If the access domain name is left blank, its value will be determined by the region parameter. |
|stsToken |String |No |STSkeyJBY2NvdW50SW\*\*\*\*\*\*\*\*\*\*\*\* |Security token in the temporary access credential; the default value is null. |
|enableVerifySSL |boolean |No |true |Configure whether to enable SSL certificate verification; the default value is False. |
|autoRecognizeContentType |boolean |No |true |Automatic MIME type recognition is enabled by default. |
|requestTimeout |number |No |120000 |HTTP request timeout duration, in milliseconds; the default value is 120,000. |
|connectionTimeout |number |No |10000 |Connection establishment timeout, in milliseconds, with a default value of 10000. |
|idleConnectionTime |number |No |60000 |If the idle time of an HTTP connection in the connection pool exceeds the value specified by this parameter, the HTTP connection will be closed. The unit is milliseconds, and the default value is 60000. |
|maxConnections |number |No |1024 |The maximum number of connections in the HTTP connection pool is 1,024 by default. |
|maxRetryCount |number |No |3 |The maximum number of retry attempts after a request failure is 3 by default. |
|proxyHost |String |No |localhost |Host address of the proxy server; currently, only the HTTP protocol is supported. The default value is null. |
|proxyPort |number |No |8080 |Port number of the proxy server. |
|enableCRC |boolean |No |false |Indicates whether CRC verification is enabled; the default value is false. |
|isCustomDomain |boolean |No |false |Whether to prepend the bucket name to the Endpoint and access TOS using the virtual host domain name method. The value descriptions are as follows:<br><br><br>* `true`: Do not concatenate.<br><br>* `false`: Concatenation.<br><br><br>The default value is false.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When accessing TOS via a custom domain, you must set <code>isCustomDomain</code> to <code>true</code>.</div><br> |
