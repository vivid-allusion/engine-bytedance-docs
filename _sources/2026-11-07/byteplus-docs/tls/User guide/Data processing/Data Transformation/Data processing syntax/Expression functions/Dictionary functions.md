---
title: "Dictionary functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/dictionary_functions"
---

This topic describes the syntax and format of dictionary functions and offers sample scenarios.

<span id="dict-make-函数"></span>
## dict_make function

This function constructs a dictionary.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Make sure the keywords and values of the function appear in pair.</div>


<span id="函数语法-格式"></span>
### Function syntax and format

```python
dict_make(key1, value1, key2, value2...)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|key |String |Yes |/ |/ |Specify a string as a field name (key) in a dictionary. |
|value |String |Yes |/ |/ |Specify a string as a field value (value) in a dictionary. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function constructs a dictionary `dict_make`. The values of the fields `key` and `value` are used to construct the dictionary.

* Transformation rule:

   ```python
   f_set("dict_make",dict_make(v("key"),v("value")))
   ```
   

* Sample log:

   ```json
   {
       "key":"key1",
       "value":"value1"
   }
   ```
   

* Transformation result:

   ```json
   {
       "key":"key",
       "value":"value"
       "dict_make":"{"key1":"value1"}"
   }
   ```
   


<span id="dict-update-函数"></span>
## dict_update function

This function uses one dictionary to update the values of another dictionary.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Make sure the keys and values of a dictionary are in string format.</div>


<span id="函数语法-格式"></span>
### Function syntax and format

```python
dict_update(dict1, dict2)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|dict1 |Dictionary |Yes |/ |/ |Specify the target dictionary to be updated. |
|dict2 |Dictionary |Yes |/ |/ |Specify dictionary information that is used to update the target dictionary. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function updates dict1 using the values of dict2. If both dictionaries contain the same values, the function overwrites dict1 with dict2. Otherwise, the function adds dict2 to dict1.

* Transformation rule:

   ```python
   f_set("dict_updated",dict_update(dict_make("hello","world"),dict_make("hello","world_modified","kv","test")))
   ```
   

* Sample log:

   ```json
   {
       "k1":"v1"
   }
   ```
   

* Transformation result:

   ```json
   {
       "k1":"v1",
       "dict_updated":"{"hello": "world_modified", "kv": "test"}"
   }
   ```
