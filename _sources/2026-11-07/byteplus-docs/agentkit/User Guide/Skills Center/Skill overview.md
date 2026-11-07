---
title: "Skill overview"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Skill_Overview"
---

Skills are reusable capability units built on the file system and serve as core capability components of an agent. They are used to standardize and encapsulate business knowledge, execution workflows, tool scripts, operational specifications, and associated resources. This enables an agent to load and execute specified capabilities with clear boundaries, much like calling a local function.

By adding a skill to a skills space and integrating the skill into the target agent, you can quickly extend the agent's task\-handling scope. This improves delivery consistency, execution stability, and the efficiency of adapting to business needs.

* **For developers**: Skills provide a way to consolidate prompts, tool call constraints, task step orchestration, and business logic into engineering assets.

* **For business users**: Skills lower the barrier to capability reuse and business experience consolidation, enabling existing materials such as PRDs, SOPs, and operations manuals to be gradually converted into capability units that an agent can use directly.

## Why you need skills

Skills enable you to consolidate fragmented capabilities scattered across documents, scripts, tool invocations, and human expertise **into standardized assets**. These assets can be retrieved, loaded, and executed by an agent. Once built, a skill can be reused across multiple tasks and sessions with consistent execution results.

**Card**

### **Capability reuse**

The same type of capability can be shared across multiple agents, eliminating the need to repeatedly write prompts, scripts, or operational rules for similar tasks. This reduces redundant work and improves the reuse rate of accumulated capabilities.

**Card**

### **Capability governance**

After skills standardize and encapsulate capabilities, you can centrally manage capability boundaries, dependencies, input/output contracts, and execution constraints. Skills are no longer implicit knowledge scattered across documents, scripts, and human expertise, but explicit, manageable assets.

**Card**

### **Version stability**

Skills support versioned publishing. A published version locks in the capability definition and resource content for a given stage, enabling stable references in production environments. Subsequent iteration by version is also supported, reducing uncertainty introduced by capability changes.

**Card**

### **Capability distribution and scope control**

Through skills spaces, skill collections can be organized by team, business domain, or runtime environment, and the distribution scope of a skill can be controlled. This improves sharing efficiency while preventing inapplicable capabilities from being called by mistake.

## Recommended scenarios

Skills are suited for encapsulating reusable agent capabilities. When a task execution workflow is standardized and repetitive, and there are clear requirements for output reliability, it can be encapsulated as a skill for an agent to call.

### **Typical scenarios**

**Workflow and execution standardization**

* Consolidate stable task workflows such as approvals and data processing into standard execution units.

* Encapsulate tool usage constraints and permission boundaries to reduce uncertainty in agent task execution.

**Output specification and consistency**

* Lock prompt strategies and response specifications into unified capabilities to ensure consistent output across different agents.

* Generate reports and plans based on fixed standards, templates, or domain knowledge.

**Knowledge and asset consolidation**

* Convert business knowledge, operations manuals, SOPs, and similar materials into reusable capability assets, reducing the cost of repeated training and configuration.

* Enable intelligent generation, structured parsing, and automated processing of complex documents.

**Capability sharing and system integration**

* Share the same type of capability across multiple agents, supporting fast reuse across teams and scenarios.

* Enable stable interaction with external APIs, databases, and other resources.

### Usage practices

After integrating a skill into an agent, you can trigger the skill to complete the corresponding task using natural language instructions.

