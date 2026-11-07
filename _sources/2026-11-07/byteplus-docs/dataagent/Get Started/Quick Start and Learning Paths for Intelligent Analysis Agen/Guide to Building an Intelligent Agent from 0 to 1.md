---
title: "Guide to Building an Intelligent Agent from 0 to 1"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Guide_to_Building_an_Intelligent_Agent_from_0_to_1"
---

This article provides a comprehensive guide to the entire process, from account registration and purchase and activation to publishing and using the intelligent agent. It covers key steps such as project creation, data preparation, intelligent agent configuration, and usage, helping users quickly build an intelligent agent.

<span id="5b0f320a"></span>
# Overall process

The overall process for building an intelligent agent from 0 to 1 is as follows. The system administrator (main account) can follow this process to build an intelligent agent for users.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3366ee8251f9429dbf901d4a7254074c~tplv-goo7wpa0wc-image.image) </span>

<span id="7e7d8c11"></span>
# Prerequisites


* Complete account registration, real\-name authentication, and purchase and activation.


<span id="c4818025"></span>
# Precautions


* Building an intelligent agent requires system administrator permissions. Please use the Volcano Engine main account to perform this operation. For related permission information, refer to [Permission Management](https://docs.byteplus.com/docs/dataagent/Permission_Management).


<span id="0cb97036"></span>
# Create a project


1. Click DataAgent product homepage "Product Experience" to enter the account login page.

2. Log in to Volcano Engine using the registered main account username and password.

3. Enter the "Intelligent Agent" product page. On the "Console" page, click "+ Add Entry", search for and add "Intelligent Agent", then click the "Intelligent Agent" product found below.

4. Create a project. On the "Project List" page, click "Create Project".

   Enter the project name and creation reason. The project administrator defaults to the main account ID used to create the project. Click "Confirm".

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">SaaS environment: Project deletion is not supported. Please create new projects with caution. System administrators can go to the "System Management" \- "System Settings" page and enable "Only the primary account can create projects" under the new project settings. In this case, only the primary account can create projects, and sub\-accounts do not have permission to create projects.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Private deployment environment: Project administrators and system administrators can delete projects in "Management Center" \- "Project Management".   </div>
   

5. Enter the project space. Click the "Project Search Bar", select the newly created "Test Project 1", and view the project content. The new project content is empty.


<span id="9af86d23"></span>
# Prepare data

This section only shows the quick start process for data preparation. For detailed steps, refer to [Data Preparation Overview](https://docs.byteplus.com/docs/dataagent/Data_Preparation_Overview).


1. Enter the dataset creation page. Select the newly created project space, click "Data Preparation" \- "Dataset".

2. Create a dataset. Click "Create" \- "Create Dataset".

   You can choose to upload Excel, CSV, and other data here. If you click "Other", you will be redirected to the data connection page.

3. Select the data connection method and complete the data connection. DataAgent provides multiple data connection methods. You can select the corresponding data connection based on the type of data source. For detailed step\-by\-step guidance and parameter descriptions for data connections, see [Overview of Data Connection](https://docs.byteplus.com/docs/dataagent/Overview_of_Data_Connection).

   Select the Excel upload method, click "Upload File", choose the file to upload, click "Next", and after confirming the data preview is correct, click "Confirm".

4. Create a dataset using the data connection. After completing [Overview of Data Connection](https://docs.byteplus.com/docs/dataagent/Overview_of_Data_Connection), the user can proceed to create a dataset. On the "Data Preparation" \- "Data Connection" page, select a data connection, click "Apply" \- "Create Dataset" to enter the data modeling page.

5. Perform data modeling. Drag the data table from the data connection onto the canvas, and select the connection method as direct connection or extraction. Different data sources support different data connection methods; for the differences between direct connection and extraction, see [Overview of Data Connection](https://docs.byteplus.com/docs/dataagent/Overview_of_Data_Connection) . In addition, you can perform operations such as custom SQL, model configuration, data filtering, synchronization configuration, and field configuration. For details, see [Overview of Dataset Creation](https://docs.byteplus.com/docs/dataagent/Overview_of_Dataset_Creation).

   
   |Connection methods |Applicable scenarios |
   |---|---|
   |Direct connection |Suitable for scenarios with small data volumes, where timely viewing of data changes is required, or for querying a single OLAP wide table. |
   |Extraction |Suitable for scenarios involving large data warehouse tables or where accelerated queries are desired through extraction. |
   

   Click "Save" and set relevant dataset information, including the dataset name, description, usage instructions, and path. After confirming the information is correct, click "Confirm". Creating a dataset takes some time. Please wait a moment.

6. Enable DataAgent analysis capabilities for the dataset. After the dataset is created, you can view the data on the "Data Preparation" \- "Dataset" page. To use this dataset as a DataAgent dataset, click "Enable DataAgent analysis capabilities". According to the actual data, select whether to use the entire table and whether to synchronize in real time, then click "Confirm" to enable vectorization.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When the vectorization status shows <strong>"Success",</strong> the created dataset can be configured in the agent. The expected waiting time is about 15 minutes.   </div>
   

   The parameter descriptions for enabling DataAgent analysis capabilities are as follows:

   
   |Parameters |Description |
   |---|---|
   |Is the dataset a full table |* Full table: A full table contains all data and overwrites old data when updated.<br><br>* Incremental table: An incremental table contains only new or changed data and appends data when updated. |
   |Is the dataset synchronized in real time |* Yes: Synchronizes source data changes in real time.<br><br>* No: Not real\-time, updates periodically. |
   |High cardinality configuration |For dimensions that are frequently mentioned in user questions and have more than 1,000 dimension values, you can specify the number of dimension values to be vectorized. For example: store name, customer name. This optimizes the processing efficiency for massive numbers of dimension values and avoids matching delays or errors caused by excessive dimension values.<br><br>Click "High cardinality dimension configuration" \- "+Add" to add dimensions and the number of dimension values. |
   

   On the dataset page, you can also preview data, set row and column permissions, and modify the dataset. For details, see [Overview of Dataset Management](https://docs.byteplus.com/docs/dataagent/Overview_of_Dataset_Management) and [Dataset List Overview](https://docs.byteplus.com/docs/dataagent/Dataset_List_Overview).

7. In addition, during the process of creating a data connection and dataset, if further data cleaning or transformation is required, after creating the data connection in **Step 3**, click "Application" \- "Create visual modeling" to enter the "Data preparation" \- "Visual modeling" page. Create a visual modeling task to further process the raw data using operators, and then create the dataset. For more details, see [Overview of Visual Modeling](https://docs.byteplus.com/docs/dataagent/Overview_of_Visual_Modeling).


<span id="b1e2e543"></span>
# Create agent

After completing data preparation, proceed to create agent.


1. Click "Agent" in the operation bar to enter the agent usage page.

   If no agents have been created yet, initially, only a default Data Agent is visible in the agent list on the left. This agent only supports uploading a small amount of data (no more than 100MB) for in\-depth research Q&A and does not support switching to "Intelligent Q&A" mode.

2. Click "Admin console" to enter the agent list page.

3. Click "Create agent". If no agents have been created yet, the agent list is empty at first. To create a new agent, click "+Create agent".

4. Enter the agent configuration page. After clicking to create agent, you will enter the agent configuration page and start agent configuration operations.


<span id="c2934cb9"></span>
# Configure agent

Enter the agent configuration page to perform two essential agent usage configurations: basic information configuration and dataset configuration. To set recommended questions, summary cards, or perform advanced operations such as Feishu endpoint configuration, Prompt configuration, or knowledge configuration, see [Overview of Creation and Configuration Procedures](https://docs.byteplus.com/docs/dataagent/Overview_of_Creation_and_Configuration_Procedures).


1. Perform basic configuration. Click "Basic information" \- "General configuration" to set up the agent, including avatar, name, description, and introduction.

2. Set the agent administrator. Users can search for account IDs here and add the member as an administrator for this intelligent agent. The intelligent agent administrator can configure, publish, take offline, delete, and add members to the intelligent agent. For details, see [Agent permissions](https://docs.byteplus.com/docs/dataagent/Detailed_Explanation_of_User_Permissions#4efb3f5c).

3. Add members to the intelligent agent. Users can search for users or user groups here to add members to the intelligent agent. Only intelligent agent members can view and use the intelligent agent in the intelligent agent list on the left side of the intelligent agent usage page. For detailed steps on creating sub\-accounts, adding new users, and granting users basic permissions to use the intelligent agent, refer to [Intelligent Analysis Agent Administrator Quick Start Guide](https://docs.byteplus.com/docs/dataagent/Intelligent_Analysis_Agent_Administrator_Quick_Start_Guide).

4. After confirming that the settings are correct, click "Save".

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the agent administrator is not in the member list, they will be automatically added after saving the settings.   </div>
   

5. After completing the basic information configuration, proceed to "Dataset configuration".

   1. Go to the "**Dataset configuration**" module of the intelligent agent.

   2. Click "**Add now**" in the center.

   3. Search for the datasets you need to add. This page supports selecting multiple datasets at once.

   4. After clicking "**Confirm**", the datasets will be added successfully. You can continue to add other datasets or remove them later.

      In addition, you can configure the semantic model, knowledge base, and filtering for datasets. For more information about these features, refer to [Dataset Configuration](https://docs.byteplus.com/docs/dataagent/Dataset_Configuration).


<span id="2844edcb"></span>
# Publish the intelligent agent


1. Basic information configuration and dataset configuration are the two essential configurations for using the intelligent agent. After completing these, you need to click the "Publish" button in the upper right corner. Only then will the intelligent agent appear in the published intelligent agent list and be available for use.

2. After publishing, click "Go to intelligent agent" to go to the intelligent agent usage page and test the intelligent agent's usage.

3. Users with intelligent agent permissions can click the intelligent agent in the "Published" intelligent agent list to enter the intelligent agent usage page.

4. The intelligent agent list on the left side of the intelligent agent usage page displays all intelligent agents that users have permission to access. Click to select an intelligent agent to start a conversation.


<span id="7749ccef"></span>
# Use the intelligent agent


1. Log in to the DataAgent product using account and password. Click "Agent" \- "Published", select an authorized agent, and enter the conversation page to use the intelligent analysis agent.

2. After entering the agent usage interface, click the switch button in the dialog box to toggle between the "Smart Query" and "In\-depth Research" features.

3. Users can click the dialog box to select a recommended question to ask, or directly enter a question to ask.

   
   |Natural language questions |Recommended questions |
   |---|---|
   |* The main usage of the agent allows users to directly describe their data query requirements to the agent in text. After receiving a reply, users can also click "Follow\-up" to continue interacting with the agent regarding related questions.<br><br>* When querying data with the agent, there is no need to select a dataset; the agent will automatically query data in the configured datasets. |* Recommended questions are provided below the dialog box, and users can click any recommended question to directly query data.<br><br>* Recommended questions support custom configuration. For specific configuration methods, see [Overview of Creation and Configuration Procedures](https://docs.byteplus.com/docs/dataagent/Overview_of_Creation_and_Configuration_Procedures). |
   

   * For more instructions on using analysis agents, refer to [Intelligent Query Agent](https://docs.byteplus.com/docs/dataagent/Intelligent_Query_Agent), [Deep Research Agent](https://docs.byteplus.com/docs/dataagent/Deep_Research_Agent), [Web Search](https://docs.byteplus.com/docs/dataagent/Web_Search), [Knowledge Document Configuration](https://docs.byteplus.com/docs/dataagent/Knowledge_Document_Configuration).

   * To integrate a published intelligent analysis agent into office software for use, or to use the intelligent analysis agent directly by calling OpenAPI, refer to [Intelligent Analysis Agent Third-Party Integration Guide](https://docs.byteplus.com/docs/dataagent/Intelligent_Analysis_Agent_Third-Party_Integration_Guide), [Invocation Methods](https://docs.byteplus.com/docs/dataagent/Invocation_Methods).
