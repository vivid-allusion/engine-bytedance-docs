---
title: "Configure SDK integration parameters"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Configure_SDK_integration_parameters"
---

To protect your application with the LLM Application Firewall using an SDK, you first need to add it as a protected asset in the console. This guide provides step\-by\-step instructions on how to configure the necessary integration parameters, such as the application name and protection policies, within the LLM Application Firewall console.

<span id="51c5a35a"></span>
## Prerequisites

You have created a protection instance. For more information, refer to [Create an LLM Application Firewall instance](https://docs.byteplus.com/docs/LLM-Application-Firewall/create_an_LLM_Application_Firewall_instance).

<span id="6654049e"></span>
## Steps


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/).

2. Select the instance's region from the top bar.

3. In the left navigation, select **Asset management**, then click **Add asset**.

4. Select **SDK integration** as the integration method, and configure the integration parameters.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/672c0ffdcb984fdc8c0e45ca8dbc9157) </span>

   * **Basic information**: Application basic information is used to identify the specific business connected to the LLM Application Firewall.

      
      |Parameters |Description |
      |---|---|
      |App name |Your custom business application name is used to distinguish different applications in the console.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Must start with a letter or a digit.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Only letters, digits, periods, underscores, and hyphens are allowed.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Length should be between 1 and 128 characters.</div><br> |
      |Description |Supplementary information about the application. |
      

   * **Protection policy configuration**

      After completing the basic information for the application, you can directly set the protection policy for the current application asset. The platform displays the default configuration of the protection policy, and the configuration is enabled.

      * If no changes are needed, you can submit the current configuration to complete the setup in the console.

      * The updated configuration will be saved as the default for future assets.

      For a detailed introduction to and configuration instructions for the corresponding policy, see [Introduction to protection policies](https://docs.byteplus.com/docs/LLM-Application-Firewall/introduction_to_protection_policy).

5. Click **Submit**.


<span id="9804376e"></span>
## What to do next

After completing the integration, you can download and use the SDK to obtain the response from the relevant interface.


1. Refer to [SDK overview](https://docs.byteplus.com/docs/LLM-Application-Firewall/SDK_overview) ** ** and download the SDK file for the corresponding language.

2. Refer to the documentation in [SDK overview](https://docs.byteplus.com/docs/LLM-Application-Firewall/SDK_overview) and integrate the SDK with your service.
