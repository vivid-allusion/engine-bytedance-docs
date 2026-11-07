---
title: "Cluster log and event alerts"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Cluster_log_and_event_alerts"
---

VKE supports integrating logs and events from various resources in clusters with TLS. This achieves persistent storage of logs and events and enables alert notifications to be received through different channels. This topic provides an example on how to configure Feishu log alerts to help you promptly detect and respond to in\-cluster exceptions.

<span id="jhB7Us51"></span>
## Background

VKE clusters support log and event collection for multiple resources, such as Kubernetes native events, container logs and events, control plane add\-on logs, and cluster audit logs. By collecting and querying logs, you can understand the running status of basic resources, key add\-ons, and applications in clusters, and perform troubleshooting when failures occur. In addition, it supports persistently storing cluster Pod events in TLS. This helps you retain and trace critical events such as resource changes, abnormal scheduling, and add\-on restarts, achieving event visibility that logs cannot provide. For more details, see the following documentation:


* [Log overview](https://docs.byteplus.com/en/docs/vke/Log-overview?lang=en)

* [Configuring and viewing persistent events](https://docs.byteplus.com/en/docs/vke/Configuring-and-viewing-persistent-events?lang=en)


On this basis, you can use the log delivery and alerting features provided by TLS. When critical logs or exceptions meet the trigger conditions, the system automatically sends alert notifications. This helps you perceive cluster risks at the earliest opportunity and shorten failure response time.

<span id="a5tHzN0u"></span>
## Prerequisites


* The cluster logs have been integrated with TLS. For details, see [Log management](https://docs.byteplus.com/en/docs/vke/Log-management?lang=en) and [Auditing clusters](https://docs.byteplus.com/en/docs/vke/Cluster-auditing?lang=en).

* The cluster events have been integrated with TLS. For details, see [Configuring and viewing persistent events](https://docs.byteplus.com/en/docs/vke/Configuring-and-viewing-persistent-events?lang=en).


<span id="9Pdgrs0X"></span>
## Procedure

TLS supports various alert notification methods. This topic provides an example on how to configure Feishu log alerts for VKE clusters. For more configuration methods, see [Alert overview](https://docs.byteplus.com/en/docs/tls/alert_overview?lang=en).

<span id="cuALSUIY"></span>
### Step 1: Configure a Feishu bot

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Feishu alert bots may vary based on different organizations. This topic uses a <strong>custom bot</strong> as an example. If you do not know the alert bot name in your organization, contact your Feishu administrator.</div>



1. Use your Feishu account to log in to Feishu and create or find the group that needs to receive alerts. Click `...` in the upper‑right corner of the group and click **Settings** from the drop‑down menu.

2. In the pop\-up panel, click **Bots** and click **Add bot**.

3. In the bot list, click **Custom Bot** and click **Add**.

4. Configure the information about the bot.

   * Specify the name and description of the bot.

   * View and configure the information about the bot.

      * Copy the **Webhook URL** of the bot. This address will be used in subsequent configuration.

      * Select **Set signature verification** and copy the **Key**. This key will be used in subsequent configuration.

5. Click **Finish** to add the bot.


<span id="DkSInkm3"></span>
### Step 2: Configure Webhook integration


1. Log in to the [TLS console](https://console.byteplus.com/tls).

2. In the top navigation bar, select the target region.

3. In the left navigation pane, click **Log alarm** \> **Notification management**.

4. Click the **Webhook integration** tab. Click **Create webhook integration** to configure the integration for the Feishu bot. Where:

   * Select **Lark** from the **Type** drop\-down list.

   * Set the **Request address** parameter to the webhook URL of the Feishu bot.

   * Set the **Encryption key** parameter to the key of the Feishu bot.

5. Click **Create** to complete the configuration.


<span id="mP2uF6Wd"></span>
### Step 3: Create a notification group


1. In the left navigation pane, click **Log alarm** \> **Notification management**. Click **Create notification group** and configure the details of the group.

2. Click **Add channel** to configure the alert notification channel. Then select the Feishu bot webhook integration configuration that has been set up.

3. Click **Create notification group** to complete the configuration.


<span id="zAkR0KFy"></span>
### Step 4: Create an alert policy


1. In the left navigation pane, click **Log alarm** \> **Alarm policy**. Click **Create alarm policy** and configure the policy details.

   * Configure the basic information and select the project for cluster integration from the **Project** drop\-down list.

   * Configure the monitoring task. In the **Execute task** section, click **Edit**. In the pop\-up dialog box, configure the monitoring target and query statement. In this example, the query statement `cluster_id: "cda****"` is used to query events of a specific cluster.

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Description      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">For details about query statements, see <a href="https://docs.byteplus.com/en/docs/tls/Query-overview-2?lang=en">Query overview</a> and <a href="https://docs.byteplus.com/en/docs/tls/Analysis-overview?lang=en">Analysis overview</a>.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">You can also use the intelligent assistant to help generate query and search statements.      </div>
      

   * Configure alert notifications. Click **Associate notification group** to associate with the created notification group.

2. (Optional) Click **Test alarm policy** to debug the alerting feature.

   * If the test is successful, the message **The test was successful** will be displayed on the page. In addition, a test alert notification will be received through the specified alert channel.

   * If the alert trigger condition, custom API callback URL, or other alert configurations are invalid, the alert test feature will return corresponding error messages. You can troubleshoot based on the error messages and retry. For details, see [Common causes for test failures](https://docs.byteplus.com/en/docs/tls/alarm_tests?lang=en#.5rWL6K-V5aSx6LSl55qE5bi46KeB5Y6f5Zug).

3. Specify other parameters and then click **Create alarm policy** to complete the configuration.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For more information about the parameters of alert policies, see <a href="https://docs.byteplus.com/en/docs/tls/create_alarm_policies?lang=en">Creating alert policies</a>.   </div>
   

<span id="zZBI12vx"></span>
## Validate results


1. After you have completed alert\-related configuration, when an alert that matches the defined rules is triggered, a notification will be sent to Feishu through the specified Feishu bot. You will receive the alert notification details in the group.

2. In the left navigation pane of the TLS console, click **Log alarm** \> **Alarm History** to view the generated log alerts.


&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;
