---
title: "View or update the configuration file (config)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/View-or-update-the-configuration-file-config"
---

You can use the `config` command to view the configuration file path and update key configuration information in the file.

<span id=".5p-l55yL6YWN572u5paH5Lu26Lev5b6E"></span>
## View configuration file path

<span id=".5ZG95Luk5qC85byP"></span>
### Command syntax


<Tabs>
<Tab zoneid="Nd35KOpu" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

&nbsp;

```Bash
./tosutil config
```





</Tab>
<Tab zoneid="W8rnCOm8" title="Windows">
<TabTitle>Windows</TabTitle>

&nbsp;

```Bash
tosutil config
```





</Tab>
</Tabs>


<span id="2ZfaRvkX"></span>
### Parameters

None

<span id=".5L2_55So56S65L6L"></span>
### Example


* Command


```Plain
./tosutil config
```



* Output


```Plain
Config file url:
  /Users/user/.tosutilconfig
```


<span id=".5Lqk5LqS5byP5qih5byP5pu05paw6YWN572u5paH5Lu2"></span>
## Update configuration file in interactive mode

<span id=".5ZG95Luk5qC85byP"></span>
### Command syntax


<Tabs>
<Tab zoneid="XnGMlZuH" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

&nbsp;

```Bash
./tosutil config -interactive [-conf=xxx]
```





</Tab>
<Tab zoneid="pij7xxR1" title="Windows">
<TabTitle>Windows</TabTitle>

&nbsp;

```Bash
tosutil config -interactive [-conf=xxx]
```





</Tab>
</Tabs>


<span id=".5Y-C5pWw6K-05piO"></span>
### Parameters


|**Parameter** |**Type** |**Description** |
|---|---|---|
|\-interactive |Bool |Update configuration using interactive mode. |
|\-conf |String |Specify the path of the configuration file to update.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter can only specify the path of the configuration file to update; it will not create a configuration file at the specified path automatically.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only supports updating endpoint, region, AKSK, and STS token information.</div><br> |


<span id=".5L2_55So56S65L6L"></span>
### Example


* Command


```Plain
./tosutil config -interactive
```



* Output


```Plain
Please input your endpoint:
 
Please input your region:
cn-beijing
Please input your ak:
 
Please input your sk:
 
Please input your sts token:
 
Config file url:
  /Users/.tosutilconfig
 
Update config file successfully!
```


<span id=".55u05o6l5pu05paw6YWN572u5paH5Lu2"></span>
## Directly update configuration file

<span id=".5ZG95Luk5qC85byP"></span>
### Command syntax


<Tabs>
<Tab zoneid="e2txsPWw" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

&nbsp;

```Bash
./tosutil config [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
<Tab zoneid="Nr6WL0CX" title="Windows">
<TabTitle>Windows</TabTitle>

&nbsp;

```Bash
tosutil config [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
</Tabs>


<span id=".5Y-C5pWw6K-05piO"></span>
### Parameters


|**Parameter** |**Type** |**Description** |
|---|---|---|
|\-e |String |Specify the endpoint to update in the configuration file. |
|\-re |String |Specify the region to update in the configuration file. |
|\-i |String |Specify the Access Key ID to update in the configuration file. |
|\-k |String |Specify the Secret Access Key to update in the configuration file. |
|\-t |String |Specify the STS token to update in the configuration file. |
|\-conf |String |Specify the path of the configuration file to update.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter can only specify the path of the configuration file to be updated; it will not automatically create a configuration file at the specified path.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only updating endpoint, region, AKSK, and STS token information is supported.</div><br> |


<span id=".5L2_55So56S65L6L"></span>
### Example


* Command


```Plain
./tosutil config -re=cn-beijing
```



* Output


```Plain
Config file url:
  /Users/.tosutilconfig
 
Update config file successfully!
```
