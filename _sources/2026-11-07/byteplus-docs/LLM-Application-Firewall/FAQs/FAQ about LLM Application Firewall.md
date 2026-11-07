---
title: "FAQ about LLM Application Firewall"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/FAQ_about_LLM_Application_Firewall"
---

To resolve common issues you might encounter while using the LLM Application Firewall, this guide provides answers to frequently asked questions. You can find solutions for problems related to permissions, asset management, protection policies, and SDK errors.

<span id="05ff58c1"></span>
## Permissions

<span id="161d6c50"></span>
### What permissions are required to use the LLM Application Firewall service?


|Service |Policy |Description |
|---|---|---|
|IAM |IAMFullAccess |Access Control administrator permissions: Grants permission to manage the access keys of all IAM users. |
||AccessKeyReadOnlyAccess |API Key read permissions: Allows querying the access keys of all IAM users. |
||AccessKeySelfManageAccess |API Key self\-management permissions: Allows IAM users to manage their own API keys. |
|LLM Application Firewall |LLMShieldFullAccess |Full Access for LLM Application Firewall console: Includes operations such as adding assets and configuring protection policies in the console. |
||LLMShieldReadOnlyAccess |Read\-only permissions for LLM Application Firewall console |
||TLSReadOnlyAccess |Read\-only permissions for logs of LLM Application Firewall |
||LLMShieldProtectSdkAccess |SDK invocation permissions for LLM Application Firewall |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div>


<div data-tips="true" data-tips-type="warning">If you need to use a sub\-account to call the LLM Application Firewall SDK, we recommend granting it at least the following permission policies to follow the principle of least privilege: <code>AccessKeySelfManageAccess</code> and <code>LLMShieldProtectSdkAccess</code>.</div>


<span id="bb0f2bd6"></span>
## Asset management

<span id="4fcaf093"></span>
### Can the LLM Application Firewall service be used if the service is not deployed on BytePlus?

To integrate the LLM Application Firewall service without using BytePlus server resources, you can use either the CNAME method or the SDK method. How do I obtain the origin IP address ranges for the LLM Application Firewall?

When adding a domain, the LLM Application Firewall will display the corresponding origin IP address after the configuration parameters have been submitted. You can also click the relevant domain on the asset management page to view the origin IP address range. For more information, see[Allow back-to-origin CIDR blocks](https://docs.byteplus.com/docs/LLM-Application-Firewall/Allow_back-to-origin_CIDR_blocks).

<span id="6327f6f6"></span>
### How can I verify that CNAME forwarding has taken effect?

You can refer to the following steps to verify whether CNAME forwarding is working.


1. **Modify the local hosts file**.

   Add a line to your local hosts file containing the LLM Application Firewall's IP address and the protected domain. This change routes local requests for the domain through the firewall.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/232496ea484a46b390b53861abf9611b" width="864px" />   </div>
   

2. **Verify whether the modification was successful**.

   If the command returns the IP address you specified in the hosts file, the change is successful.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/66978d95b55b4ce09d4721037f75c6d6" width="904px" />   </div>
   

3. **Verify whether the access configuration has taken effect**.

   To verify whether the website integration configuration is effective, directly access the protected domain locally. If access is successful, the configuration is successful.


<span id="7a632801"></span>
### How do I obtain the IP address of the LLM Application Firewall?


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/).

2. In the top bar, select the region to which the instance belongs.

3. Select **Asset Management** in the left navigation.

4. Select the corresponding asset.

   1. Click **Advanced Filter**.

   2. Set the access method to **traffic integration**.

   3. Click the asset name.

5. On the Basic Information page, obtain the CNAME value.

6. Open the terminal and run `ping <copied CNAME value>`.

   The following diagram illustrates Mac OS as an example.

   * ①: The copied CNAME value.

   * ②: LLM Application Firewall IP address.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c88e5d248b494a6ea7477949e1688586) </span>


<span id="1deb2957"></span>
## Attack details

<span id="08a67b18"></span>
### What does the "System prohibits access except via APIKEY" rule mean?


* **Reason**: The "System prohibits access except via APIKEY" rule is a built\-in system denylist rule. This rule will intercept all access requests that do not use APIKEY. Therefore, if your business is integrated through the BytePlus Ark platform and uses the AK/SK authentication method, it will trigger the denylist rule, resulting in the request being blocked.

* **Solution**: It is recommended to obtain the APIKEY first, then make the call.


<span id="2d2b2025"></span>
### How do I obtain an API key?


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/).

2. Select the instance's region from the top bar.

3. Select **Asset management** in the left navigation.

4. Click **More filters**, then select **Model service integration** as the integration method.

5. Click the corresponding protected website in the list to view the basic information of the website.

6. Obtain the **Ark application API Key**, and enter it into the Ark SDK initialization configuration.


<span id="a2b18c15"></span>
## Protection policy

<span id="b4aca722"></span>
### Will enabling the "block" action affect normal business operations?

The LLM Application Firewall does not block legitimate business requests. To avoid impacting normal business operations, you can first enable observation mode. In this mode, all attack logs that match detection rules are recorded and reported to the log management page. You can review event logs of the "observation" type on this page. If no false positives occur over an extended period, you can switch from "observation" mode to "interception" mode. Once interception is enabled, all attack traffic that matches detection rules will be intercepted.

<span id="564c6c35"></span>
### After the protection policy switch is disabled, does the LLM Application Firewall still record logs?

When all protection features are disabled, only traffic forwarding is performed. Attack attempts are not intercepted, recorded, or reported, and no logs are generated.

<span id="982ee88c"></span>
### Why did the custom watchlist not take effect after configuration?

This may be because the rule switch for your custom watchlist is turned off. Please go to the [Protection > Large Model Protection > custom watchlist](https://console.byteplus.com/omni-shield/llm-shield/region:llm-shield+ap-southeast-1/policy/custom-thesaurus) list and ensure that the rule switch for the corresponding custom watchlist is enabled.

<span id="d08a84fd"></span>
### How do I configure a protection policy for domains accessed via the SDK?

You can configure a prompt protection policy in the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/), and then obtain detection results and optimized prompts and responses on the server via SDK calls.

<span id="313342d0"></span>
## SDK error troubleshooting

<span id="98398ef7"></span>
### Error occurs when installing Python SDK on Windows systems: “Failed building wheel for byteplus\-python\-sdk”


* **Cause**: The Windows system has a maximum path length limitation, which leads to this issue during installation.

* **Solution**:

   1. Press `Win+R`, enter `regedit`, and open the Registry Editor.

   2. Simply set the variable `LongPathsEnabled` under the path `\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\FileSystem` to `1`.


<span id="fd5ea0bd"></span>
### An error occurs when calling the SDK: "Service is not configure".


* **Reason**: This error occurs because the required policy for the account cannot be found, which prevents SDK service calls.

* **Solution**: Ensure that the relevant protected domain information has already been added to the LLM Application Firewall console. 


<span id="0877f4a3"></span>
### Why do I get a 404 error when calling the Ark SDK with an Ark platform integration?


* **Error examples**:

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/066dd85cb1cb4a86b5d4490e6fd7f295) </span>

* **Reason**: After integrating the Ark SDK, an error in the initialization of the base_url routing configuration prevented Ark access requests from being properly routed to the LLM Application Firewall. For example, `https://<Protected domain name>/api/v3/chat/completions` is often used, but the correct path is `https://<Protected domain name>/api/v3/`.

* **Solution**: Modify the base_url setting of Ark SDK as shown in the figure below.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/80ce88a9956948ed8841bf4b483785fd) </span>
