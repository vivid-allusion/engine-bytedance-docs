---
title: "Quick start guide for SQL review tickets"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Quick_start_guide_for_SQL_review_tickets"
---

DBW provides the SQL review ticket feature, which helps you check for syntax errors and performance issues in SQL statements before submission. This enhances the standardization and systematization of database management, reduces human errors, and ensures the security, accuracy, and compliance of database operations. This topic explains how to create an SQL review ticket on the DBW console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A RDS for MySQL instance has been created and is in the running state. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id=".5oiR5pivLWRidy3nmoTns7vnu5_nrqHnkIblkZg="></span>
## I am a DBW administrator

There is a primary account A, a sub\-account B, and a target instance Test. Sub\-account B intends to execute SQL statements in the target instance Test. Before execution, they need to confirm that the SQL statements do not have syntax or performance issues.

<span id=".5q2l6aqk5LiA77ya5a2Q6LSm5Y-3LWIt5bey55Sz6K-35oiQ5Li6LWRidy3nrqHnkIblkZg="></span>
### Step 1: Sub\-account B has applied to become a DBW administrator


1. Sub\-account B logs on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket List** page, click **Permission application**.

5. On the **Permission application** tab, click **Apply for permission** and configure the relevant parameters.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <strong>DBW role</strong> needs to be set as <strong>Administrator</strong>.   </div>
   

6. Click **Submit ticket**.

7. Primary account A logs on to the [DBW console](https://console.byteplus.com/dbw) to approve the ticket.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information about applying for roles, refer to <a href="https://docs.byteplus.com/en/docs/DBW/user-management">User management</a>.</div>


<span id=".5q2l6aqk5LqM77ya5a2Q6LSm5Y-3LWIt55Sz6K-355uu5qCH5a6e5L6LLXRlc3Qt5p2D6ZmQ44CC"></span>
### Step 2: Sub\-account B applies for permission to the target instance Test.


1. Sub\-account B logs on to the [DBW Console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region. 

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket List** page, click **Permission application**.

5. On the **Permission application** tab, click **Apply for permission** and configure the relevant parameters.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Select <strong>Authorized instance</strong> for <strong>Application type</strong>, <strong>RDS for MySQL</strong> for <strong>Database type</strong>, and choose the target instance for <strong>Authorized instance</strong>.   </div>
   

6. Click **Submit application**.

7. Primary account A logs on to the [DBW Console](https://console.byteplus.com/dbw) to approve the ticket.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information on applying for permissions, refer to <a href="https://docs.byteplus.com/en/docs/DBW/Creating_an_operation_permission_ticket">Creating operation permission tickets</a>.</div>


<span id=".5q2l6aqk5LiJ77ya5Yib5bu65a6J5YWo6KeE5YiZ"></span>
### Step 3: Create a security rule


1. Sub\-account B logs on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Security rules**.

4. On the **Security rule sets** page, click **Create security rule set**.

5. In the **Create security rule set** dialog, set the **Rule set name** and **Database type**.

   Take **RDS for** **MySQL** as an example for **Database type**.

6. Click **OK**.

   Custom SQL review security rules are currently not supported. For more information on creating security rule sets, refer to [Security rule set management](https://docs.byteplus.com/en/docs/DBW/security-rule-set-management-for-mysql).


<span id=".5q2l6aqk5Zub77ya5byA5ZCv5a6J5YWo566h5o6n"></span>
### Step 4: Enable security control


1. Sub\-account B logs on to the [DBW Console](https://console.byteplus.com/dbw).

2. On the top menu bar, select a region.

3. On the left navigation bar, click **Instance list** .

4. On the **Instance list** page, select the database type as **RDS for** **MySQL** in the top\-left corner, and click the pen icon under the **Security control** column of the target instance.

5. In the **Set security control** dialog box, configure the relevant parameters to enable security control for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more information on enabling the security rule set for an instance, refer to <a href="https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql">Enabling security control</a>.   </div>
   

<span id=".5q2l6aqk5LqU77ya5Yib5bu6LXNxbC3lrqHmoLjlt6XljZU="></span>
### Step 5: Create a SQL review ticket


1. Sub\-account B logs on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select a region.

3. On the left navigation bar, select **Data management** \>**Ticket list**.

4. On the **Ticket List** page, click **SQL** r**eview**

5. In the **SQL** **review** tab, click **Create SQL review ticket**

6. In the **SQL** r**eview ticket** control panel, configure the parameters for the SQL review ticket

7. Click **Submit ticket**

   After submission, the SQL text in the ticket will be validated according to the system's security rules. For more information on creating SQL review tickets, refer to [Creating SQL review tickets](https://docs.byteplus.com/en/docs/DBW/Creating_an_SQL_review_ticket).


<span id=".5oiR5pivLWRidy3mma7pgJrnlKjmiLc="></span>
## I am a DBW normal user

There is currently a sub\-account C applying to become a normal user of DBW and needs to create an SQL review ticket.

<span id=".5q2l6aqk5LiA77ya55Sz6K-35oiQ5Li6LWRidy3nmoTmma7pgJrnlKjmiLfjgII="></span>
### Step 1: Apply to become a normal user of DBW.


1. Sub\-account C logs on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, click **Permission application**.

5. On the **Permission application** tab, click **Apply for permission** and configure the relevant parameters.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Set the <strong>DBW Role</strong> to <strong>normal user</strong>.   </div>
   

6. Click **Submit ticket**.

7. Primary account A or sub\-account B logs on to the [DBW console](https://console.byteplus.com/dbw) to approve the ticket.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more information on applying for roles, refer to <a href="https://docs.byteplus.com/en/docs/DBW/user-management">User management</a>.   </div>
   

<span id=".5q2l6aqk5LqM77ya5Yib5bu6LXNxbC3lrqHmoLjlt6XljZU="></span>
### Step 2: Create an SQL review ticket

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The instance for creating an SQL review ticket has enabled security control. For detailed steps on enabling security control by a DBW administrator, refer to <a href="https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql">Enabling security control</a>.</div>



1. Sub\-account C logs into the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, click **SQL** r**eview**.

5. In the **SQL** **review** tab, click **Create SQL review ticket**.

6. In the **SQL** r**eview ticket** control panel, configure the parameters for the SQL review ticket.

7. Click **Submit ticket**.

   After the ticket is submitted, the SQL text in the ticket will be validated according to the security rules provided by the system. For more information on creating an SQL review ticket, refer to [Creating SQL review tickets](https://docs.byteplus.com/en/docs/DBW/Creating_an_SQL_review_ticket).
