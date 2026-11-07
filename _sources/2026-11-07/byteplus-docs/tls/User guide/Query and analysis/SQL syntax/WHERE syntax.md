---
title: "WHERE syntax"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/WHERE-syntax-2"
---

The WHERE syntax extracts logs that meet the specified condition.

<span id="Syntax format"></span>
## Syntax format

The WHERE syntax format is as follows:

```SQL
* | SELECT Key WHERE Key COMPARISON_OPERATOR VALUE
```


The Key parameter specifies the name of a log field. The supported comparison operators include `=`, `<>`, `>`, `<`, `>=`, `<=`, `BETWEEN`, `IN`, and `LIKE`.

Complying with SQL\-92, Torch Log Service (TLS) does not support AS aliases in the WHERE syntax. Otherwise, an error is reported.

<span id="Examples"></span>
## Examples

<span id="6199422d"></span>
### Example 1


* Scenario

   Query the logs whose status code is greater than 200.

* Query and analysis statement

   ```SQL
   * | SELECT * WHERE status > 200
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a4fca50adc0349a7b83ad3139fb57550~tplv-goo7wpa0wc-image.image) </span>


<span id="ed79c281"></span>
### Example 2


* Scenario

   Count the number of POST requests.

* Query and analysis statement

   ```SQL
   * | SELECT COUNT(*) as count WHERE Method='POST'
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa4e968619404364827771cf51f2b9bc~tplv-goo7wpa0wc-image.image) </span>
