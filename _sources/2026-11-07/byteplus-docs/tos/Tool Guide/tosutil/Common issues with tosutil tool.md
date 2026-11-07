---
title: "Common issues with tosutil tool"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Tosutil-tool-faq"
---

This article introduces common issues encountered while using the tosutil tool.

<span id=".5ZyoLXdpbmRvd3MtMTAt57O757uf55qELWNtZC3lkb3ku6Tnqpflj6PmiafooYwtdG9zdXRpbC3lkb3ku6TvvIzljZXlh7vmiJbmu5rliqjpvKDmoIflkI7vvIzov5vluqbmnaHljaHpob_mgI7kuYjlip7vvJ8="></span>
## When executing tosutil commands in the CMD window on Windows 10, the progress bar freezes after clicking or scrolling the mouse. How to fix it?

This issue occurs because Windows 10 CMD window has **Quick Edit Mode** enabled by default. Clicking the mouse triggers Quick Edit Mode, causing standard output to freeze and the tosutil progress bar to stall.

It is recommended to disable Quick Edit Mode. Follow these steps:

Right\-click **Command Prompt** at the top left corner of the CMD window, click **Defaults**, then uncheck **Quick Edit Mode** in the **Edit Options** section and click **OK**.

<span id=".5ZyoLXdpbmRvd3Mt57O757uf5LiL5L2_55SoLXRvc3V0aWwt5bel5YW35LiL6L295paH5Lu25pe25paH5Lu25ZCN6LaF5Ye65pON5L2c57O757uf6ZmQ5Yi277yM5aaC5L2V6Kej5Yaz77yf"></span>
## How to resolve filename length limit issues when downloading files with tosutil on Windows?

Windows has a relatively small filename length limit. If the file extension is long, it may exceed the limit. To fix this, specify a temporary download directory as follows:


* Specify `defaultTempFileDir=xxx` in the configuration file.

* Use the `cp` command with the parameter `-tempFileDir=xxx`.


<span id=".dG9zdXRpbC3lt6XlhbfmiqXplJktc2VydmVyLXJldHVybmVkLWFuLWludmFsaWQtYm9keS3mgI7kuYjlip7vvJ8="></span>
## What to do if the tosutil tool reports "server returned an invalid body"?

The above error usually occurs because the TOS service domain name (Endpoint) is configured incorrectly. The TOS SDK currently only supports TOS protocol domain names (for example, the Beijing region domain is tos\-cn\-beijing.bytepluses.com.cn) and does not support S3 protocol domain names (for example, the Beijing region domain is  tos\-s3\-cn\-beijing.bytepluses.com.cn).

You need to configure the domain name to the TOS\-supported domain information. For information about TOS\-supported domains, please refer to [Region and Endpoint](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

<span id=".dG9zdXRpbC3lt6XlhbfkuIrkvKDmiJbkuIvovb3lpKfmlofku7bml7bvvIzlh7rnjrDov5vluqbmnaHlm57pgIDmiJblvZLpm7bnmoTmg4XlhrXmgI7kuYjlip7vvJ8="></span>
## What to do if the tosutil tool’s progress bar rolls back or resets to zero when uploading or downloading large files?

The above issue usually occurs due to slow or unstable client network, causing the tosutil tool to retry, which recalculates the progress during retries.

It is recommended to first troubleshoot network issues. If you temporarily cannot resolve the network problems, try specifying a smaller part size when running the command, such as setting `-ps=5mb`.

If the above steps do not resolve your issue, please [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001170) to contact technical support.

<span id=".dG9zdXRpbC3lt6XlhbfkuIrkvKDmiqXplJktdXNlLW9mLWNsb3NlZC1uZXR3b3JrLWNvbm5lY3Rpb24t5oCO5LmI5Yqe77yf"></span>
## What to do if the tosutil tool reports an upload error "use of closed network connection"?

This error usually happens because of unstable network between the client and TOS server or the client exceeding bandwidth limits (client bandwidth maxed out). You can try the following actions:


1. Troubleshoot network issues.

2. Adjust tosutil tool configurations and execution parameters by setting the `-p` and `-j` parameters to lower values; avoid setting concurrency too high. Example of configuration parameters:

   ```yaml
   # .tosutilconfig file
   
   # increase the retry count
   maxRetryCount=10
   # increase the timeout period
   socketTimeout=300
   ```
   


If the above steps do not resolve your issue, please [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001170) to contact technical support.

<span id="288f1d84"></span>
## How to update the key for the tosutil tool?

You need to initialize the tosutil tool to update the key. For details, see [Step One: Initialization](https://docs.byteplus.com/docs/tos/Quick-start#.5q2l6aqk5LiA77ya5Yid5aeL5YyW6YWN572u).

<span id="bedffd9b"></span>
## What to do if some files fail to upload when using the tosutil cp command?

We recommend checking the logs at `/root/.tosutil_log/tosutil.log` and using the failure information in the logs to identify and resolve the problem.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The default path for logs is <code>/root/.tosutil_log/tosutil.log</code>. The log path can be modified in the tosutil configuration file or retrieved from it.</div>


<span id="8aeb733b"></span>
## How to limit the size and number of tosutil log files?

You can specify the log file size and the number of log files in the tosutil configuration file through the `utilMaxLogSize` and `utilLogBackups` parameters. For detailed information, refer to the [configuration file instructions](https://docs.byteplus.com/docs/tos/profile-description).
