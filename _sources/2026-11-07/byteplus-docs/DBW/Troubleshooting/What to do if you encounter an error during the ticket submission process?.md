---
title: "What to do if you encounter an error during the ticket submission process?"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/error_during_the_ticket_submission_process"
---

When submitting a ticket, you may encounter the following types of errors:


* **Pre\-check failed**

   If after submitting the ticket, the **ticket status** shows as **pre\-check failed**, you can resolve it by following these steps:

   1. On the **ticket list** page, click the ticket ID.

   2. On the **ticket details** page, hover over the check result of the failed item to view the reason for failure.

   3. Click **Edit Ticket**, and in the **Edit Ticket** dialog, modify the SQL statement based on the failure prompt.

   4. Click **Submit Ticket**.

* **Execution failed**

   If the ticket pre\-check is successful but execution fails, it is usually due to the following reasons:

   * Insufficient permissions: If you encounter insufficient permissions, you can contact the primary account of BytePlus or the system administrator of DBW to add the relevant permissions to your account. For detailed steps, refer to [Granting user permissions](https://docs.byteplus.com/en/docs/DBW/user-management-for-mysql). After the authorization is completed, you need to resubmit the ticket. For detailed steps, refer to [Creating a ticket](https://docs.byteplus.com/en/docs/DBW/creating-ticket-for-mysql).

   * MySQL native errors: If you encounter MySQL native errors such as syntax errors, key conflicts, data type mismatches, table not found, field not found, permission issues, or connection issues, you need to check and modify the MySQL errors yourself. After completing the modifications, you need to resubmit the ticket. For detailed steps, refer to [Creating a ticket](https://docs.byteplus.com/en/docs/DBW/creating-ticket-for-mysql).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you encounter other unresolved errors, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to contact technical support.</div>
