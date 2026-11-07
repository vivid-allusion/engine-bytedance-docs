---
title: "What if the approver cannot approve in time due to certain reasons?"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/why-total-number-of-session-on-session-management--different-number-of-connections-on-mysql-instance"
---

* Solution 1: You can contact the administrator of the main account for approval, as the main account can approve all tickets by default.

* Solution 2: Modify the approver. There are two scenarios for modifying the approver:

   * When enabling security control for the instance, the default approval process is selected: If it is the default approval process, you need to modify the DBA and Owner of the instance on the instance list page. For detailed steps, refer to [Enabling security control for RDS for MySQL instances](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql), [Enabling security control for NDB for MySQL instances](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control), [Enabling security control for RDS for PostgreSQL instances](https://docs.byteplus.com/en/docs/DBW/enabling-security-control), and [Enabling security control for RDS for SQL Server instances](https://docs.byteplus.com/en/docs/DBW/enabling-security-control_).

   * When enabling security control for the instance, a custom process is selected: If it is a custom approval process, you can modify the approver of the approval node in the instance approval process. For detailed steps, refer to [Editing approval nodes](https://docs.byteplus.com/en/docs/DBW/Approval_node_management#.57yW6L6R5a6h5om56IqC54K5).
