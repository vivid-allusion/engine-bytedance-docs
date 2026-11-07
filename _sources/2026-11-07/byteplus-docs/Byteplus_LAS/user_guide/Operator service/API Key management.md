---
title: "API Key management"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/API_key_management"
---

<span id="59d15c5d"></span>
# Function overview

The API Key provides authentication credentials for model\-related operators offered by the LAS Data Lake Service. For details on how to use the API Key with specific model operators and more information about the corresponding operators, see [Supported operators: online operators](https://docs.byteplus.com/docs/undefined/6a0311a8f7159d0515296c0f).

<span id="67c5508d"></span>
# Limitations


* Currently, each primary account supports the creation of up to 20 LAS API Keys.


<span id="e820aa13"></span>
# Create and manage LAS API Key

<span id="dd238975"></span>
## Create LAS API Key


1. Log in to [LAS console ](https://console.byteplus.com/las/region:las+ap-southeast-1/next/home?) **\>**  Resource management  **\>**  API key management page, and click the Create API key in the upper left corner.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4e0b25cffc843039753fca8e34c48f8~tplv-goo7wpa0wc-image.image) </span>

2. In the pop\-up submission form, the LAS Data Lake Service will generate a default name in the predefined format `api-key-{current timestamp}`. You can also customize your own name.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Naming rules are as follows:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Length: 1–100 characters   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Only Chinese characters, uppercase and lowercase letters, or digits can be used as the first character   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Only hyphens "\-" and underscores "_" are supported; special characters are not allowed   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aec548fe025a4a39b50a14d57d104d1a~tplv-goo7wpa0wc-image.image) </span>

3. Click **Create** to submit the creation request. The newly created API key instance will appear in the list.

4. For each tenant, the LAS Data Lake Service currently supports creating up to 5 API keys. More API key support coming soon.


<span id="aad3d9b1"></span>
## Get LAS API Key

After creating an LAS API Key, you can click the View button on the LAS API Key list page to view the value of the API Key, or click the Copy button to quickly copy the value of the corresponding LAS API Key.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f35c398707c6456baaa5a2611a6722ab~tplv-goo7wpa0wc-image.image) </span>

For each API key instance, the following information is currently displayed: **Name, API key, status,** Creation time\*\*,**Creator and other information, and two operations: Disable**/\*\*delete.

By default, the actual content of the API key is hidden. To display it, click the `👁️ butto`n.

<span id="e6880c7d"></span>
## Disable LAS API Key

The LAS Data Lake Service supports temporarily disabling API keys to flexibly address certain security requirements.

To prevent accidental operations, the LAS Data Lake Service requires manual input of the characters `Confirm Disable` for secondary confirmation before submitting the disable request.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46b3a614eba2452fbf24758973c875c6~tplv-goo7wpa0wc-image.image) </span>

After submitting the request, the API key will transition to the disabled state and take effect in about 1–2 minutes.

<span id="716d2916"></span>
## Delete LAS API Key

The LAS Data Lake Service supports deleting API keys. Similar to disabling, to prevent accidental operations, the LAS Data Lake Service requires manual input of the characters `Confirm Delete` for secondary confirmation before submitting the delete request.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f786eaefd0ba4310a39ba5c23bdceeae~tplv-goo7wpa0wc-image.image) </span>

After submitting the request, the API key will be deleted immediately and take effect in about 1–2 minutes.

<span id="8596fe57"></span>
# Configure and use LAS API Key

When using the LAS development environment to call operators for data processing task development, it is recommended to configure the API Key in environment variables rather than hardcoding it in the code. This prevents the API Key from being exposed with the code, which could result in quota usage by others and incur additional costs. For detailed configuration guidance, see [Obtain and configure the API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key).
