---
title: "How to set up Feishu, DingTalk, and WeCom alert notifications"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/How_to_set_up_Lark_DingTalk_and_WeChat_Work_alarm_notifications"
---

TLS supports sending alert notifications via Feishu messages, that is, by setting up alert notifications through the custom bot channel in Feishu groups. After an alert is successfully configured and triggered, TLS will send an alert notification message to the specified Feishu group via a bot.

<span id="80f70780"></span>
## Configure Feishu bot notifications


1. Add a custom bot to a Feishu group chat

   Create a custom bot in the Feishu group where TLS alert notifications need to be received. For information on how to create, please refer to the [Feishu official documentation](https://open.feishu.cn/document/ukTMukTMukTM/ucTM5YjL3ETO24yNxkjN?lang=zh-CN#d65d109d).

2. Get the group bot Webhook address.

   For information on how to obtain, refer to the [Feishu official documentation](https://open.feishu.cn/document/ukTMukTMukTM/ucTM5YjL3ETO24yNxkjN?lang=zh-CN#d3815c88).

3. Create an alert group in the [TLS console](https://console.byteplus.com/tls), and enter the **alert group name**, **notification type**, and **notification channel**.

   In this case, the receiving channel is set to **custom interface callback**, and the **custom interface callback configuration** is specified as well. For other parameter configuration methods, please refer to [Create Notification Group](https://docs.byteplus.com/docs/tls/create_alarm_notification_groups).

   
   |Configuration |Description |
   |---|---|
   |Request method |The request method of the callback interface. Here, you should set it to the **POST** method. |
   |Request address |You must enter the request URL for the callback interface using the webhook address obtained in Step 2, for example `https://open.feishu.cn/open-apis/bot/v2/hook/xxxxxxxxxxxxxxxxx`. |
   |Request headers |Request header fields configuration It is recommended to retain the `"content-type": "application/json"` field that is by default populated by TLS. You may also refer to the official Feishu documentation to add additional request header information. |
   |Content template |The specific content and format of the alert notification must comply with the callback interface requirements of the [Feishu Open Platform](https://open.feishu.cn/document/ukTMukTMukTM/ucTM5YjL3ETO24yNxkjN?lang=zh-CN#8b0f2a1b). TLS will send alert notifications according to the **content to be sent** defined in the content template.<br><br><br>* For information on configuring content templates, please refer to [Create a content template](https://docs.byteplus.com/docs/tls/content_templates).<br><br>   You can also directly use the default template provided by TLS. The default template is suitable for Feishu group bots.<br><br>* You can use the `at` tag to mention a specific person with @. For instructions on usage and how to obtain `user_id`, please refer to [How to mention a specific person with @](https://open.larkoffice.com/document/client-docs/bot-v3/add-custom-bot#272b1dee).<br><br>   ```Markdown```<br>```   <at id=user_id></at>```<br>```   ```<br>    |
   

   For example, to monitor website visits, configure the following content template:

   ```json
   {
     "msg_type": "interactive",
     "card": {
       "config": {
         "wide_screen_mode": true
       },
       "elements": [
         {
           "content": "Dear users, Hello！\nYour account (Master Account ID：{{AccountID}} ）of log service{%if NotifyType==1%}trigger alarm{%else%}revover alarm{%endif%}\nAlarm Policy：{{Alarm}}\nAlarm topic：{{AlarmTopicName}}\nFirst Trigger time：{{StartTime}}\nTriggering conditions：{{Condition}}\nCurrent query results：[{%-for x in TriggerParams-%}{{-x-}} {%-endfor-%}];\nAdditional Notification content：{{NotifyMsg|escapejs}}\n\nThanks for supporting Torch Log Service",
           "tag": "markdown"
         }
       ],
       "header": {
         "template": "{%if NotifyType==1%}red{%else%}green{%endif%}",
         "title": {
           "content": "【Torch Log Service】【Log Service】{%if NotifyType==1%}trigger alarm{%else%}revover alarm{%endif%}",
           "tag": "plain_text"
         }
       }
     }
   }
   ```
   

4. View alarm notifications.


<span id="bca90e08"></span>
## Configure WeCom notifications


1. Add a custom bot to a corporate WeChat group chat.

   Create a custom bot in the WeCom group that needs to receive TLS alert notifications. For information on creation methods, please refer to the [WeCom official documentation](https://open.work.weixin.qq.com/help2/pc/14931?person_id=1&searchData=#%E4%BA%8C%E3%80%81%E7%BE%A4%E6%9C%BA%E5%99%A8%E4%BA%BA%E6%B7%BB%E5%8A%A0%E5%85%A5%E5%8F%A3).

2. Obtain the webhook address for the group bot.

   For information on obtaining methods, please refer to the [WeCom official documentation](https://open.work.weixin.qq.com/help2/pc/14931?person_id=1&searchData=#%E4%BA%94%E3%80%81%E7%BE%A4%E6%9C%BA%E5%99%A8%E4%BA%BAWebhood%E5%9C%B0%E5%9D%80).

3. Create an alert group in the [TLS console](https://console.byteplus.com/tls), and enter the **alert group name**, **notification type**, and **notification channel**.

   In this context, within the notification channel, the receiving channel is set to use a custom interface callback, while also specifying the **custom interface callback configuration**. For other parameter configuration methods, please refer to [Create a notification group](https://docs.byteplus.com/docs/tls/create_alarm_notification_groups).

   
   |Configuration |Description |
   |---|---|
   |Request method |The request method of the callback interface. Here, you should set it to the **POST** method. |
   |Request address |The request URL for the callback interface must be set to the webhook address obtained in Step 2. For example, `https://qyapi.weixin.qq.com/cgi-bin/webhook/send?key=693a91f6-7xxx-4bc4-97a0-0ec2sifa5aaa` *.*  |
   |Request headers |Request header field configuration. It is recommended to retain the `"content-type": "application/json"` field that is automatically populated by TLS. You can also refer to the official WeCom documentation to add additional request header information. |
   |Request body |The specific content of the alert notification and its format must comply with the callback interface requirements of [WeCom](https://developer.work.weixin.qq.com/document/path/91770#%E6%B6%88%E6%81%AF%E7%B1%BB%E5%9E%8B%E5%8F%8A%E6%95%B0%E6%8D%AE%E6%A0%BC%E5%BC%8F). TLS will send alert notifications using the **message content** defined in the content template.<br><br>For information on how to configure content templates, please refer to [Create a content template](https://docs.byteplus.com/docs/tls/content_templates). |
   

   As an example of monitoring a website's access situation, configure the following content template:

   ```json
   {
       "msgtype": "text",
       "text": {
           "content": " Dear users, Hello！\nYour account (Master Account ID：{{AccountID}} ）of log service{%if NotifyType==1%}trigger alarm{%else%}revover alarm{%endif%}\nAlarm Policy：{{Alarm}}\nAlarm topic：{{AlarmTopicName}}\nAlarm level：{{Severity}}\nFirst Trigger time：{{StartTime}}\nTriggering conditions：{{Condition}}\nCurrent query results：[{%-for x in TriggerParams-%}{{-x-}} {%-endfor-%}];\nAdditional Notification content：{{NotifyMsg|escapejs}}\n\nThanks for supporting Torch Log Service"
       }
   }
   ```
   

4. View alert notifications.


<span id="3a53c121"></span>
## Configure DingTalk group bot notifications


1. Add a custom bot in a DingTalk group chat.

   Create a custom bot in the DingTalk group that needs to receive TLS alert notifications. Please refer to the [DingTalk official documentation](https://open.dingtalk.com/document/orgapp/custom-robot-access#title-jfe-yo9-jl2) for creation methods.

2. Obtain the webhook address for the group bot.

   For the method of obtaining, please refer to the [DingTalk official documentation](https://open.dingtalk.com/document/orgapp/custom-robot-access#title-jfe-yo9-jl2).

3. Create an alert group in the [TLS console](https://console.byteplus.com/tls), and fill in the **alert group name**, **notification type**, and **notification channel**.

   Among the notification channels, the receiving channel is set as a custom interface callback, while specifying the **custom interface callback configuration**. For other parameter configuration methods, please refer to the [Create notification group](https://docs.byteplus.com/docs/tls/create_alarm_notification_groups) section.

   
   |Configuration |Description |
   |---|---|
   |Request method |Request method of the callback interface. Here, it should be set to the **POST** method. |
   |Request address |The request address for the callback interface must be filled in with the webhook address obtained in Step 2, for example `https://oapi.dingtalk.com/robot/send?access_token=XXXXXX` *.*  |
   |Request headers |The request header field configuration. It is recommended to retain the default `"content-type": "application/json"` field pre\-filled by TLS. You may also refer to the [official documentation](https://open.dingtalk.com/document/orgapp/custom-robot-access#title-72m-8ag-pqw) of the DingTalk open platform to append additional request header information. |
   |Request body |The format of the alert notification must comply with the callback interface requirements of the [DingTalk Open Platform](https://open.dingtalk.com/document/orgapp/custom-robot-access#title-72m-8ag-pqw). TLS will send alert notifications according to the **content to be sent** defined in the content template.<br><br>For the method for configuring content templates, please refer to [Create a content template](https://docs.byteplus.com/docs/tls/content_templates). |
   

   Taking monitoring website visits as an example, configure the following content template:

   ```json
   {
       "msgtype": "text",
       "text": {
           "content": "Dear users, Hello！\nYour account (Master Account ID：{{AccountID}} ）of log service{%if NotifyType==1%}trigger alarm{%else%}revover alarm{%endif%}\nAlarm Policy：{{Alarm}}\nAlarm topic：{{AlarmTopicName}}\nAlarm level：{{Severity}}\nFirst Trigger time：{{StartTime}}\nTriggering conditions：{{Condition}}\nCurrent query results：[{%-for x in TriggerParams-%}{{-x-}} {%-endfor-%}];\nAdditional Notification content：{{NotifyMsg|escapejs}}\n\nThanks for supporting Torch Log Service"
       },
       "at": {
           "isAtAll": true
       }
   }
   ```
   

4. View alert notifications.
