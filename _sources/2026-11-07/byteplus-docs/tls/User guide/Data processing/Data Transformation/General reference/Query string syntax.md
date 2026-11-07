---
title: "Query string syntax"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/query_string_syntax"
---

In the data transformation functions of Torch Log Service (TLS), string syntax is used to specify search rules and data filtering methods. This topic describes the general rules for query string syntax in data transformation functions.

<span id=".6YCC55So6IyD5Zu0"></span>
## Applicable scope

When you use the following data transformation functions, you can filter data through query string syntax.


|Type |Function |Scenario |
|---|---|---|
|Event verification function |[f_search function](https://docs.byteplus.com/docs/tls/event_verification_functions#f-search-%E5%87%BD%E6%95%B0) |You can use a query string to determine whether the field value of a specified event meets specified conditions. |


<span id=".5Yqf6IO95qaC6KeI"></span>
## Feature overview

The query string syntax supports features such as keyword search and fuzzy matching. The following table describes which search features are supported by key\-value search and full\-text search modes.


|**Feature** |**Key\-value Search** |**Full\-text Search** |
|---|---|---|
|Keyword search |Supported |Supported |
|Fuzzy matching |Supported |Supported |
|Exact matching |Supported |Not supported |
|Regular expression\-based matching |Supported |Not supported |
|Numerical comparison and range judgment |Supported |Not supported |
|Logical relationship judgment |Supported |Supported |
|Field judgment |Supported |Not supported |


<span id=".54m55q6K5a2X56ym6L2s5LmJ"></span>
## Special character escaping

If you use the query string syntax, escape the following characters: asterisks ( `*` ), colons ( `:` ), parentheses ( `()` ), single quotation marks ( `''` ), double quotation marks ( `""` ), question marks ( `?` ), and tildes ( `~` ). Escape methods include:


|**Escape Method** |Description |
|---|---|
|Field name escaping |Escape field names containing special characters with backslashes (`\`). Example: `new\*:content` and `\(path\)\?:api`.<br><br>If a field name is in Chinese, enclose the field name with double quotation marks(""). Example: `e_search('"Chinese field":"Chinese value"')`. |
|Search value escaping |Escape search values containing special characters with backslashes (`\`). For example, in `e_search('content:a\*b')`, a backslash ( \ ) is used to escape an asterisk ( \* ). |


<span id=".5YWz6ZSu6K-N5qOA57Si"></span>
## **Keyword search**


|Search Method |Description |
|---|---|
|Full\-text search |This method searches for a specified string in all field values. Add double quotation marks ( "" ) when you search for Chinese keywords.<br><br>Syntax format:<br><br>```Python```<br>```f_search('Keyword 1')```<br><br><br>Example:<br><br><br>* `f_search('"Chinese characters"')`: This function searches for a specified string `Chinese characters`.<br><br>* `f_search('"byte dance"')`: The searched keywords contain spaces.<br><br>* `f_search('byte dance')`: This function searches for multiple keywords. By default, the OR relationship is between the keywords. |
|Key\-value search |This method searches for a specified string in all values of a field.<br><br>Syntax format:<br><br>```Python```<br>```f_search('key:value')```<br><br><br>Example:<br><br><br>* `f_search('method: get')`: This function determines whether the values of the field `method` contain the keyword `get`.<br><br>* `f_search('company: "by enn"')`: This function determines whether the values of the field `company` contain the keyword `enn`. The keyword contains a space.<br><br>* `f_search('company: by enn')`: This function is equivalent to `f_search('company: by OR enn')`. The sample function determines whether the values of the field `company` contain the keyword `by`, or whether the full text of a log contains `enn`. |


<span id=".5qih57OK5Yy56YWN"></span>
## **Fuzzy matching**

Query string syntax supports fuzzy matching. This means you can perform matching through wildcards. Currently supported wildcards:


* Asterisks ( `*` ): This wildcard matches zero or more strings.

* Question marks ( `?` ): This wildcard matches a character or a Chinese character with equal width.


The syntax for fuzzy matching is as follows:


|Search Method |Description |
|---|---|
|Full\-text search |This method performs fuzzy matching in all fields.<br><br>Syntax format:<br><br>```Python```<br>```f_search('Keyword')```<br><br><br>Example:<br><br><br>* `f_search('dance*')`: This function searches for all strings starting with dance, such as dancers.<br><br>* `f_search('dance?')`: This function searches for a 6\-digit string starting with dance, such as dancer. |
|Key\-value search |This function performs fuzzy matching in the field values of a specified field.<br><br>Syntax format:<br><br>```Python```<br>```f_search('key:value*')```<br><br><br>Example:<br><br><br>* `f_search('company: byt*dance')`: The wildcard matches zero or more characters.<br><br>* `f_search('company: tik?ok')`: The wildcard matches one character. |


<span id=".5a6M5YWo5Yy56YWN"></span>
## **Exact matching**

The query string syntax supports exact matching. Exact matching means the value of a field should exactly match a specified string.


* Syntax format:

   ```Python
   f_search('key==value')
   ```
   

* Example: `f_search('company== "byte dance"')`: This function searches for a value of the field `company` that is equal to `byte dance`.


<span id=".5q2j5YiZ6KGo6L6-5byPLeWMuemFjQ=="></span>
## **Regular expression\-based matching**

Query string syntax supports regular expression\-based matching. This means the values of a specified field are matched through regular expressions.


* Syntax format:

   ```Python
   f_search('key~=Regular expression')
   ```
   

* Syntax description:

   * If the regular expression contains a backslash (`\`), enclose the expression in a double quotation mark ("").

   * By default, regular expression\-based matching is considered as partial matching. If you want your function to perform exact matching, add a caret (`^`) at the beginning of your regular expression and a dollar sign (`$`) at the end of the expression. Example: `^\d+$`.

* Example:

   * `f_search('path~= "\d+"')`: This function matches the values of the path field that contain a digit.

   * `f_search('id~= "^\d+$"')`: This function matches the values of the id field that contain only digits.


<span id=".5pWw5YC85q-U6L6D5LiO6IyD5Zu05Yik5pat"></span>
## **Numerical comparison and range judgment**

Query string syntax supports numerical comparison and numerical range judgment. Supported comparison operators include `>`, `>=`, `=`, `<`, and `<=`.


|Feature |Description |
|---|---|
|Numerical comparison |This feature compares the value of a specified field with a certain numerical value.<br><br>Examples:<br><br>```Python```<br>```f_search('count >= 9')  #  >=9```<br>```f_search('count > 9')   #  > 9```<br>```f_search('count = 9')   #  = 9```<br>```f_search('count <= 9')  #  <=9```<br>```f_search('count < 9')   #  < 9```<br> |
|Numerical range judgment |This feature judges whether the value of a specified field is within a numerical range. Make sure your numerical range is a closed interval.<br><br>Examples:<br><br>```Python```<br>```f_search('age: [1, 18]') # >=1 and  <=18```<br> |


<span id=".6YC76L6R5YWz57O7"></span>
## **Logical relationship judgment**

This feature judges the logical relationships between multiple search results. This feature allows you to adjust the comparison order of logical relationships through parentheses`()`.


|**Logical Relationship** |**Keyword** |
|---|---|
|AND |Use keywords such as `AND` and `&&`. Only uppercase letters are supported. |
|OR |Use keywords such as `OR` and `\|\|`. |
|No |Use keywords such as `NOT` and `!`. Only uppercase letters are supported. |


Example:

```Python
f_search('byte OR dance') # Make sure your logical operator is in uppercase
f_search('byte AND (dancer OR dance)')
f_search('byte AND  ( NOT dancer OR tiktok)')
f_search("byte && dance")    # AND
f_search("byte || dance")    # OR
f_search("byte || !dance")   # OR NOT
```


<span id=".5a2X5q615Yik5pat"></span>
## **Field judgment**

This feature uses a search string to judge a field.

Example:


* `f_search('field:*')`: This function judges whether the field `field` exists.

* `f_search('NOT field:*')`: This function judges whether the field `field` does not exist.

* `f_search('field~=".+"')`: This function judges whether the field `field` exists.

* `f_search('NOT field~=".+"')`: This function judges whether the field `field` does not exist.
