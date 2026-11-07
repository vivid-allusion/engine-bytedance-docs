---
title: "Key-value extraction functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/key_value_extraction_functions"
---

This topic describes the syntax and formats of key\-value extraction functions and offers sample scenarios.

<span id="ext-sep-函数"></span>
## ext_sep function

This function extracts field value content based on a single\-character delimiter.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
ext_sep(field, output="Target field name1,Target field name2,Target field name...", sep=",", quote="\"", restrict=False, mode="overwrite")
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|field |String |Yes |/ |/ |Specify the name of a field of which you want to separate the values. |
|output |String |Yes |/ |/ |Specify one or more field names that are output after extraction. Separate the field names with commas ( , ). |
|sep |String |No |, |/ |Specify a delimiter. |
|quote |String |No |" |/ |Specify a pair of characters. Strings within the character pair are not separated. |
|restrict |Boolean |No |False |/ |When the number of extracted values is inconsistent with the number of target fields entered:<br><br><br>* True: ignores this situation and performs no extraction.<br><br>* False: tries to match the first few fields. |
|mode |String |No |overwrite |overwrite,fill |Specify the processing logic used when a specified field does not exist.<br><br><br>* overwrite: performs overwriting.<br><br>* fill: sets the target field when it does not exist. |


<span id="函数示例"></span>
### Sample function


* Scenario: This function extracts the values of the field `content` in a log to multiple fields based on commas ( , ).

* Transformation rule:

   ```python
   ext_sep("content", "city-1,city-2,city-3")
   ```
   

* Sample log:

   ```json
   {
       "content":"shanghai,hangzhou,chengdu"
   }
   ```
   

* Transformation result:

   ```json
   {
       "content":"shanghai,hangzhou,chengdu",
       "city-1":"shanghai",
       "city-2":"hangzhou",
       "city-3":"chengdu"
   }
   ```
   


<span id="ext-sepstr-函数"></span>
## ext_sepstr function

This function extracts field value content based on the specified string.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
ext_sepstr(field, output="Target field name1,Target field name2,Target field name...", sep="||", restrict=False, mode="overwrite")
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|field |String |Yes |/ |/ |Specify the name of a field of which you want to separate the values. |
|output |String |Yes |/ |/ |Specify one or more field names that are output after extraction. Separate the field names with commas ( , ). |
|sep |String |No |, |/ |Specify a string as the delimiter. |
|restrict |Boolean |No |False |/ |When the number of extracted values is inconsistent with the number of target fields entered:<br><br><br>* True: ignores this situation and performs no extraction.<br><br>* False: tries to match the first few fields. |
|mode |String |No |overwrite |overwrite,fill |Specify the processing logic used when a specified field does not exist.<br><br><br>* overwrite: performs overwriting.<br><br>* fill: sets the target field when it does not exist. |


<span id="函数示例"></span>
### Sample function


* Scenario: Based on the string `||`, this function extracts the values of the field `content` in a log to multiple fields.

* Transformation rule:

   ```python
   ext_sepstr("content", "city-1,city-2,city-3")
   ```
   

* Sample log:

   ```json
   {
       "content":"shanghai||hangzhou||chengdu"
   }
   ```
   

* Transformation result:

   ```json
   {
       "content":"shanghai||hangzhou||chengdu"
       "city-1":"shanghai",
       "city-2":"hangzhou",
       "city-3":"chengdu"
   }
   ```
   


<span id="ext-json-函数"></span>
## ext_json function

