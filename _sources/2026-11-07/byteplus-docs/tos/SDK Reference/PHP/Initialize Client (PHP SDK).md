---
title: "Initialize Client (PHP SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Initializing-the-client-side-php-sdk"
---

TosClient is the PHP client for TOS, providing a suite of interfaces for interacting with TOS services to manage resources such as buckets and objects.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* [Installing the SDK](https://docs.byteplus.com/docs/tos/Install-the-php-sdk)

* [Obtaining AKSK information](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey)


<span id=".6YWN572u6ZW_5pyf6K6_6Zeu5Yet6K-B"></span>
## Configuring long\-term access credentials

Before initializing the SDK, you need to first configure long\-term access credentials. This section describes the procedures for configuring long\-term access credentials on different operating systems.


<Tabs>
<Tab zoneid="VWexNRJHa3" title="macOS">
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
<Tab zoneid="tL0tz2JVOb" title="Linux">
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
<Tab zoneid="cMrzE2GRa8" title="Windows">
<TabTitle>Windows</TabTitle>

1. Open the command\-line tool, execute the following command, and add the AKSK information.


```Shell
set TOS_ACCESS_KEY=AKTPYmI1Z****
set TOS_SECRET_KEY=T1dJM01UU****
```



2. Execute the following command to apply the configuration settings.


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


<span id=".5Yib5bu6LXRvc2NsaWVudA=="></span>
## Create TosClient


* Using region and endpoint


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Endpoint is the access domain name for TOS external services. For information on Endpoints supported by TOS, please refer to <a href="https://docs.byteplus.com/docs/tos/docs-region-and-endpoint">Regions and endpoints</a>.</div>


* <div data-tips="true" data-tips-type="tip">AKSK information can be obtained from environment variables. For the configuration method, please refer to <a href="https://docs.byteplus.com/docs/tos/Initializing-the-client-side-php-sdk">Access credential configuration</a>.</div>



```php
<?php

require_once __DIR__ . '/vendor/autoload.php';

use Tos\TosClient;

$region = 'your region';
$endpoint = 'your endpoint';

$ak = getenv('TOS_ACCESS_KEY'); 
$sk = getenv('TOS_SECRET_KEY'); 

try {
    $client = new TosClient([
        'region' => $region,
        'endpoint' => $endpoint,
        'ak' => $ak,
        'sk' => $sk,
    ]);
} catch (\RuntimeException $ex) {
    echo 'create TosClient failed, message: ' . $ex->getMessage() . PHP_EOL;
}
```



* Using [STS](https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service)


```php
<?php

require_once __DIR__ . '/vendor/autoload.php';

use Tos\TosClient;

$region = 'your region';
$endpoint = 'your endpoint';
$ak = 'your access key';
$sk = 'your secret key';
$securityToken = 'your security token';

try {
    $client = new TosClient([
        'region' => $region,
        'endpoint' => $endpoint,
        'ak' => $ak,
        'sk' => $sk,
        'securityToken' => $securityToken
    ]);
} catch (\RuntimeException $ex) {
    echo 'create TosClient failed, message: ' . $ex->getMessage() . PHP_EOL;
}
```


<span id=".6YWN572u5Yid5aeL5YyW5Y-C5pWw"></span>
## Configuration initialization parameters

You can configure TosClient during its creation by specifying initialization parameters. For the parameters that can be configured, please refer to the table below.


|Parameter | Type |Required  |Example value |Description |
|---|---|---|---|---|
|region |String |Yes |cn\-beijing |Region where the TOS server is located. |
|endpoint |String |Optional; when left empty, the value is determined by the `region` parameter. |https://tos\-ap\-southeast\-1.bytepluses.com |TOS server domain name: If no protocol is specified, HTTPS is used by default. The complete format is: `https://{host}:{port}`. |
|ak |String |Mandatory for standard buckets; optional if the bucket allows anonymous access. |AKTPYmI1ZGQwMDA0NjlhNGFkMzhjNzM0N2Q0OTQ3ZTV\*\*\*\* |The Access Key ID in the access key. |
|sk |String |Mandatory for standard buckets; optional if the bucket allows anonymous access. |T1dJM01UUXpOak0wTVdWak5EUmtOR0poWldJNU1HWmxaV1V5TkdReVl6\*\*\*\* |The Secret Access Key in the access key. |
|securityToken |String |No |3ZDA5MjY4NWYwMDQyYThlIiwiU2Vzc2lvbk5hbWUiOiJ0b3Nfcm9sZV9z\*\*\*\*\*\*\*\*\*\*\*\* |Temporarily authorized Security Token Service (STS). |
|connectionTimeout |float |No |30000 |Connection establishment timeout, unit: milliseconds; default value: 10,000 milliseconds. |
|socketTimeout |float |No |60000 |Socket read/write timeout period, unit: milliseconds; default is 30,000 milliseconds. |
|enableVerifySSL |bool |No |true |Whether to enable SSL certificate verification; the default value is true. |
|autoRecognizeContentType |bool |No |true |Whether MIME type detection is performed automatically; the default value is true. |
|isCustomDomain |bool |No |true |Indicates whether the bucket name is prefixed to the Endpoint to access TOS via a virtual host domain name. The value descriptions are as follows:<br><br><br>* `true`: No concatenation.<br><br>* `false`: Concatenation.<br><br><br>The default value is false.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When accessing TOS via a custom domain, you must set <code>isCustomDomain</code> to <code>true</code>.</div><br> |
