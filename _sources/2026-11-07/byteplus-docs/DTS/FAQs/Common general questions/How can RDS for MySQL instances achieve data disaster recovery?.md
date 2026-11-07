---
title: "How can RDS for MySQL instances achieve data disaster recovery?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/How_can_RDS_for_MySQL"
---

The RDS for MySQL instance can pass Database Transmission Service (DTS) to achieve real\-time synchronization of data between the primary instance and the remote disaster recovery instance. Both the primary instance and the disaster recovery instance are deployed with a primary\-secondary high\-availability architecture. In scenarios such as sudden disasters in the region where the primary instance is located, which may lead to the inability to connect to either the primary or secondary instance, you can switch the disaster recovery instance to act as the primary instance. After modifying the database connection address on the application side, normal business access can be restored. For specific procedures, refer to [Creating a remote disaster recovery instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_data_synchronization_task).
