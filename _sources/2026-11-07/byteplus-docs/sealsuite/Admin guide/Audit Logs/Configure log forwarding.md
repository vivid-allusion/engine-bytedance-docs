---
title: "Configure log forwarding"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configure-log-forwarding"
---

Log forwarding sends business logs recorded by SealSuite to an enterprise\-owned Syslog server or Elasticsearch cluster. This helps with centralized analysis and long\-term retention. You can enable forwarding separately for each log type and configure multiple protocols at the same time. When forwarding is enabled for the first time, only newly generated logs are sent. Historical logs generated before forwarding was enabled are not sent.

Syslog is a protocol used by computer systems to send event log data to a central location for storage. SealSuite sends Syslog data in the format defined by RFC 5424.

<span id=".5YeG5aSH5bel5L2c"></span>
## Prepare for configuration

Before you begin, make sure you have an available Syslog server that supports TCP, UDP, or TCP + TLS, or an Elasticsearch cluster with an index created and an account that has write permissions. The following network requirements must also be met:

**SaaS edition**


* **Connectivity**: Your Syslog server or Elasticsearch cluster must have a public IP address, or it must be connected to the SealSuite cloud through a dedicated line.

* **Firewall policy**: Allow inbound traffic from SealSuite cloud servers on your enterprise firewall. The destination port depends on the configuration below.


**Private deployment edition**

Private deployment environments are usually deployed on an enterprise intranet. For forwarding configurations, focus on **routing connectivity** between internal nodes.


* **Connectivity**: Make sure the SealSuite backend management server can reach your Syslog or Elasticsearch server over the network.

* **Port allowlisting**: Allow the corresponding protocol ports on the intranet firewall.


<span id=".5bCG5pel5b-X5aSW5Y-R5YiwLXN5c2xvZw=="></span>
## Forward logs to Syslog


1. Log in to the Admin Console.

2. In the left navigation pane, choose **Audit Logs**.

3. In the upper\-right corner of the **Audit Logs** page, click **Export Logs**.

   <span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/log-audit-en-20260922/ztna-connect-wide-en.png) </span>

4. In the scenario list on the **Export Logs** page, search for the log type to forward and enable the switch.

5. In the upper\-right corner of the page, click **Edit** to configure protocol parameters.

   <span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/log-audit-en-20260922/ztna-export-wide-en.png) </span>

6. Enable the Syslog switch and configure the following parameters.

&nbsp;

   
   |**Parameter** |**Description** |
   |---|---|
   |**Protocol** |Under **Protocol**, select **TCP**, **UDP**, or **TCP + TLS**. |
   |**Address** |Enter the IP address and listening port of the server where the Syslog program is deployed. Use the `IP:port` format, such as `192.168.1.50:514` or `log.example.com:6514`. |
   

7. After confirming that the parameters are correct, click **Save** in the upper\-right corner of the page to apply the configuration.


<span id=".5bCG5pel5b-X5aSW5Y-R5YiwLWVsYXN0aWNzZWFyY2g="></span>
## Forward logs to Elasticsearch


1. Log in to the Admin Console.

2. In the left navigation pane, choose **Audit Logs**.

3. In the upper\-right corner of the **Audit Logs** page, click **Export Logs**.

   <span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/log-audit-en-20260922/ztna-connect-wide-en.png) </span>

4. In the scenario list on the **Export Logs** page, search for the log type to forward and enable the switch.

5. In the upper\-right corner of the page, click **Edit** to configure protocol parameters.

6. Enable the Elasticsearch switch and configure the following parameters.

   <span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/log-audit-en-20260922/ztna-export-es-en.png) </span>

&nbsp;

   
   |**Parameter** |**Description** |
   |---|---|
   |**Server address** |Enter the full URL of the Elasticsearch service. Make sure to include the URL scheme (`http` or `https`) and port number, such as `http://192.168.1.100:9200` or `https://es.example.com:9200`. |
   |**Index name** |Enter the Index Name used to store logs. Lowercase letters and underscores are recommended. Example: `feilian_device_logs` |
   |**Username/password** |Enter the username and password of an account that has write permissions on the index. |
   

7. After confirming that the parameters are correct, click **Save** in the upper\-right corner of the page to apply the configuration.


<span id=".6aqM6K-B5o6l5pS257uT5p6c"></span>
## Verify receiving results

After configuration is complete, trigger a behavior event to generate a new log of the selected type. Then check whether the corresponding record is received on the receiving end.

For example, to verify ZTNA connection logs, connect and disconnect the proxy, then check x_key, employee, device, connection time, and operation type. To verify Administrator operation logs, create a new configuration change and check admin_audit_log.

<span id=".6Zeu6aKY5o6S5p-l"></span>
## Troubleshoot issues

If no logs are received, first confirm that the forwarding switch is enabled and the configuration is saved. Then check the receiving address, listening port, firewall, and network connectivity. For Elasticsearch, also check the index name, account permissions, and errors returned by the service. During verification, generate new logs instead of checking only historical records created before the first configuration.

<span id="faq"></span>
## FAQ

<span id=".5pel5b-X5aSW5Y-R5piv5a6e5pe25aSW5Y-R5ZCX"></span>
### Is log forwarding real\-time?

Under normal conditions, logs are forwarded within **1 minute** after they are generated. If a forwarding task is stopped by user action or interrupted by a network exception, forwarding resumes from the last successfully forwarded log. When forwarding is configured for the first time, only newly generated logs are sent. Historical logs are not sent.

<span id=".572R57uc5byC5bi45pe25pel5b-X5aSW5Y-R5Lya6YeN6K-V5ZCX"></span>
### Does log forwarding retry after a network exception?

Retry behavior depends on the forwarding protocol:


* **Elasticsearch**: If the service returns a parameter error, the log is discarded and is not retried. If a network error occurs, SealSuite keeps retrying. No retry limit is currently set.

* **Syslog (UDP)** : UDP cannot guarantee message delivery. Each log is sent only once and is not retried.
