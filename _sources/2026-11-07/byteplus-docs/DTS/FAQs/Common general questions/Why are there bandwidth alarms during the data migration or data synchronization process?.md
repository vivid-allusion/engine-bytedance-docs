---
title: "Why are there bandwidth alarms during the data migration or data synchronization process?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Why_are_there_bandwidth_alarms"
---

* **Possible cause 1**: Insufficient bandwidth.

   **Solution**: You need to prepare sufficient egress bandwidth before data migration or data synchronization, otherwise, the migration or synchronization rate will be affected.

* **Possible cause 2**: Data verification task occupies bandwidth, resulting in bandwidth shortage alarms.

   **Solution**: You can perform data verification after the data migration or data synchronization after the task is complete or during business off\-peak hours.
