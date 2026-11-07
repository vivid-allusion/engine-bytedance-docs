---
title: "Creating expert agents"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Configuring_expert_agents"
---

The intelligent O&M assistant provides agent management capabilities. This topic describes how to create a custom expert agent.

## Background

An expert agent is a domain\-specific subagent in the intelligent O&M assistant. It has an independent system prompt and supports associating data sources, knowledge bases, skills, and IAM roles as needed. It is primarily used to organize evidence retrieval, reasoning logic, and conclusion generation for specific O&M domains. You can distill troubleshooting methods, judgment criteria, and remediation paths for specific domains or scenarios into reusable, configurable, and traceable expert agents.

The intelligent O&M platform includes preset official agents that cover common scenarios such as performance and capacity assessment. You can use them based on your actual needs.

## Prerequisites

* A prompt of no more than 2,000 characters has been prepared with key information such as the agent's role and working approach clearly defined. The use of Markdown syntax is recommended.

* (Optional) To configure a skill for an expert agent, upload the skill to the intelligent O&M assistant in advance. A skill is a standardized capability package built for specific scenarios. Configuring skills for an agent gives it a complete operational specification. This enables the agent to independently identify intent, complete professional tasks by following defined processes, and execute business operations. For more information, see [Upload a skill](https://docs.byteplus.com/en/docs/Observability_Platform/Configuring_skills).

* (Optional) If you need to grant the expert agent additional resource access permissions through an IAM role, create a role that trusts `apmplus_server` in advance. For a more detailed description, refer to [Role management](https://docs.byteplus.com/en/docs/IAM/RoleManagement).

## Procedure

1. Log in to the [Intelligent O&M platform](https://console.byteplus.com/observe/devops).

2. In the left navigation pane, select **Expert Agent**.

3. Click **Create Agent**. Configure agent\-related information and click **Create Agent** in the upper\-right corner.

   |Parameter |Description |
   |---|---|
   |Name |Specify a name for the expert agent. Duplicate names are not allowed. |
   |Skill |Select the skills that you want to allow the current agent to call. |
   |Prompt |Paste or enter the prompt for defining the role of the expert agent. We recommend that the prompt include key information such as role definition, capability boundaries, behavioral constraints, workflow, output specifications, and fallback handling. |
   |IAM role |Select a role that trusts `apmplus_server` to grant additional resource access permissions to the expert agent. This allows the expert agent to read monitoring data, logs, and configuration information across services during investigations. It can then collect evidence more comprehensively without expanding personnel permissions.<br><br>> **tip**<br><br><br>> When creating a role, select the `apmplus_server` service to establish trust for `apmplus_server`. You can also add the `apmplus_server` service to the trust policy file of an existing role for trust authorization. For a more detailed description, refer to [Role management](https://docs.byteplus.com/en/docs/IAM/RoleManagement).<br> |
