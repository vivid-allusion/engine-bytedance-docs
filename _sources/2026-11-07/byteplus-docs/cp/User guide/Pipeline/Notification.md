---
title: "Notification"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Notification"
---

CP supports pushing pipeline messages via site message, SMS, email, webhook, and Feishu bot, helping you quickly understand build and deploy results. You can select notification events and notification methods according to actual needs. This article introduces how to configure pipeline notification.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Pipeline has been created. For specific operations, see [create pipeline](https://docs.byteplus.com/en/docs/cp/Create_pipelines).

* Channels for message notification have been configured.

   * Site message: BytePlus root user can receive site messages by default. IAM users need to contact the BytePlus root user to grant the [SiteMessageReadOnlyAccess](https://console.byteplus.com/iam/policymanage/System/SiteMessageReadOnlyAccess) policy to obtain permission to view site messages.

   * To receive message notifications via SMS, confirm that the notification account has configured a security phone. Go to [account management](https://console.byteplus.com/user/basics/) to view phone binding status.

   * To receive message notifications via email, confirm that the notification account has configured a security email. Go to [account management](https://console.byteplus.com/user/basics/) to view email binding status.

   * Webhook notification:

      * Feishu bot: You need to add the Feishu bot in advance and prepare the bot's hookurl address. For specific operations, refer to [Feishu developer guide](https://open.feishu.cn/document/ukTMukTMukTM/ucTM5YjL3ETO24yNxkjN).

      * General format: You need to prepare the hookurl address for receiving notifications in advance.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits

To avoid frequent message flooding, site message, SMS, and email have restrictions on message receiving frequency. For details, see [limit](https://docs.byteplus.com/en/docs/cp/Limit).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Go to the notification tab of the pipeline.

   1. Login to [CP console ](https://console.byteplus.com/cp).

   2. In the left navigation bar, select **workspace**.

   3. Click the target workspace name to enter the current workspace.

   4. In the left navigation bar, select **pipeline** to enter the pipeline page.

   5. In the pipeline list, select the target pipeline and click  **`...`**   **\> edit** to enter the process orchestration tab of the current pipeline.

   6. Click **notification** to switch to the notification tab.

2. Turn on the **notification** switch and configure notification events, notification methods, and notification content. Supports multiple selections, with **Start running** and **Site message** checked by default.

   * **Notification event**

      
      |Parameter |Description |
      |---|---|
      |Start running |When the pipeline starts running, a message notification will be pushed. |
      |Success |When the pipeline runs successfully, a message notification will be pushed. |
      |Run failure |When the pipeline fails to run, a message notification will be pushed. |
      |Run termination |When the pipeline is manually terminated, a message notification will be pushed. |
      

   * **Notification method**

      
      |Parameter |Description |
      |---|---|
      |Internal message |After you turn on this feature, messages will be pushed to BytePlus's **Message Center \> Operations message**. |
      |SMS |The message will be pushed to the specified user via SMS.<br><br>After enabling, the system will notify the pipeline runner by default. You can also add the pipeline creator or other accounts as recipients. For duplicate recipient accounts, the pipeline will only send the notification once. |
      |Email |The message will be pushed to the specified user via Email.<br><br>After enabling, the system will notify the pipeline runner by default. You can also add the pipeline creator or other accounts as recipients. For duplicate recipient accounts, the pipeline will only send the notification once. |
      |Webhook notification |The message will be pushed to the target URL via Webhook. Supports two methods: Larkbot and general format. Please select according to your needs.<br><br><br>* **Larkbot**: The message will be pushed to the Larkbot you added during preparation.<br><br>   * **Webhook address**: Enter the hook URL address of the Larkbot.<br><br>   * **Token**: Optional. Used in the request header to verify the validity of the push.<br><br>   * **Notification content**: Feishu bot supports custom notification content templates. Optional items include **Basic information, trigger user, trigger event, trigger time, trigger details, link address**. By default, all items are checked; at least one item must be checked.<br><br>* **General format**: The pipeline will push a POST request to the target URL. For details, see the POST request sample below.<br><br>   * **Webhook address**: Enter the hook URL address of the platform or tool that needs to receive the notification.<br><br>   * **Token**: Optional. Used in the request header to verify the legitimacy of the push. |
      

   * **Notification content**

      * Template: The notification content templates for site message, SMS, Email, and Larkbot are as follows.

      ```Plain Text
      //站内信/短信/邮件的通知内容
      
      基本信息：${流水线名称}-${运行ID}
      触发人：${触发人}
      触发事件：${触发事件}
      触发详情：${触发详情}
      链接地址：${链接地址}
      ${自定义内容}
      
      //飞书机器人的通知内容
      
      基本信息：${流水线名称}-${运行ID}
      触发人：${触发人}
      触发事件：${触发事件}
      触发详情：${触发详情}
      链接地址：${链接地址}
      自定义内容：${自定义内容}
      ```
      

      * Custom content: In addition to the system's built\-in notification content templates, you can enter custom notification content in the text box, with a limit of 200 characters.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Custom notification content can reference pipeline variables. For instructions on referencing, see <a href="https://docs.byteplus.com/en/docs/cp/Use_variables">Use variables</a>.      </div>
      

3. After the pipeline notification configuration is completed, click **Save** in the lower right corner to save the pipeline configuration.


<span id=".cG9zdC3or7fmsYLmoLfkvos="></span>
## POST request example

The notification content in the general Webhook format is a POST request. Detailed examples are as follows:

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">In the code, the <code>Status</code> field indicates the pipeline running state. For descriptions of each state, see <a href="https://docs.byteplus.com/en/docs/cp/Pipeline_status">Pipeline state</a>.</div>


```JSON
//Webhook notification sample at the pipeline level
{
  "ID": "6303544fa425e9b6b7fc****",  //Notification record ID
  "PipelineName": "Java项目-dev",  //Pipeline name
  "PipelineRunID": "6303544fa425e9b6b7fc****",  //Pipeline runtime record ID
  "URL": "https://console.byteplus.com/cp/workspace/****/pipeline/****/detail/record/****",  //Pipeline runtime record URL
  "TriggerBy": {
    "AccountId": 210013****,  //BytePlus root user ID
    "UserId": 107****,  //Runner ID
  },
  "Status": "Enqueued",  //Pipeline state
  "Message": " 2022-08-22 18:02:55 开始运行",  //Abnormal information
  "Resources": [
    {
      "Name": "gitee",  //Code source name
      "ID": "***",  //Code source ID
      "Type": "***"  //Code source type
      "Configuration": {
        "Git": {
            "Url":"xxx", //Code source URL
            "UserName":"xxx", //Username
            "Password":"xxx" //Password
        }
      }
    }
  ],
  "Params": [
    {
      "Key": "image",  //Current pipeline variable name
      "Value": "xxx",  //Variable value
      "Dynamic": true,  //Is dynamic variable when true
      "Secret": true  //Is privacy variable when true
    }
  ],
  "CustomContent": "" //Custom content
}
```
