---
title: "Importing session resources"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Importing_session_resources"
---

This topic describes how to import an existing database resource as an AgentKit session resource. After the import, AgentKit can use this database to store and manage application session data.

<span id="1hcNAHc3"></span>
## Prerequisites


* (Optional) If you are using a [Serverless PostgreSQL](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Creating_a_workspace) database as your AgentKit session resource, make sure you have [created an instance](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Creating_a_workspace), [created a branch](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Creating_a_branch) for the instance, and created [compute resources](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Creating_a_compute), [an account](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Creating_an_account), and [a database](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Creating_a_database) for the branch.

* (Optional) If you are using an [RDS PostgreSQL](https://docs.byteplus.com/en/docs/RDS_for_PG/about_rds_for_postgresql) database as your AgentKit session resource, make sure you have [created an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance) and [created a database and account](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_databases_and_accounts) for the instance.

* (Optional) If you are using an [RDS MySQL](https://docs.byteplus.com/en/docs/RDS_for_MySQL/about_rds_for_mysql) database as your AgentKit session resource, make sure you have [created an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/create_instance) and [created a database and account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_databases_and_accounts) for the instance.


<span id="W3ugiQgj"></span>
## Billing

When you use the following database services in AgentKit, each service charges fees independently under its own billing rules. **AgentKit does not charge or collect these fees**.


* **Serverless PostgreSQL**: Charges are based on the compute resources and storage capacity actually used. For details, see [Billing items and prices](https://docs.byteplus.com/en/docs/aidap/Billing_items_and_prices).

* **RDS PostgreSQL**: Charges are based on the usage of resources such as instance type and storage capacity. For details, see [Billing items and prices](https://docs.byteplus.com/en/docs/RDS_for_PG/charge_items_and_price).

* **RDS for MySQL**: Charges may include fees for instance types, data storage, backup storage, database proxy services, and public network traffic. The charges depend on your actual usage. For details, see [Billing items and prices](https://docs.byteplus.com/en/docs/RDS_for_MySQL/charge_items_and_price).


<span id="v6efhImC"></span>
## Importing session resources


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Basic Components \> Sessions".

3. Click the "Import resource" button.

4. In the dialog box that appears, select the target resource type and configure the parameters based on the table below.

   * **Serverless PostgreSQL**

      > Suitable for scenarios with low system load that require elastic, on\-demand scaling.      
      

      
      |Parameter |Description |
      |---|---|
      |Workspace |Select the workspace that hosts the Serverless PostgreSQL resource.<br><br>> A workspace is used to centrally manage the branches, compute, accounts, and databases under an instance. Select a workspace where the required resources have already been prepared. |
      |Branch |Select the database branch used to store session data.<br><br>> A branch is an isolated database environment within a workspace. We recommend that you select a business branch already prepared for AgentKit to avoid mixing it with test data or other business data. |
      |Computing power |Select the compute resource associated with this branch.<br><br>> The compute resource determines the database's capacity to process session read and write requests. Select a suitable compute resource based on your application's session volume and concurrent access load. |
      |Account |Select the database account that AgentKit uses to access this branch's database.<br><br>> This account must have permission to access the target database and perform read and write operations on session data. |
      |Database |Select the database used to store AgentKit session data.<br><br>> After the import, AgentKit writes session\-related data to this database. Avoid selecting a database that stores unrelated business data. |
      

   * **RDS PostgreSQL**

      > Suitable for scenarios with a large volume of session data, high access load, or where you need a fixed database instance to host session data.      
      

      
      |Parameter |Description |
      |---|---|
      |Instance |Select the RDS PostgreSQL instance used to host session data. Make sure this instance already has a database and account created, and has a specification that can handle the session read/write load required by your business. |
      |Connection |Select the connection method AgentKit uses to access this instance. Choose a reachable connection address based on the instance's network environment to ensure AgentKit can properly access the target instance. |
      |Account |Select the database account that AgentKit uses to access this instance. This account must have permission to access the target database and perform read and write operations on session data. |
      |Database |Select the database used to store AgentKit session data. We recommend that you use a database created specifically for the Sessions feature to facilitate permission control and management. |
      

   * **RDS MySQL**

      > Suitable for scenarios where you already use MySQL, or where you want to host session data on an RDS MySQL instance.      
      

      
      |Parameter |Description |
      |---|---|
      |Instance |Select the RDS MySQL instance used to store session data. Make sure this instance already has a database and account created, and has a specification that can handle the session read/write load required by your business. |
      |Connection |Select the connection method AgentKit uses to access this instance. Choose a reachable connection address based on the instance's network environment to ensure AgentKit can properly access the target instance. |
      |Account |Select the database account that AgentKit uses to access this instance. This account must have permission to access the target database and perform read and write operations on session data. |
      |Database |Select the database used to store AgentKit session data. We recommend that you use a database created specifically for the Sessions feature to facilitate permission control and data maintenance. |
      

5. Click "Confirm" to complete the operation.
