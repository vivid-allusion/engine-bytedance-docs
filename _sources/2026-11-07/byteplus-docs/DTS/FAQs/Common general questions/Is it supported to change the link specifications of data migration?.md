---
title: "Is it supported to change the link specifications of data migration?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/can_I_change_the_link_specification_for_data_migration"
---

Currently only supported to change the link specifications of Synchronization tasks and migration tasks, with details as follows:


* The link specification can only be changed when the migration progress enters the incremental migration or incremental synchronization phase. For detailed operations, refer to [Changing the migration task specification](https://docs.byteplus.com/en/docs/DTS/modifying_migration_task_specifications?lang=zh) and [Changing the synchronization task specification](https://docs.byteplus.com/en/docs/DTS/modifying_synchronization_task_specifications?lang=zh).

* Before the specification change officially takes effect, the task can not be reconfigured again.