|Practice |Description |
|---|---|
|**Standardized process execution** |Once a stable business workflow is encapsulated as a skill, the agent can automatically complete the task following standard steps, reducing manual intervention and execution deviations.<br><br><br>* **Example 1**: Enter "Run an inspection on the online service order\-service." The agent calls the inspection skill, checks the service health status, API responses, and alert records in sequence according to preset steps, and outputs an inspection report.<br><br>* **Example 2**: Enter "Initiate an approval process. Applicant: Zhang San. Approval type: permission change." The agent calls the approval skill, automatically fills in the approval form, and submits it to the corresponding approval workflow. |
|**Output specification control** |Once prompt strategies and response specifications are converted into a skill, different agents can produce consistent content structure and wording in the same scenario.<br><br>**Example**: Enter "Generate the release notice for this iteration." The agent calls the notice generation skill and outputs a standardized release notice containing the version number, change details, impact scope, and contact information, based on a preset template. |
|**Knowledge and SOP asset consolidation** |Once operation manuals, business rules, and SOPs are encapsulated as a skill, the agent can complete tasks directly based on the consolidated knowledge without repeated configuration.<br><br>**Example**: Enter "Check this API documentation for sensitive field exposure issues according to the data security specifications." The agent calls the data security review skill, checks each item against the built\-in SOP, and outputs a compliance report. |
|**Cross\-agent capability sharing** |A skill can be published to multiple skills spaces for reuse by different agents, enabling fast cross\-team replication of best practices.<br><br>**Example**: Once the "Log summary generation" skill is published to the skills spaces of both the O&M team and the development team, agents from both teams can call the skill directly to generate log summaries without having to develop it separately. |

## Concepts

|Concept |Description |
|---|---|
|Skills |A skill is a standardized **capability unit** encapsulated for a specific task, integrating the knowledge description, execution workflow, code scripts, and associated resources required for the task. An agent can execute various specialized tasks on demand and in a stable manner, much like calling a function library.<br><br>Compared with a conversational prompt designed for one\-off tasks, a skill operates at a higher level of abstraction. With on\-demand loading, it also eliminates the need to repeatedly provide the same information across multiple conversation turns, improving task execution efficiency. |
|Skills space |A skills space is used to organize skill collections by team, business domain, environment, or scenario. It serves as the primary mechanism for skill distribution and scope control. A skill can be added to one or more skills spaces, allowing the corresponding agent to discover and call it on demand at runtime. |

## How it works

**Encapsulation**

Standardize and encapsulate the knowledge, workflows, scripts, and resources required for a specific task into an independent capability unit.

**Registration**

Publish a skill to a skills space to make it visible to agents. Skills that have not been added to a skills space cannot be called.

**Triggering**

Upon receiving a natural language instruction, the agent discovers and matches the target skill through the skills space and calls the skill.

**Execution**

The skill completes the task according to its encapsulated workflow and constraints and returns the result to the agent.

## Permission boundaries

**Card**

### Ownership and access control

The permission scope of a skill is determined by three factors: **skill ownership (** who owns, edits, and maintains the skill), **space distribution permissions** (which skills spaces the skill is distributed to and which members can access it), and **agent call permissions (** which agents are allowed to use the skill). A skill can be owned by an individual, a team, or an organization. The ownership determines its visibility and publishing scope.

**Card**

### Access isolation at the skills space level

A **skills space** manages the collection of skills that can be integrated and called by agents. Only skills that have been added to the target **skills space** can be selected and used by the agents or runtimes associated with that space. Direct invocation across spaces is not supported.

**Card**

### Distinction between call and management permissions

Call permission for a skill is not equivalent to management permission for the skill. An agent with call permission can use the configured skill at runtime, but this does not grant permission to modify, publish, or delete the skill.

## Relationships with other components

The relationship between a skill and other components can be summarized as follows:

|**Component** |**Role** |**Relationship with skill** |
|---|---|---|
|Skills |A task\-oriented capability encapsulation unit. |Defines capability boundaries, knowledge structure, and execution rules. |
|Tool |The execution carrier for invocable actions. |Selected, organized, and constrained by a skill. |
|MCP |The standard integration protocol for external tools and services. |Provides skills with an extensible source of external capabilities. |
|Runtime |The execution and scheduling environment for an agent. |Discovers, loads, and calls skills during task execution. |

