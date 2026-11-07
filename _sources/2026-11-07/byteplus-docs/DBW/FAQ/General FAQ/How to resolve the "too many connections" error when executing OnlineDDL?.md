---
title: "How to resolve the \"too many connections\" error when executing OnlineDDL?"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/too_many_connections"
---

**Possible cause**: If the table has foreign key dependencies, executing OnlineDDL on the target table may cause `INSERT` operations to be blocked.

**Solution**: Adjust the foreign keys of the target table before executing OnlineDDL.
