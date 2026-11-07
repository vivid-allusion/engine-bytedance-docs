---
title: "Initialize the client (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Initializing-the-client-side-python-sdk"
---

YTosClient offers a series of interfaces to interact with TOS services, managing resources such as buckets and objects on TOS services. TosClient can be initialized using AccessKey/SecretKey, STS (Security Token Service), and other methods. During initialization, optional parameters such as connection timeout, retry count on timeout, and maximum idle connections can be set. This article explains how to initialize the TOS Python SDK.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* [Install the SDK](https://docs.byteplus.com/docs/tos/Install-the-python-sdk)

* [Obtain AKSK information](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey)


<span id="9e10ce79"></span>
## Notes

In single\-process, multi\-threaded scenarios, it is recommended to use a single TosClient to avoid repeated initialization of TosClient. In multi\-process scenarios, multiple TosClients need to be created and cannot share the same TosClient, otherwise there will be multi\-process concurrency security issues, which may lead to data corruption in read and write requests.

<span id=".6YWN572u6ZW_5pyf6K6_6Zeu5Yet6K-B"></span>
## Configure long\-term access credentials

Before initializing the SDK, configure long\-term access credentials first. This section explains the steps to configure long\-term access credentials on different operating systems.


<Tabs>
<Tab zoneid="fbHy3mRVHH" title="macOS">
<TabTitle>macOS</TabTitle>

1. Open the terminal and execute the following command to open the file.


```Shell
nano ~/.bash_profile
```



2. Add the AKSK information at the end of the file.


```Shell
export TOS_ACCESS_KEY=AKTPYmI1Z****
export TOS_SECRET_KEY=T1dJM01UU****
```



3. Save the file and exit.

4. Execute the following command to apply the configuration.


```Shell
source ~/.bash_profile
```



5. Execute the following command to verify the configuration.


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
<Tab zoneid="dXgcicRuwy" title="Linux">
<TabTitle>Linux</TabTitle>

1. Open the terminal and run the following command to open the file.


```Shell
sudo vim /etc/profile
```



2. Add AKSK information at the end of the file.


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


If the configuration is successful, the following example is returned:

&nbsp;




</Tab>
<Tab zoneid="uNFEMATaxA" title="Windows">
<TabTitle>Windows</TabTitle>

1. open the command line tool and run the following command to add AKSK information.


```Shell
set TOS_ACCESS_KEY=AKTPYmI1Z****
set TOS_SECRET_KEY=T1dJM01UU****
```



2. run the following command to apply the configuration.


```Shell
setx TOS_ACCESS_KEY "%TOS_ACCESS_KEY%"
setx TOS_SECRET_KEY "%TOS_SECRET_KEY%"
```



3. restart the command line tool, then run the following command to verify the configuration.


```Shell
echo %TOS_ACCESS_KEY%
echo %TOS_SECRET_KEY%
```


if the configuration is successful, the following example will be returned:

```Shell
AKTPYmI1Z****
T1dJM01UU****
```



</Tab>
</Tabs>


<span id=".5Yib5bu6LXRvc2NsaWVudA=="></span>
## Create TosClient

<span id=".5L2_55So5b-F6YCJ5Y-C5pWw5Yid5aeL5YyW"></span>
### **Initialize with required parameters**

The following code initializes using the TOS domain name.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Endpoint is the publicly accessible domain name for TOS. For supported TOS Endpoint information, see <a href="https://docs.byteplus.com/docs/tos/docs-region-and-endpoint">Endpoint</a>.</div>


* <div data-tips="true" data-tips-type="tip">AKSK information can be obtained from environment variables. For configuration, see <a href="https://docs.byteplus.com/docs/tos/Initializing-the-client-side-python-sdk">Configure access credentials</a>.</div>



```python
import os
import tos

# Set AKSK via environment variables
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')

endpoint = "your endpoint"
region = "your region"

client = tos.TosClientV2(ak, sk, endpoint, region)
```


<span id=".5L2_55So5Y-v6YCJ5Y-C5pWw"></span>
### **Use optional parameters**

The following code initializes using optional parameters.

```Python
import tos
import os

# ak and sk are security keys in temporary access credentials (AccessKeyId, SecretAccessKey)
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
sts_token = "your security token"

endpoint = "your endpoint"
region = "your region"

# Initialize TosClient using the authentication information in temporary access credentials
client = tos.TosClientV2(ak, sk, endpoint, region,
                         # Set STS through the optional security_token parameter
                         security_token=sts_token,
                         # Set connection timeout (in seconds) through the optional connection_time parameter
                         connection_time=10,
                         # Set socket read/write timeout (in seconds) through the optional socket_timeout parameter
                         socket_timeout=30)
```


<span id=".5bi46KeB6YWN572u5Zy65pmv"></span>
## Common configuration scenarios

<span id=".6YWN572uLXN0cw=="></span>
### Configure STS

You can issue temporary access credentials to other users through the STS service. Within the credentials' validity period, users can access your TOS resources without exposing your long\-term keys, ensuring the security of your TOS resources.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can obtain temporary access credentials via the AssumeRole interface of the STS service. These credentials include security keys (AccessKeyId, SecretAccessKey) and a security token (SessionToken). You can then use this information to access the TOS service. For basic operations on setting up the STS service, refer to <a href="https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service">using STS temporary AK/SK+Token to access BytePlus TOS</a>.</div>


The following code initializes using STS.

```python
import os
import tos

# ak and sk are security keys (AccessKeyId, SecretAccessKey) in temporary access credentials
ak = "your access key"
sk = "your secret key"
# sts_token is the security token (SessionToken) in temporary access credentials
sts_token = "your security token"

endpoint = "your endpoint"
region = "your region"

# Initialize TosClient using authentication information from temporary access credentials
client = tos.TosClientV2(ak, sk, endpoint, region, security_token=sts_token)
```


<span id=".6YWN572u6LaF5pe25py65Yi2"></span>
### Configure timeout mechanism

You can configure network request timeout when initializing TosClient by adding optional parameters. Currently, the TOS Python SDK supports configuring connection timeout `connection_time` and request timeout `socket_timeout`.

The following code configures timeout when initializing TosClient.

```Python
import tos
import os

# Get AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')

endpoint = "your endpoint"
region = "your region"

# create a TosClientV2 object and set the connection timeout to 30 seconds and the socket read/write timeout to 60 seconds
# connection_time is the connection timeout, and socket_timeout is the request timeout.
client = tos.TosClientV2(ak, sk, endpoint, region, connection_time=30, socket_timeout=60)
```


<span id=".6YWN572u6YeN6K-V562W55Wl"></span>
### Configure retry policy

Network fluctuations or short\-term TOS service exceptions (returning a 500 status code) can cause TOS service call failures. To address this, the Python SDK has an internal retry mechanism. Idempotent operation interfaces retry using an exponential backoff strategy after failure, while non\-idempotent interfaces throw the corresponding exception directly. You can add optional parameters to configure the number of retries when initializing TosClient.

```python
import os
import tos

# Obtain AKSK information from environment variables
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')

endpoint = "your endpoint"
region = "your region"

# Create a TosClientV2 object and set the timeout retry count to 3. The retry policy uses an exponential backoff strategy with a base time of 100ms: the first retry waits 100ms, the second 200ms, and the third 400ms.
client = tos.TosClientV2(ak, sk, endpoint, region, max_retry_count=3)
```


<span id=".6YWN572u5pWw5o2u5qCh6aqM"></span>
### Configure data validation

When uploading or downloading objects, TOS returns the object's CRC value. The SDK verifies that the locally calculated CRC matches the CRC returned by TOS to ensure data integrity during upload and download. To ensure data integrity during uploads and downloads, the SDK enables CRC data validation by default. You can disable the CRC validation feature by adding optional parameters when initializing TosClient.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">It is strongly recommended not to disable CRC data validation. If this feature is disabled, TOS does not guarantee data integrity during uploads and downloads.</div>


```python
import os
import tos

# Get AKSK information from environment variables
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')

endpoint = "your endpoint"
region = "your region"

# Create a TosClientV2 object and disable CRC data verification by setting enable_crc=False
client = tos.TosClientV2(ak, sk, endpoint, region, enable_crc=True)
```


<span id=".6YWN572u5Luj55CG5pyN5Yqh5Zmo"></span>
### Configure proxy server

The TOS Python SDK supports accessing TOS services through a proxy server. You can configure the proxy server by adding optional parameters when initializing TosClient.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, only HTTP protocol proxy is supported.</div>


```python
import os
import tos

# Get AKSK information from environment variables
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')

endpoint = "your endpoint"
region = "your region"

# Create a TosClientV2 object and configure a proxy using optional parameters proxy_host, proxy_port, proxy_username, and proxy_password
client = tos.TosClientV2(ak, sk, endpoint, region, proxy_host='<your proxy host>', proxy_port=80, proxy_username='<your proxy user name>', proxy_password='<your proxy password>')
```


<span id=".6YWN572u6L-e5o6l5rGg"></span>
### Configure connection pool

TOS Python SDK supports connection pool configuration. You can add an optional parameter to set the pool size when initializing TosClient.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The default connection pool size is 1024. It is recommended to use a single TosClient instance for single\-process, multi\-threaded scenarios.</div>


```python
import os
import tos

# Set AKSK via environment variables
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')

endpoint = "your endpoint"
region = "your region"

# Create a TosClientV2 object and set max_connections=1024 to configure the connection pool size to 1024
client = tos.TosClientV2(ak, sk, endpoint, region, max_connections=1024)
```


<span id="8c49636e"></span>
### Associate a custom domain

TOS Python SDK supports setting custom domains. You can pass a custom domain as the Host when initializing TosClient. After specifying a custom domain, you do not need to pass the Bucket in SDK interfaces.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before using a custom domain, you need to configure it on the server side. For details, see <a href="https://docs.byteplus.com/docs/tos/Set-up-a-custom-domain-name">Associating a custom domain</a>.</div>


```Python
import os
import tos

# set AKSK via environment variables
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
# fill in your custom domain and the corresponding region of your Bucket for custom_domain and your region # for example, for North China 2 (Beijing), fill in cn-beijing for your region
custom_domain = "your custom endpoint"
region = "your region"

# create a TosClientV2 object and set is_custom_domain=True to indicate the current domain is a custom domain
# before using a custom domain, configure it on TOS
# details: https://docs.byteplus.com/en/docs/6349/128983
client = tos.TosClientV2(ak, sk, custom_domain, region, is_custom_domain=True)
```


<span id="0d1ed57a"></span>
### Configure ECS password\-free login

Passwordless login refers to authentication that does not require specifying a key, but instead uses temporary security credentials provided by the Security Token Service (STS) to verify identity and complete authorization. This method does not require revealing a long\-term AccessKey, thus ensuring the security of keys under the account.

TOS Python SDK supports ECS password\-free login. You can add the `credentials_provider` parameter when initializing TosClient.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before using ECS password\-free login, first bind an IAM role to ECS. For details, see <a href="https://docs.byteplus.com/en/docs/ecs/AssociateInstancesIamRole">Binding IAM Role to ECS</a>, and initialize TosClient using the role name as a parameter.</div>


```Python

endpoint = "your endpoint"
region = "your region"
role_name = "your role name"

# Create a TosClientV2 object and set icredentials_provider=tos.EcsCredentialsProvider() to use ECS keyless login
# Create an IAM role and bind it to ECS before using password-free login for ECS
# Details: https://docs.byteplus.com/en/docs/6396/120181
client = tos.TosClientV2(endpoint=endpoint, region=region, credentials_provider=tos.EcsCredentialsProvider(role_name))
```


<span id=".5Yid5aeL5YyW5Y-C5pWw5YiX6KGo"></span>
## Initialization parameter list

The following parameters are supported for initializing TosClient.


|**Parameter** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|ak |str |Yes |AKTPYmI1ZGQwMDA0NjlhNGFkMzhjNzM0N2Q0OTQ3ZTV\*\*\*\* |Access Key ID, also known as Key ID. |
|sk |str |Yes |T1dJM01UUXpOak0wTVdWak5EUmtOR0poWldJNU1HWmxaV1V5TkdReVl6\*\*\*\* |SecretAccess Key, the private access key. |
|endpoint |str |Yes |tos\-ap\-southeast\-1.bytepluses.com |Access domain name. |
|region |str |Yes |cn\-beijing |TOS server region. |
|security_token |str |No |STSeyJBY2NvdW50SWQiOjIxMDAwMDUyMjQsIklkZW50aXR5VHlwZSI6NCwiSWRlbnRpdHlJZCI6MTE3MjI5NiwiQ2hhbm5lbCI6IlVzZXIiLCJBY2Nlc3NLZXlJZCI6IkFLVFBZbUkxWkdRd01EQTBOamxoTkdGa016aGpOek0wTjJRME9UUTNaVFZqTXpFIiwiU2l\*\*\*\* |Security token in temporary access credentials. |
|enable_verify_ssl |bool |No |True |Configure whether to enable SSL certificate verification. |
|auto_recognize_content_type |bool |No |True |Automatically identify MIME type. |
|connection_timeout |int |No |10 |Set the connection timeout in seconds. |
|max_connections |int |No |1024 |Set connection pool size. |
|enable_crc |bool |No |True |Enable or disable CRC data verification. |
|max_retry_count |int |No |3 |Maximum retry attempts for request failure. |
|dns_cache_time |int |No |5 |DNS cache validity period in minutes.<br><br>Default is 0. A value less than or equal to 0 means DNS caching is disabled. |
|proxy_host |str |No |None |Proxy server host address, currently only supports HTTP protocol. |
|proxy_port |int |No |None |Proxy server port number. |
|proxy_username |str |No |None |Username for connecting to the proxy server. |
|proxy_password |str |No |None |The username and password used to connect to the proxy server. |
|is_custom_domain |bool |No |False |Whether to append the bucket name before the endpoint to access TOS via virtual\-hosted style. The values are described as follows:<br><br><br>* `true`: Do not append.<br><br>* `false`: Append.<br><br><br>Default is false.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Set <code>isCustomDomain</code> to <code>true</code> when accessing TOS through a custom domain.</div><br> |
|high_latency_log_threshold |int |No |100 |A value greater than 0 indicates high latency logging is enabled, unit: KB. The default is 100. When the total transmission rate of a single request is below this value and the total request duration exceeds 500 milliseconds, a WARN level log is recorded. |
|socket_timeout |int |No |30 |Socket read and write timeout for a single request after connection is established.<br><br>Unit: seconds. Default is 30 seconds. |
|credentials_provider |object |No |None |Supports permanent access keys, temporary access keys, ECS password\-free login, environment variable access key retrieval, and other methods via `credentials_provider`. |
