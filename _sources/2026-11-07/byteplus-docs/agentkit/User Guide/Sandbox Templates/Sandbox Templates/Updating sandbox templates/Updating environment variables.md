---
title: "Updating environment variables"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Updating_environment_variables"
---

Environment variables are used to pass configuration parameters, such as API keys, debug flags, and path settings, to applications running in a sandbox instance. When you need to adjust these runtime parameters, update the environment variables. This topic describes how to update environment variables.

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Sandbox Templates".

3. In the "Sandbox templates" list, click the target template name. On the Configuration information tab, click "Edit" in the "Environment variables" section **.**

4. In the "Editing environment variables" panel, modify environment variables. For details, see [Creating sandbox templates](https://docs.byteplus.com/en/docs/agentkit/Creating_tools). After editing is complete, click "Confirm".

   * **Form\-based editing**: Configure environment variables as key\-value pairs. This option is suitable for a small number of simple key\-value pairs. Click **Add environment variable**, and configure **Key** and **Value** based on the variable input requirements prompted by the console interface.

   * **JSON\-formatted editing**: Configure environment variables using a JSON file. This option is suitable for batch configuration or complex structured data.

5. After a successful update, go to the "Configuration information" tab and confirm that the environment variable list has been updated in the **Environment variables** section. After environment variables are updated, newly created instances will use the updated environment variables. Existing instances must be recreated for the changes to take effect.
