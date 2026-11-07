---
title: "View configuration information"
product: "ContextSearch"
product_code: "contextsearch"
source: "https://docs.byteplus.com/en/docs/contextsearch/View_multimodal_configuration_information"
---

After creating a multimodal search scenario, you can view its configuration information and modify related settings based on business needs. This topic describes how to view the configuration information of a multimodal search scenario.

## Prerequisites

Created and initialized multimodal search scenarios. For detailed operations, see [Create a scenario](https://docs.byteplus.com/en/docs/contextsearch/Create_a_scenario) and [Initialize a multimodal search scenario](https://docs.byteplus.com/en/docs/contextsearch/Initialize_a_multimodal_search_scenario).

## Procedure

1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. In the left navigation pane, select **My Scene**, then click the target multimodal search scenario.

4. Click the ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_77957c2465a295f7c4c33f66bd77ad27.png) icon on the right side of the page to open the **Scene Configuration** panel and view various multimodal scene information.

   |**Category** |**Details** |
   |---|---|
   |Basic information |Includes the scene name, creation time, and description for the multimodal search scene. |
   |Search resources |Includes search resources used by the multimodal search scene. You can click the **Change specification** button on the right to modify the configuration. |
   |Import resource |Includes import resources used by the multimodal search scenario. You can click the **Start**, **Stop**, and **Change specification** buttons on the right to perform the corresponding actions. |
   |Agent Team Resources |Includes the Agent Team Resources used in the multimodal search scene. You can click the **Start** or **Stop** button on the right to perform the corresponding operation.<br><br>> **tip**<br><br><br>> Agent Team Resources are only visible when the **Enable Agent Team** switch is turned on.<br> |
   |Storage configuration |Includes the storage type and instance name/ID used by the multimodal search scene. You can click the edit icon on the right to modify the instance password. |
   |Access information |Includes the virtual private cloud, availability zone, subnet, private network access status, public network access status, private network access address, and public access address of the multimodal search scenario. After turning on private network access or public network access, you can view the corresponding access address. |
   |Embedding model |Includes the embedding model and inference service used by the multimodal search scene. You can click the edit icon on the right to modify the model, inference service, and API key in use. |
   |LLM configuration |Includes large language models and inference services used in multimodal search scenarios. You can click the edit icon on the right to modify the model, inference service, and API key in use. |
   |Rerank configuration |Includes the Rerank models and inference services used by the multimodal search scene. You can click the edit icon on the right to modify the model, inference service, and API Key used. |
   |ASR configuration |Includes automatic speech recognition models and inference services used in multimodal search scenarios. You can toggle ASR on or off using the switch on the right or click the edit icon to modify the model, inference service, and API key. |
   |Agent Team |Turning on enables multi\-Agent intelligent building, automatically generating scene configurations and outputs through conversations. |
   |Advanced configurations |Includes user\-defined parameters used in multimodal search scenarios. You can click the edit icon on the right to add, modify, or delete the user\-defined parameters used. |

## More operations

You can click **Get credentials** at the top right of the **Scene configuration** area, then view the credentials used for interface authentication in the **Credential information** window.
