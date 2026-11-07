---
title: "Document Database for MongoDB skill user guide"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/Volcano_Engine_Document_Database_for_MongoDB_skill_user_guide"
---

This topic describes how to integrate and use the BytePlus Document Database for MongoDB skill in Agent applications, helping you quickly implement intelligent querying and information retrieval for MongoDB instances.

<span id="ZtXLy5vF"></span>
## Background information

In traditional usage scenarios, users typically need to query information and monitor the status of MongoDB instances by using the console or calling APIs. In complex usage scenarios that involve multiple sub\-scenarios, users often need to click repeatedly and switch between pages, resulting in a lengthy operational workflow with considerable repetitive work. This also places certain demands on user experience and operational efficiency.

With the BytePlus Document Database for MongoDB skill, you can directly interact with the Agent using natural language. The Agent automatically understands your intent and calls the corresponding capabilities to assist in querying and retrieving information from MongoDB instances, thereby lowering the entry barrier and improving daily information retrieval efficiency.

<span id="FP8JJPOh"></span>
## Features and scenarios

MongoDB skill currently provides 4 read\-only query capabilities, with the usage scenarios for each capability listed below.


|**Feature** |**Description** |**Applicable scenarios** |
|---|---|---|
|Query instances |Retrieve summary information for all MongoDB instances under your account, including instance ID, running status, and billing method. |Routine checks, quickly understanding the running status and billing method of all instances. |
|View instance details |Get complete configuration information for the specified instance, including network, storage, database version, and node information. |Information verification or troubleshooting, viewing the instance's detailed configuration.<br><br> |
|Query instance backups<br><br> |Query the list of backup files for a specified instance, including backup file names, backup policies, and backup statuses. |Backup check, confirming whether the recent backup was successful and the backup strategy.<br><br> |
|Query parameter configuration |Query the current database parameter settings of a specified instance, such as `maxIncomingConnections`. |Parameter tuning or troubleshooting, retrieving current parameter values as a reference. |


<span id="qr2BJI6G"></span>
## Prerequisite

An API Access Key (AK/SK) has been created for the Document Database for MongoDB skill.

<span id="zFSyzcuM"></span>
## Installation and configuration

This topic primarily uses OpenClaw and ArkClaw as examples to explain how to install the MongoDB skill. In addition to the agents mentioned above, Trae, Claude Code, and other agents that support the Agent Skills protocol also support loading this skill. For specific installation commands, refer to [Find Skill Installation Guide](https://findskill.com/volcengine/mongodb/volcengine-mongodb), or download the ZIP package for manual installation.


<Tabs>
<Tab zoneid="OFXtyyJUUe" title="Install MongoDB skill in OpenClaw">
<TabTitle>Install MongoDB skill in OpenClaw</TabTitle>

1. Install Node.js 22 or later. For details, see [Node.js](https://nodejs.org/en).

2. Install OpenClaw

   1. Select the appropriate command to install OpenClaw based on your operating system

      * For macOS and Linux:

         ```Plain Text
         curl -fsSL https://openclaw.ai/install.sh | bash
         ```
         

      * For Windows (using PowerShell):

         ```Plain Text
         iwr -useb https://openclaw.ai/install.ps1 | iex
         ```
         

   2. Run the following command to initialize OpenClaw and configure it step by step according to the prompts.

      ```Plain Text
      openclaw onboard --install-daemon
      ```
      

      After successful installation, you can run the `openclaw --version` command to verify the installation.

3. Install MongoDB skill

   Run the following command to install the MongoDB skill.

   ```Plain Text
   npx skills add https://skills.volces.com/skills/volcengine/mongodb -s volcengine-mongodb --agent openclaw
   ```
   

5. Configure access credentials

   Configure the following environment variables in the Agent runtime environment.

   ```Plain Text
   export VOLCENGINE_ACCESS_KEY="your-access-key" # Required. Enter the Access Key obtained from the API Access Key page.
   export VOLCENGINE_SECRET_KEY="your-secret-key" # Required. Enter the Secret Key obtained from the API Access Key page.
   export VOLCENGINE_REGION="cn-beijing"  # optional, defaults to cn-beijing.
   ```
   


</Tab>
<Tab zoneid="pfCnHQ5Zb2" title="Install MongoDB skill in ArkClaw">
<TabTitle>Install MongoDB skill in ArkClaw</TabTitle>

1. Log in to [ArkClaw console](https://console.byteplus.com/arkclaw/).

2. Initiate an ArkClaw task. For detailed steps, see [Initiating tasks](https://docs.byteplus.com/en/docs/ArkClaw/Initiating_tasks_?_gl=1*1ogal2b*_gcl_au*MTk4MjUxMzA1MS4xNzc5MzM1NTk0*_ga*NTcxODYyMi4xNzc0OTI2NzQ1*_ga_2377LE7GQM*czE3ODI4OTgzNTMkbzMkZzEkdDE3ODI4OTgzNTQkajU5JGwwJGgxNDM3NTkzNDM2*_ga_3H57BBC3B9*czE3ODI4OTgzNDEkbzMkZzEkdDE3ODI4OTgzNTQkajQ3JGwwJGgxOTQ3NTg2OTY.&_vtm_=a38233.b43311.0_0.0_0.0.34_7654903473058219573).

3. Install MongoDB skill.

   1. In the left navigation bar, select **Skills Center**.

   2. On the **Skill square** page, find volcengine\-mongodb and click **Add**.

4. In the ArkClaw dialog, enter the following information:

   * **VOLCENGINE_ACCESS_KEY** \- BytePlus Access Key

   * **VOLCENGINE_SECRET_KEY** \- BytePlus Secret Key

   * **VOLCENGINE_REGION** (Optional, default cn\-beijing) — The region where the instance is located.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Each time a new session is created, the Agent must re\-verify your Access Key and Secret Key before invoking the skill.   </div>
   


</Tab>
</Tabs>


<span id="2yesvTbE"></span>
## Usage demonstration

After completing the configuration, you can interact with the Agent using natural language to query and retrieve information about MongoDB instances. The following typical conversation examples demonstrate how the skill is used and its interaction process in real\-world scenarios.

<span id="V4adSmzz"></span>
### Query instances

You can directly query the running status and basic information of all MongoDB instances under your account using natural language. The Agent calls the MongoDB skill to retrieve the latest instance data and returns key information such as the instance ID, running status, and billing method.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5d64ab6bc68a94f12a5dcbff964c7ada.png) </span>

<span id="OZD3sXf7"></span>
### Query instance details

<div style="text-align: center">
When you need to understand the detailed configuration of a specific instance, simply provide the instance ID or instance name in the conversation. The Agent calls the MongoDB skill to retrieve the complete information for that instance and returns detailed data such as basic information, resource usage overview, and node information.<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_868179c3ea4b636962110087dc91233f.png" /></div>


<span id="w6prjRK3"></span>
### Query instance backups

When you need to check an instance's backup status, simply provide the instance ID or instance name in the conversation and issue a backup query command. The Agent calls the MongoDB skill to retrieve the latest backup list and returns key information such as the backup file name, backup policy, and backup status.

<div style="text-align: center">
<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bb58ea99eb6231c7cc1262cee1058f5b.png" /></div>


<span id="8jJGZLy0"></span>
### Query parameter configuration

When you need to view an instance's database parameter settings, simply provide the instance ID or instance name in the conversation. The Agent calls the MongoDB skill to retrieve the instance's complete current parameter configuration and returns key information such as all parameter names, their current values, and default values. You can also specify particular parameter names for a precise query.

<div style="text-align: center">
<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_471610730e2a98f2d7f78e28e5c0d678.png" /></div>
