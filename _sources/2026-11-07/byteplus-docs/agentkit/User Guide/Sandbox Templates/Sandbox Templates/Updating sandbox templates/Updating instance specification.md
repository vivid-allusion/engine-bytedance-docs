---
title: "Updating instance specification"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Updating_instance_specification"
---

The instance specification (vCPU and memory) of a sandbox instance determines the instance's computing capacity. When the business load changes (for example, when you need to process larger\-scale code compilation or higher\-concurrency tasks), you can adjust compute resources by updating the instance specification. This topic describes how to update the instance specification.

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Sandbox Templates".

3. In the "Sandbox templates" list, click the target template name. On the "Configuration information" tab, find the "Instance specification" field in the "Basic information" section and click the ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1a5bf12c121e79c81297d621ca1c2dd4.png)****.

4. In the dialog box that appears, update the instance specifications and click "Confirm" to complete the operation.

   * **Configuration requirements**

      * vCPU: 2–16 cores.

      * Memory: 4–128 GiB.

   * **vCPU and memory ratio requirements**:

      * If the vCPU value is an integer, the ratio must be 1:2, 1:4, or 1:8.

      * If the vCPU value is not an integer, the ratio must be 1:2 or 1:4.

   > **tip**

   > The range of instance types varies by preset template.

   * > Instances created from the ArkClaw Sandbox and Hermes Sandbox templates can be configured with 4–16 vCPUs and 8–128 GiB of memory.

   * > Instances created from the Code Sandbox, Skills Sandbox, and AIO Sandbox templates can be configured with 2–16 vCPUs and 4–128 GiB of memory.

5. After a successful update, go to the "Configuration information" tab and confirm that the instance specification has been updated to the new vCPU and memory values in the **Basic information** section. Instance specification updates do not apply to existing instances. Newly created instances will use the updated specification.
