---
title: "Integrating session resources in agents"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Integrating_session_resources_in_agents"
---

This topic uses [VeADK ](https://deepwiki.com/volcengine/veadk-python/7.5-prompt-optimization)as an example to describe how to integrate a session resource into your agent code. After integration, the agent can write session context to the specified session resource and read historical session information in subsequent conversations.

<span id="jbbdcv3C"></span>
## Prerequisites


* Python 3.10 or later is installed.

* VeADK is installed.

* A session resource has been [imported ](https://docs.byteplus.com/en/docs/agentkit/Deleting_session_resources)or [created](https://docs.byteplus.com/en/docs/agentkit/Creating_session_resources).

* You have [obtained an Access Key ID and Secret Access Key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey) in the BytePlus console. You can create and obtain an **Access Key ID** and **Secret Access Key** on the [Access Key Management](https://console.byteplus.com/iam/keymanage/) page. 


<span id="Wd0sb4og"></span>
## Step 1: Obtain and configure environment variables

When integrating a session resource into your agent, you need to configure the environment variables for the session resource first. You can complete this configuration using either of the following methods.


* Method 1: Associate the session resource in the agent runtime

   If the agent has been deployed or is planned to be deployed to the agent runtime, we recommend associating the session resource directly in the runtime. After association, the system automatically injects the required environment variables. You do not need to manually configure them in your code. For more information, see [Updating associated components](https://docs.byteplus.com/en/docs/agentkit/Updating_runtime_configuration).

* Method 2: Manually configure environment variables in your local development environment

   If you need to develop or test the agent locally, first obtain the environment variable information from the console, and then configure it in your local runtime environment.

   1. Obtain information of the configured environment.

      1. Log in the [AgentKit console](https://console.byteplus.com/agentkit). 

      2. In the left\-side navigation pane, select "Basic components \> Sessions".

      3. Click the target session resource ID to enter the "Basic information" tab.

      4. Click the "Integration code" tab to obtain the database configuration information for the session resource.

      5. (Optional) The console does not display the database password. If you have forgotten the password, click the "Original database" button, go to the "**Compute specification**" tab, click the "Connection" button, and obtain the database password from the **Parameters** section of the **connection string**.

   2. Configure environment variables.

      Based on the environment variable configuration information on the "Integration code" tab, complete the configuration in your local development environment, and make sure the process running your agent code can read these environment variables.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">When passing the password on the command line, wrap it in single quotes to prevent the shell from escaping special characters such as % and $, ensuring the original password is passed through unchanged. Avoid using the password unquoted or wrapping it only in double quotes, as this may cause characters to be parsed and result in password validation failures.      </div>
      

      
      <Tabs>
      <Tab zoneid="WxtD7Fki" title="Serverless PostgreSQL">
      <TabTitle>Serverless PostgreSQL</TabTitle>
      
      ```Python
      export DATABASE_POSTGRESQL_HOST=cp-gutsy-steep-aee4****.pg.aidap-global.ap-southeast-1.volces.com  #Database address
      export DATABASE_POSTGRESQL_USER=user_admin          #Database username
      export DATABASE_POSTGRESQL_DATABASE=my_s_pg         #Database name
      export DATABASE_POSTGRESQL_PASSWORD=****            #Database password
      ```
      
      
      
      
      
      </Tab>
      <Tab zoneid="O9GTM3GK" title="MySQL">
      <TabTitle>MySQL</TabTitle>
      
      ```Python
      export DATABASE_MYSQL_HOST=mysql7057f1e1****.rds.ivolces.com:3306 #Database address
      export DATABASE_MYSQL_USER=user_admin       #Database username
      export DATABASE_MYSQL_DATABASE=my_sql       #Database name
      export DATABASE_MYSQL_PASSWORD=***          #Database password
      ```
      
      
      
      
      
      </Tab>
      <Tab zoneid="jn1fGRll" title="PostgreSQL">
      <TabTitle>PostgreSQL</TabTitle>
      
      ```Python
      export DATABASE_POSTGRESQL_HOST=postgres4b7435db****.rds-pg.ivolces.com:5432 #Database address
      export DATABASE_POSTGRESQL_USER=user_admin         #Database username
      export DATABASE_POSTGRESQL_DATABASE=my_pg          #Database name
      export DATABASE_POSTGRESQL_PASSWORD=****           #Database password
      ```
      
      
      
      
      
      </Tab>
      </Tabs>
      


<span id="3qaSIptE"></span>
## Step 2: Code integration


1. Install Python dependencies.

   * **Serverless PostgreSQL and PostgreSQL**

      ```Bash
      pip install veadk-python greenlet psycopg[binary]
      ```
      

   * **MySQL**

      ```Bash
      pip install veadk-python
      ```
      

2. Integration example.

   Replace the ShortTermMemory parameter value based on your needs. Valid values:

   * `postgresql`: Serverless PostgreSQL and RDS PostgreSQL.

   * `mysql`: RDS MySQL.

   ```Python
   import asyncio
   from veadk import Agent, Runner
   from veadk.memory.short_term_memory import ShortTermMemory
   
   app_name = "app_short_term_1"
   user_id = "user_short_term_1"
   session_id = "session_short_term_1"
   
   agent = Agent()
   short_term_memory = ShortTermMemory(    
       backend="postgresql", # Specify the storage method for ShortTermMemory. Valid values: postgresql and mysql. When you specify postgresql, Serverless PostgreSQL and RDS PostgreSQL are included.
   )
   runner = Runner(
       agent=agent, short_term_memory=short_term_memory, app_name=app_name, user_id=user_id
   )
   
   async def main():
       response1 = await runner.run(
           messages="I bought 20 ice creams on July 15th.", session_id=session_id
       )
       print(f"response of round 1: {response1}")
   
       response2 = await runner.run(
           messages="When did I buy the ice cream?", session_id=session_id
       )
       print(f"response of round 2: {response2}")
   
   if __name__ == "__main__":
       asyncio.run(main())
   ```
   


<span id="UZPKgtkj"></span>
## Deploy the agent to the cloud\-based production environment

After completing local development and testing, you can deploy the agent integrated with the session resource to the agent runtime.


1. Package the code: Ensure all dependencies are correctly specified in `requirements.txt`.

2. Deploy the agent to the agent runtime. During deployment, the system automatically injects the necessary environment information. This eliminates the need to manually configure the session resource environment variables. The following two deployment methods are currently supported:

   * [Creating runtimes (CLI tool)](https://docs.byteplus.com/en/docs/agentkit/Creating_runtime_via_CLI_tool)

   * [Creating runtimes (console)](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console)
