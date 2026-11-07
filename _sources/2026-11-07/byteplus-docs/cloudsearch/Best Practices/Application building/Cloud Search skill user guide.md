---
title: "Cloud Search skill user guide"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Cloud-Search-skill-user-guide"
---

This topic describes how to integrate and use the Cloud Search skill in Agent applications, helping developers quickly build intelligent search and knowledge enhancement capabilities based on cloud search service instances.

<span id="ibsvGmVC"></span>
## Background

Under traditional usage, operators and developers usually create, configure, operate, and manage cloud search service instances through the console or API calls. This process often involves resource specification selection, network configuration, access control, index management, and query tuning, which includes multiple steps, lengthy operations, repetitive tasks, and requires experience and operational skills.

With BytePlus Cloud Search skill, you can interact with the AI Agent using natural language. The Agent automatically understands your intent and calls the corresponding capabilities to assist with the management, operation, and data handling of BytePlus Elasticsearch and OpenSearch instances, thus lowering the usage threshold and improving daily operation and data management efficiency.

The Cloud Search skill covers the following two main capability areas.

<span id="RunTrcS3"></span>
### **Control plane**

Control plane capabilities focus on lifecycle management and resource operation scenarios of Elasticsearch and OpenSearch instances. You can perform operations such as instance creation, specification adjustment, status inspection, connection information queries, access configuration management, and instance release through natural language.

At the same time, the Agent can assist in querying available VPCs, subnets, node specifications, version information, and other basic resource data. This reduces manual operations during environment preparation and resource configuration, improving resource management efficiency.

<span id="Khc9iYjQ"></span>
### **Data plane**

Data plane capabilities mainly address index and data operation scenarios in Elasticsearch and OpenSearch instances. You can use the Agent to perform operations such as index creation, mapping configuration, document writing, conditional queries, full\-text search, aggregation analysis, and data deletion.

For common data query and diagnosis scenarios, the skill provides preset script capabilities to improve execution efficiency and result consistency. For more flexible data read and write needs, the skill offers SDK or API invocation specifications, with the Agent generating and executing the corresponding code based on specific scenarios.

Considering data security and operational risks, it is advisable to authorize the Agent cautiously when performing sensitive or high\-risk data write, modify, and delete operations.

<span id="HfeQngya"></span>
## Prerequisites

An API access key (AK/SK) has been created for the Cloud Search skill.

<span id="66M1rzLy"></span>
## Install configuration


1. Install the skill.

   See [Find Skill installation page](https://findskill.com/volcengine/escloud/byted-escloud?utm_source=chatgpt.com) for installation instructions. Execute the corresponding command or download the ZIP package for manual installation based on the Agent type used.

   
   <Tabs>
   <Tab zoneid="7bVvLL8r" title="OpenClaw">
   <TabTitle>OpenClaw</TabTitle>
   
   ```Bash
   npx skills add https://skills.volces.com/skills/volcengine/escloud -s byted-escloud --agent openclaw
   ```
   
   
   
   </Tab>
   <Tab zoneid="EhOq9G2E" title="Trae">
   <TabTitle>Trae</TabTitle>
   
   ```Bash
   npx skills add https://skills.volces.com/skills/volcengine/escloud -s byted-escloud --agent trae
   ```
   
   
   
   </Tab>
   </Tabs>
   

2. Configure access credentials.

   Set the following environment variables in the Agent runtime environment.

   ```Bash
   VOLCENGINE_ACCESS_KEY="您创建的 Access Key"
   VOLCENGINE_SECRET_KEY="您创建的 Secret Key"
   VOLCENGINE_REGION="cn-beijing" # Default Beijing region, adjustable as needed
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">No manual AK/SK configuration is required in ArkClaw. The system automatically injects the API Token and completes control plane authentication via access control mechanisms.   </div>
   

3. Confirm that the skill is loaded.

   After installation, use the skill management commands provided by the Agent to confirm whether the skill is loaded correctly. e.g., execute the following command in OpenClaw.

   ```Bash
   openclaw skills list
   ```
   

   When the status of `byted-escloud` shows `ready`, it means the skill has loaded successfully.

   ```Plain Text
   │ ✓ ready   │ 📦 volcengine-    │ Manages BytePlus (Volcengine) ESCloud/Cloud Search (Elasticsearch + OpenSearch) clusters: control plane provisioning/scale/delete via volcengine-python-sdk and data plane index/doc CRUD + search via opensearch-py. Use when the user mentions ESCloud/          │ openclaw-managed │
   │           │ escloud          │ ESCloud/Elasticsearch/OpenSearch on Volcengine/BytePlus or asks to provision/operate those clusters there.                                                                                                                                                    │
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After updating the skill, some Agent environments may not automatically reload the plugin. If abilities are not effective or versions are not updated, recreate the conversation (such as by executing <code>/new</code>) before use.   </div>
   

<span id="AWqloLTQ"></span>
## Use the demo

After configuration, the Agent has full capability to operate the Cloud Search service instance. The following typical conversation examples show how the skill is used and interacts in real scenarios.

<span id="oRSEeEUB"></span>
### Create an instance

When you submit natural language requests like "create instance," the Agent automatically calls the skill to parse the required parameters and guides you through the instance creation process. During the process, the Agent usually confirms key configurations step by step, such as VPC and subnet selection, instance name, access password, and node specifications, to ensure the resources are created as expected. The whole process requires no manual input of complex parameters; just follow the prompts to confirm and complete the configuration and creation.

<span id="Kx1WGuS3"></span>
### Query instance information

After instance creation, you can query the instance's running status and basic information directly using natural language. The agent calls ESCloud skill to obtain the latest instance data and returns key information such as current status, specification configuration, and operation details.

<span id="ux3CR5HW"></span>
### Scaling

When the workload changes, you can send scaling requests using natural language. The agent interprets the target specification or capacity adjustment intent, then calls ESCloud skill to dynamically modify instance resources, including node specification upgrades and quantity adjustments.

<span id="pinHJlHW"></span>
### Delete an instance

When the instance is no longer needed or resources must be freed, you can request instance deletion through natural language. The agent identifies the deletion request and calls ESCloud skill to execute the instance deletion process.
