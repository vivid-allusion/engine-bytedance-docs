---
title: "What are the usage scenarios of quotation marks in query and analysis statements?"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/the-usage-scenarios-of-quotation-marks-in-query-and-analysis-statements"
---

This topic introduces the use of quotation marks in query and analysis statements.

<span id="72c10e42"></span>
## Usage Instructions


* In query and analysis statements, if there are special characters (such as spaces), query operators (such as and, or), index segmentation symbols in the field name or field value, they need to be enclosed in double quotation marks `"`. For more explanations and examples about the query syntax, please refer to [Log query syntax](https://docs.byteplus.com/docs/tls/Log-query-syntax-2).

* In analysis statements (SQL statements), single quotation marks `'` need to be used to enclose characters representing strings. Characters without quotation marks or enclosed in double quotation marks `"` are field names or column names. For example, `'time'` represents a string, while `time` or `"time"` represents a field name or column name.


<span id="a87b78fe"></span>
## Differences between single quotation marks and double quotation marks

In query statements, characters enclosed in both single quotation marks `'` and double quotation marks `"` represent strings. Except for the following two points, the semantics of single quotation marks `'` and double quotation marks `"` are the same.


* Phrase query needs to be in the form of `#""`, and single quotation marks `'` cannot be used to replace double quotation marks `"`.

* Asterisks `*` and question marks `?` enclosed in double quotation marks `"` do not represent wildcards but only ordinary characters; asterisks `*` and question marks `?` enclosed in single quotation marks `'` represent wildcards. For example:

   * `"abc*"` represents a normal query, querying the string `abc*`.

   * `'abc*'` represents a wildcard query, querying the strings starting with `abc`.


<span id="ca6814a6"></span>
## Using quotation marks in query statements


* Example 1: Query the logs where the value of the `Req Size` field is greater than 100.

   There is a space in the field `Req Size`, so it needs to be enclosed with double quotation marks `"` in the query statement.

   ```SQL
   "Req Size" > 100
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee48ff836dc84fa082c2afe4e241e80e~tplv-goo7wpa0wc-image.image) </span>

* Example 2: Query the logs that contain the keywords `open failed`.

   ```SQL
   "open failed"
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a04dda13e9124554946d52fe06ee6b65~tplv-goo7wpa0wc-image.image) </span>

* Example 3: Query the logs in which the `message` field contains the keywords `error and failed`.

   Here, `and` is an ordinary query string, not a query operator.

   ```SQL
   message:"error and failed"
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/af854048eb324b0db46fd1d2b0d8cb51~tplv-goo7wpa0wc-image.image) </span>


<span id="efd2f3d5"></span>
## Using quotation marks in SQL analysis statements


* Example 1: Count the number of requests corresponding to each request method.

   ```SQL
   * | SELECT Method, COUNT(*) AS "request total" GROUP BY Method
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0fb68628043943618e7b23478c11cee2~tplv-goo7wpa0wc-image.image) </span>

* Example 2: Count the number of logs corresponding to each log level.

   The `logging` field is in JSON format, and the `level` field is its child node. When performing query and analysis, the field format is `logging.level`.

   ```SQL
   * | SELECT "logging.level", COUNT(*) AS PV GROUP BY "logging.level"
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2089b1ac6fb046b2a3b8217bfb21cc1c~tplv-goo7wpa0wc-image.image) </span>
