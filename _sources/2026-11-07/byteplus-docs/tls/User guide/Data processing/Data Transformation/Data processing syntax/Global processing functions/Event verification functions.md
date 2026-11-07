---
title: "Event verification functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/event_verification_functions"
---

<span id="f-match-函数"></span>
## f_match function

This function judges whether a specified log field value matches a regular expression and returns the judgment result. The judgment result can be True or False.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
f_match(field,regex=regular expression,full=False)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|field |String |Yes |/ |/ |Specify a field name. When the specified field does not exist, the function returns False. |
|regex |String |Yes |/ |/ |Specify a regular expression. |
|full |Bool |No |False |* False<br><br>* True |Specify whether to perform exact matching. The default value False specifies partial matching. Examples: If your string completely matches the value of a regular expression, the string and the value are an exact match. For example, the abcd exactly matches `\w+`. You can add `^` and `$` to the beginning and end of your regular expression to change partial matching scenarios to exact matching scenarios. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function judges whether the `content` field in a log matches a regular expression.

* Transformation rule:

   ```python
   f_set("f_match_part",f_match("content","12"))
   f_set("f_match_full",f_match("content","12",True))
   ```
   

* Sample log:

   ```json
   {
       "content": "1234"
   }
   ```
   

* Transformation result:

   ```json
   {
       "content": "1234",
       "f_match_part": "True",
       "f_match_full": "False"
   }
   ```
   


<span id="f-search-函数"></span>
## f_search function

This function judges whether content in the log that matches your query statement exists. If so, the function returns True. Otherwise, the function returns False.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
f_search(query=query conditions)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|query |string |Yes |/ |/ |Specify a query string. A query string is used to filter logs quickly. For more information, refer to [Query string syntax](https://docs.byteplus.com/docs/tls/query_string_syntax). |


<span id="函数示例"></span>
### Sample function


* Scenario: The function judges whether a value that is greater than 0 exists in the log field `count`.

* Transformation rule:

   ```python
   f_set("f_search",f_search("count > 0"))
   ```
   

* Sample log:

   ```json
   {
       "count": "100"
   }
   ```
   

* Transformation result:

   ```json
   {
       "count": "100",
       "f_search": "True"
   }
   ```
   


Examples of common syntax rules:

```python
# Full text.
f_search("byte dance")    # Perform a full-text search. Two substrings are OR relationship.
f_search('"byte dance"')   # Perform a full-text search. The search keyword is a complete substring.

# Field:string.
f_search("method: get")         # Search for a specified word.
f_search('company: "byte dance"')   # Search for a substring with spaces.
f_search('company: byte dance')   # Search for company:byte or company:dance.

# Exact matching.
f_search('company== "byte dance"')  

# Wildcard-based search. An asterisk ( * ) matches 0 or more characters, and a question mark ( ? ) matches 1 character.
f_search('company: do*y?n')  # Perform exact matching.
f_search('company: byt*dance')   # The string byt*dance only contains an asterisk ( * ), and double quotation marks ('") are not required to enclose the string.
f_search('company: tik?ok')    # The string tik?ok only contains a half-width question mark ( ? ), and double quotation marks ('") are not required to enclose the string.

# Field name escaping.
f_search('"Chinese character field": abc')                     # Type Chinese characters directly.
f_search("\*a: value")              # Escape special characters with backslashes ( \ ).
f_search("__tag__\:field: value")  # Escape characters with backslashes ( \ ).

# Regular expression-based matching.
f_search('company~="byt[\w]dance"')   # Perform matching based on a regular expression.

# Number
f_search('amount: [10,200]')  # >=10 and <=200
f_search('distance >=10')           # >= 10
f_search('distance > 20')            # > 20

# Relational operators.
f_search('byte OR dance') # Make sure the relational operators are in uppercase.
f_search('byte AND  ( NOT dancer OR tiktok)')
f_search('byte AND (dancer OR dance)')
f_search("byte || !dance")   # OR NOT
f_search("byte || dance")    # OR
f_search("byte && dance")    # AND
```
