---
title: "JSON parser"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/JSON_parser"
---

You can use the JSON parser plug\-in to expand the JSON structure and parse the fields in a JSON log entry. This topic describes the parameters that are used to configure the JSON parser and offers a sample configuration.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Each key in a JSON structured log entry must be unique.</div>


* <div data-tips="true" data-tips-type="tip">LogCollector v 1.0.12 and later support this plug\-in. For more information on how to view the LogCollector version, refer to <a href="https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host#%E6%9F%A5%E7%9C%8B%E8%BD%AF%E4%BB%B6%E7%89%88%E6%9C%AC">View software version</a>.</div>



<span id="参数说明"></span>
## Parameter description


|Parameter |Type |Required |Description |
|---|---|---|---|
|field |String |Yes |The name of the field that the LogCollector plug\-in processes. |
|when |Object |No |The conditions for triggering the plug\-in. The plug\-in is triggered only when the specified conditions evaluate to `true`. For more information, refer to [List of execution conditions](https://docs.byteplus.com/docs/tls/Set_plug-in_execution_conditions#%E6%89%A7%E8%A1%8C%E6%9D%A1%E4%BB%B6%E5%88%97%E8%A1%A8). |
|trim_keys.mode |string |No |`trim_keys` specifies whether to delete the strings at the two ends of the keys, and `mode` specifies the deletion method.<br><br><br>* none: retains the strings at the two ends of each key.<br><br>* all: deletes the strings at both ends of each key. This is the default value.<br><br>* left: deletes the string at the beginning of each key.<br><br>* right: deletes the string at the end of each key. |
|trim_keys.chars |string |No |`trim_keys` specifies whether to delete the strings at the two ends of the keys, and `chars` specifies the range of characters to delete. The default value is a double quotation mark ( " ). |
|trim_values.mode |String |No |`trim_values` specifies whether to delete the strings at the two ends of the values, and `mode` specifies the deletion method.<br><br><br>* none: retains the strings at the two ends of each key.<br><br>* all: deletes the strings at both ends of each value. This is the default value.<br><br>* left: deletes the string at the beginning of each value.<br><br>* right: deletes the string at the end of each value. |
|trim_values.chars |String |No |`trim_values` specifies whether to delete the strings at the two ends of the values, and `chars` specifies the range of characters to delete. The default value is a double quotation mark ( " ). |
|allow_empty_values |boolean |No |If the value of a field contains subfields with empty values after parsing, this parameter specifies whether to retain the key\-value pairs of such subfields.<br><br><br>* true: retains the key\-value pairs with empty values are retained.<br><br>* false: removes the key\-value pairs with empty values. This is the default value. |
|allow_overwrite_keys |boolean |No |If a key specified is duplicated with an existing key in the collection rule, this parameter specifies whether to overwrite the existing key.<br><br><br>* true: overwrites the existing key<br><br>* false: returns an error. If keys are duplicated, the LogCollector plug\-in fails to parse the log. This is the default value. |


<span id="配置示例"></span>
## Configuration examples


* Logs

   ```Plain
   "json_key": "{\"data\":\"Click Here\",\"size\":36,\"style\":\"bold\",\"name\":\"text1\",\"hOffset\":250,\"vOffset\":100,\"alignment\":\"#center#\",\"#onMouseUp#\":\"sun1.opacity = (sun1.opacity / 100) * 90;\"}"
   ```
   

* LogCollector plug\-in configuration

   ```json
   {
       "processors":[
           {
               "json":{
                   "field":"json_key",
                   "trim_keys":{
                       "mode":"all",
                       "chars":"#"
                   },
                   "trim_values":{
                       "mode":"all",
                       "chars":"#"
                   },
                   "allow_overwrite_keys":true,
                   "allow_empty_values":true
               }
           }
       ]
   }
   ```
   

* Result

   ```Plain
   "data": "Click Here"
   "size": "36"
   "style": "bold"
   "name": "text1"
   "hOffset": "250"
   "vOffset": "100"
   "alignment": "center"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   ```
