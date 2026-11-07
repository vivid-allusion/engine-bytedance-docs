---
title: "View asset details"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/View_asset_details"
---

After assets are integrated with the LLM Application Firewall, you can view each asset's basic information, security protection data, associated protection policy, and attack log information on the asset management page.

<span id="bb98342d"></span>
## Prerequisites

You have already integrated your assets into the LLM Application Firewall. For details, see [Introduction to assets integration](https://docs.byteplus.com/docs/LLM-Application-Firewall/introduction_to_assets_integration).

<span id="ef38c5cc"></span>
## View basic information of assets

The App ID is the unique identifier of an asset, used to distinguish assets during SDK calls. The API Key is the asset's authorization key, used to verify the asset's identity during SDK calls. Follow these steps:


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/).

2. In the top bar, select your instance's region.

3. In the left navigation, select **Asset Management**, and click the asset name to view asset basic information.

   The basic information varies depending on the access method:

   
   <Tabs>
   <Tab zoneid="wyfRaQaK0x" title="SDK integration">
   <TabTitle>SDK integration</TabTitle>
   
   * **Key information**: AppID
   
   * **Usage scenario**: Pass the AppID when calling the SDK to enable the LLM Application Firewall to distinguish between different assets.
   
   
   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/07044a64a69b48029d21e2ca8468e7d6) </span>
   
   
   
   
   </Tab>
   <Tab zoneid="N4iterIlO0" title="Traffic integration">
   <TabTitle>Traffic integration</TabTitle>
   
   * **Key information**: CNAME value
   
   * **Usage scenario**: Go to the business domain name service provider and configure this CNAME address in the business domain name resolution settings to route traffic through the LLM Application Firewall for protection.
   
      <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f9389da7111c464398d18f916e135ba5) </span>
   
   
   </Tab>
   <Tab zoneid="m7btxsH4HS" title="Model service integration">
   <TabTitle>Model service integration</TabTitle>
   
   * **Key information**: Protected domain name
   
   * **Usage scenarios**: In your business requests, use this protected domain name as the request address to enable security protection through the LLM Application Firewall.
   
   
   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/531f25062a08490aab6d8a48dfb75e9f) </span>
   
   
   </Tab>
   </Tabs>
   


<span id="4d63eb79"></span>
## View asset security protection data


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/).

2. Select the instance's region from the top bar.

3. Select **Asset management** in the left navigation.

4. Select the **Overview** tab to view the protection data for the asset.


<span id="5249c011"></span>
## View protection policies for an asset


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/).

2. Select the region associated with the instance in the top bar.

3. Select **Asset management** in the left navigation.

4. Select the **Protection policy** tab to view the protection policy for the asset.

5. You can also click **Add rule** to configure a new protection policy for the asset.


<span id="4897332a"></span>
## View attack logs for an asset


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/).

2. In the top bar, select the region for the instance.

3. In the left navigation, select **Asset management**.

4. Select the **Attack Log** tab to view the attack log details for the asset.
