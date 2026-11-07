---
title: "Why is the post-schema migration/synchronization not started, yet the status is shown as \"Completed\"?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Why_is_the_post-schema"
---

When there are no post\-migration or post\-synchronization objects (e.g., triggers or events) present in the source database, DTS automatically marks the post\-schema migration or synchronization as "Completed".

To ensure the performance of data migration and the stability of the migration task, some database migration objects will be created after the incremental migration is completed. The objects that need to undergo post\-schema migration include:


* RDS for MySQL: trigger, event.

* RDS for PostgreSQL: ordinary trigger, event trigger, RULE, exclusive constraint, foreign key constraint, check constraint, Domain constraint, and Sequence value setting.
