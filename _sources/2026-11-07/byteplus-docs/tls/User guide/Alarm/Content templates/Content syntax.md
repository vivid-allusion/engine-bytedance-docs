---
title: "Content syntax"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/content_syntax"
---

Log Service provides diverse alarm notification content syntax, such as special character escaping and conditional judgments for variables, enabling you to customize the content and display style of alarm notifications in advanced usage scenarios. This makes the alarm notifications richer and clearer.

<span id=".5Yqf6IO95qaC6L-w"></span>
## Feature overview

Log Service offers built\-in content syntax in its alarm feature, supporting custom design of alarm notification content and style to meet various notification content customization needs across different scenarios. When designing alarm notification content, follow the content syntax described here to achieve a better user experience.

The syntax provided by Log Service is as follows:


|Type |Syntax |Description |
|---|---|---|
|Basic syntax support |[data type](https://docs.byteplus.com/docs/tls/content_syntax#.5pWw5o2u57G75Z6L) |supports integers, floating\-point numbers, strings, arrays, dictionaries, and other data types. |
||[delimiter](https://docs.byteplus.com/docs/tls/content_syntax#.5YiG6ZqU56ym) |Separators separate different types of objects. |
||[Operator](https://docs.byteplus.com/docs/tls/content_syntax#.5pON5L2c56ym) |Supports operators such as arithmetic operations. |
|Actions |[Remove whitespace](https://docs.byteplus.com/docs/tls/content_syntax#.5Yig6Zmk56m655m956ym) |Remove whitespace at the specified position. |
||[Conditional statement](https://docs.byteplus.com/docs/tls/content_syntax#.5p2h5Lu25Yik5pat) |Use parameters or logical comparison expressions for conditional judgment. |
||[iteration](https://docs.byteplus.com/docs/tls/content_syntax#.6L-t5Luj) |Iterate over arrays and objects using for loops. |
||[special character escape](https://docs.byteplus.com/docs/tls/content_syntax#.54m55q6K5a2X56ym6L2s5LmJ) |Use the verbatim tag to escape special statements. |
||[content comment](https://docs.byteplus.com/docs/tls/content_syntax#.5YaF5a655rOo6YeK) |Insert comment information in notification content using comment syntax. |
||[Variable definition](https://docs.byteplus.com/docs/tls/content_syntax#.5Y-Y6YeP5a6a5LmJ) |Define variables using the with statement. |


<span id=".5pWw5o2u57G75Z6L"></span>
## Data type

The content variable syntax is similar to Python syntax and supports the following data types.


|Data type |Description |
|---|---|
|Number |Includes integer and double types, such as 1, 3.1, \-2, etc. |
|String |All strings must be enclosed in double quotes (`""`) or single quotes (`''`). Special characters in strings must be escaped, supporting the backslash (`\`), for example, `""source""` should be written as `"\\\"source\\\""`. |
|Boolean |Supports boolean values, true and false. |
|null value |None。 |
|List |Supports list types. Lists have different names in various programming languages, such as arrays, lists, slices, etc. For example, `list("abc", "xyz")`. |
|dictionary |Supports dictionary type. Dictionaries have different names in various programming languages, such as object or dictionary. For example, `dict("abc", "xyz")`. |


<span id=".5YiG6ZqU56ym"></span>
## Delimiter

Delimiters separate different object types. The supported delimiters in Log Service alarm notifications include:


|delimiter |use cases |Example |
|---|---|---|
|`{{ }}` |usable in variables or expressions, it is the basic format for variables and expressions. |* Variable: `{{AccountID}}`<br><br>* Expression: `{{ 1 \\+ 2 }}`<br><br>* Number: `{{ 123 }}`<br><br>* String: `{{ "abc" }}` or `{{ 'xyz' }}` requires double quotes (`""`) or single quotes (`''`).<br><br>* Function call: `{{list(a,b,c,d)}}` |
|`{% %}` |Used for control statements. |```Python```<br>```{% if count >0 %}```<br>```Error present```<br>```{% else %}```<br>```No error```<br>```{% endif %}```<br> |
|`{# #}` |Used to insert comment information in the notification content; comments appear only in the configuration of the alarm policy and are not sent to recipients with the notification content. |```Plain```<br>```{# this is a single-line comment #}```<br>``````<br>```{% comment %}```<br>```this is the first line of a multi-line comment```<br>```this is the second line of a multi-line comment```<br>```{% endcomment %}```<br> |


<span id=".5pON5L2c56ym"></span>
## operator

The following operators are supported in log service alarm notifications. Arithmetic and comparison operators usually apply only to numeric variables or constants.


|category |operator |Description |
|---|---|---|
|arithmetic operations |`+` |Addition |
||`-` |Subtraction |
||`*` |Multiplication |
||`/` |division returns a floating\-point value. |
||`%` |modulus |
|comparison operations |`==` |equals |
||`!=` |not equal to |
||`>` |greater than |
||`>=` |greater than or equal to |
||`<` |less than |
||`<=` |less than or equal to |
|logical operation |`&&` or `and` |And operation |
||`\|\|` or `or` |Or operation |
||`!`or `not` |negation |
|Other operations |`In` |Used to determine if it contains; returns a Boolean result after judgment.<br><br>For example, perform judgment on the following types:<br><br><br>* Array: `{{ 400 in list(401, 402, 403) }}`.<br><br>* Object: `{{ "abc" in dict("abc", "xyz") }}`.<br><br>* String: `{{ "error" in "errorLog" }}`. |
||`()` |operation combination, for example: `{{ x > y and (x > z or y > z) }}`. |


<span id=".5Yig6Zmk56m655m956ym"></span>
## Remove whitespace

By default, within content enclosed by delimiters:


* Spaces between delimiters and other elements are ignored, such as spaces between delimiters and expressions or delimiters and variables. For example, `{{ AccountID }}` is equivalent to `{{AccountID}}`; this variable is replaced by the actual account ID in the notification content.

* Whitespace outside the delimiters is preserved, including spaces, tabs, and newlines outside the delimiters. For example, `User {{AccountID}}'s {{Topics}} triggered an alarm rule.` Whitespace before and after the two variables is preserved.

   Alarm notification syntax supports hyphen (\-)`-`Remove extra whitespace characters using the ) method. Add a hyphen at the start or end of the delimiter to remove all adjacent whitespace before and after the delimiter. For example, the rendering result of `{{ abc -}} and {{- xyz }}` is `abc and xyz`.

   You can also remove whitespace using the following methods:

   * Delete all whitespace characters immediately following the delimiter on the left: `{{-` or `{%-`

   * Remove all whitespace immediately following the delimiter on the right: `-}}` or `-%}`


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Clearing whitespace only affects spaces outside the separators. For example, <code>{{ "abc " }} {{- "xyz"}}</code> formats to <code>abc xyz</code>.</div>


* <div data-tips="true" data-tips-type="tip">Hyphen (<code>-</code>Do not insert spaces between the ) and the separator, or they will be treated as regular characters. For example, the whitespace trimming syntax in <code>{{- abc }}</code> is valid, and it formats to <code>abc</code>; the trimming operation in <code>{{ - abc }}</code> is invalid and formats to <code>-abc</code>.</div>


* <div data-tips="true" data-tips-type="tip">Empty lines are deleted by default and do not require this syntax to remove.</div>



<span id=".5p2h5Lu25Yik5pat"></span>
## Conditional judgment

In notification content, the log service can conditionally evaluate parameters or logical comparison expressions using specified if conditions and dynamically display content based on the evaluation result.


* Truth value judgment: passing an ordinary variable or constant after `if` means evaluating the truthiness of that value. The log service treats the following characters as false; all other values are treated as true:

   Boolean value `false`, numbers`0`empty string `""`

* Comparison judgment: passing a logical comparison expression after `if` means evaluating according to the comparison result. For example, `{{ if ConsecutiveAlertNums >= 5 }}` is used to determine when the number of consecutive alerts is 5 or more.


Condition checks support the following formats:


|**Usage** |**Example** |
|---|---|
|if |```Python```<br>```{% if ConsecutiveAlertNums >= 300 %}  ```<br>```Continuous alarm  ```<br>```{% endif %}```<br> |
|if\-else |```Python```<br>```{% if ConsecutiveAlertNums >= 300 %}```<br>```Persistent alert```<br>```{% else %}```<br>```Brief alert```<br>```{% endif %}```<br> |
|if\-elif |```Python```<br>```{% if ConsecutiveAlertNums >= 300 %}\nContinuous alarm\n{% elif ConsecutiveAlertNums >= 150 %}\nBrief alarm\n{% endif %}```<br> |
|if\-elif\-else |```Python```<br>```{% if ConsecutiveAlertNums >= 300 %}```<br>```continuous alarm```<br>```{% elif ConsecutiveAlertNums>=100 && type == 2 %}```<br>```alarm recovery```<br>```{% else  %}```<br>```short alarm```<br>```{% endif %}```<br> |
|If nested |```Python```<br>```{% if ConsecutiveAlertNums >= 300 %}\nContinuous alert\n{% else %}\n    {% if ConsecutiveAlertNums >= 150 && type==1 %}\n    Temporary alert\n    {% elif type==2 %}\n    alert recovery\n    {% endif %}\n{% endif %}```<br> |


<span id=".6L-t5Luj"></span>
## Iteration

In alarm notifications, Log Service supports iterating over arrays and objects using for loop statements. The supported iteration methods are as follows:


|Usage |example |
|---|---|
|array iteration |```Python```<br>```{% for log in QueryResultStr %}```<br>```{{ log }}```<br>```{% endfor %}```<br> |
|Array iteration, including index access |* Access array elements by index:<br><br>   ```Python```<br>```   {%-for i in until(Topics```<br>```   {{i}}:{{Topics[i]}}```<br>```   {%endfor-%}```<br>```   ```<br>   <br><br>* Loop starting from the specified index:<br><br>   ```Python```<br>```   {%-for i in untilStep(1,Topics```<br>```   {{i}}:{{Topics[i]}}```<br>```   {%endfor-%}```<br>```   ```<br>    |
|Object iteration |Use a for loop to iterate over an object converted into key\-value pair (`Key:Value`) format.<br><br>```Python```<br>```{% for key, val in dict("a",1,"b",2) %}```<br>```{{ key }}: {{ val }}```<br>```{% endfor %}```<br> |
|nested loop |```Python```<br>```{%-for logs in QueryLog%}```<br>```{%- for log in logs%}```<br>```{{log.name}}```<br>```{{log.type}}```<br>```{{log.double_key}}```<br>```{{log.obj_key.key1}}```<br>```{{log.obj_key.key2}}```<br>```{{log.obj_key.key_long}}```<br>```{{log.obj_key.key_double}}```<br>```{%endfor-%}```<br>```{%endfor-%}```<br> |


<span id=".54m55q6K5a2X56ym6L2s5LmJ"></span>
## Special character escaping

If you need to include special strings like `{{` in alarm notification content that should not be interpreted as delimiters or variable syntax, you must escape these special strings when configuring the notification content. Wrap the content that should be output in its original style using the verbatim tag.

For example, the following configuration preserves all content between `{% verbatim %}` and `{% endverbatim %}`.

```Python
{% verbatim %}
{{ QueryResultStr }}
{% endverbatim %}
```


After escaping and formatting, the output is as follows:

```Python
{{ QueryResultStr }}
```


<span id=".5YaF5a655rOo6YeK"></span>
## Content annotations

You can insert annotation information in the notification content using annotation syntax. Annotations only appear in the alarm policy configuration and are not sent to recipients with the notification content.


|Comment types |grammar |Example |
|---|---|---|
|Single\-line comments |```Plain```<br>```{# #}```<br> |```Plain```<br>```{# this is a comment line #}```<br> |
|multi\-line comment |```Python```<br>```{% comment %}```<br>```{% endcomment %}```<br> |```Python```<br>```{% comment %}\nThis is the first line of a multi-line comment\nThis is the second line\n{% endcomment %}```<br> |


<span id=".5Y-Y6YeP5a6a5LmJ"></span>
## Variable definitions


* Define variables using the with statement. The syntax is as follows:

   ```Python
   {%with t=list("a","b")%}
   {%endwith%}
   ```
   

* Define variables using the set keyword. The syntax is as follows:

   ```Python
   {% set t=0 %}
   ```
