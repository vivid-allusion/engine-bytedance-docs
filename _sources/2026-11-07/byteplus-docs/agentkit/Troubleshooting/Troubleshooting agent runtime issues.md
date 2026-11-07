---
title: "Troubleshooting agent runtime issues"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Troubleshooting_agent_runtime_issues"
---

This topic describes how to troubleshoot errors that occur in the AgentKit agent runtime during deployment, release, and authentication.

## Release is stuck, or the resource is locked

**Issue description**

The release process is stuck, and the system returns the message "The specified operation is rejected because your resource has been locked by another operation".

**Possible causes**

Function instance resources may be insufficient. As a result, the related resources are being used and locked by another operation, and the current release operation cannot proceed.

**Solution**

1. Check whether any agent runtime instances under the current account are still in the **Starting ** state.

2. Wait until the state of the related instances becomes stable, and then retry the release operation.

3. If any abnormal instance remains in the **Starting** state for a long time, confirm that terminating the instance does not affect your business, terminate the abnormal instance, and then release the runtime again.

   > **warning**

   > Terminating an instance may interrupt requests that are being processed. If the impact scope cannot be determined, do not directly terminate production instances.

## The runtime fails to start or is in the "Unavailable" status

**Issue description**

The runtime fails to start or is in the "**Unavailable**" status after it is created. The issue persists after the agent is deleted and re\-created.

**Solution**

> **warning**

> Do not delete and re\-create the runtime as a first step. The deletion may affect the access address, configuration, and associated resources. If deletion is necessary, first back up the required configuration and confirm the impact scope.

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the agent runtime list, find the agent whose status is **Unavailable**, hover over the status, click "View logs", and use the logs to identify issues such as runtime configuration, startup commands, or dependencies.

3. If the log contains` IndexError: list index out of range`, review the **Traceback (error stack information) ** in the error log and locate the file and code line where the error occurs. Locate the file, code line, and function call site where the error occurs, and check whether the list accessed at that location is empty or whether the index is out of range.

4. After the configuration or code is corrected, re\-create the runtime.

5. If the issue persists after multiple retries, record the agent ID, creation time, and log information, and then contact BytePlus technical support.

## VeADK LongTermMemory fails to initialize

**Issue description**

When the AgentKit runtime initializes the VeADK long\-term memory component, validation reports an error, and the program fails during the startup phase.

```Bash
[LTM] veadk LongTermMemory Initialization failed: 1 validation error for LongTermMemory
Value error, API Key not set, auto‑fetching api key needs `api_key_id` or `project_id`
```

**Possible causes**

The current LongTermMemory uses Mem0 as the memory backend, but the API key required by Mem0 is not obtained during initialization.

**Solution**

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Memory".

3. Click the target memory name to open the details page.

4. Click the "Integration code" tab to obtain the **DATABASE_MEM0_API_KEY** value for the current memory.

5. Pass the DATABASE_MEM0_API_KEY value to the environment variables of the runtime, and reinitialize the runtime.

   ```Bash
   DATABASE_MEM0_API_KEY=xxx # API Key for memory inbound identity authentication.
   ```

6. If the issue persists, record the error information and contact BytePlus technical support.

## Runtime authentication fails

**Issue description**

The online test returns the message "Authentication of the current Runtime failed. Messages cannot be sent at this time" or "Permission denied".

**Possible causes**

The current operating account does not have the ** AgentKitFullAccess** permission.

**Solution**

1. Confirm whether the account on which the error occurs is an IAM user.

2. Log in to the[ IAM console](https://console.byteplus.com/iam/) and check whether the **AgentKitFullAccess** policy has been attached to the IAM user.

   > **tip**

   > The AgentKitFullAccess policy permission can be used to troubleshoot this issue. However, it does not necessarily represent the minimum required permission. Before you grant permissions in a production environment, complete the approval process based on the least\-privilege principle of your organization.

3. If this policy is not granted, contact an administrator who has the required permissions to complete the authorization.

4. After authorization is complete, retest directly. The runtime does not need to be released again.

5. If the issue persists, record the agent ID and contact BytePlus technical support.