* **Skills and tools**

   A [tool](https://docs.byteplus.com/en/docs/agentkit/Tool_overview?lang=en) is the carrier for callable actions, such as accessing an API, executing a script, reading a resource, or calling an external service. A skill, on the other hand, describes capabilities for an agent and defines the boundaries for execution orchestration, determining in which scenarios and according to which rules specific tools are used.

   Think of a tool as "action capability" and a skill as "task capability". A tool handles execution. A skill organizes and constrains execution.

* **Skills and MCP**

   [MCP](https://docs.byteplus.com/en/docs/agentkit/MCP_Overview?lang=en) is used to integrate external tools or services via a standard protocol. A skill can reference MCP tools in its capability implementation, enabling the agent to access external resources under a unified protocol.

   This relationship allows a skill to not only encapsulate static knowledge but also integrate dynamic tool capabilities, extending the agent's execution depth and external connectivity.

* **Skills and runtimes**

   A [runtime](https://docs.byteplus.com/en/docs/agentkit/Agent_runtime_overview?lang=en) is the execution environment for an agent, responsible for carrying the task execution chain. Within a runtime, a skill participates in task execution as a schedulable capability resource, matched and called by the runtime based on task intent, context, and available capabilities.

## Procedure

Manually create skills based on your business scenarios to flexibly customize dedicated business capabilities. Manual creation is suitable for scenarios where the skill structure design is already defined, you want full control over how capabilities are organized, or you need fine\-grained skill management within an existing space system.

1. [Create a skills space](https://docs.byteplus.com/en/docs/agentkit/Skills_space?lang=en)

   Agents can query a skill and retrieve its files only after the skill has been added to a skills space. You can create a dedicated skills space as a storage container for skills to manage capabilities by category.

2. **Create skills**

   You can select any of the following methods to create skills based on your existing resources, development approaches, and business requirements.

   * [Manually creating skills](https://docs.byteplus.com/en/docs/agentkit/create_skills)

      You can create a skill by cloning **a preset skill**, **uploading a compressed package**, or pulling a file from **TOS**. This is suitable for scenarios with a complete capability package, where preset capabilities need to be reused, or where the directory structure, scripts, and configuration files need to be maintained independently.

3. **View evaluation and quality assurance**: Through quality checks, security scanning, and skill evaluation, identify structural and formatting defects, security risks, and capability gaps early. This reduces the risk of runtime errors, security vulnerabilities, or subpar performance after a skill is published and ensures the skill delivery quality.

   * [Viewing and fixing quality check issues](https://docs.byteplus.com/en/docs/agentkit/Viewing-and-fixing-quality-check-issues?lang=en)

      View the most recent static quality check results for the current skill version to understand the distribution of structural, formatting, resource reference, and basic security issues in the skill. Use the detected issues to locate the affected files and fix the issues.

   * [Viewing and fixing security scan issues](https://docs.byteplus.com/en/docs/agentkit/Viewing-and-fixing-security-scan-issues?lang=en)

      View the **security scanning status** and issue counts by risk level for the current skill version. Identify potential security risks in the code, configuration, and resources, and remediate high\-risk security issues.

4. [Add a skill in a skills space](https://docs.byteplus.com/en/docs/agentkit/Adding_and_Removing_Skills?lang=en) (optional)

   If the skill was not added to a skills space during creation, complete this step so that the agent can call the skill.

5. Update and publish a new skill version (optional)

   1. [Update a skill](https://docs.byteplus.com/en/docs/agentkit/Updating_Skills?lang=en): When a skill has entered the continuous iteration stage, you can upgrade the skill by updating the code package or editing files online. An update only generates a new version and does not automatically apply the new capabilities to the agent.

   2. [Publish a new skill version](https://docs.byteplus.com/en/docs/agentkit/Publishing_Skills?lang=en): Deliver the updated skill version to the target **skills space**. The updated capabilities take effect in the agent invocation chain only after publishing is complete.

## Next steps

Regardless of the method you use to build a skill, you need to [integrate the skill into an agent](https://docs.byteplus.com/en/docs/agentkit/Integrating_Skills_into_agent?lang=en) and [deploy the agent to an agent runtime](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console?lang=en). The agent can discover and call the corresponding skill in real task scenarios only after the agent is deployed.
