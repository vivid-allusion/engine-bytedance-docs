---
title: "Model Intergration"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/model-intergration"
---

The model intergration page is used to centrally manage the models that need to be accessed or have been accessed under the tenant, and to maintain available access sources for different model types. The page entrance is **Setting \> Enterprise Configuration \> Model Integration**. After entering, you can view the list of model connections and **connect** to add model configuration through the upper right corner.

# Prerequisites/Precautions

Before adding a model, please confirm the following conditions.

## Permissions and environment

* Has logged in to the console of the corresponding tenant and has model integration management permission;

* Access information such as model supplier, model inference access point, model name, api_key has been obtained.

## Configuration rule

* Only one default model is allowed for each model type.

* When selecting **Volcano Ark** or **agent_plan**, the system will pre\-fill **base_url**; if the page displays prompt information, you can hover over the mouse to view;

* **Large model firewall** is only used for access scenarios that require protected domain names.

> **注意**

> Deleting a model affects subsequent model selection and invocation. If the model is the default model of the current type, first confirm that there is an alternative model or that the business allows no default model for a short period of time.

# Connect model

This section is used to guide the administrator through a new model integration configuration. Please prepare the supplier information, inference access point, model name and api_key before operation; fill in the fields in page order during the configuration process, complete the connection test first, and then save and return to the list check state.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/720b97c036404f81b20934ccf3c2c283~tplv-goo7wpa0wc-image.image)

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b75c7ae626c42aba8de202f45687dd5~tplv-goo7wpa0wc-image.image)

1. Log in to the BytePlus console with your account password, select iDA \> Select project and enter the product.

2. In the agent list, click the corresponding agent to enter the Q&A interface, and move the mouse to the lower left corner of the user list and click Setting.

3. Through the Setting side navigation, select **Enterprise Configuration \> Model Integration**, click the **Connect** button in the upper right corner, and fill in the relevant configuration items. The following is the configuration item description:

|Configuration item |Is it required? |Description |
|---|---|---|
|Model Type |Yes |Select the capability type of the model. Drop down and select Text model, Multimodal model, Image generation model, Video model. |
|Provider |Yes |Select the model source. Support Volcano Ark, Volcano agent_plan, Large model firewall. |
|Model inference entry point name |Yes |Fill in an easily identifiable entry point name. It is recommended to include model usage or provider information. |
|Model inference entry point |Yes |Fill in the inference entry point ID or access address assigned by the platform. |
|Model name |Yes |Select the models allowed under the current model type from the drop\-down box.<br><br>If not, first check the model type, provider, and entry point configuration. |
|api_key |Yes |Enter the required key for model integration. The key is hidden by default and will not be displayed in the clear text of the list after saving. |
|Access firewall |Required conditions |If the model call requires firewall security control, check the **access firewall** option and fill in the protected domain name as prompted on the page.<br><br>> **说明**<br><br><br>> When the current model type is an image generation model or a video model, the large model firewall should not be selected as the provider.<br> |

4. After completing the required fields, click **Test Connection**. Wait for the system to validate the model inference access point, model name, and api_key.

5. After passing the test, click **Save**. After returning to the list, confirm that the new model appears in the corresponding model type list and the status is **configured**.

# Common problem

|Question content |Answer |
|---|---|
|Why can't I see api_key in the list? |api_key is not displayed in the list to avoid key leaks. When you need to update the key, follow the edit or re\-access process currently supported by the system. |
|Why is there no option in the model name drop\-down box? |Prioritize checking that whether the model type, provider, model inference entry point, and api_key filled in are correct. The Model Name drop\-down box displays only the models that are allowed and can be returned under the current model type. |
|When do I need to configure a firewall? |Configuration is required when a model invocation portal requires security controls, or when a provider selects a large model firewall. Ordinary Volcano Ark or Volcano Agent Plan access usually does not require filling additional protection domain name, which is subject to the page prompts. |
|Are both SaaS and privatization configured here? |No. SaaS uses the model integration page for product dimension model integration; the privatization environment inherits the Minibase model management and does not repeatedly build this integration page. |
|Does the agent\-level model configuration need to be completed on this page? |This page deals with model integration for the product dimension. Agent\-level model configuration is used to select a default model within the range of available models or to allow users to switch models on the session side, which can be configured in the agent model configuration. |
