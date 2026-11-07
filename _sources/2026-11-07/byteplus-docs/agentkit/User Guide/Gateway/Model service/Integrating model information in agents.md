---
title: "Integrating model information in agents"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Integrating_model_information_in_agents"
---

This topic uses an agent built with [VeADK](https://docs.veadk.xyz/productions/veadk/preview/en) as an example to describe how to integrate a model connected to the model service into your agent code.

## Prerequisites

* Python 3.10 or later is installed.

* You have created a model service and connected a model. If you are using a model group to call models, you have also created the model group and granted it to the Proxy API Key you are using. For detailed instructions, refer to [Creating model services](https://docs.byteplus.com/en/docs/agentkit/Creating_model_service) and [Creating and managing model groups](https://docs.byteplus.com/en/docs/agentkit/create-and-manage-model-group).

* You have built an agent with [VeADK](https://docs.veadk.xyz/productions/veadk/preview/en). For detailed instructions, refer to [Developing and deploying agents with VeADK](https://docs.byteplus.com/en/docs/agentkit/agent_development_and_deployment_tutorial?lang=en).

## Procedure

### **Step 1: Obtain a sample call from the Model service console**

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> Model service", and click the "Basic information" tab.

3. After you select an authorized Proxy API Key and a call target, copy the system\-generated code from the "AgentKit Runtime" tab. The code includes the model service Base URL, API Key, and model name. **When you call a model group, set the model name to the model group's invocation name**.

   > **tip**

   > The system automatically generates sample code. This topic uses a model call in the AgentKit runtime environment as an example and therefore uses the AgentKit Runtime sample. If you need to quickly integrate a model into your own application, you can select the OpenAI SDK (Python) or cURL sample.

   * **AgentKit Runtime**: Applicable to scenarios where you call models directly within the AgentKit framework. The code contains `MODEL_AGENT_API_BASE` (the Base URL of the model service), `MODEL_AGENT_API_KEY` (the value of the Proxy API Key), and `MODEL_AGENT_NAME` (the model identifier). When you use a model group, set `MODEL_AGENT_NAME` to the model group invocation name. After you configure these three environment variables in the agent runtime environment, the integration is complete.

   * **OpenAI SDK (Python)** : Applicable to scenarios where you integrate models over the OpenAI\-compatible protocol. You can copy the sample code and use it directly.

   * **cURL**: Applicable to quick tests or non\-SDK scenarios. You can initiate calls directly from the command line.

4. Under "API Access Key" in the , click the "Create Access Key" button to create an Access Key. After creation, copy the Access Key ID (AK) and Secret Access Key (SK).

### **Step 2: Write environment variables to the local project**

1. Open a local terminal window and execute the following command to reactivate the virtual environment.

   ```Bash
   source .venv/bin/activate
   ```

2. Execute the following command to go to the root directory of your agent project.

   ```Bash
   cd <Project directory>
   ```

3. Execute the following commands respectively to configure environment variables.

   > **tip**

   > `MODEL_AGENT_API_KEY`is an authentication credential. We do not recommend writing it to a static `.env` file. In this topic, MODEL_AGENT_API_KEY is configured in environment variables.

   ```Bash
   # The platform AK and SK.
   export BYTEPLUS_ACCESS_KEY=<your_access_key>
   export BYTEPLUS_SECRET_KEY=<your_secret_key>
   ```

   |Parameter​ |Source |
   |---|---|
   |<your_access_key\> |Information about the platform Access Key ID (AK). |
   |<your_secret_key\> |The Secret Access Key (SK) of the platform. |

4. Execute `vim .env` to open the .env file in the root directory of the project. Press the `i` key on your keyboard to enter edit mode. Then, add the following variables (obtained from the model service sample code), press `esc` to exit edit mode, and enter `:wq` to save and exit the file.

   ```Bash
   # Model service configuration
   MODEL_AGENT_API_BASE=<base_url>
   MODEL_AGENT_NAME=<model_name>
   MODEL_AGENT_API_KEY=<model_api_key>
   ```

   |Parameter​ |Source |
   |---|---|
   |<base_url\> |The Base URL of the model provider obtained from the sample code of the model service. The Base URL does not include` /chat/completions`. Do not use MODEL_ENDPOINT. |
   |<model_name\> |The model name obtained from the model service sample code. To call a model group, enter the model group invocation name, not the model ID of a provider within the group. The model name used in this example is deepseek\-v4\-pro\-ga\-260813. |
   |<model_api_key\> |The API Key obtained from the sample code of the model service.<br><br>> **tip**<br><br><br>> This API Key is the key proxied by the gateway instance, not the actual API Key that you configured for the upstream model provider. The actual API Key of the upstream model provider is hosted only in the model gateway and is not exposed to the agent.<br> |

### **Step 3: Test and verify locally**

1. In the same terminal window, execute the` veadk web `command to start the VeADK Web interface.

   > **tip**

   > The prerequisites for this procedure require that you have built an agent using [VeADK](https://docs.veadk.xyz/productions/veadk/preview/en). Therefore, you can directly execute the `veadk web` command to start the VeADK Web interface. If you have not built an agent yet, the interface cannot be started with this command. In this case, first see [Developing and deploying agents with VeADK](https://docs.byteplus.com/en/docs/agentkit/agent_development_and_deployment_tutorial?lang=en).

2. Verify whether the model takes effect.

   * **Verification 1**: In the local browser on the terminal where your project is located, enter the VeADK Web URL. Select the target agent, and then enter the prompt "Hello". If a response is returned as expected, the model is enabled.

   * **Verification 2**: Execute `vim .env` to open the .env file in the root directory of the project. Press the `i` key on your keyboard to enter edit mode, and add `#` before the `MODEL_AGENT_API_KEY=<model_api_key>` configuration to comment out this line.

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9b2ebe832e8ac4bd2107e69ced67e995.png)

      In the VeADK interface, enter the prompt "Hello" to the target agent again. If a response cannot be returned as expected, the model is unavailable.

   * **Verification 3**: Log in to the [AgentKit console](https://console.byteplus.com/agentkit).  Choose "Gateway \> Model service", and then click the "Monitoring" tab to view the number of model call requests. If the number of model requests is not 0, the model has been called as expected.

### **Step 4: Release the agent runtime**

In the terminal window where VeADK runs, press Ctrl + C on your keyboard to stop the process. Then, execute the` agentkit launch` command to push the local configuration to the agent runtime on the AgentKit platform.
