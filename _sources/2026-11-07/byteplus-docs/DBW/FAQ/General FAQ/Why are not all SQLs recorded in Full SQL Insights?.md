---
title: "Why are not all SQLs recorded in Full SQL Insights?"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/SQLs_in_SQL_insight"
---

* **Possible Reason One**: Full SQL Insights only supports recording the most recent 10,000 SQL templates.

* **Possible Reason Two**: The maximum length of SQL statements recorded in Full SQL Insights is 4096 bytes; any part exceeding this limit will not be recorded. The maximum length of SQL statements recorded by the instance is controlled by parameters:

   * When the parameter value is less than or equal to 4096 bytes, the maximum length of SQL statements is the parameter setting value, and any part exceeding this limit will not be recorded. Since prefix annotations are added during information collection and processing, the actual maximum length of recorded SQL statements is slightly less than the parameter setting value.

   * When the parameter value is greater than 4096 bytes, the maximum length of SQL statements is 4096 bytes, and any part exceeding this limit will not be recorded. Since prefix annotations are added during information collection and processing, the actual maximum length of recorded SQL statements is slightly less than 4096 bytes.
