---
title: "Creating session resources"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Creating_session_resources"
---

This topic describes how to create a session resource in the AgentKit console. After creation, AgentKit can use this resource to store and manage application session data.

<span id="DK2NVhFx"></span>
## Usage notes

Currently, only [Serverless PostgreSQL‌](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Creating_a_workspace?lang=en) session resources can be created. If you want to use an [RDS PostgreSQL](https://docs.byteplus.com/en/docs/RDS_for_PG/about_rds_for_postgresql) or [RDS MySQL](https://docs.byteplus.com/en/docs/RDS_for_MySQL/about_rds_for_mysql) session resource, first create the instance, database, and account in the corresponding product console, and then import the database for use in AgentKit. For more information, see [Importing session resources](https://docs.byteplus.com/en/docs/agentkit/Importing_session_resources).

<span id="cwGFTgBJ"></span>
## Serverless PostgreSQL billing instructions

When you create and use the Serverless PostgreSQL database service in AgentKit, the fees incurred are independently charged by the Serverless PostgreSQL service according to its own billing rules. **AgentKit does not charge or collect these fees**. For details, refer to [Billing items and prices](https://docs.byteplus.com/en/docs/aidap/Billing_items_and_prices).

<span id="BSNVmmKp"></span>
## Procedure


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Basic Components \> Sessions".

3. Click the "Create resource" button.

4. If this is the first time you create a resource, the system prompts you to activate the **Serverless PostgreSQL (AIDAP)**  service. Follow the on\-screen instructions to complete the activation before continuing to create the resource.

5. In the pop\-up dialog box, configure the following parameters.

   
   |Parameter​ |Description |
   |---|---|
   |Term |Specify a name for the session database resource.<br><br>We recommend using a name that reflects its purpose or business scenario to make it easier to identify and manage the resource later in the resource list. |
   |Type |Currently, only Serverless PostgreSQL is supported.<br><br>> BytePlus Serverless PostgreSQL is a lightweight, maintenance\-free PG database billed on an elastic, Pay\-as\-you\-go basis. In the AgentKit Sessions feature, it stores the short\-term context of agent conversations, and is suitable for business scenarios with low system load that require elastic resource scaling. |
   |Access mode |Select the network method used by the AgentKit agent runtime to access the session resource. The session resource is mainly used to store session data.<br><br><br>* Public network: the default access method. This option cannot be unselected.<br><br>   > The public network connection provided by the **Serverless PostgreSQL** service has limited bandwidth and carries some stability risk. We strongly recommend using the public network connection only for testing and validation, and using a private network connection for production business scenarios.   <br>   <br><br>* Private network: Can be enabled in addition to public network access. If the agent runtime is deployed in a VPC, or if you want session data to travel over a private network link for better security and stability, we recommend enabling private network access and selecting a private network and subnet that are consistent with those of the AgentKit agent runtime. If no VPC is available, click **Create VPC** to create one, and then refresh the list and select again. Only one subnet can be selected for each availability zone. |
   

6. Click "Confirm" to complete the operation.
