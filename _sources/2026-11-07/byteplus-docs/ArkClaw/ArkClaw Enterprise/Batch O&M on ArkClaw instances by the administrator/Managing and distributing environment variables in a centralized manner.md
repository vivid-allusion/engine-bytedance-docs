---
title: "Managing and distributing environment variables in a centralized manner"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Managing_and_distributing_environment_variables_in_a_centralized_manner"
---

Administrators have permissions to configure and distribute environment variables in a centralized manner. After the configuration is complete and submitted, the system automatically triggers configuration synchronization logic and distributes the configured environment variables to all ArkClaw instances under the current workspace. You do not need to manually reload configurations or restart services for all instances because the environment variable configurations will be automatically loaded and applied. This achieves centralized management, batch synchronization, and consistency management of environment variable configurations across multiple instances. This topic describes how administrators manage and distribute environment variables in a centralized manner.

<span id="dXw1QmjN"></span>
## Background

Environment variables are dynamic key\-value pairs used to store configuration information in an operating system, such as paths, configurations, and system parameters. They are global, dynamic, and inheritable. Environment variables can achieve separation of configuration from code and isolation across multiple environments. This prevents hard‑coding of sensitive information, improves security and maintainability, simplifies program path identification, and supports cloud‑native containerized deployment.

In ArkClaw, environment variables are a core configuration method. They are commonly used for specifying the home directory, configuration file, and state storage paths, configuring security information such as gateway tokens and model API keys, adjusting runtime parameters such as log level and execution timeout, and configuring proxy configurations and custom skill paths. They support containerization, CI/CD automation, and quick switching between multiple models. This allows you to flexibly control how the program runs without the need to modify configuration files.

<span id="p5Zb5m6P"></span>
## Limits


* Environment variables are globally unique. When an administrator distributes environment variables in a centralized manner, existing environment variables with the same name in ArkClaw will be overwritten.

* During configuration center initialization, initial configurations can currently be distributed in batches only to ArkClaw instances that are in the "Running" state.


<span id="BUyxWqT1"></span>
## Procedure

<span id="VBUxDnFr"></span>
### Step 1: Enable the environment variable feature

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You need to enable the global environment variable feature when using it for the first time. The initialization operation can be repeatedly performed.</div>



1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click **O&M \> Batch O&M**.

3. Click **Global environment variable** in the upper\-right corner of the page to go to the environment variable management page.

4. Click **Enable feature** on the initialization page to enable the environment variable feature and complete initialization for instances in the "Running" state. The initialization process will apply key configurations to all existing ArkClaw instances. The process takes several minutes, which can be prolonged if more instances are involved.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If some instances fail to be initialized or are missed during initialization, you can click <strong>Re‑initialize configuration center</strong> in the upper‑right corner of the Environment variable page to establish connections again and apply initial configurations.   </div>
   

5. Go back to the Batch management page and click the **Jobs** tab to view the execution result. "Configuration center initialization" is displayed in the "Command name" column for the initialization job.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When a large number of instances exist, initialization will be automatically performed in batches. Each job supports up to 50 instances.   </div>
   

6. Click **Execution result** in the Actions column that corresponds to the job to view detailed results of the initialization job, such as the instance list, failed instance list, execution status, and execution logs.


<span id="xhPLbtcv"></span>
### Step 2: Configure custom environment variables


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click **O&M \> Batch O&M**.

3. Click **Global environment variable** in the upper\-right corner of the page to go to the environment variable management page. On this page, you can view existing environment variables, including system preset environment variables and custom environment variables.

4. Switch to the **Custom** tab. Click **Edit** or **Add** to configure custom environment variables based on your business requirements. You can add, modify, and delete environment variables. Then, click **Save changes**.

   <div data-tips="true" data-tips-type="danger" data-tips-is-title="true" data-wrapper-indent="1">danger   </div>
   

   * <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">Environment variables are globally unique, and keys cannot be duplicated.   </div>
   

   * <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">Deleted environment variables cannot be recovered. Proceed with caution.   </div>
   

5. After the environment variables are configured, they will be automatically distributed and applied to all instances under the current workspace.
