---
title: "Deploying veFaaS functions"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Deploying_veFaaS_functions"
---

Functions in veFaaS are the basic units of compute services. To use a function, write your business function code and configure the conditions under which the function runs. You do not need to configure or manage servers or other infrastructure, allowing your business to run reliably without O&M overhead. This topic describes the basic capabilities and workflow of veFaaS functions to help you quickly deploy a veFaaS function.

## Prerequisites

* You have completed account registration and authentication.

* You have activated veFaaS. You can log in to the[ Function Service Console ](https://console.byteplus.com/vefaas)and activate veFaaS as guided by the console.

* (Optional) To enable the VPC invocation feature, make sure that you have activated BytePlus VPC and have created a VPC, subnet, and security group in the region where the function is to be deployed. For more information, see [Creating VPCs ](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC)and [Creating security groups](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group).

* (Optional) To deliver function logs using a custom log set, make sure that you have activated BytePlus TLS and have created a log set. For more information, see [Creating log projects](https://docs.byteplus.com/en/docs/tls/Managing_projects#.5Yib5bu65pel5b-X6aG555uu) and [Creating log topics](https://docs.byteplus.com/en/docs/tls/Managing_topics#.5Yib5bu65pel5b-X5Li76aKY).

## Step 1: Prepare a function template

We have prepared a skill to help you develop complete function code. You can also develop the function code yourself based on your actual requirements. If you develop the code yourself, follow the relevant protocol constraints. For more information, see[ Function development specifications](https://docs.byteplus.com/en/docs/agentkit/Function_development_specifications).

> **tip**

> Skill development supports two runtimes: Python 3.12 and Node.js 20.x. Select a runtime based on your requirements.

### Develop functions with a skill

1. Click the following skill installation package to download it to your local computer.

   [agentkit-gateway-custom-service-extension.zip](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d71593fb32ca50e9803a1b1fedee4e6d.zip)

2. Send the skill installation package to your AI tool (such as Trae or Codex) and enter the prompt: Install this skill.

3. Enter a prompt to have the AI use the skill to generate a veFaaS function code package and save it locally.

   When you use the skill in Trae, you are prompted to answer configuration questions. For the target object, select "MCP service". Select the options for the other configuration questions based on your requirements.

4. Generate the file and save it locally. In this example, the output is `agentkit-mcp-header-inject-python3.12.zip`.

## Step 2: Create a function

1. Log in to the [Function Service Console](https://console.byteplus.com/vefaas) and select the target region in the top navigation bar.

2. In the left navigation pane, select "Function \> Function management" and click the "Create function" button.

3. Select **Event function** or **Web app function**. This topic uses **Event function** as an example: select the "Event function" tab and click "Create Event Function".

   > **warning**

   > You must select **Event function** or **Web app function** for a veFaaS function used for gateway rules. If you use function code developed with the skill we provide, you can only select**Event function.**

4. Configure the function parameters as required below. This section describes only the required parameters. For descriptions of other parameters, see [Creating event functions](https://docs.byteplus.com/en/docs/faas/Creating_event_functions).

   |**Parameter** |**Description** |
   |---|---|
   |Term |A custom function name. In this example, it is set to `hello-faas-demo`.<br><br>Function names must be unique under the same account and cannot be modified after creation. |
   |Runtime |The runtime environment for running the function code. Retain the default value, **Python 3.12**. |
   |Code package type |Select ** Upload code locally**, click "Click to upload", and select the code package developed with the skill above. This example uses `agentkit-mcp-header-inject-python3.12.zip`. |

5. Click the "Agree and create" button to finish creating the function.

## Step 3: Publish the function

1. After the veFaaS function is created, the system automatically redirects to the function details page. Click "Release" in the upper\-right corner.

2. On the "Release function" panel, select the function version, enter the version description, set the publishing method, and click "Confirm".

3. Wait until the publishing progress reaches 100%, indicating that the function has been published successfully.
