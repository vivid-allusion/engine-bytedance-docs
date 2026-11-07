---
title: "Data masking plug-in"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Data_masking_plug-in"
---

Data masking is a common method to protect sensitive data and can effectively prevent data leaks. When you collect logs using LogCollector, specify the fields that you want to mask for the desensitize plug\-in. This way, the plug\-in can replace sensitive log content with corresponding MD5 values.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">LogCollector V1.0.34 and later support this plug\-in. For more information on how to view the LogCollector version, refer to <a href="https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host#%E6%9F%A5%E7%9C%8B%E8%BD%AF%E4%BB%B6%E7%89%88%E6%9C%AC">View software version</a>.</div>


* <div data-tips="true" data-tips-type="tip">In scenarios in which you configure the desensitize plug\-in, we recommend that you disable <strong>Upload parsing failure log</strong> and <strong>Upload original log</strong> to protect your sensitive information.</div>



<span id="参数说明"></span>
## Parameter description


|Parameter |Type |Required |Description |
|---|---|---|---|
|field |String |Yes |Specify the name of the field that you want to mask.<br><br>Make sure the field names are unique. Do not leave this parameter empty or specify a period ( . ) for it. |
|type |String |Yes |Specify the method of masking sensitive log content. Valid values:<br><br><br>* md5: MD5 masking. It means that the plug\-in converts the log content to its corresponding MD5 value through data masking. |
|extract_type |String |Yes |Specify the method of extracting sensitive log content. Valid values:<br><br><br>* full: The entire log content of the original field is considered sensitive, and the plug\-in masks the content.<br><br>* regex: The log content that matches a specified regular expression within the original field is considered sensitive, and the plug\-in masks the content. |
|when |Object |No |Specify the condition for executing the plug\-in. The plug\-in is executed only when the specified condition is true. For more information, refer to [List of execution conditions](https://docs.byteplus.com/docs/tls/Set_plug-in_execution_conditions#%E6%89%A7%E8%A1%8C%E6%9D%A1%E4%BB%B6%E5%88%97%E8%A1%A8). |
|pattern |String |No |Specify the regular expression used to match sensitive log content. This parameter is required when you set extract_type to regex.<br><br>When multiple pieces of sensitive log content in the original field match the regular expression, the plug\-in mask them all. |
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
               "desensitize":[
                   {
                       "field":"alignment",
                       "type":"md5",
                       "extract_type":"full"
                   },
                   {
                       "field":"data",
                       "type":"md5",
                       "extract_type":"regex",
                       "pattern":"[a-h]+"
                   }
               ]
           }
       ]
   }
   ```
   

* Result

   ```Plain
   "data": "Cli4a8a08f09d37b73795649038408b5f33k He1671797c52e15f763380b45e841ec32re1671797c52e15f763380b45e841ec32"
   "size": "36"
   "style": "bold"
   "name": "text1"
   "hOffset": "250"
   "vOffset": "100"
   "alignment": "adb115059e28d960fa8badfac5516667"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   "time": "Today is 2023-06-08. Tomorrow is 2023-06-09."
   ```
