---
title: "Regular expressions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/regular_expressions"
---

This topic describes the functions that support regular expressions and the matching methods.

<span id=".5pSv5oyB5q2j5YiZ6KGo6L6-5byP55qE5Ye95pWw"></span>
## Functions supporting regular expressions


|Name |Matching Method |
|---|---|
|`f_match` |This function is controlled by the parameters. By default, the function performs partial matching. |
|`f_search` |This function performs partial matching. |


<span id=".5q2j5YiZ5Yy56YWN"></span>
## **Regular expression\-based matching**

Regular expressions support the following matching methods: exact matching and partial matching.


* Exact matching: This method matches the value of a regular expression with a string that is the same as the value. For example, `1234` fully conforms to the rules specified by the regular expression `\d+`.

* Partial matching: This method matches the value of a regular expression with a string that is partially the same as the value. Functions such as `f_search` support partial matching. You can add `^` and `$` at the beginning and end respectively to convert partial matching to exact matching. For example, the format is `^regular expression$`. For more information, refer to [Regular expression operations](https://docs.python.org/zh-cn/3.7/library/re.html).


Examples of matching modes are as follows:


* `f_match("abc123", "\d+")`: The string matches the regular expression. By default, the partial matching mode is used.

* `f_match("abc123", "\d+", full=True)`: The string does not match the regular expression. The exact matching mode is set.

* `f_match("abc123", "^\d+$")`: The string does not match the regular expression. This mode is equivalent to the exact matching mode.

* `f_search('error~="\d+"')`: This function judges whether the value of the field `error` matches the regular expression. This mode is equivalent to the partial matching mode.

* `f_search('error~="^\d+$"')`: This function judges whether the value of the field `error` matches the regular expression. This mode is equivalent to the exact matching mode.
