---
title: "Calling model services"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/call-model-service"
---

Model services provide unified call examples for provider models and model groups. On the model service details page, you can select the target to call and an authorized Proxy API Key, and copy the AgentKit Runtime, OpenAI SDK (Python), or cURL examples for quick integration with your application.

## Prerequisites

* A model service has been created, and the provider model or model group has been configured. For details, see [Creating model services](https://docs.byteplus.com/en/docs/agentkit/Creating_model_service?lang=en).

* A Proxy API Key has been created, and the target to call has been authorized for this key. For details, see [Managing Proxy API Keys](https://docs.byteplus.com/en/docs/agentkit/Managing_model_service?lang=en#w6JOgibZ).

* To call a model group, you need to create a model group and complete authorization first. For details, see [Creating and managing model groups](https://docs.byteplus.com/en/docs/agentkit/create-and-manage-model-group).

## Procedure

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, select "Gateway \> Model integration" to go to the "Model service" page.

3. In the "Sample call" section of the "Basic information" tab, select a call method.

   * **Vendor model**: Select a model provider, an authorized Proxy API Key, and a specific model.

   * **Model group**: Select an authorized Proxy API Key and the call name of a model group. In the application request, set the model field to the call name of a model group. The gateway selects an upstream model within the group based on the model group configuration.

4. Select the code example type as required and click "Copy code".

   |**Example type** |**Application scenarios** |
   |---|---|
   |AgentKit Runtime |Call a model in AgentKit Runtime. The example includes environment variables for the model service address, Proxy API Key, and model name. |
   |OpenAI SDK (Python) |Python applications that use an OpenAI\-compatible SDK. |
   |cURL |Quickly verify connectivity, or call the model without using SDKs. |

## Sample call

The following are general examples for calling model services. For actual calls, we recommend obtaining the examples directly from the console.

**AgentKit Runtime**

The following is an example of calling models in AgentKit Runtime:

```Plain Text
export MODEL_AGENT_API_BASE=<Model_BASE_URL>
export MODEL_AGENT_API_KEY=<Proxy_API_Key>
export MODEL_AGENT_NAME=<Model_ID_Or_ModelGroupCallName>
```

**OpenAI SDK (Python)**

The following is an example of calling models by using the OpenAI SDK (Python):

```Python
from openai import OpenAI

client = OpenAI(
    base_url="<Model_BASE_URL>/v1",
    api_key="<Proxy_API_Key>",
)

response = client.chat.completions.create(
    model="<Model_ID_Or_ModelGroupCallName>",
    messages=[{"role": "user", "content": "Hello, please introduce yourself."}],
)

print(response.choices[0].message.content)
```

**cURL**

The following is an example of calling models by using cURL:

```Bash
curl "<Model_BASE_URL>/v1/chat/completions"   -H "Authorization: Bearer <Proxy_API_Key>"   -H "Content-Type: application/json"   -d '{
    "model": "<Model_ID_Or_ModelGroupCallName>",
    "messages": [
      {"role": "user", "content": "Hello, please introduce yourself."}
    ]
  }'
```

**Parameter description**

|**Parameter​**  |**Description** |
|---|---|
|`MODEL_AGENT_API_BASE` |The unified Base URL of the model service. You do not need to append the provider access path when calling the model service. |
|`MODEL_AGENT_API_KEY` |The value of the Proxy API Key. This is used to call the model service. **Note that this key is not the provider API Key**. |
|`MODEL_AGENT_NAME` |The name of the target to call.<br><br><br>* Specify the ID of a specific model when calling a provider model.<br><br>* Specify the call name of a model group when calling a model group. |
|`model` |The model name passed in when you call a model with the OpenAI SDK or cURL. The name follows the same rules as `MODEL_AGENT_NAME`. |

> **warning**

* > **Proxy API Key is a sensitive credential**. Inject it through environment variables, key management services, or secure configuration centers. Avoid writing it into code repositories, logs, tickets, or public documents. If you suspect the Key has been leaked, immediately disable or delete it on the "Proxy API Key management" tab.

* > When calling a model service, use the unified address of the model service and the Proxy API Key. The request address does not contain the provider path. Set the `model` field to the call name of a model group. The gateway performs authorization validation accordingly and selects an upstream model based on weights.

##
