---
title: "Milvus for VectorDB skill user guide"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Milvus_for_VectorDB_skill_user_guide"
---

This topic describes how to integrate and use BytePlus Milvus skill in Agent applications, helping developers quickly build AI capabilities for vector data management and intelligent retrieval.

<span id="UxUDGLHS"></span>
## Background

In traditional use, operators and developers usually create, configure, operate, and manage vector database instances via the console or API calls. This process often involves selecting resource specifications, network configuration, Collection and index management, data import, and search tuning, which entails a long operation chain and requires some experience and operation skills.

With BytePlus Milvus for VectorDB skill, you can interact with the AI Agent directly through natural language. The Agent automatically understands your intent and calls the corresponding capabilities, assisting in Milvus instance management and data operations, thereby lowering the usage threshold and improving daily operations and vector data management efficiency.

Milvus for VectorDB skill primarily covers the following two capability areas.

<span id="JIn7RQES"></span>
### Control plane

The control plane capabilities focus mainly on the lifecycle management and resource operation scenarios of Milvus for VectorDB instances. You can perform cluster creation, scaling, status inspection, connection information queries, and instance release operations through natural language.

At the same time, the Agent can assist in querying basic resource information such as available VPCs, subnets, and node specifications, reducing manual operations during environment preparation and cloud resource configuration, and improving resource management efficiency.

<span id="ka4VTAEJ"></span>
### Data plane

The data plane capabilities mainly target vector data management and retrieval scenarios in Milvus for VectorDB instances. You can use the Agent to create collections, define schemas, build vector indexes, write data, perform vector searches, conditional queries, and delete data.

For common data query and retrieval scenarios, skill provides preset scripts to improve execution efficiency and result consistency; for more flexible data read and write needs, skill offers SDK call specifications, with the Agent generating and executing corresponding code based on the specific scenario.

Considering data security and operational risks, it is recommended to cautiously authorize the Agent to perform sensitive or high\-risk data write, modify, and delete operations.

<span id="gdmGqdjl"></span>
## Prerequisites

An API access key (AK/SK) has been created for the Milvus skill.

<span id="r4SKiK8d"></span>
## Installation and configuration


