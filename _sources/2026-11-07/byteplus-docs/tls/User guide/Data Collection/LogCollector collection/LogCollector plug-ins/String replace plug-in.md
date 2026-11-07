---
title: "String replace plug-in"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/String_replace_plug-in"
---

When you collect logs through LogCollector, you can use the replace plug\-in to replace the strings in specified fields. Regular expression matching and content matching methods are supported.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">LogCollector V1.0.34 and later support this plug\-in. For more information on how to view the LogCollector version, refer to <a href="https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host#%E6%9F%A5%E7%9C%8B%E8%BD%AF%E4%BB%B6%E7%89%88%E6%9C%AC">View software version</a>.</div>


* <div data-tips="true" data-tips-type="tip">You can also use the replace plug\-in for data masking. It means that you can use this plug\-in to replace the sensitive characters in specified fields with other strings. For example, you can replace the middle four digits of a phone number with \*\*\*\*. In such scenarios, we recommend that you disable <strong>Upload parsing failure log</strong> and <strong>Upload original log</strong> to protect your sensitive information.</div>



<span id="参数说明"></span>
## Parameter description


|Parameter |Type |Required |Description |
|---|---|---|---|
|field |String |Yes |Specify the names of the fields for which you want to replace the content.<br><br>Do not specify periods ( . ), empty values, or duplicate values for this parameter. |
|type |String |Yes |Specify the method of replacing log content. Valid values:<br><br><br>* string: string\-based replacement.<br><br>* regex: regular expression\-based replacement. |
|pattern |String |Yes |Specify the mode for matching log content. When one or more partsin the original fields match the value of pattern, the plug\-in replaces all the parts with the value specified for replacement.<br><br><br>* If type is set to string, specify a string of log content for pattern.<br><br>* If type is set to regex, specify a regular expression used to match log content for pattern. You can set capturing groups for your regular expressions. |
|replacement |String |Yes |Specify the string used to replace the specified log content.<br><br>To use capturing groups in regular expressions, make sure the value of replacement includes placeholders in `$n` format to reference the captured content. Note that n is the number of a capturing group in regular expressions and the starting number is 1. Count the number from the left side to the right side. |
|when |Object |No |Specify the condition for executing the plug\-in. The plug\-in is executed only when the specified condition is true. For more information, refer to [List of execution conditions](https://docs.byteplus.com/docs/tls/Set_plug-in_execution_conditions#%E6%89%A7%E8%A1%8C%E6%9D%A1%E4%BB%B6%E5%88%97%E8%A1%A8). |
|ignore_missing |Boolean |No |Specify whether to ignore a field that does not exist.<br><br><br>* true: When the field does not exist, the plug\-in ignores it. This value is the default value.<br><br>* false: When the field does not exist, the plug\-in reports an error. |


<span id="配置示例"></span>
## Configuration examples


* Key\-value pair logs processed through a collection mode or other processor plug\-ins:

   ```Plain
   "data": "Click Here"
   "size": "36"
   "style": "bold"
   "name": "text1"
   "hOffset": "250"
   "vOffset": "100"
   "alignment": "center"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   "time": "Today is 2023-06-08. Tomorrow is 2023-06-09."
   ```
   

* Configuration for the LogCollector plug\-in processor:

   ```json
   {
       "processors":[
           {
               "replace":[
                   {
                       "field":"alignment",
                       "type":"string",
                       "pattern":"en",
                       "replacement":"xx"
                   },
                   {
                       "field":"data",
                       "type":"regex",
                       "pattern":"[a-h]+",
                       "replacement":"xx"
                   },
                   {
                       "field":"time",
                       "type":"regex",
                       "pattern":"(\\d{4})-(\\d{2})-(\\d{2})",
                       "replacement":"$2/$3/$1"
                   }
               ]
           }
       ]
   }
   ```
   

* Processing result:

   ```Plain
   "data": "Clixxk Hxxrxx"
   "size": "36"
   "style": "bold"
   "name": "text1"
   "hOffset": "250"
   "vOffset": "100"
   "alignment": "cxxter"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   "time": "Today is 06/08/2023. Tomorrow is 06/09/2023."
   ```
