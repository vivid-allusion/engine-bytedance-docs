---
title: "Updating template types"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Updating_tool_types"
---

After a sandbox template is created, if your business requirements change (for example, you need to switch from a code sandbox to a browser sandbox), you can update the template type to adapt to the new use case. The template type determines the tool capabilities available to sandbox instances. After the update, newly created instances will use the new tool type. This topic describes how to update the template type.

## Supported tools

AgentKit provides preset tools, custom tools, and [VeADK](https://docs.veadk.xyz/productions/veadk/preview/en) built\-in tools. For details, see [Sandbox template types](https://docs.byteplus.com/en/docs/agentkit/Tool_type).

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Sandbox Templates".

3. In the "Sandbox templates" list, click the target template name. On the "Configuration information" tab, find the "Type" field in the "Basic information" section and click the ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1a5bf12c121e79c81297d621ca1c2dd4.png)****.

4. In the "Edit tool type" panel, update the tool type and click "Confirm".

5. After a successful update, go to the "Configuration information" tab and check the "Basic Information" section to confirm that the sandbox template type has been updated.

   The types of existing instances are not automatically changed after the template type is updated. Newly created sandbox instances will use the updated type.