1. Install the skill.

   Refer to the installation instructions on the [Find Skill installation page](https://findskill.com/volcengine/milvus/byted-milvus). Execute the corresponding commands depending on the Agent type used, or download the ZIP package for manual installation.

   
   <Tabs>
   <Tab zoneid="AjPHruKh" title="OpenClaw">
   <TabTitle>OpenClaw</TabTitle>
   
   ```Bash
   npx skills add https://skills.volces.com/skills/volcengine/milvus -s byted-milvus --agent openclaw
   ```
   
   
   
   </Tab>
   <Tab zoneid="38kjOudd" title="Trae">
   <TabTitle>Trae</TabTitle>
   
   ```Bash
   npx skills add https://skills.volces.com/skills/volcengine/milvus -s byted-milvus --agent trae
   ```
   
   
   
   </Tab>
   </Tabs>
   

2. Configure access credentials.

   Set the following environment variables in the Agent's runtime environment.

   ```Bash
   VOLCENGINE_ACCESS_KEY="您创建的 Access Key"
   VOLCENGINE_SECRET_KEY="您创建的 Secret Key"
   VOLCENGINE_REGION="cn-beijing" # default Beijing region, adjustable as needed
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">No manual AK/SK configuration is needed in ArkClaw. The system automatically injects the API Token and completes control plane authentication via access control mechanisms.   </div>
   

3. Confirm that the skill is loaded.

   After installation, confirm that the skill has loaded correctly using the skill management commands provided by the Agent. For example, execute the following command in OpenClaw.

   ```Bash
   openclaw skills list
   ```
   

   When the status of `byted-milvus` shows `ready`, it indicates that the skill has loaded successfully.

   ```Plain Text
   │ ✓ ready   │ 📦 byted-    │ Manages Milvus instances on BytePlus (Volcengine) using the bundled CLIs: provision, inspect, scale, and delete clusters; manage collections and run CRUD/search. Use when the user mentions Milvus on Volcengine/BytePlus or asks to operate/provision     │ openclaw-managed │
   │           │ milvus       │ Milvus there.                                                                                                                                                                                                                                                           │                  │
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After updating the skill, some Agent environments may not automatically reload the plugin. If abilities are not effective or versions are not updated, recreate the conversation (such as by executing <code>/new</code>) before use.   </div>
   

<span id="wUbnWBnc"></span>
## Control panel demo

After completing the configuration, the Agent fully supports operating the Milvus for VectorDB instance. The following typical conversation examples demonstrate how to use the skill and the interaction process in real scenarios.

<span id="eEikevm0"></span>
### Create an instance

When you make natural language requests such as "create an instance," the Agent automatically calls the skill to parse the required parameters and guides you through the instance creation process. During execution, the Agent usually confirms key configurations step by step, such as VPC and subnet selection, instance name, password, and node specifications, ensuring resource creation meets expectations. The entire process requires no manual input of complex parameters; just confirm the prompts to complete the configuration and creation.

<span id="1Qfk2uPI"></span>
### Query instance information

After the instance is created, you can directly query the instance running state and basic information using natural language. The agent calls Milvus skill to get the latest instance data and returns key information such as current status, specification configuration, and running conditions.

<span id="u2a1FgCF"></span>
### Scaling

When the business load changes, you can initiate scaling requests through natural language. The agent analyzes the target specification or capacity adjustment intent and calls Milvus Skill to dynamically change instance resources, including node specification upgrades and quantity adjustments.

<span id="daKnpujF"></span>
### Delete an instance

When the instance is no longer in use or you need to release resources, you can initiate a delete instance request via natural language. The agent recognizes the delete intent and calls Milvus skill to execute the instance deletion process.

<span id="Ir4YtZm7"></span>
## Data plane usage demonstration

Data plane operations are usually more flexible, including standardized high\-frequency queries as well as complex data read, write, and retrieval requirements. This skill provides preset script capabilities for common query and diagnostic tasks to improve execution efficiency and consistency; for more flexible data operations, the skill offers SDK call specifications allowing the model or Agent to dynamically generate and execute code based on your requests.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Different models and Agents may vary in code generation, tool invocation, and execution stability. Considering data security and operational risks, it is advisable to cautiously authorize Agents to perform sensitive or high\-risk data write, modify, and delete operations.</div>


* <div data-tips="true" data-tips-type="warning">Before executing data plane operations, ensure the target Milvus cluster has enabled public network access so the Agent can connect to and access the respective instance. You can currently apply for and bind a public IP through the control plane skill or directly request it in natural language, with the control plane assisting in enabling cluster public network access.</div>



<span id="LHrlE4UF"></span>
### View collection details

You can directly view the collection information in the current Milvus instance using natural language. The Agent will call the data plane skill to obtain the collection list.

<span id="PYlzlUTc"></span>
### Create a collection

You can directly create a collection using natural language, and the Agent will automatically parse and supplement the necessary parameters based on your needs.

<span id="sMWggFi6"></span>
### Delete a collection

You can initiate a delete request in natural language when a collection is no longer in use. The Agent automatically identifies the target collection and calls the data plane skill to perform the deletion.

<span id="SMUUibLG"></span>
### Write data

After creating a collection, you can write vector data into it using natural language. The Agent automatically validates the field structure based on the collection schema and assists with organizing and writing vector, scalar, and primary key data.

<span id="scO2TUis"></span>
### Query data

You can query data in the collection directly using natural language. The Agent generates corresponding query conditions or vector search requests based on your description and calls the data plane skill to return matching results.

<span id="dC44IfW3"></span>
### Update data

You can update existing data in a Collection using natural language. The agent automatically generates the corresponding data update logic based on the primary key, filter conditions, or target fields provided by the user, then calls the data skill to execute the modifications. During the update process, the agent validates field types and data structures against the Collection schema to reduce the risk of data anomalies caused by parameter errors.

<span id="waIEaMFu"></span>
### Delete data

You can delete specified data in a Collection using natural language. The agent automatically generates the corresponding data delete request based on the provided primary key, filter conditions, or deletion scope, then calls the data skill to execute the operation.
