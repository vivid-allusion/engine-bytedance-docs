---
title: "Client Initialization (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Initializing-the-client-side-net-sdk"
---

TosClient provides a series of interfaces for interacting with TOS services, enabling the management of resources such as buckets and objects within TOS. TosClient can be initialized using methods such as AccessKey/SecretKey, STS (Security Token Service), and others. During initialization, you may configure optional parameters such as connection establishment timeout and maximum number of idle connections. This article describes how to initialize the TOS .NET SDK.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* [Installing the SDK](https://docs.byteplus.com/docs/tos/Instal-the-net-sdk)

* [Obtaining AKSK Information](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey)


<span id=".6YWN572u6ZW_5pyf6K6_6Zeu5Yet6K-B"></span>
## Configuring Long\-Term Access Credentials

Before initializing the SDK, you need to first configure long\-term access credentials. This section outlines the procedures for configuring long\-term access credentials on different operating systems.


<Tabs>
<Tab zoneid="hqB9veWv40" title="macOS">
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


If the configuration is successful, the following example is returned:

```Shell
AKTPYmI1Z****
T1dJM01UU****
```



</Tab>
<Tab zoneid="H7dPTfedBI" title="Linux">
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

4. Execute the following commands for the configuration information to take effect.


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
<Tab zoneid="DkPJgXStkv" title="Windows">
<TabTitle>Windows</TabTitle>

1. Open the command\-line tool, execute the following command, and add the AKSK information.


```Shell
set TOS_ACCESS_KEY=AKTPYmI1Z****
set TOS_SECRET_KEY=T1dJM01UU****
```



2. Execute the following command for the configuration to take effect.


```Shell
setx TOS_ACCESS_KEY "%TOS_ACCESS_KEY%"
setx TOS_SECRET_KEY "%TOS_SECRET_KEY%"
```



3. Restart the command\-line tool, and then execute the following command to verify the configuration information.


```Shell
echo %TOS_ACCESS_KEY%
echo %TOS_SECRET_KEY%
```


If the configuration is successful, the following example is returned:

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



* <div data-tips="true" data-tips-type="tip">The Endpoint is the access domain name for TOS external services. For information on Endpoints supported by TOS, please refer to <a href="https://docs.byteplus.com/docs/tos/docs-region-and-endpoint">Access Domain Name Endpoint</a>.</div>


* <div data-tips="true" data-tips-type="tip">AKSK information can be obtained from environment variables. For configuration instructions, see <a href="https://docs.byteplus.com/docs/tos/Initializing-the-client-side-net-sdk">Configuring Access Credentials</a>.</div>



```C#
using TOS;

namespace ConsoleApp
{
    internal class Program
    {
        private static void Main(string[] args)
        {
            var ak = Environment.GetEnvironmentVariable("TOS_ACCESS_KEY");
            var sk = Environment.GetEnvironmentVariable("TOS_SECRET_KEY");
            var endpoint = "*** Provide your endpoint ***";
            var region = "*** Provide your region ***";

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();
        }
    }
}
```


<span id=".5L2_55So5Y-v6YCJ5Y-C5pWw5Yid5aeL5YyW"></span>
### Use optional parameters to initialize

The TOS .NET SDK provides multiple optional parameters to customize the configuration of TosClient. The following code demonstrates how to customize the connection establishment timeout and read/write timeout settings for TosClient.

```C#
using TOS;

namespace ConsoleApp
{
    internal class Program
    {
        private static void Main(string[] args)
        {
            var ak = Environment.GetEnvironmentVariable("TOS_ACCESS_KEY");
            var sk = Environment.GetEnvironmentVariable("TOS_SECRET_KEY");
            var endpoint = "*** Provide your endpoint ***";
            var region = "*** Provide your region ***";

            var client = TosClientBuilder.Builder().
                SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).
                SetConnectionTimeout(30000).SetSocketTimeout(30000).
                Build();
        }
    }
}
```


<span id=".5bi46KeB6YWN572u5Zy65pmv"></span>
## Common Configuration Scenarios

<span id=".6YWN572u6LaF5pe25py65Yi2"></span>
### Configure Timeout Mechanism

In the SDK, the timeout duration can be adjusted using optional parameters. The following functions are available to configure the timeout parameters:


* `SetConnectionTimeout`: Sets the connection timeout, which specifies the maximum waiting time during the connection establishment phase, measured in milliseconds. The default value is 10,000, equivalent to 10 seconds.

* `SetSocketTimeout`: Sets the timeout for reading and writing network streams, specifying the maximum wait time for a single read or write operation in milliseconds. The default value is 30000 (30 seconds).


The following code demonstrates how to configure the SDK timeout.

```C#
using TOS;

namespace ConsoleApp
{
    internal class Program
    {
        private static void Main(string[] args)
        {
            var ak = Environment.GetEnvironmentVariable("TOS_ACCESS_KEY");
            var sk = Environment.GetEnvironmentVariable("TOS_SECRET_KEY");
            var endpoint = "*** Provide your endpoint ***";
            var region = "*** Provide your region ***";

            var client = TosClientBuilder.Builder().
                SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).
                SetConnectionTimeout(10000).SetSocketTimeout(30000).
                Build();
        }
    }
}
```


<span id=".6YWN572u6L-e5o6l5rGg"></span>
### Configuring the Connection Pool

The TOS .NET SDK supports connection pool configuration. When initializing TosClient, you can add the `MaxConnections` parameter to specify the maximum number of connections in the pool.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The default configuration for the connection pool size is 1024.</div>


The following code demonstrates how to configure the connection pool size for the SDK.

```C#
using TOS;

namespace ConsoleApp
{
    internal class Program
    {
        private static void Main(string[] args)
        {
            var ak = Environment.GetEnvironmentVariable("TOS_ACCESS_KEY");
            var sk = Environment.GetEnvironmentVariable("TOS_SECRET_KEY");
            var endpoint = "*** Provide your endpoint ***";
            var region = "*** Provide your region ***";

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region)
                .SetMaxConnections(1024).Build();
        }
    }
}
```


<span id=".5Yid5aeL5YyW5Y-C5pWw5YiX6KGo"></span>
## Initialization Parameter List


|**Parameter Name** | ** **  | ** **  |**Example value** |**Description** |
|---|---|---|---|---|
|AK |String |Yes |AKTPYmI1ZGQwMDA0NjlhNGFkMzhjNzM0N2Q0OTQ3ZTV\*\*\*\* |Access Key ID, that is, Key ID. |
|SK |String |Yes |T1dJM01UUXpOak0wTVdWak5E0poWldJNU1HWmxaV1V5TkdReVl6\*\*\*\* |SecretAccess Key, that is, the private access key. |
|Endpoint |String |Optional; if left blank, the value is determined by the Region parameter. |tos\-ap\-southeast\-1.bytepluses.com |TOS server\-side access domain name. |
|Region |String |Optional; required if Endpoint is empty. |cn\-beijing |The region where the TOS server is located. |
|SecurityToken |String |No |STSeyJBY2NvdW50SWQiOjIxMDAwMDUyMjQsIklkZW50aXR5VHlwZSI6NCwiSWRlbnRpdHlJZCI6MTE3MjI5NiwiQ2hhbm5lbCI6IlVzZXIiLCJBY2Nlc3NLZXlJZCI6IkFLVFBZbUkxWkdRd01mxoTkdGa016aGpOek0wTjJRME9UUTNaVFZqTXpFIiwiU2l\*\*\*\* |The security token within the temporary access credential. |
|EnableVerifySSL |Bool |No |true |Configures whether SSL certificate verification is enabled; the default value is true. |
|SocketTimeout |Int |No |30000 |Socket read/write timeout duration, measured in milliseconds, with a default value of 30,000 ms (30 seconds). |
|ConnectionTimeout |Int |No |10000 |Set the connection establishment timeout in milliseconds. The default value is 10,000 ms (10 seconds). |
|MaxConnections |Int |No |1024 |Set the maximum number of connections for the connection pool; the default value is 1024. |
|IdleConnectionTime |Int |No |60\*1000 (ms) |Configure the maximum connection idle time; if this duration is exceeded, the connection will be closed. The default value is 60 seconds. |
