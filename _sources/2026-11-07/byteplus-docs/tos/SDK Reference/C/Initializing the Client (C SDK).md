---
title: "Initializing the Client (C SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Initializing-the-client-side-c-sdk"
---

TosClient provides a series of interfaces for interacting with the TOS service, enabling management of resources such as buckets and objects on the TOS service. TosClient can be initialized using methods such as AccessKey/SecretKey, STS (Security Token Service), etc. During initialization, you can configure optional parameters such as the connection establishment timeout and the maximum number of idle connections. This article describes how to initialize the TOS C SDK.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* [Install C SDK](https://docs.byteplus.com/docs/tos/Install-the-c-sdk)

* [Obtain AKSK Information](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey)


<span id=".6YWN572u6ZW_5pyf6K6_6Zeu5Yet6K-B"></span>
## Configure Long\-Term Access Credential

Before initializing the SDK, you must first configure long\-term access credentials. This chapter describes the steps for configuring long\-term access credentials on different operating systems.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The use of the C SDK on Windows systems is currently not supported.</div>



<Tabs>
<Tab zoneid="WbLo2IEpdx" title="macOS">
<TabTitle>macOS</TabTitle>

1. Open the terminal and execute the following command to open the file.


```Shell
nano ~/.bash_profile
```



2. Add AKSK information at the end of the file.


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


If the configuration is successful, the following example is returned:

```Shell
AKTPYmI1Z****
T1dJM01UU****
```



</Tab>
<Tab zoneid="QEJaPnfqsP" title="Linux">
<TabTitle>Linux</TabTitle>

1. Open the terminal and execute the following command to open the file.


```Shell
sudo vim /etc/profile
```



2. Add AKSK information at the end of the file.


```Shell
export TOS_ACCESS_KEY=AKTPYmI1Z****
export TOS_SECRET_KEY=T1dJM01UU****
```



3. Save the file and exit.

4. Execute the following commands to make the configuration information take effect.


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
</Tabs>


<span id=".5Yib5bu6LXRvc2NsaWVudA=="></span>
## Create TosClient

<span id=".5L2_55So5b-F6YCJ5Y-C5pWw5Yid5aeL5YyW"></span>
### Initialize with required parameters

The following code demonstrates how to initialize TosClient using required parameters such as the TOS domain name, AK, SK, Endpoint, and Region.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Endpoint is the access domain name for TOS external services. For information about endpoints supported by TOS, see <a href="https://docs.byteplus.com/docs/tos/docs-region-and-endpoint">Access Domain Endpoint</a>.</div>


* <div data-tips="true" data-tips-type="tip">AKSK information can be obtained from environment variables. For configuration methods, see <a href="https://docs.byteplus.com/docs/tos/Initializing-the-client-side-net-sdk">Configure Access Credentials</a>.</div>



```C
char* ak = getenv("TOS_ACCESS_KEY");
char* sk = getenv("TOS_SECRET_KEY");

void init_client_demo()
{
  
    tos_pool_t *pool;
    tos_client_t *client;
    
  
    tos_pool_create(&pool, NULL);
    
    
    
    client = tos_client_create(pool);
    client->config = tos_config_create(client->pool);
    
 
   
    tos_str_set(&client->config->endpoint, "*** Provide your endpoint ***");
    tos_str_set(&client->config->region, "*** Provide your region ***");
    tos_str_set(&client->config->access_key_id, ak);
    tos_str_set(&client->config->access_key_secret, sk);

    tos_pool_destroy(pool);
}
```


<span id=".5L2_55So5Y-v6YCJ5Y-C5pWw5Yid5aeL5YyW"></span>
### Initialize Using Optional Parameters

The TOS C SDK provides multiple optional parameters to customize the configuration of TosClient. The following code demonstrates how to customize the connection establishment timeout and read/write timeout settings for TosClient.

```C
char* ak = getenv("TOS_ACCESS_KEY");
char* sk = getenv("TOS_SECRET_KEY");

void init_client_demo()
{
   
    tos_pool_t *pool;
    tos_client_t *client;
    
    
    tos_pool_create(&pool, NULL);
    
   
     
    client = tos_client_create(pool);
    client->config = tos_config_create(client->pool);
    

 
    tos_str_set(&client->config->endpoint, "*** Provide your endpoint ***");
    tos_str_set(&client->config->region, "*** Provide your region ***");
    tos_str_set(&client->config->access_key_id, ak);
    tos_str_set(&client->config->access_key_secret, sk);

   
     

    client->ctl->options->connect_timeout = 5; 
    client->ctl->options->socket_timeout = 60; 
    tos_pool_destroy(pool);
}
```


<span id=".5bi46KeB6YWN572u5Zy65pmv"></span>
## Common Configuration Scenarios

<span id=".6YWN572u6LaF5pe25py65Yi2"></span>
### Configure Timeout Mechanism

In the SDK, the timeout duration can be adjusted using optional parameters, and the timeout parameters can be configured through the following functions:


* connect_timeout: Specifies the connection timeout, which is the maximum wait time during the connection establishment phase, measured in seconds. The default value is 10, meaning 10 seconds.

* `SetSocketTimeout`: Sets the timeout for reading and writing network streams, specifying the maximum wait time for a single Read/Write operation in seconds. The default value is 120, that is, 120 seconds.


The following code demonstrates how to set the SDK timeout.

```C
char* ak = getenv("TOS_ACCESS_KEY");
char* sk = getenv("TOS_SECRET_KEY");

void init_client_demo()
{
   
    tos_pool_t *pool;
    tos_client_t *client;
    
    
    tos_pool_create(&pool, NULL);
    
   

  
    client = tos_client_create(pool);
    client->config = tos_config_create(client->pool);
    
  

    tos_str_set(&client->config->endpoint, "*** Provide your endpoint ***");
    tos_str_set(&client->config->region, "*** Provide your region ***");
    tos_str_set(&client->config->access_key_id, ak);
    tos_str_set(&client->config->access_key_secret, sk);

   
    
  
    client->ctl->options->connect_timeout = 5; 
    client->ctl->options->socket_timeout = 60; 
    tos_pool_destroy(pool);
}
```


<span id=".5Yid5aeL5YyW5Y-C5pWw5YiX6KGo"></span>
## Initialization Parameter List


|**Parameter Name** |**Parameter Type** |**Is it mandatory** |**Example Value** |**Description** |
|---|---|---|---|---|
|access_key_id |String |Required |AKTPYmI1ZGQwMDA0NjlhNGFkMzhjNzM0N2Q0OTQ3ZTV\*\*\*\* |Access Key ID (key ID). |
|access_key_secret |String |Required |T1dJM01UUXpOak0wTVdWak5E0poWldJNU1HWmxaV1V5TkdReVl6\*\*\*\* |SecretAccess Key, i.e., the private access key. |
|endpoint |String |Optional; if left empty, the value is determined by the Region parameter. |tos\-ap\-southeast\-1.bytepluses.com |TOS server\-side access domain name. |
|region |String |Optional; required if Endpoint is empty |cn\-beijing |Region where the TOS server is located. |
|sts_token |String |Optional |STSeyJBY2NvdW50SWQiOjIxMDAwMDUyMjQsIklkZW50aXR5VHlwZSI6NCwiSWRlbnRpdHlJZCI6MTE3MjI5NiwiQ2hhbm5lbCI6IlVzZXIiLCJBY2Nlc3NLZXlJZCI6IkFLVFBZbUkxWkdRd01mxoTkdGa016aGpOek0wTjJRME9UUTNaVFZqTXpFIiwiU2l\*\*\*\* |The security token in the temporary access credential. |
|socket_timeout |Int |Optional |120 |Socket read/write timeout period, measured in milliseconds, with a default value of 30000 ms (i.e., 30 s). |
|connect_timeout |Int |Optional |10 |Set the connection establishment timeout in milliseconds. The default value is 10000 ms, which is equivalent to 10 seconds. |