This function expands the JSON strings of a specified field.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If duplicate keys exist at different levels of the JSON field, we recommend that you use parameters for filtering a node list such as include_node, or set fmt to full for specifying that keys are formatted to full paths. This can prevent the values of the keys from being overwritten. For example, a JSON string is <code>{ "time": "2023”, "info": { "time": "10:45" } }</code>. After expansion, the value of the field <code>time</code> may be <code>2023</code> or <code>10:45</code>. If you want to specify the <code>time</code> field in <code>info</code> as the <code>time</code> field that you want to expand, set the ext_json function to <code>ext_json("data",include_path="data.info.time")</code> or <code>ext_json("data",fmt="full")</code>.</div>


<span id="函数语法-格式"></span>
### Function syntax and format

```python
ext_json(field, depth=2, prefix="pre_",suffix="_",fmt="simple",sep=".",expand_array=True)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|field |String |Yes |/ |/ |Specify the name of the original field that you want to expand. |
|depth |Number |No |100 |1～500 |Specify the JSON string level that you want to expand. |
|prefix |String |No |No prefix added |/ |Specify the prefix of the node at the deepest level of the expanded JSON string.<br><br>Only the deepest JSON level is prefixed. |
|suffix |String |No |No suffix added |/ |Specify the suffix of the node at the deepest level of the expanded JSON string.<br><br>Only the deepest JSON level is suffixed. |
|fmt |String |No |simple |* full<br><br>* simple |Specify a formatting method. Valid values:<br><br><br>* full: sets a full path generated by merging the parent node and the current node as a field name. The field name is in the following format: `{parent}{sep}{prefix}{key}{suffix}`. The delimiter is the character specified by the `sep` parameter. The default value of sep is `.`. For example, if you specify that the JSON string key is extracted from the data field, the field name is formatted to `data.key`.<br><br>* simple: sets a node name as a field name. The format is `{prefix}{key}{suffix}`. |
|sep |String |No |. |/ |Specify a delimiter for formatting parent and child nodes. You can set this parameter when the value of parameter fmt is full. |
|expand_array |Boolean |No |True |* True<br><br>* False |Specify whether to expand an array.<br><br><br>* True: expands the elements in the array as the keys.<br><br>* False: uses the whole array as the value without expansion. |
|include_node |String |No |No processing |/ |Specify the names of nodes that you do not want to filter out. The system uses a regular expression for matching. By default, nodes of which the names contain Chinese characters, digits, letters, or `_.-` are automatically expanded.<br><br>After setting the node allowlist, only those included in the list appear in the results. For example, you can set `ext_json("json_data_filed", ...., include_node="k\d+")`. |
|exclude_node |String |No |No processing |/ |Specify the nodes that you want to filter out. The system uses a regular expression for matching.<br><br>After setting the node denylist, those within the list are filtered out. For example, you can set `ext_json("json_data_filed", ...., exclude_node="k\d+")`. |
|include_path |String |No |No processing |/ |Specify a node path that you want to include during filtering. The system uses a regular expression for matching.<br><br>The regular expressions for `include_path` and `exclue_path` start matching from the beginning of the specified paths. Separate a path to be matched with periods `( . )`. For example, you can set `ext_json("json_data_filed", ...., include_path="content.k\d+")`. |
|exclude_path |String |No |No processing |/ |Specify a node path that you want to exclude during filtering. The system uses a regular expression for matching.<br><br>The regular expressions for `include_path` and `exclue_path` start matching from the beginning of the specified paths. Separate a path to be matched with periods `( . )`. For example, you can set `ext_json("json_data_filed", ...., exclude_path="content.k\d+")`. |


<span id="函数示例"></span>
### Sample function

Example 1:


* Scenario: The function expands JSON data from the log field `content`. In this case, the function sets `pre_` as the prefix and `suf_` as the suffix. In addition, fmt uses the default value simple.

* Transformation rule:

   ```python
   ext_json("content",prefix="pre_",suffix="suf_")
   ```
   

* Sample log:

   ```json
   {
       "content":"{\"k1\": \"v1\",\"k2\": {\"k3\": \"v3\"}}"
   }
   ```
   

* Transformation result:

   ```json
   {
       "content":"{\"k1\": \"v1\",\"k2\": {\"k3\": \"v3\"}}",
       "pre_k1suf_":"v1",
       "pre_k3suf_":"v3"
   }
   ```
   


Example 2:


* Scenario: The function expands JSON data from the log field `content`. In this case, the function sets fmt to full and depth to 1.

* Transformation rule:

   ```python
   ext_json("content",depth=1,fmt="full")
   ```
   

* Sample log:

   ```json
   {
       "content":"{\"k1\": \"v1\",\"k2\": {\"k3\": \"v3\"}}"
   }
   ```
   

* Transformation result:

   ```json
   {
       "content":"{\"k1\": \"v1\",\"k2\": {\"k3\": \"v3\"}}",
       "content.k1":"v1",
       "content.k2":"{\"k3\": \"v3\"}}"
   }
   ```
   


Example 3:


* Scenario: The function expands JSON data from the log field `content`. In this case, the function reserves the data of the k1 node.

* Transformation rule:

   ```python
   ext_json("content",include_node="k1")
   ```
   

* Sample log:

   ```json
   {
       "content":"{\"k1\": \"v1\",\"k2\": {\"k3\": \"v3\"}}"
   }
   ```
   

* Transformation result:

   ```json
   {
       "content":"{\"k1\": \"v1\",\"k2\": {\"k3\": \"v3\"}}",
       "k1":"v1"
   }
   ```
   


<span id="ext-json-jmes-函数"></span>
## ext_json_jmes function

This function extracts field values from a JSON field using a jmes expression.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
ext_json_jmes(field, jmes="jmes path of JSON field", output="Target field", ignore_null=True, mode="overwrite")
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|field |String |Yes |/ |/ |Specify the name of the original field from which you want to extract values. |
|jmes |String |Yes |/ |/ |Specify a jmes expression. |
|output |String |Yes |/ |/ |Specify a field name that is output after extraction. |
|ignore_null |Boolean |No |True |/ |Specify whether to ignore a node with a null value:<br><br><br>* True: ignores the null field value.<br><br>* False: outputs an empty string when the extraction result is null. |
|mode |String |No |overwrite |overwrite,fill |Specify the processing logic used when a specified field does not exist.<br><br><br>* overwrite: performs overwriting.<br><br>* fill: sets the target field when it does not exist. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function extracts a field value from the log field `content` according to the "k3.k4" jmes path, then outputs the result to field`k3-k4`.

* Transformation rule:

   ```python
   ext_json_jmes("content", jmes="k3.k4", output="k3-k4")
   ```
   

* Sample log:

   ```json
   {
       "content":"{\"k1\": 123, \"k2\": \"456\", \"k3\": {\"k4\": -34.5, \"k5\": true}}"
   }
   ```
   

* Transformation result:

   ```json
   {
       "content":"{\"k1\": 123, \"k2\": \"456\", \"k3\": {\"k4\": \"-34.5\", \"k5\": True}}",
       "k3-k4":"-34.5"
   }
   ```
   


<span id="ext-kv-函数"></span>
## ext_kv function

This function extracts field values based on two\-level delimiters.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
ext_kv(field, pair_sep="\s", kv_sep="=", prefix="", suffix="", mode="overwrite")
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|field |String |Yes |/ |/ |Specify a source field name. |
|pair_sep |String |No |\s (space) |/ |Specify a first\-level delimiter that is used to separate multiple key\-value pairs. |
|kv_sep |String |No |= |/ |Specify a second\-level delimiter that is used to separate keys and values. |
|prefix |String |No |/ |/ |Specify the prefix of the fields generated after extraction. |
|suffix |String |No |/ |/ |Specify the suffix of the fields generated after extraction. |
|mode |String |No |fill |overwrite,fill |Specify the processing logic used when the specified field does not exist.<br><br><br>* overwrite: performs overwriting.<br><br>* fill: sets the target field when it does not exist. |


<span id="函数示例"></span>
### Sample function


* Scenario: After extracting the values of the field `content` in the log, the function separates the values into key\-value pairs based on ampersands ( & ), then separates the key\-value pairs into keys and values based on equal signs ( = ).

* Transformation rule:

   ```python
   ext_kv("content", pair_sep="&", kv_sep="=")
   ```
   

* Sample log:

   ```json
   {
       "content":"f1=a&f2=b&f3=c"
   }
   ```
   

* Transformation result:

   ```json
   {
       "content":"f1=a&f2=b&f3=c",
       "f1":"a",
       "f2":"b",
       "f3":"c"
   }
   ```
   


<span id="ext-regex-函数"></span>
## ext_regex function

This function extracts the value of a specified field according to a specified regular expression, then assigns it to another field.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
ext_regex(field,regex="regex",output=output field,mode="overwrite")
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|field |String |Yes |/ |/ |Specify the name of a field from which you want to extract values. If the specified field does not exist, no operations are performed. |
|regex |String |Yes |/ |/ |Specify a regular expression that is used to extract values from the field. Field values that match the regular expression rules are extracted. |
|output |String |No |/ |/ |Specify one or more fields that are output after matching. If the specified field does not exist, no operations are performed. Separate the fields with commas ( , ). |
|mode |String |No |fill |* overwrite<br><br>* fill |specifies how the value of an output field is overwritten by a specified field.<br><br><br>* overwrite: performs overwriting under all circumstances by default.<br><br>* fill: sets the target field when it does not exist. |


<span id="函数示例"></span>
### Sample function

Example 1:


* Scenario: The function extracts caller from the log field `call_record`.

* Transformation rule:

   ```python
   ext_regex("call_record","\d{11}","caller")
   ```
   

* Sample log:

   ```json
   {
       "call_record": "caller:13800000000 called:13800000001"
   }
   ```
   

* Transformation result:

   ```json
   {
       "call_record": "caller:13800000000 called:13800000001",
       "caller": "13800000000"
   }
   ```
   


Example 2:


* Scenario: The function extracts caller and called from the log field `call_record`.

* Transformation rule:

   ```python
   ext_regex("call_record","\d{11}","caller,called")
   ```
   

* Sample log:

   ```json
   {
       "call_record": "caller:13800000000 called:13800000001"
   }
   ```
   

* Transformation result:

   ```json
   {
       "call_record": "caller:13800000000 called:13800000001",
       "caller": "13800000000",
       "called": "13800000001"
   }
   ```
   


Example 3:


* Scenario: The function extracts caller from the log field `call_record`, then overwrites the field `origin_caller`.

* Transformation rule:

   ```python
   ext_regex("call_record","\d{11}","origin_caller","overwrite")
   ```
   

* Sample log:

   ```json
   {
       "call_record": "caller:13800000000 called:13800000001",
       "origin_caller": "13800000002"
   }
   ```
   

* Transformation result:

   ```json
   {
       "call_record": "caller:13800000000 called:13800000001",
       "origin_caller": "13800000000"
   }
   ```
   


<span id="ext-grok-函数"></span>
## ext_grok function

This function extracts specific values based on regular expressions. Grok expressions already define common regular expressions that include multiple items such as IP addresses and file paths. You can directly use grok expressions. For more information on common grok expressions, refer to [Official documentation](https://pkg.go.dev/github.com/trivago/grok#pkg-variables).

<span id="函数语法-格式"></span>
### Function syntax and format

```python
ext_grok(field,Common grok expression,extend=custom grok expression)
```


The following table describes the parameters.


|Parameter |Type |Required |Description |
|---|---|---|---|
|field |String |Yes |Specify the name of the field from which you want to extract values. |
|grok |String |Yes |Set an official grok expression. |
|extend |Dict |No |Specify a custom grok expression. Make sure the keys and values are in string format. |


<span id="函数示例"></span>
### Sample function

Example 1:


* Scenario: The function calculates the year, month, day and quoted string in the log field `content`.

* Transformation rule:

   ```python
   ext_grok("content","%{YEAR:year} %{MONTH:month} %{MONTHDAY:day} %{QUOTEDSTRING:motto}")
   ```
   

* Sample log:

   ```json
   {
       "content":"2023 August 7 \"It is sunny day\""
   }
   ```
   

* Transformation result:

   ```json
   {
       "content":"2023 August 7 "It is sunny day"",
       "year": "2023",
       "month": "August",
       "day": "7",
       "motto": "\"It is sunny day\""
   }
   ```
   


Example 2:


* Scenario: The function extracts IDs from a log based on a custom Grok expression.

* Transformation rule:

   ```python
   ext_grok("content", "%{ID1:user_id1},%{ID2:user_id2}",extend=dict_make("ID1","%{WORD}-%{INT}","ID2","%{WORD}-%{WORD}"))
   ```
   

* Sample log:

   ```json
   {
       "content": "Chengdu-1023,Chongqing-Chongqing"
   }
   ```
   

* Transformation result:

   ```json
   {
       "content": "Chengdu-1023,Chongqing-Chongqing",
       "user_id1": "Chengdu-1023",
       "user_id2": "Chongqing-Chongqing"
   }
   ```
