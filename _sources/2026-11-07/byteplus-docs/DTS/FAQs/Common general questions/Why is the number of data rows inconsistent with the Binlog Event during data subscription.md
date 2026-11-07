---
title: "Why is the number of data rows inconsistent with the Binlog Event during data subscription?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/why_is_the_number_of_data_rows_inconsistent"
---

This topic uses Kafka consuming MySQL data as an example to introduce the working mechanism of Kafka consuming MySQL Binlog.

The MySQL Binlog Event is the message content of Kafka, and one Binlog Event may contain multiple rows of data. Kafka only transmits these Binlog Events as messages. The details are as follows:


* **MySQL Binlog Event**

   * Binlog Event: MySQL is used to record structured logs of Database changes (for example, `INSERT`, `UPDATE`, `DELETE`). A Binlog Event can contain one or more row changes in MySQL.

   * Multiple row changes: A Binlog Event can correspond to a data modification action and may contain multiple rows of data. For example, a complex `UPDATE` action can modify multiple rows of data, and these changes are recorded in one Binlog Event.

* **Kafka as the transmission medium for Binlog Event**

   * Message content: When a Binlog Event is transmitted to Kafka, the content of the Kafka message is the Binlog Event, not the specific row data. In fact, every Kafka message contains a combination of one or more row change events.

   * Number of messages: In Kafka, the number of messages is actually determined by the number of Binlog Events, rather than the specific number of rows. Since a Binlog Event may contain multiple rows of data changes, there is no direct linear relationship between the number of messages and the number of rows changed in Kafka.


Therefore, messages in Kafka reflect the number of Binlog Events rather than the specific number of rows.
