---
title: "Overview"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/data-security-overview"
---

Data Security provides DataLeap users with capabilities such as control over data permissions, data protection throughout the lifecycle, ensuring the security of big data assets.

In this platform, you can easily complete the management tasks such as applying for resources, approval, and data classification, with the following core functions:


* Data Permission Management

   Provides refined functions such as data permission application, permission approval, and permission audit, achieving minimal permission control, while making it easy for you to view the progress of each stage of the approval process and follow up in a timely manner. Details can be found in [Apply Permission](https://docs.byteplus.com/docs/dataleap/Apply_Permission), [Approve Applications](https://docs.byteplus.com/docs/dataleap/Approval_Applications), etc.

* Data Content Security Management

   Provides functionality for data behavior auditing, classification, data protection, etc., capable of quickly and timely identifying data with potential security risks, minimizing unauthorized data use, leakage, and abuse, thereby ensuring the security and reliability of data content.


<span id="_1-基本概念"></span>
## Restriction


* Sub\-accounts must have **ByteHouseCEStandardAccess** permission to manage ByteHouseCE data permissions on the **Data Security** side. The activation of sub\-accounts requires the following actions:

   1. The main account grants the sub\-account **ByteHouseCEStandardAccess** permission in the **access console**.

   2. The sub\-account logs in to the **ByteHouse CE Console** once.

* It is suggested that the main account should not grant the following permissions to sub\-accounts, otherwise these sub\-accounts will bypass **DataLeap\-Data Security** and possess super permissions for the corresponding data type.

   * ByteHouseCE: **ByteHouseCEFullAccess** policy, **system_admin** or **cluster_admin** roles.

   * ByteHouse CDW: **ByteHouseFullAccess** policy, **AccountAdmin** or **SystemAdmin** roles.


<span id="87399304"></span>
## Basic Concepts


|Name |Description |
|---|---|
|Datasource |Refers to the type of datasource; currently, data security supports datasource types such as LAS, EMR Hive, EMR StarRocks, ByteHouse CDW, ByteHouse CE, etc. |
|Resource Type |In the scenario of big data security, resources include databases, tables, row\-level\-access, data columns, etc.<br><br><br>* **Row Constraints**<br><br>   If the following conditions exist, administrators can set row constraints on the product.<br><br>   * For large tables (such as tables with significant traffic), granting access to the entire table poses a high risk.<br><br>   * Applicants are required to access the table based on specific conditions.<br><br>   * It is desired that different business units manage approvals, revocations, and other permission management autonomously.<br><br>* **Data Columns**<br><br>   Includes three types of columns: sensitive, ordinary, and encrypted. Initially, all fields start as ordinary columns. They can be set as sensitive columns through **Permission Settings**, and as encrypted columns through **Data Encryption**.<br><br>   * **Sensitive Columns**<br><br>      If there are several highly sensitive data columns in the table (for example, idcard, phone, etc.), users need to submit an application individually, and management can be finely controlled by column for revocation and authorization. At this time, administrators can set these as sensitive columns in the product. When setting, one can choose whether the original rights holders of the table need to apply for sensitive column permissions.<br><br>   * **Ordinary Column**<br><br>      Data columns not set as sensitive or encrypted do not require separate application for access rights.<br><br>   * **Encrypted Column**<br><br>      Table fields encrypted through data encryption tasks require separate application for decryption column permissions for accessing decrypted data; otherwise, only ciphertext is available for viewing. |
|Confidentiality Level |Data can be classified into different confidentiality levels, with confidentiality increasing from L1 to L4, meaning L1 has the lowest confidentiality level and L4 the highest. |
|Permission Audit |To ensure the reasonableness of authorizations and to avoid potential data security risks, both the authority owner and administrators can audit work orders for requested and proactive authorizations regularly through the permission audit feature. |
|Data Classification |Data classification and grading serve as a vital foundation for the refined management of data security, enabling support for security strategies through precise and comprehensive classification and grading. By classifying and grading data, organizations can recognize the specific value the data offers and determine an appropriate strategy to protect the integrity, confidentiality, and availability of data. |
|Data Encryption |By implementing visual static encryption tasks, encryption of table fields is completed, ensuring the protection of sensitive data. |
|Data Decryption |Data decryption is achieved through visual static decryption tasks. |
|Data Desensitization |Data desensitization is accomplished through visual static desensitization tasks, processing sensitive data. Through data desensitization, the genuine information in the raw data is hidden or altered, thereby preventing unauthorized users from accessing the true values of sensitive information. |


<span id="_2-基础角色"></span>
## **Basic Roles**

In data security scenarios, resource users can be divided into two roles based on their capabilities and the method of obtaining permissions: producers and managers.


* Producer: Refers to a DB admin or table owner who can set resource information, manage permissions, and by default does not participate in the approval of the application.

* Manager: Refers to the authority owner responsible for resource security. They participate in approvals, can set the approval process, and manage permissions for the resources they are responsible for.

   * Different resource levels can be subdivided into different authority owners, including Database Authority Owner, Table Authority Owner, Row Authority Owner, and Column Authority Owner.

   * Authority Owners can manage their own resources, as well as those at lower levels. Example: The authority owner of a database can manage both the database and the tables, rows, and columns within that database.


The capabilities of different roles are shown in the following table.


|Capability Classification |Producer (Warehouse Manager, Table Owner) |Manager (DB/Table/Row/Column Permission Owner) |
|---|---|---|
|Management capabilities (Authorize/Revoke/Settings Classification, etc.) |Supported |Supported |
|Set or Transfer Authority Owner Role |Supported, also supports modifying the permission owner for lower hierarchy resources. |Supported, also supports modifying the permission owner for lower hierarchy resources. |
|Resource Permission Granting Method |Default permissions, settings can be modified. |Must be applied for or explicitly authorized. |
|Permission Approval |Not supported, configuration possible later. |Supported |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If the producer is set as the authority owner, then the producer is the manager, possessing the capability to participate in the approval process as well.</div>


* <div data-tips="true" data-tips-type="tip">When setting up the approval process, the producer can be added as an approver.</div>



<span id="_3-权限申请类型"></span>
## **Application Types**

<span id="_3-1-主要流程"></span>
### Main Process

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81d4523845ea4165841d983564a15ef7~tplv-goo7wpa0wc-image.image) </span>

