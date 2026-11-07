---
title: "DISTINCT clause"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/DISTINCT-clause-2"
---

The DISTINCT clause is used in a SELECT statement to remove duplicate values from a column. This topic describes the syntax of the DISTINCT clause and offers typical examples.

<span id="Syntax format"></span>
## Syntax format

The DISTINCT clause removes duplicate values from a column and returns the unique value of the specified field. If a field has multiple duplicate values, use the DISTINCT clause to extract the unique value and delete duplicate data.

The syntax format of the DISTINCT clause is as follows:

```SQL
DISTINCT Key|(Key)
```


Key specifies the name of a log field. If you set Key to \*, the DISTINCT clause removes duplicate values from all columns in logs.

You can use the DISTINCT clause in a SELECT statement to get the unique value of the field specified in the SELECT statement.

<span id="Examples"></span>
## Examples


* Example 1:

   * Scenario: Query the unique values in the TopicID column.

   * Query and analysis statement

      ```SQL
      * | SELECT DISTINCT TopicID WHERE TopicID !='' 
      ```
      

      or

      ```SQL
      * | SELECT DISTINCT(TopicID) WHERE TopicID !=''
      ```
      

   * Query and analysis results

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f6442f034f44657809773f8ccd8114d~tplv-goo7wpa0wc-image.image) </span>

* Example 2:

   * Scenario: Query the number of active topics in the past 10 minutes.

   * Query and analysis statement

      ```SQL
      * | SELECT COUNT(DISTINCT TopicID) WHERE TopicID !='' 
      
      Or
      
      * | SELECT COUNT(DISTINCT(TopicID)) WHERE TopicID !=''
      ```
      

   * Query and analysis results

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f74c443eeb504ed59d5f501dce8e5d00~tplv-goo7wpa0wc-image.image) </span>
