---
title: "Command format"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Command-format"
---

This article introduces the basic format and common basic parameters of the commands supported by the tosutil tool.

<span id=".5Z-65pys5qC85byP"></span>
##  Basic format


* windows system

   ```Plain
   tosutil [command] [args...] [options...]
   ```
   

* macOS/linux system

   ```Plain
   ./tosutil [command] [args...] [options...]
   ```
   



|Parameter |Description |
|---|---|
|[command] |The **command** to run, such as `ls`, `cp`, `rm`, etc. |
|[args...] |The **basic parameters** for running the command, usually mandatory, may include multiple parameters separated by spaces. |
|[options...] |Optional **parameters** for running the command. When multiple parameters exist, use`-`as the parameter name start and use`=`Separate as a parameter value, for example `-limit=100`.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When the optional parameter is a boolean type, it supports only starting with<code>-</code>(without<code>=</code>), indicating the value is <strong>true</strong>.</div><br> |


<span id=".5bi46KeB5Z-65pys5Y-C5pWw"></span>
##  Common basic parameters


|parameter |description |
|---|---|
|cloud_url |path on TOS, formatted as `tos://bucket/[prefix]`, where `prefix` is optional and represents the object name or prefix. |
|file_url |Represents the local file path. |
|folder_url |Represents the local folder path. |


<span id=".6YCa55So5Y-v6YCJ5Y-C5pWw"></span>
## Universal optional parameters

Except for some special auxiliary commands, all commands can include optional parameters. The optional parameters are explained as follows.


|parameter |Description |
|---|---|
|\-e |endpoint of the TOS server used to execute this command. |
|\-re |region of the TOS server used to execute this command.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">for supported endpoint and region information of TOS, see <a href="https://docs.byteplus.com/docs/tos/docs-region-and-endpoint">Region and Endpoint</a>.</div><br> |
|\-i |Represents the Access Key ID used to execute this command.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When accessing TOS anonymously, you do not need to specify the Access Key ID; set the parameter to <code>-i=</code>.</div><br> |
|\-k |represents the Secret Access Key used to execute this command.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When accessing TOS anonymously, you do not need to specify the Secret Access Key; set the parameter to <code>-k=</code>.</div><br> |
|\-t |Represents the Security Token used to execute this command; required when using temporary AccessKey.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When accessing TOS anonymously, you do not need to specify the Security Token; set the parameter to <code>-t=</code>.</div><br> |
|\-conf |Represents the configuration file path used to execute this command. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When your command sets both the <code>-conf</code> and <code>-e/-re/-i/-k/-t</code> parameters, the <code>-conf</code> parameter remains valid. However, Access key, Secret key, and other parameters in the configuration file at this path do not take effect; the <code>-e/-re/-i/-k/-t</code> parameters specified when running the command take priority.</div>