Databases, tables, rows, and columns are all treated as separate resource entities, with supported application types as follows:


* Database permission application

* Entire table permission application

* Row\-level access application

* Column application


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Entire table permissions include row\-level\-access permissions; when applying for row\-level\-access, you can apply for entire table permissions or by row.</div>


* <div data-tips="true" data-tips-type="warning">Entire table permissions do not include sensitive column and encryption column permissions; relevant column permissions must be applied for before their information can be used.</div>



<span id="_3-1-整库权限申请"></span>
### Database permission application

To avoid frequent table applications, DataLeap Data Security supports setting database granularity for applications, and it can be configured whether to open this application.

<span id="_3-2-整表权限申请"></span>
### Entire table permission application

Entire table permission application is the most common usage scenario. To avoid frequent row data applications, DataLeap Data Security supports setting entire table granularity for applications, and it can be configured whether to open this application.

Based on the specific settings of the manager for permissions, tables with row\-level access restrictions or sensitive columns may appear, allowing for individual applications.

<span id="_3-3-行限制申请"></span>
### Row\-level Access Application

If a table has row restrictions, you can apply for row\-level access as needed. The application supports submitting requests based on the enumerated values of controlled fields, and you can manually add enumerated values during the process.

For example, if a manager wants to control user access based on the field "city", and sets row restrictions "city = Beijing" and "city = Shanghai" and closes the entire table permission application, users can only apply for access based on the row restrictions "city = Beijing" and "city = Shanghai" subsequently. After the application, you can access data that meets certain filter conditions, such as where city = 'Beijing'. For a detailed example, see the **example explanation** section.

<span id="_3-4-敏感列申请"></span>
### Column Application

If a table has sensitive columns or encrypted columns set, you can apply as needed for access to sensitive columns or encrypted columns.

For example, if the manager has set up a sensitive column "city", then users must apply for permission for the sensitive column "city" before they can access data in the "city" column. For a detailed example, see the **example explanation** section.

<span id="_3-5-示例详解"></span>
### Example Explanation

Mr. Zhang has a data table with the following information: he has set row restrictions "sex=F" and a sensitive column "city".


|name |age |sex |city(Sensitive column) |
|---|---|---|---|
|zhangsan |71 |F |Beijing |
|lisi |58 |M |Guangzhou |
|wangwu |61 |M |Beijing |
|zhaoliu |46 |F |Tianjin |
|sunqi |64 |M |Shanghai |


After Mr. Zhang applies for different permissions, the accessible range varies.


* Apply for entire table permissions: You can query all data except sensitive columns.

   
   |name |age |sex |
   |---|---|---|
   |zhangsan |71 |F |
   |lisi |58 |M |
   |wangwu |61 |M |
   |zhaoliu |46 |F |
   |sunqi |64 |M |
   

   Example SQL query statement as follows.

   * Correct Example

      ```undefined
      select name,age,sex from db.table
      ```
      

   * Example of No Access

      ```undefined
      select name,city from db.table  /No sensitive column permission
      ```
      

* Apply for entire table permissions + Sensitive column "city": You can freely access all data in the table, SQL query statement example as follows.

   ```undefined
   select * from db.table
   ```
   

   ```undefined
   select name,city from db.table
   ```
   

* Apply for row\-level access "sex=F": You can view all data with "sex=F" excluding sensitive columns.

   
   |name |age |sex |
   |---|---|---|
   |zhangsan |71 |F |
   |zhaoliu |46 |F |
   

   Example SQL query statement as follows.

   * Correct Example

      ```plain
      select name,age,sex from db.table where sex = 'F'
      ```
      

   * Example of No Access

      ```plain
      select name,city from db.table where sex = 'F' /No sensitive column permission
      ```
      

      ```plaintext
      select * from db.table   /No permission for the entire table and sensitive columns
      ```
      

      ```plaintext
      select name,age,sex from db.table  /No permission for the entire table
      ```
      

* Apply row\-level access "sex=F" + sensitive column "city": view all data for "sex=F".

   
   |name |age |sex |city (Sensitive column) |
   |---|---|---|---|
   |zhangsan |71 |F |Beijing |
   |zhaoliu |46 |F |Tianjin |
   

   Example of an SQL query statement is as follows.

   * Correct example

      ```plaintext
      select * from db.table where sex = 'F'
      ```
      

      ```plaintext
      select name,sex,city from db.table where sex = 'F'
      ```
      

   * Example of unauthorized access

      ```plaintext
      select * from db.table  /No permission for the entire table, and must specify a WHERE clause in the SQL statement
      ```
      

      ```plaintext
      select name,sex from db.table  /No permission for the entire table, and must specify a WHERE clause in the SQL statement
      ```
