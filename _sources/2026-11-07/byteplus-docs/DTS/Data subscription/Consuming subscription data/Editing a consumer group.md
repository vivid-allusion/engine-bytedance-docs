---
title: "Editing a consumer group"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/editing_a_consumer_group"
---

This topic introduces how to modify Kafka users' passwords and delete consumer groups on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A consumer group for built\-in middleware has been created. For detailed steps, refer to [Creating a new consumer group](https://docs.byteplus.com/en/docs/DTS/adding_a_consumer_group).

<span id=".5L-u5pS55raI6LS557uE5a-G56CB"></span>
## Modify consumer group password


1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data subscription**.

4. On the **Data subscription list ** page, click the target data subscription task name.

5. On the page of the target data subscription task, click **Data consumption**.

6. On the **Data consumption group** tab, select **Action** column under the target consumption group  **...**   **\> Modify password**.

7. In the **Modify password** dialog box, set and confirm the password. The password rules are as follows:

   * The length must be between 8 and 32 characters.

   * It contains at least three of the following: uppercase letters, lowercase letters, digits, and special characters. Special characters are `_#!@$%^&*()+=-`.

8. Click **OK**.


<span id=".5Yig6Zmk5raI6LS557uE"></span>
## Delete a consumer group


1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data subscription**.

4. On the **Data subscription list ** page, click the target data subscription task name.

5. On the page of the target data subscription task, click **Data consumption**.

6. On the **Data consumption group** tab, select **Action** column under the target consumption group  **...**  \> **Delete**.

7. In **Are you sure you want to delete the selected consumer group? ** dialog box, click **Delete**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Deleted tasks can not be recovered, and executed operations will not be rolled back. Proceed with caution.   </div>
   

<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[UpdateSubscriptionGroup](https://docs.byteplus.com/en/docs/DTS/updatesubscriptiongroup) |Call the UpdateSubscriptionGroup API to modify consumer group information. |
|[DeleteSubscriptionGroup](https://docs.byteplus.com/en/docs/DTS/deletesubscriptiongroup) |Call the DeleteSubscriptionGroup API to delete a consumer group. |
