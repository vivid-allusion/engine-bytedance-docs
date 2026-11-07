---
title: "Modifying the account password for the source or target database of the data synchronization task"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/modifying_the_account_password_of_source_database_or_destination_database_of_a_synchronization_t"
---

When you change the database account password for data synchronization, you must update the corresponding password to the new password on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

[A data synchronization task has been created](https://docs.byteplus.com/en/docs/DTS/creating_and_initiating_a_synchronization_task).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.


3. In the left navigation bar, click **Data synchronization**.

4. On the **Synchronization task list** page, click the target task name.

5. On the **Task details** tab, locate the **Source database information** or **Target database information** area, and modify the database account password of the source or target database as needed.

6. Click the icon after the **Database account**<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png) </span>icon next to the Database account. In the **Modify password** dialog box, enter the new password for the target database account in the **Password** input box.

7. Click **Test connection** to verify if the database connection succeeded.

8. Click **OK**.
