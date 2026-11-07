---
title: "Create content template"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/content_templates"
---

The log service sends alarm notifications to specified notification channels according to the content defined in the content template. This document introduces the steps to create a content template.

<span id="f5ac1803"></span>
## Background information

The alarm notification content template is a predefined text template used to specify the content and format of alarm notifications. The content template supports adding variables, functions, text, and other elements. When sending alarm notifications, the log service automatically replaces variables in the notification content with their actual values. For a detailed list of content variables, please refer to [content variables](https://docs.byteplus.com/docs/tls/content_variables).

The log service provides a default content template (default\-template), which cannot be modified or deleted. You can create custom content templates based on the default template.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can define the complete alarm notification content directly in the content template and leave the <strong>notification content</strong> in the alarm policy empty. For alarm notifications triggered by <strong>alarm trigger</strong> type, you can also configure a general alarm notification structure in the content template and reference the <strong>notification content</strong> configured in the alarm policy through the variable <code>{{NotifyMsg}}</code>.</div>


<span id="a11ea690"></span>
## Procedure


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls).

2. On the top navigation bar, select the region where the log service is located.

3. In the left navigation bar, select **common functions** \> **log alarm** \> **notification management**.

4. Under the **content templates** tab, click **create content template**.

5. Fill in the content template configuration.

   1. Set the **template name**.

   2. Set content templates for each notification channel.

      * Email

         
         |Configuration |Description |
         |---|---|
         |Fixed content language |The fixed content language in alarm notifications can be either Chinese or English. |
         |Topic |Email subject. |
         |Send content |Alert notification content supports plain text format and allows insertion of content variables and content functions. For details, refer to [content variables](https://docs.byteplus.com/docs/tls/content_variables) and [content functions](https://docs.byteplus.com/docs/tls/content_functions).<br><br>You can also click **fill in default content** to use built\-in notification content. For specific content, refer to [email](https://docs.byteplus.com/docs/tls/content_templates#bcf3b252).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The notification content length after variable rendering is limited to 8 KB; it will be truncated if it exceeds this limit.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Leaving the <strong>body</strong> blank uses the default content.</div><br> |
         

      * Lark

         
         |configuration |Description |
         |---|---|
         |title |Subject of the alarm notification content. |
         |Send content |Alarm notification content supports Markdown format and allows insertion of content variables and content functions. For details, see [content variables](https://docs.byteplus.com/docs/tls/content_variables) and [content functions](https://docs.byteplus.com/docs/tls/content_functions).<br><br>You can also click **Fill with default content** to use the built\-in notification content. For content syntax supported by Lark, please refer to [Lark rich text](https://open.larkoffice.com/document/uAjLw4CM/ukzMukzMukzM/feishu-cards/card-components/content-components/rich-text). For Lark alarm template content, please refer to [Lark, DingTalk, WeCom](https://docs.byteplus.com/docs/tls/content_templates#204b8f67).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The notification content length after variable rendering is limited to 8 KB; content exceeding this limit will be truncated.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Leaving <strong>the body</strong> empty means using the default content.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Due to Lark’s restrictions, including plaintext phone numbers, plaintext email addresses, or other sensitive information in notification content may cause alarm notifications to fail to send via the Lark channel. For detailed explanation, please refer to <a href="https://open.larkoffice.com/search?from=header&page=1&pageSize=10&q=%E8%B0%83%E7%94%A8%E6%9C%8D%E5%8A%A1%E7%AB%AF%20API%20%E6%8A%A5%E9%94%99%EF%BC%9A230028&topicFilter=&type=history">Error 230028</a>.</div><br> |
         

      * DingTalk

         
         |Configuration |Description |
         |---|---|
         |Send content |Alarm notification content supports Markdown format and allows inserting content variables and functions. For detailed explanations, refer to [content variables](https://docs.byteplus.com/docs/tls/content_variables) and [content functions](https://docs.byteplus.com/docs/tls/content_functions).<br><br>You can also click **fill with default content** to use built\-in notification content. For specific content, refer to [Lark, DingTalk, WeCom](https://docs.byteplus.com/docs/tls/content_templates#204b8f67).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The maximum length of the notification content after variable rendering is 8 KB; content exceeding this limit will be truncated.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Leaving the <strong>main text</strong> blank means using the default content.</div><br> |
         

      * WeCom

         
         |Configuration |Description |
         |---|---|
         |Content to send |Alert notification content supports Markdown format and allows insertion of content variables and functions. For details, refer to [content variables](https://docs.byteplus.com/docs/tls/content_variables) and [content functions](https://docs.byteplus.com/docs/tls/content_functions).<br><br>You can also click **fill in default content** to use built\-in notification messages. Refer to [Lark, DingTalk, Enterprise WeChat](https://docs.byteplus.com/docs/tls/content_templates#204b8f67) for specific content.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The rendered notification content length after variable substitution is limited to 4 KB; exceeding this limit will cause truncation.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>The body</strong> is empty, which means the default content is used.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you set the <strong>alert method</strong> in the notification group to <strong>everyone</strong> or <strong>specified persons</strong>, notifications sent to Enterprise WeChat will be in plain text and do not support Markdown format.</div><br> |
         

      * Custom Webhook

         
         |Configuration |Description |
         |---|---|
         |send content |Alert notification content, usually in JSON format, supports inserting content variables and content functions. For details, please refer to [content variables](https://docs.byteplus.com/docs/tls/content_variables) and [content functions](https://docs.byteplus.com/docs/tls/content_functions).<br><br>You can also click **Fill with default content** to use the built\-in notification content. For details, please refer to [custom Webhook](https://docs.byteplus.com/docs/tls/content_templates#8af98848).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The notification content length after variable rendering is limited to 16 KB; content exceeding this limit will be truncated.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Leaving the <strong>body</strong> blank means using the default content.</div><br> |
         

6. Click **OK**.

   The system will automatically verify the content variables and syntax you configured. If an error message appears, modify the content according to the message.


<span id="2b1f0b64"></span>
## Default content

The log service provides default notification content, which you can customize based on the default.

<span id="bcf3b252"></span>
### Email

```Plain
Alarm Policy：{{Alarm}}<br> 
Alarm project：{{ProjectName}}<br> 
Alarm topic：{{AlarmTopicName}}<br> 
Alarm level：{{Severity}}<br>
First Trigger time：{{StartTime}}<br> 
Triggering conditions：{{Condition}}<br> 
notification type：{%if NotifyType==1%}trigger alarm{%else%}revover alarm{%endif%} <br> 
Alarm duration：{{Duration}}<br> 
Additional Notification content：{{NotifyMsg}}
```


<span id="204b8f67"></span>
### Lark, DingTalk, WeCom

```Plain
Dear users, Hello！\nYour account (Master Account ID：{{AccountID}} ）of log service{%if NotifyType==1%}trigger alarm{%else%}revover alarm{%endif%}\nAlarm Policy：{{Alarm}}\nAlarm topic：{{AlarmTopicName}}\nAlarm level：{{Severity}}\nFirst Trigger time：{{StartTime}}\nTriggering conditions：{{Condition}}\nCurrent query results：[{%-for x in TriggerParams-%}{{-x-}} {%-endfor-%}];\nAdditional Notification content：{{NotifyMsg|escapejs}}\n\nThanks for supporting Torch Log Service
```


<span id="8af98848"></span>
### Custom Webhook

```JSON
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


<span id="669657c4"></span>
## Custom content format

The log service supports custom notification content. The content format description is as follows:

<span id="3bf19c6e"></span>
### Email

The email channel supports HTML tags in notification content. For more information, see [HTML elements reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Element).


|Parameter |data format |
|---|---|
|Line break |```HTML```<br>``````<br>``````<br> |
|Add link |```HTML```<br>```<a href="https://example.com">Link</a>```<br> |
|Bold |```HTML```<br>```<strong>Bold</strong>```<br> |
|Italic |```HTML```<br>```<i>This can't be real!</i>```<br> |


<span id="421f7ea2"></span>
### Lark

Lark channel notification content supports Markdown syntax. The related element formats are shown in the table below. For more information, see [Lark rich text](https://open.larkoffice.com/document/uAjLw4CM/ukzMukzMukzM/feishu-cards/card-components/content-components/rich-text).


|Parameter |Data format |
|---|---|
|Line break |```Markdown```<br>```first line<br />second line```<br>```first line```<br>```second line```<br> |
|Italic |```Markdown```<br>```*Italic*```<br> |
|Bold |```Markdown```<br>```**bold**```<br>```or```<br>```__bold__```<br> |
|Strikethrough |```Markdown```<br>```~~Strikethrough~~```<br> |
|Hyperlink |```Markdown```<br>```<a href='https://open.Lark.cn'></a>```<br> |
|@everyone |```Markdown```<br>```<at id=all></at>```<br> |
|@mention |```Markdown```<br>```<at id=user_id></at>```<br><br><br>Refer to [how to mention a user](https://open.larkoffice.com/document/client-docs/bot-v3/add-custom-bot#272b1dee) for the method to get the specified person's `user_id` |
|Colored text style |```Markdown```<br>```<font color='green'>\n  this is green text\n</font>\n<font color='red'>\n  this is red text\n</font>\n<font color='grey'>\n  this is grey text\n</font>```<br> |
|Image |```Markdown```<br>```![hover_text](image_key)```<br> |
|Divider |```Markdown```<br>```\n ---\n```<br> |
|Ordered list |```Markdown```<br>```1. Ordered list 1\n    1. Ordered list 1.1\n2. Ordered list 2```<br> |
|unordered list |```Markdown```<br>```- Unordered list 1```<br>```    - Unordered list 1.1```<br>```- Unordered list 2```<br> |
|Tags |```Markdown```<br>```<text_tag color='red'>Label text</text_tag>```<br> |


<span id="4af06ab5"></span>
### DingTalk

DingTalk channel notification content supports Markdown syntax. The related element formats are shown in the table below. For more information, see [message types for custom robot message sending](https://open.dingtalk.com/document/orgapp/custom-bot-send-message-type#66407430cd5xr).


|Parameter |Data format |
|---|---|
|title |```Markdown```<br>```# Heading level 1\n## Heading level 2\n### Heading level 3\n#### Heading level 4\n##### Heading level 5\n###### Heading level 6```<br> |
|Quote |```Markdown```<br>```> A man who stands for nothing will fall for anything.```<br> |
|Bold and italic text |```Markdown```<br>```**bold**```<br>```*italic*```<br> |
|Link |```Markdown```<br>```[this is a link](http://name.com)```<br> |
|Image |```Markdown```<br>```![](http://name.com/pic.jpg)```<br><br><br>It is recommended not to exceed 20 images. |
|Unordered list |```Markdown```<br>```- item1```<br>```- item2```<br> |
|ordered list |```Markdown```<br>```1. item1```<br>```2. item2```<br> |


<span id="c4dc8698"></span>
### WeCom

WeCom channel notification content supports Markdown syntax. The related element formats are shown in the table below. For more information, see [WeCom notification content Markdown syntax](https://developer.work.weixin.qq.com/document/path/91770#markdown%E7%B1%BB%E5%9E%8B).


|Parameter |Data format |
|---|---|
|Title |```Markdown```<br>```# heading one\n## heading two\n### heading three\n#### heading four\n##### heading five\n###### heading six```<br> |
|bold |```Markdown```<br>```**bold**```<br> |
|Link |```Markdown```<br>```[This is a link](http://work.weixin.qq.com/api/doc)```<br> |
|Inline code segment |```Markdown```<br>````code````<br> |
|Quote |```Markdown```<br>```> Quoted text```<br> |
|Font color |```Markdown```<br>```<font color="info">green</font>```<br>```<font color="comment">gray</font>```<br>```<font color="warning">orange-red</font>```<br> |
