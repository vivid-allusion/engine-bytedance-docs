---
title: "What should I do if I encounter the error OnlineDDLErrorCode_DuplicateKeyOrColumn while executing a lock-free schema change task?"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/OnlineDDLErrorCode"
---

**Possible cause**: The target table already contains a duplicate Key or Column.

**Solution**: Check if the target table already contains a duplicate Key or Column. If it does, modify the Key or Column name you intend to add.
