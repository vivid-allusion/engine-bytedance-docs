---
title: "Regular expression functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/regular_expression_functions"
---

This topic describes the syntax and format of a regular expression function and offers a sample scenario.

<span id="regex-replace-函数"></span>
## regex_replace function

This function matches and replaces strings based on a regular expression. The function is mainly used in scenarios in which data masking is required.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
regex_replace(value, regex="regular expression", replace="", count=0)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value |String |Yes |/ |/ |Specify a value to be processed. |
|regex |String |Yes |/ |/ |Specify a regular expression. |
|replace |String |No |Empty string |/ |Specify a string used for replacement. By default, an empty string is used. |
|count |Number |No |0 |/ |Specify the number of times that the function replaces strings. By default, the function replaces all strings that match the regular expression. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function replaces numeric values in the log field `content` with asterisks (`*`), then outputs the replacement result to the field `regex_replace`.

* Transformation rule:

   ```python
   f_set("regex_replace", regex_replace(v("content"), "\\d+", "*"))
   ```
   

* Sample log:

   ```json
   {
       "content":"abc1def23ghi4567jk"
   }
   ```
   

* Transformation result:

   ```json
   {
       "content":"abc1def23ghi4567jk",
       "regex_replace":"abc*def*ghi*jk"
   }
   ```
