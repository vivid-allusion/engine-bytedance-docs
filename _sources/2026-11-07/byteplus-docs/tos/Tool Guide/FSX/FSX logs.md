---
title: "FSX logs"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/FSX_logs"
---

This topic explains how to use logs to troubleshoot issues that arise while using FSX.

<span id="la5ilrqy"></span>
### Where to find the logs

By default, log files are stored in the `/var/log/fsx` directory.


* To view FSX client logs, navigate to `/var/log/fsx/fusedaemon/tos/fusedaemon`.

* To view TOS server interaction logs, navigate to `/var/log/fsx/fusedaemon/tos/tos-fuse`.


For deeper diagnostics and troubleshooting, you may need to set the log level to debug. Use the following commands to do so:


* Set the log level of FSX client logs to debug:


```Plain Text
cd /opt/fsx/bin && ./fusetool flags set --instance tos --flag v --value 20 --force
```



* Set the log level of TOS server interaction logs to debug:


```Plain Text
cd /opt/fsx/bin &&  ./fusetool flags set --instance tos --flag tosfuse_log_level --value 1  --force
```


<span id="sXk9HhXZ"></span>
### Log collection

If you encounter any issues while using FSX, we recommend first running the `/opt/fsx/tools/sysinfo_collector.sh` script. This script automatically collects system information, mount point details, system logs, and other relevant data. Then, it generates a compressed file named `system_info__.tar.gz` in the script's directory. [Submit this file via a ticket](https://console.byteplus.com/workorder/create?step=1&SubProductID=P00001170), and our team will help resolve the issue.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Do not run the <code>/opt/fsx/tools/</code><code>sysinfo_collector.sh</code> script in the <strong>mount directory</strong>. The script may fail to execute when run from a mount point that is in an abnormal state.</div>
