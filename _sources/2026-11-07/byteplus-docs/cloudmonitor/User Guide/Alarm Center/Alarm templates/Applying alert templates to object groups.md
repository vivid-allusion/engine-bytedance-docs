---
title: "Applying alert templates to object groups"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Applying-an-alarm-template-to-a-resource-group"
---

You need to apply an alert template to cloud service resources in a object group. In this way, the Cloud Monitor console will automatically generate the corresponding alert policy.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An object group has been created. For details, see [Creating object groups](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-a-resource-group).

* Contacts and contact groups are created. For more details, refer to [Creating contacts and contact groups](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-contact-and-an-alarm-contact-group).

* A callback URL is created. For more details, see [Creating callback URLs](https://docs.byteplus.com/en/docs/cloudmonitor/Managing-callback-address#414fd7c7).


<span id="B5PmbFob"></span>
## Limits


* Each alert template can be bound to at most 100 object groups.

* Each object group can be bound to up to 20 alert templates.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, click **Alert Center** \> **Alert Template**.

3. Find the target alert template in the alert template list, and click **Apply to group** in the **Actions** column.

4. In the **Apply alert template to object group** dialog box, click **Add object group**.

5. Expand the object group, select the created object group, and configure the notification settings.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dbd4be0435e1534b71c9314d49fea522.png) </span>

   
   |Parameter |Descriptions |
   |---|---|
   |Object Group |Select a created object group.<br><br><br>* If the resource type specified in the alert template is the same as that in the object group, Cloud Monitor will generate a corresponding alert policy based on the resource type and dimension. The generated alert policy will be named {alert rule name}&{object group name}.<br><br>   For example, if the alert rule is named **rule** and the object group is named **group**, the generated alert policy will be named **rule&group**.<br><br>* You cannot edit and delete the alert policy generated through the alert template. |
   |Notification method |Select an alert notification channel.  <br><br><br>* **Manual selection:**  Manually configure a notification method of the alert policy.<br><br>* **Notification policy**: Specify a configured notification policy. For more details, refer to [Creating notification policies](https://docs.byteplus.com/en/docs/cloudmonitor/Create_a_notification_policy). |
   |Alert channel |* If you select one or more of the following options for **Alert channel**: **Email**, **Phone**, or **SMS**, the **Alert contact group** parameter will be displayed on the page.<br><br>   * At least one contact group must be specified as the recipient of alert notifications.<br><br>   * At most five contact groups can be specified as the recipients of alert notifications.<br><br>* If you set the **Alert channel** parameter to **Alert callback**, the **Alert callback** text box will be displayed on the page.<br><br>   * You can select created webhook URLs. Up to eight webhook URLs can be selected.<br><br>   * You can enter only one webhook URL.<br><br>   * For more information about alert webhook URLs, refer to [Alert webhook usage](https://docs.byteplus.com/en/docs/cloudmonitor/Webhook-instructions).<br><br>   * Alert webhooks can be associated with robots in Feishu, DingTalk, and WeCom groups to automatically push alert notifications. For specific operations, refer to [Receiving alert notifications by Feishu group](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-Feishu-groups), [Receiving alert notifications by DingTalk group](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-DingTalk-groups), and [Receiving alert notifications by WeChat group](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-WeChat-groups).<br><br>* If you set the **Alert channel** parameter to **Orchestration**, the **Orchestration plan** will be displayed on the page, and you can select an existing orchestration plan. |
   |Effective time |Configure the active ​time for alerting. |
   |Project |Select the project to which the object group belongs. The default project is used by default. |
   

6. Click **Submit** to complete the configuration.


<span id="xgd8qLWu"></span>
## Verifying results

After the configuration is complete, you can view the associations between alert templates, object groups, and alert policies in the alert template list.

Click the name of the alert template to enter the alert template details page, where you can view details about the alert template. The details include the basic information, associations, cloud product, and alert policy.
