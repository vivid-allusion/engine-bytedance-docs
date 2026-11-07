---
title: "Frequently asked questions about alarm notification content"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Alarm_notification_content_FAQs"
---

<span id="7721beeb"></span>
## If the alarm notification content contains special characters, how should they be handled?

If special characters in the alert notification content cause the alert notification to fail, you can add the filter `{{variable|escapejs}}` to its variable. TLS converts special characters in specified strings or specified variables into Unicode\-encoded strings based on this configuration. For a detailed explanation, see [Filter](https://docs.byteplus.com/docs/tls/content_variables#244b43bd).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After Feishu, DingTalk, or WeCom receive an alert notification, they will convert Unicode\-encoded strings back into special characters.</div>


For example, if you set the following notification content containing special characters in an alarm policy and reference this content in the content template (with the variable name `{{NotifyMsg}}`), you can use the following variables and filters to perform Unicode encoding on the special characters.


* Notification content in the alarm policy

   ```SQL
   {
    "projectname":"test1",
    "description":"test",
    "region": "cn-north-1"
   }
   ```
   

* Configuration of variables in content templates

   ```SQL
   Original notification content: {{NotifyMsg|escapejs}}
   ```
   


<span id="d6cb1e4a"></span>
## How can you prevent alert notification content from being truncated?

All alert notification channels have a limit on the length of notification content. If the length of the rendered notification content exceeds this limit, the excess portion will be truncated. For information about notification content length limits, please refer to [Create Content Template](https://docs.byteplus.com/docs/tls/content_templates).

You can use the for loop statement to iterate over arrays and objects to prevent notification content from being truncated. Example:

```JSON
{%-for logs in QueryLog%}
{%- for log in logs%}
{{log.msg}}
{%endfor-%}
{%endfor-%}
```


<span id="0651b758"></span>
## How to reference the content that triggered the alert in the alert notifications?

You can add the variable `{{FireResults}}` or `{{Results}}` to the alert notification content template to include the detailed content that triggered the alert in the notification. For detailed information about alarm variables, please refer to [content variables](https://docs.byteplus.com/docs/tls/content_variables). Example as follows:


* Query and analysis results

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_14469674ecd4c548441c09fc298bc6ba.png) </span>

* `{{FireResults}}` Variable example:

   * Content template

      ```JSON
      The data that triggers the alarm is {{toJson(FireResults)|escapejs}}
      ```
      

   * Alert notification

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_94ab96b0e953af3b208dbc520126095c.png) </span>

* `{{Results}}` Variable example

   * Content template

      ```JSON
      {{toJson(Results[0].RawResults)|escapejs}}
      ```
      

   * Alert notification

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1160e7552d9b1795f45a2f4b53b3a595.png) </span>


<span id="1a74832f"></span>
## How can notification content be formatted, calculated, or otherwise processed?

TLS provides a wide range of [content syntax](https://docs.byteplus.com/docs/tls/content_syntax) and [content functions](https://docs.byteplus.com/docs/tls/content_functions) for processing alert notification content. You can use content functions and content syntax to format and custom design data, text, variables, and other content.
