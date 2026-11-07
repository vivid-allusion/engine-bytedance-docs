---
title: "AgentKit Runtime update"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/AgentKit_Runtime_update"
---

Pass add **AgentKit Runtime update ** task in pipeline orchestration to Complete the Update of AgentKit Runtime. This article describes how to Use pipeline tasks to Update the Runtime via TOS zip package OR Image.

<span id="rUO5eAgV"></span>
## Background

AgentKit is a development tool platform provided by BytePlus to Support the building, Deploy, and operation of AI Agents. It helps developers and enterprises lower the threshold for Agent development, providing Security, built\-in tools, memory, knowledge, Monitoring, evaluation, and other infrastructure beyond the Model for Agents, enabling enterprises to efficiently build, Deploy, and operate complex and intelligent enterprise\-level Agents.

AgentKit Agent Runtime provides a Security\-isolated, framework\- and Model\-independent managed Runtime environment for Agents.

<span id="fWoguESL"></span>
## Prerequisites

Created AgentKit Runtime. For Actions details, see [create Runtime (Console)](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console) or [create Runtime (CLI tool)](https://docs.byteplus.com/en/docs/agentkit/Creating_runtime_via_CLI_tool).

<span id="NcsrXvna"></span>
## Description


|Parameter |Description |
|---|---|
|Job name |Default is AgentKit Runtime Update, custom job names are supported. |
|Upstream task |show the upstream serial Job name of the current task. When there are none upstream tasks, show as `-`. |
|Region |Select the Region where the AgentKit Runtime is located. |
|Runtime ID |Select the AgentKit Runtime to Update. |
|artifact |settings the artifact to be Deployed.<br><br><br>* **Artifact repository type**: Support TOS zip package and Image types.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Please ensure that the selected artifact Type in the pipeline and veFaaS Service are consistent. For example, both are Top zip package or both are Image.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If the input Artifact name does not exist or is Error, it may cause the artifact to not be correctly Replaced during this Deploy, resulting in Deployment failed or not meeting the expected Deploy outcome.</div><br><br><br>* **Artifact Source**: Support upstream products and Custom methods.<br><br>   * **Upstream products**: Only supported when the upstream product is Building images. Select this Item when the Image to be Deployed is sourced from the output of an upstream task. For example: In pipeline orchestration **compile build \> Building images Push to Container Registry \> function Deploy** task, select the output of the upstream Building images task as the Image.<br><br>      * When the artifact Type is **TOS zip package**: Only supported when the upstream output is **TOS upload**. For methods to create upstream products, see [TOS upload](https://docs.byteplus.com/en/docs/cp/TOS_upload).<br><br>      * Artifact repository type is **Image**: Supported only when the upstream artifact is built as an image. For methods to create upstream artifacts, see [Building images Push](https://docs.byteplus.com/en/docs/cp/Build_and_push_images).<br><br>   * **Custom**: Enter the complete address of a Created image or TOS.<br><br>      * Artifact repository type is **TOS zip package**: Enter the complete address of a Created TOS. The TOS address format is a string in the form `bucket_name:object_key`, for example, `vefaas-test:vefaas-python38-default.zip`.<br><br>      * Artifact repository type is **Image**: Enter the complete address of a Created image. The image address format is `host/namespace/repo:tag`. When entering the image address, referencing pipeline variables is supported. |
|task output |Show parameters used to query the task output State. After this task is Complete, output the ID of the AgentKit Runtime. |
|Advanced settings |**Webhook notification**: Support sending task\-level messages via both generic Webhook format and Feishu bot, helping you stay informed about task updates in a timely manner. For details, see [Webhook notification](https://docs.byteplus.com/en/docs/cp/Webhook_notification). |
