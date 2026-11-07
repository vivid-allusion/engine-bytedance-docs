---
title: "Updating environment variables"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Updating_runtime_environment_variables"
---

Environment variables are used to store non\-code configuration information required for agent runtime, such as interface keys, service addresses, feature switches, rate limit thresholds, and model parameters. Modifications to environment variables are saved only as a draft and ** do not take effect immediately**. After you modify the environment variables, publish the agent runtime to generate a new version. The latest version is then automatically used for subsequent agent runtime calls.

<span id="Hffw6FgD"></span>
## Applicable scenario

Update the environment variables of an agent runtime in the following scenarios:


1. **Credential changes**: A third\-party API‑Key, access token, or account key expires or requires a rotation update.

2. **Runtime environment changes**: You switch an agent between the test, staging, and production environments and need to modify the database address, callback domain name, and backend service address.

3. **Business parameter adjustment**: Adjust runtime control parameters such as the timeout period, log level, request limit, and feature switches.

4. **Configuration iteration**: Add environment variables that an agent depends on, or remove obsolete variables.

5. **Exception configuration fixes**: An existing variable is set incorrectly and causes errors or abnormal behavior when the agent is called, so you need to correct the configuration.


<span id="CBIufbDQ"></span>
## Usage notes


* **Version requirement**: In preview mode, you can update the configuration only for the Latest version. In non\-preview mode, you do not need to specify a version and can update directly.

* **Effective conditions**: After you update the environment variables, the new configuration takes effect only after **republishing**, and a new version is generated simultaneously. Once published, the latest version is automatically used for subsequent agent runtime calls. [View release history](https://docs.byteplus.com/en/docs/agentkit/Viewing_release_history).


<span id="fhNuZv9V"></span>
## Procedure


1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Agent Runtime".

3. In the agent runtime list, click the name of the target agent runtime.

4. In the "Environment variables" section of the **Configuration information** tab, click the "Edit" button **.** 

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">In preview mode, configuration updates are supported only for the Latest version. Switch the version to Latest before you perform the operation.   </div>
   

5. In the "Editing environment variables" panel, ** add** or **modify** environment variables as needed.

6. Click "Confirm" to save the configuration.

7.  Publish the agent runtime to apply the new configuration:

   * Preview mode: Click "Save" to save the configuration. After you save the configuration, you can test the Latest version or[ publish it as an official version](https://docs.byteplus.com/en/docs/agentkit/Releasing_runtimes).

   * Non\-preview mode: After updating the configuration, click "Publish" in the upper\-right corner of the page. The new configuration takes effect only after republishing.
