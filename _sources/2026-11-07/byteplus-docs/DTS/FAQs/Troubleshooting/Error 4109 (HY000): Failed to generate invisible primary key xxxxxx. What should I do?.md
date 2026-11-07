---
title: "Error 4109 (HY000): Failed to generate invisible primary key xxxxxx. What should I do?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Error_4109_HY000_"
---

Error 4109 (HY000): Failed to generate invisible primary key. Auto\-increment column already exists. You can solve it according to the following solution:

**Possible causes**: In MySQL 8.0 and later, the Generated Invisible Primary Key (GIPK) allows automatic generation of an invisible primary key on tables without primary keys. This feature can help solve problems in some replication or cluster environments for tables without primary keys. However, when GIPK is disabled on the source, this error will be triggered if there is an auto\-increment column in the table without an explicit primary key.

**Solution**: You can submit a ticket to enable the GIPK of the source instance or close the GIPK of the target instance.
