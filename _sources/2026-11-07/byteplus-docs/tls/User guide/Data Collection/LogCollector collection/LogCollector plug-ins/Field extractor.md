---
title: "Field extractor"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Field_extractor"
---

This topic describes how to use the field extraction plug\-ins of LogCollector.

<span id="delimiter-插件"></span>
## delimiter plug\-in

You can use the delimiter plug\-in to specify that LogCollector extracts log fields in delimiter\-based mode.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">LogCollector V1.0.12 and later support this plug\-in. For more information on how to view the LogCollector version, refer to <a href="https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host#%E6%9F%A5%E7%9C%8B%E8%BD%AF%E4%BB%B6%E7%89%88%E6%9C%AC">View software version</a>.</div>


<span id="参数说明"></span>
### Parameter description


|Parameter |Type |Required |Description |
|---|---|---|---|
|field |String |Yes |Specify the name of the field to be processed by the LogCollector plug\-in.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You cannot set a delimiter to an invisible character.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can specify one delimiter, and the delimiter can contain multiple characters.</div><br> |
|quote |String |No |Specify the quote. The content enclosed in a quote is parsed into a complete field without being separated by a delimiter.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You cannot set this parameter to an invisible character.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can specify one quote, and the quote can contain multiple characters.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">LogCollector V1.0.34 and later allow you to set a quote.</div><br> |
|keys |Array of String |Yes |Specify the keys of the subfields parsed from the specified field. Make sure the order of keys matches that of the subfields and the number of keys is the same as that of subfields. Otherwise, the system fails to execute the LogCollector plug\-in configuration.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The values of key cannot be empty or duplicate.</div><br> |
|when |Object |No |Specify the condition for executing the plug\-in. The plug\-in is executed only when the specified condition is true. For more information, refer to [List of execution conditions](https://docs.byteplus.com/docs/tls/Set_plug-in_execution_conditions#%E6%89%A7%E8%A1%8C%E6%9D%A1%E4%BB%B6%E5%88%97%E8%A1%A8). |
|trim_values.mode |String |No |`trim_values` specifies whether to delete the strings at the two ends of the values, and `mode` specifies the deletion method.<br><br><br>* none: retains the strings at the two ends of each key.<br><br>* all: deletes the strings at both ends of each value. This is the default value.<br><br>* left: deletes the string at the beginning of each value.<br><br>* right: deletes the string at the end of each value. |
|trim_values.chars |String |No |`trim_values` specifies whether to delete the strings at the two ends of the values, and `chars` specifies the range of characters to delete. The default value is a double quotation mark ( " ). |
|allow_empty_values |Boolean |No |Specify whether to retain a key\-value pair in which the subfield value parsed from the specified field is empty.<br><br><br>* true: retains the key\-value pairs with empty values are retained.<br><br>* false: removes the key\-value pairs with empty values. This is the default value. |
|allow_overwrite_keys |Boolean |No |If a key specified is duplicated with an existing key in the collection rule, this parameter specifies whether to overwrite the existing key.<br><br><br>* true: overwrites the existing key<br><br>* false: returns an error. If keys are duplicated, the LogCollector plug\-in fails to parse the log. This is the default value. |


<span id="配置示例"></span>
### Configuration examples


* Log:

   ```Plain
   "delimiter_key": "\"Click&&Here\"&&36&&bold&&text1&&250&&100&&#center#&&sun1.opacity = (sun1.opacity / 100) * 90;"
   ```
   

* LogCollector plug\-in configuration for data processing

   ```json
   {
       "processors":[
           {
               "delimiter": {
                   "field": "delimiter_key",
                   "delimiter": "&&",
                   "quote": "\"",
                   "keys": [
                       "data",
                       "size",
                       "style",
                       "name",
                       "hOffset",
                       "vOffset",
                       "alignment",
                       "onMouseUp"
                   ],
                   "trim_values": {
                       "mode": "all",
                       "chars": "#"
                   },
                   "allow_overwrite_keys": true,
                   "allow_empty_values": true
               }
           }
       ]
   }
   ```
   

* Result

   ```json
   "data": "\"Click&&Here\""
   "size": "36"
   "style": "bold"
   "name": "text1"
   "hOffset": "250"
   "vOffset": "100"
   "alignment": "center"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   ```
   


<span id="fullregex-插件"></span>
## fullregex plug\-in

You can use the fullregex plug\-in to specify that LogCollector extracts log fields in full regex\-based mode.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">LogCollector V1.0.12 and later support this plug\-in. For more information on how to view the LogCollector version, refer to <a href="https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host#%E6%9F%A5%E7%9C%8B%E8%BD%AF%E4%BB%B6%E7%89%88%E6%9C%AC">View software version</a>.</div>


<span id="参数说明"></span>
### Parameter description


|Parameter |Type |Required |Description |
|---|---|---|---|
|field |String |Yes |Specify the name of the field to be processed by the LogCollector plug\-in. |
|pattern |String |Yes |Specify the regular expression. A capturing group corresponds to a parsed value. |
|keys |Array of String |Yes |Specify the keys of the subfields parsed from the specified field. Make sure the order of keys matches that of the subfields.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The values of key cannot be empty or duplicate.</div><br> |
|when |Object |No |The conditions for triggering the plug\-in. The plug\-in is triggered only when the specified conditions evaluate to `true`. For more information, refer to [List of execution conditions](https://docs.byteplus.com/docs/tls/Set_plug-in_execution_conditions#%E6%89%A7%E8%A1%8C%E6%9D%A1%E4%BB%B6%E5%88%97%E8%A1%A8). |
|trim_values.mode |String |No |`trim_values` specifies whether to delete the strings at the two ends of the values, and `mode` specifies the deletion method.<br><br><br>* none: retains the strings at the two ends of each key.<br><br>* all: deletes the strings at both ends of each value. This is the default value.<br><br>* left: deletes the string at the beginning of each value.<br><br>* right: deletes the string at the end of each value. |
|trim_values.chars |String |No |`trim_values` specifies whether to delete the strings at the two ends of the values, and `chars` specifies the range of characters to delete. The default value is a double quotation mark ( " ). |
|allow_empty_values |boolean |No |Specify whether to retain a key\-value pair in which the subfield value parsed from the specified field is empty.<br><br><br>* true: retains the key\-value pairs with empty values are retained.<br><br>* false: removes the key\-value pairs with empty values. This is the default value. |
|allow_overwrite_keys |boolean |No |If a key specified is duplicated with an existing key in the collection rule, this parameter specifies whether to overwrite the existing key.<br><br><br>* true: overwrites the existing key<br><br>* false: returns an error. If keys are duplicated, the LogCollector plug\-in fails to parse the log. This is the default value. |


<span id="配置示例"></span>
### Configuration examples


* Logs

   ```Plain
   "fullregex_key": "Click Here, 36, bold, text1, 250, 100, #center#, sun1.opacity = (sun1.opacity / 100) * 90;",
   ```
   

* LogCollector plug\-in configuration

   ```json
   {
       "processors":[
           {
               "fullregex": {
                   "field": "fullregex_key",
                   "pattern": "([\\s\\w]+),\\s(\\d+),\\s(\\w+),\\s(\\w+),\\s(\\d+),\\s(\\d+),\\s(\\S+\\w+\\S+),\\s(.*).*",
                   "keys": [
                       "data",
                       "size",
                       "style",
                       "name",
                       "hOffset",
                       "vOffset",
                       "alignment",
                       "onMouseUp"
                   ],
                   "trim_values": {
                       "mode": "all",
                       "chars": "#"
                   },
                   "allow_overwrite_keys": true,
                   "allow_empty_values": true
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
   


<span id="kv-插件"></span>
## kv plug\-in

You can use the kv plug\-in to extract log fields. This topic describes the parameters of the kv plug\-in and offers a configuration example.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">LogCollector V1.0.12 and later support this plug\-in. For more information on how to view the LogCollector version, refer to <a href="https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host#%E6%9F%A5%E7%9C%8B%E8%BD%AF%E4%BB%B6%E7%89%88%E6%9C%AC">View software version</a>.</div>


<span id="参数说明"></span>
### Parameter description


|Parameter |Type |Required |Description |
|---|---|---|---|
|field |String |Yes |Specify the name of the field to be processed by the LogCollector plug\-in. |
|when |Object |No |Specify the condition for executing the plug\-in. The plug\-in is executed only when the specified condition is true. For more information, refer to [List of execution conditions](https://docs.byteplus.com/docs/tls/Set_plug-in_execution_conditions#%E6%89%A7%E8%A1%8C%E6%9D%A1%E4%BB%B6%E5%88%97%E8%A1%A8). |
|split_pattern |string |No |Specify the delimiter between key\-value pairs. If this parameter is not specified, the delimiter is a space. |
|quote |String |No |Specify the quote. The content enclosed in a quote is parsed into a complete field without being separated by a delimiter.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You cannot set this parameter to an invisible character.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can specify one quote, and the quote can contain multiple characters.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">LogCollector V1.0.34 and later allow you to set a quote.</div><br> |
|kv_split_pattern |string |No |Specify the delimiter between the key and value of each key\-value pair. If this parameter is not specified, the delimiter is an equal sign ( = ). |
|trim_keys.mode |string |No |`trim_keys` specifies whether to delete the strings at the two ends of the keys, and `mode` specifies the deletion method.<br><br><br>* none: retains the strings at the two ends of each key.<br><br>* all: deletes the strings at both ends of each key. This is the default value.<br><br>* left: deletes the string at the beginning of each key.<br><br>* right: deletes the string at the end of each key. |
|trim_keys.chars |string |No |`trim_keys` specifies whether to delete the strings at the two ends of the keys, and `chars` specifies the range of characters to delete. The default value is a double quotation mark ( " ). |
|trim_values.mode |String |No |trim_values specifies whether to delete the strings at both ends of the values, and mode specifies the deletion method.<br><br><br>* none: retains the strings at the two ends of each key.<br><br>* all: deletes the strings at both ends of each value. This is the default value.<br><br>* left: deletes the string at the beginning of each value.<br><br>* right: deletes the string at the end of each value. |
|trim_values.chars |String |No |`trim_values` specifies whether to delete the strings at the two ends of the values, and `chars` specifies the range of characters to delete. The default value is a double quotation mark ( " ). |
|allow_empty_values |boolean |No |Specify whether to retain a key\-value pair in which the subfield value parsed from the specified field is empty.<br><br><br>* true: retains the key\-value pairs with empty values are retained.<br><br>* false: removes the key\-value pairs with empty values. This is the default value. |
|allow_overwrite_keys |boolean |No |If a key specified is duplicated with an existing key in the collection rule, this parameter specifies whether to overwrite the existing key.<br><br><br>* true: overwrites the existing key<br><br>* false: returns an error. If keys are duplicated, the LogCollector plug\-in fails to parse the log. This is the default value. |


<span id="配置示例"></span>
### Configuration examples


* Logs

   ```Plain
   "kv_key": "data: \"Click,Here\", size: 36, style: bold, name: text1, hOffset: 250, vOffset: 100, #alignment#: #center#, onMouseUp: sun1.opacity = (sun1.opacity / 100) * 90;"
   ```
   

* LogCollector plug\-in configuration

   ```json
   {
       "processors":[
           {
               "kv": {
                   "field": "kv_key",
                   "split_pattern": ",",
                   "kv_split_pattern": ":\\s+",
                   "quote": "\"",
                   "trim_keys": {
                       "mode": "all",
                       "chars": "#"
                   },
                   "trim_values": {
                       "mode": "all",
                       "chars": "#"
                   },
                   "allow_overwrite_keys": true,
                   "allow_empty_values": true
               }
           }
       ]
   }
   ```
   

* Result

   ```Plain
   "data": "\"Click,Here\""
   "size": "36"
   "style": "bold"
   "name": "text1"
   "hOffset": "250"
   "vOffset": "100"
   "alignment": "center"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   ```
