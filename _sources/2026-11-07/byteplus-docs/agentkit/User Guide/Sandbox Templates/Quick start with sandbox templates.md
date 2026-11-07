---
title: "Quick start with sandbox templates"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Quick_start_with_sandbox_templates"
---

This topic is for users who are new to AgentKit, with an agent built with **VeADK (Python) and the AIO Sandbox (code sandbox) ** as an example. The following sections guide you from scratch through the complete workflow for creating a sandbox template, integrating the template into the agent, and performing the call and verification.

## Application scenarios

When an agent needs to run code, execute commands, or produce intermediate files in an isolated environment, we recommend that you use sandbox tools of the AIO Sandbox type. The value of these sandbox tools is that the runtime environment can be called on demand by the agent as a "tool", and the platform centrally manages the environment lifecycle and security isolation.

## **Sandbox instance call mechanism**

AIO Sandbox code sandbox tools support session\-based intelligent scheduling management:

* **Automatic creation**: When a `session_id` is used to initiate a request for the first time, the system automatically creates a corresponding tool instance.

* **Session reuse**: Multiple requests with the same `session_id` share the same tool instance, ensuring continuity of the code execution context.

* **Lifecycle**: Each instance has a default validity period of 30 minutes and is automatically terminated upon expiration. You can also manually adjust the instance lifecycle duration. For details, refer to [Updating lifecycle duration](https://docs.byteplus.com/en/docs/agentkit/Modify_the_lifecycle_duration_of_a_tool_instance).

* **Isolation**: Requests with different `session_id` values run in independent sandbox environments and do not affect each other.

## Prerequisites

Before you begin, make sure that you have completed all of the following preparations. Otherwise, you cannot complete the subsequent operations.

* **Basic permissions:**  You can log in to the [AgentKit console](https://console.byteplus.com/agentkit) and have permission to create tools.

* **Local Python environment:**  We recommend Python 3.10 or later, and you can install dependencies properly.

* The agent has been built with [VeADK](https://docs.veadk.xyz/productions/veadk/preview/en) and published to the agent runtime in the AgentKit console. For details, refer to[ Developing and deploying agents with VeADK](https://docs.byteplus.com/en/docs/agentkit/agent_development_and_deployment_tutorial?lang=en).

* **AK/SK (required for local operations): ** You have logged in to the platform console and [obtained the AK/SK](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey). You can create and obtain an **Access Key ID ** and ** Secret Access Key**[ on the Access Key Management](https://console.byteplus.com/iam/keymanage/) page.

* The following configurations are optional. Select them as needed. Some optional configurations may incur fees, such as TOS. This topic does not cover these configurations for simplicity.

   *  **(Optional) TOS**: If you need to use TOS to store sandbox template data, make sure that the following requirements are met: [TOS is activated](https://console.byteplus.com/tos), and a TOS bucket has been created in the region where you want to create the sandbox template. For details, see[ Creating buckets](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

   *  **(Optional) Logs**: If you need to view the service runtime logs, make sure that[ Observability Platform](https://console.byteplus.com/observe/dashboard/dashboard?) has been activated.

   *  **(Optional) VPC**: If you need to access the sandbox template over a VPC, make sure that BytePlus VPC has been activated and that a VPC and subnet have been created in the region where you want to create the sandbox template. For more information, see [Creating VPCs](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [Creating subnets](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).

* (Optional) A gateway instance has been created. All demo operations in this topic use **Shared mode** to create sandbox templates.

## Procedure

### Step 1: Create an AIO Sandbox template

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Sandbox Template".

3. Click the "Create sandbox template" button. On the creation page, configure the parameters described in the table below. After the parameters are configured, click the "Create" button to complete the operation.

   > **tip**

   > In this practice, only the required parameters are configured. Keep the default values for parameters not mentioned. For information about all parameters, see [Creating sandbox templates](https://docs.byteplus.com/en/docs/agentkit/Creating_tools).

   |Parameter​ |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Term |Set the name for the newly created sandbox template.<br><br>> **warning**<br><br><br><br>* > Sandbox template names must be unique within the same account.<br><br><br>* > Once a sandbox template is created, its name cannot be changed.<br> |Sandbox_9dzj1f |
   |Type<br><br> |Select the type of preset sandbox template. Here, select **Preset template** and **AIO Sandbox.** <br><br><br>* **AIO Sandbox**: An all\-in\-one runtime environment for AI agents. Includes Browser, Terminal, and Code runtime environments. Suitable for multi\-step, complex tasks, with automatic switching between runtime environments based on the task. |AIO Sandbox |
   |**Network configuration** |||
   |Network access |Configure the access method for the newly created sandbox template.<br><br><br>* **Private network**: Access the sandbox template over a private network for higher security. Select the target VPC and subnet from the drop\-down lists. Only one subnet can be selected for each availability zone.<br><br>* **Public network**: Access the sandbox template over the public network. This is the default access method. |Public network |
   |**Permission and access control** || |
   |Inbound identity authentication |Configure the authentication information for the hosted resources of the sandbox template to control who can access these resources. Here, select **API Key**.<br><br>> **tip**<br><br><br>> After you enter a name, the system automatically creates an API Key and associates it with the sandbox template. After the sandbox template is created, you can view the API Key on the target sandbox template details page.<br> |apikey_fqahex2m |
   |**Advanced configuration** |||
   |Snapshot |Specifies whether to enable the snapshot feature. Here, this parameter is set to **enabled.** <br><br><br>* Disabled by default. If you need to retain intermediate outputs or resume from a previous state, enabling this feature is recommended. For one\-off tasks or cost\-sensitive scenarios, enabling this feature is not recommended.<br><br>* Once the snapshot feature is enabled, the platform automatically creates a snapshot before the sandbox template instance expires, saving the instance data and environment for later instance restoration. For restoration operations, see [Using snapshots to restore instances](https://docs.byteplus.com/en/docs/agentkit/Using_snapshots_to_restore_instances).<br><br>* After the snapshot feature is enabled, snapshot creation is only triggered by the system before the instance expires. Instances that are manually deleted or abnormally reclaimed are not retained. |Enable |
   |Observability service |Specifies whether to enable the observability service. Here, this parameter is set to **disabled.** <br><br>> **warning**<br><br><br>> The observability service is **enabled by default**. When you enable the observability service, the platform also activates the APMPlus and TLS services and authorizes APMPlus to write logs. Fees are incurred during service usage. For details, see the[log billing instructions](https://docs.byteplus.com/en/docs/tls/billable_items).<br> |Disabled |

### Step 2: Obtain the local environment variables and perform integration into your agent

In this section, you integrate the sandbox template into an agent built with VeADK. Since your local machine is used first for operation, you need to manually configure the sandbox template ID and the AK/SK information.

1. On the "Integration information" tab of the sandbox template **Sandbox_9dzj1f**, obtain the environment variable configuration information.

2. Under "API Access Key" in the [IAM console](https://console.byteplus.com/iam/keymanage), click the "Create Access Key" button to create an Access Key. After creation, copy the Access Key ID (AK) and Secret Access Key (SK).

3. The structure of the agent project that you built locally with VeADK is as follows. You need to add the AK/SK information and the sandbox template ID for the agent.

   * **Project structure**

      ```Plain Text
      your_project
      ├── __init__.py 
      ├── .env        
      └── agent.py    
      ```

   * **Set environment variables in the local environment**

      1. Open a terminal on your local machine, and then execute the` source .venv/bin/activate `command to activate the virtual environment.

      2. Enter the following commands to set environment variables and add AK/SK information. Replace `<your_access_key>` and `<your_secret_key>` with your actual AK/SK information.

      > **warning**

      * > Since AK/SK are highly sensitive credentials, directly writing them into static configuration files, such as `.env`, poses a security risk. When you configure AK/SK in the local development environment, we recommend managing them by exporting session\-level environment variables in the terminal.

      * > Terminal session\-level environment variables are temporary and apply only to the current terminal window. Configure the environment variables again after you close and reopen the terminal window or open a new one.

      ```Bash
      export BYTEPLUS_ACCESS_KEY=<your_access_key>
      export BYTEPLUS_SECRET_KEY=<your_secret_key>
      ```

      3. Execute the` cd <agent_project_root_directory>` command to enter the agent project root directory. Replace `<agent_project_root_directory>` with the actual path of your root directory.

   * **Configure environment variables in **  **`.env`**

      4. In the same terminal window, execute the following commands to append the sandbox template ID and region to the **` .env`** file. These commands only append information and do not overwrite the existing sandbox template configuration.

      ```Bash
      echo "AGENTKIT_TOOL_ID=<tool_id>" >> <Agent project root directory>/.env
      echo "AGENTKIT_TOOL_REGION=<tool_region>" >> <Agent project root directory>/.env
      ```

      |Parameter​ |Source |
      |---|---|
      |<tool_id\> |Replace the value with the ID of the sandbox template, which has been obtained in the previous steps. |
      |<tool_region\> |Replace the value with the region where the sandbox template resides, which has been obtained in the previous steps. |
      |<agent_project_root_directory\> |Replace the value with the actual root directory of your agent project, such as `/Users/Doc/personal_assistant`. |

      4. Execute the following command to check whether the information has been added.

      ```JSON
      cat <Agent project root directory>/.env
      ```

      **Operation result**: The command output includes the added sandbox template information.

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_255e9484af2cc73feeec04fc635bf107.png)

### Step 3: Verify the result

1. In the same terminal window, execute the` veadk web `command to start the VeADK Web interface.

   > **tip**

   > The prerequisites for this procedure require that you have built an agent using [VeADK](https://docs.veadk.xyz/productions/veadk/preview/en). Therefore, you can directly execute the `veadk web` command to start the VeADK Web interface. If you have not built an agent yet, the interface cannot be started with this command. In this case, first see [Developing and deploying agents with VeADK](https://docs.byteplus.com/en/docs/agentkit/agent_development_and_deployment_tutorial?lang=en).

2. In the local browser on the terminal where your project is located, enter the VeADK Web URL and select the target agent. Then, enter the prompt "What is the sum from 1 to 100? Write Python code to calculate it." If "run_code" appears during execution, the agent has started a sandbox instance and is processing the task in the instance.

3. Return to the terminal where veadk web is running and press Ctrl+C to stop the process. Then, execute the `agentkit launch `command to push the local configuration to the AgentKit agent runtime.

4. Return to the[ AgentKit console](https://console.byteplus.com/agentkit).  On the Instance management tab of the sandbox template **Sandbox_9dzj1f**, you can see that the sandbox instance has been created and used by the agent.

   > **tip**

   > In this practice, you enable the Snapshot feature in step 1 when you create the sandbox template. If no instance is displayed on the Instance management tab, the instance lifecycle may have ended. In this case, you can view the information about one instance on the Snapshot tab.

## Troubleshooting

If the procedure does not work as expected, we recommend that you troubleshoot in the following order:

* **Missing environment variables: Check whether ** `AGENTKIT_TOOL_ID`, `BYTEPLUS_ACCESS_KEY`, and `BYTEPLUS_SECRET_KEY` are all correctly set.

* **Region consistency**: The `<tool_region>` value that you configure when appending the sandbox template information must be consistent with the region that you select when creating the sandbox template.

* **AK/SK permissions**: Make sure that the account to which the AK/SK belongs has permissions to access AgentKit resources.

* **Sandbox template status**: Make sure the sandbox template is created and not deleted. If necessary, you can view the sandbox template status in the console.
