---
title: "FAQs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/sqoop_faqs"
---

<span id="sqoop-eval无法执行多query"></span>
## sqoop eval cannot execute multiple queries


* Phenomenon description: Error message "You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'show databases' at line 1"

* Cause analysis: Multiple query execution is disabled by default

* Solution: Add allowMultiQueries=true to the connection string when connecting to MySQL
