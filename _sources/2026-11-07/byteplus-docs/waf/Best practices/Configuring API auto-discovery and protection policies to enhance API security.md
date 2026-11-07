---
title: "Configuring API auto-discovery and protection policies to enhance API security"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/Best_practices_for_basic_policy_configuratiojn"
---

Web application services involve a large number of APIs, which are used to connect clients and servers and transmit data. BytePlus WAF enhances API security by identifying and monitoring unusual activities and blocking unauthorized requests based on established protection policies. This document describes how to use the API protection function to improve API security.

<span id="92c67e84"></span>
## Why is API security important? 

API attacks may involve unauthorized access, data breaches, denial of service, or manipulation of APIs to operate in unintended ways.


* Since APIs frequently manage sensitive data, an attack on an API could result in the exposure of this information, causing significant privacy and security concerns.

* API attacks can lead to application failures and service disruptions, affecting normal user activities.


<span id="e26cb24c"></span>
## What problems can the WAF API protection policies address? 

API protection policies enable the WAF to inspect API request traffic based on predetermined API formats and parameters. This allows it to filter and block unauthorized API requests that meet certain rules.


* **Identify invalid parameters**: WAF can detect invalid parameters in request traffic based on predefined rules, which helps intercept potentially risky requests and ensures business security and stability.

* **Block sensitive information**: The API auto\-discovery feature can automatically detect and block sensitive information, such as birthdates, bank card numbers, email addresses, and ID card numbers, within incoming request traffic. This ensures that user privacy remains protected during data transmission.

* **Monitor API call frequency**: For APIs added to the list, WAF tracks the number of calls made in the last 30 days and the highest QPS observed in the past 24 hours. It allows sorting based on call count and peak QPS, enhancing your efficiency in managing APIs.

* **Comprehensive management of APIs**: WAF employs a hybrid approach of manual uploads and automatic discovery, reducing the burden of manual input while guaranteeing complete coverage of APIs.


<span id="7dc13795"></span>
## Prerequisites

You have connected the website that needs to be protected to the WAF instance. For access\-related operations, please refer to [Overview of Access Methods](https://arcosite.bytedance.net/sites/1677824701538/64019309401f3c022207e76d/editor/646cb3e253a6a0022635a11e/?docLang=zh).

<span id="1da54107"></span>
## Step 1: Activate the API protection policy

<span id="41ff7e78"></span>
#### Steps


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. In the top menu bar, select the region of your instance.

3. On the left\-side navigation pane, choose **Protection Policies \> API Protection**.

4. Select the target domain name.

5. Confirm that the protection mode of the current domain is "Protection enabled". Otherwise, click **Change protection mode** to modify it.

6. Turn on the policy enable switch.


<span id="be67901f"></span>
#### Effect description

After enabling, the API icon for the domain in the domain list will display in green, indicating that the API protection function for the current domain is enabled.

<span id="4e9bb7c3"></span>
## Step 2: Configure API protection policies

You can set API protection policies for specific API paths and request methods by manual registration, or use the API auto\-discovery feature to automatically record risky API request behaviors.

<span id="cb3ce8a1"></span>
### Manual registration

If you have identified risky API paths, you can manually add them or upload a JSON file to record APIs with fixed features as assets.

<span id="cbc5b6a9"></span>
#### Steps


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. In the top menu bar, select the region of your instance.

3. On the left\-side navigation pane, choose **Protection Policies \> API Protection**.

4. Select the target domain name.

5. Add an API by manually filling out a form or uploading a file.

   * Manual addition: Manually filling out a form.

      
      |**Parameter** |**Note** |Example |
      |---|---|---|
      |Name |The name of the API request.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Start with a letter or digit.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Allowed characters include letters, digits, periods (.), underscores (_), and hyphens (\-).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The length must be between 1 and 128 characters.</div><br> |DeleteFile |
      |Description |Enter the relevant details for the API. |Used to protect against unauthorized deletion operations |
      |Endpoint |Enter the API endpoint. Up to 128 characters are allowed. It should be in swagger path format, excluding domain names and parameters. |/api/v1/delete_project_file |
      |request method |Select the API request method, which supports GET, PUT, POST, DELETE, OPTIONS, HEAD, PATCH, and TRACE. |DELETE |
      |Action |Action performed by WAF when a request triggers the rules of **Invalid parameters**.<br><br><br>* Observation: Allow the traffic to pass through, but record the behavior in the attack log.<br><br>* Block: Block the traffic and report the behavior in the attack log. If a custom interception response page is configured, WAF will return the configured interception response page information to the client side. |Block |
      |Enable |Enable or disable the rule for the API. |Keep it enabled |
      |API parameters |* Fill in the details of the API parameters, including the name, position, format, and whether they are required, along with other relevant information.<br><br>* When the **parameter format** or **whether it is a required parameter** of the request is inconsistent with the configuration, the request will be deemed an Invalid API parameters. |* Parameter name: ID<br><br>* Parameter position: query<br><br>* Parameter format: string |
      

   * File upload: Import APIs from a JSON format file.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Use a JSON file in Swagger 3.0 format. The maximum file size allowed per upload is 500 KB.      </div>
      

      2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">An existing API will be overwritten if imported repeatedly.      </div>
      

      3. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The imported APIs are automatically assigned default policies and set to 'observe' mode. You can adjust the settings once the import process is complete.      </div>
      

6. Click **OK** to complete the rule configuration.


<span id="5b45a6ee"></span>
#### Configuration Effect Description

Once the configuration is complete, you can access the API information in the API protection list. The default status of a manually registered API is "Confirmed".

<span id="20a2beda"></span>
### Enable API Auto\-Discovery

WAF automatically discovers API assets and parameter information based on intelligent detection and learning capabilities, and records them in the asset list. API auto\-discovery can bolster your API security by identifying and auto\-adding APIs that have not been manually registered. \nBy default, automatically added APIs are in the "Discovered" state and the "Observe" action is performed. You can manually verify the API information and modify the action. Once verified, the API status will change to "Confirmed".

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This feature is currently in a limited\-time free trial and is only available for Enterprise and higher plans.</div>


<span id="2e75062a"></span>
#### Procedure


1. Log in to [the Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. Select the instance region in the top menu bar.

3. On the left\-side navigation pane, choose **Protection Policies \> API** **Protection**.

4. Select the target domain name.

5. Enable auto\-discovery function.


<span id="5bee59f8"></span>
#### Effect description

Once activated, the AI icon in the domain list will turn green to indicate that API auto\-discovery is enabled for the selected domain.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the API protection policy is disabled, the AI icon will appear in yellow, signaling that API auto\-discovery is not currently active.</div>


If the WAF detects an API that has not yet been added, it will automatically add an API with the status "Discovering."

<span id="9e10bf3b"></span>
### Set default actions for unregistered APIs

Unregistered APIs refer to those that are neither added manually nor listed in API auto\-discovery, meaning routing check policies will be executed for API path access requests in states other than "Discovered" and "Confirmed." You can set uniform handling actions for these APIs, including observe, do not check, or intercept, with the default action being **do not check**.

<span id="e9578b69"></span>
#### Description of actions


* Observe: Allow the traffic to pass through, but record the behavior in the attack log.

* Do not inspect: Allow the traffic to pass through and record behavior in the access log.

* Intercept: Intercept the request traffic and report the request behavior to the attack log. If a custom interception response page is configured, WAF will return the configured interception response page information to the client side.


<span id="a8f95c5d"></span>
#### Steps


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. Select the instance region in the top menu bar.

3. On the left\-side navigation pane, choose **Protection Policies \> API Protection**.

4. Select the target domain name.

5. Set the action for unregistered APIs.


If you are uncertain about potential risks but want to ensure normal access, you can set the action to **Observe**. Then, determine whether to allow the requests based on the number of calls, the peak QPS, and the log analysis.

<span id="b5051b7d"></span>
## Step 3: Mange Risk

For example, after enabling the API auto\-discovery feature for a certain domain, an API named `/passport/proto******` is generated and shows a status of "Discovering". You've confirmed that this API is an essential API requiring completion. For further action, please refer to the steps below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">APIs that are registered manually are managed in a similar way, but they do not require manual confirmation. They can also be edited or discarded.</div>


<span id="b3161628"></span>
### Verify auto\-discovered APIs


1. Click **Confirm** in the Operation column.

2. Confirm the API name, description, endpoint, parameters, and other information according to the figure below.

3. Click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The API status switches to "Confirmed", and WAF performs detection based on the updated rules. For subsequent requests, the action is "Observe," meaning that the relevant requests are permitted.   </div>
   

4. Monitor the number of API calls, the peak QPS, and logs.

   If an attack is detected, it is advisable to modify the action of the corresponding rule to ensure business security.


<span id="67eb75c4"></span>
### Adjusting policy actions

For instance, if the API experiences significantly higher call volumes and QPS peaks compared to other interfaces, along with logs of invalid parameters and behaviors indicative of sensitive information attacks, you should configure the action for invalid parameters and sensitive information policies to "Block."


* Invalid parameters: You can directly set the action of the corresponding API to "Block" in the list.

* Sensitive information:

   1. In the API list, click the name of the corresponding API to enter the details page.

   2. In the request parameter list, select the sensitive information tag, and set the action of the tag.

      * Block sensitive information: Block the content corresponding to the sensitive tag. 

      * Only delete the tags, do not block sensitive information: Remove the sensitive information tags from the rules, allowing the corresponding content.


<span id="tF3ain6v"></span>
## WAF API protection types 

When any of these four situations are identified, the associated request behavior will be considered an API attack, prompting the execution of protective measures.


|Policy type |Description |Supported operations |
|---|---|---|
|Unregistered API exceptions |* If the action for unregistered APIs is set to "Block", all requests to unregistered APIs are considered "Unregistered API exceptions".<br><br>* If the action for unregistered APIs is set to "Observe" or "Do not inspect", requests to them are allowed and do not trigger the policy of "Unregistered API exceptions". |* Observe<br><br>* Do not inspect<br><br>* Block |
|Invalid API parameters |If the request's **Required** and **Data type** attributes do not match the parameter information in the configuration rules, the request will be identified as a parameter anomaly. The actions below are supported by this type of policy.<br><br><br>* Observe: Allow the traffic to pass through, but record the behavior in the attack log.<br><br>* Intercept: Intercept the request traffic and report the request behavior to the attack log. If a custom interception response page is configured, WAF will return the configured interception response page information to the client side. |* Observe<br><br>* Block |
|Discarded APIs |When an API is marked as "Discarded," it becomes inaccessible, and any related requests will activate the "Discarded APIs" rule, which blocks access to the API. |Discarded |
|Sensitive information |* WAF will tag APIs containing sensitive information detected in requests or responses, such as ID card numbers, bank card numbers, phone numbers, email addresses, addresses, birthdates, and names. Setting the action of a tag to "Block" prevents the transmission of associated sensitive information.<br><br>* You can manually remove a tag to prevent the WAF from detecting sensitive information associated with the API, allowing it to pass through. |* Block<br><br>* Delete |


<span id="53b15edc"></span>
## API status transition description

After the API policy configuration is complete, the corresponding assets will be generated in the API protection policy list. Among them, the status of manually registered API APIs is "Confirmed"; the status of APIs automatically discovered by API for the first time is "Discovering." You can refer to the following description to understand the different statuses of APIs and the operations that can be performed.

<span id="e144b380"></span>
### API auto\-discovery


|Status |Description |Whether the rule is performed |Next steps |
|---|---|---|---|
|Discovering |* When the WAF API auto\-discovery identifies relevant business APIs that have not been manually added, it automatically generates an API with the status "Discovering."<br><br>* At this point, the APIs are not verified and confirmed, and the associated rules will not be implemented. |No |* **Continue to discover**: AI will proceed with auto\-discovery. If the API is verified to be a business\-related API, its status will be updated to "Discovered."<br><br>* **Confirm**: Manually verify the API information that has been discovered. Once you confirm and submit, the API status will be updated to "Confirmed."<br><br>* **Discard**: Discard this API, and its status will be updated to "Discarded."<br><br>* **Ignore**: Ignore this API, and its status will be updated to "Dismissed." |
|Discovered |* When an API in the "Discovered” status is verified during the continuous discovery process, it will change to the "Confirmed” status.<br><br>* WAF will automatically monitor and block corresponding traffic based on predefined rules, even if you do not confirm the API details. |Yes |* **Confirm**: Confirm the automatically discovered API parameters, after confirmation and submission, the asset will switch to "Confirmed" status.<br><br>* **Abandon**: Abandon the asset, and the asset will switch to "Abandoned" status.<br><br>* **Ignore**: Ignore the asset, and the asset will switch to "Ignored" status. |
|Confirmed |* After manual verification, the identified APIs will be updated to "Confirmed" status.<br><br>* WAF will then automatically observe/block the corresponding traffic according to the confirmed rules. |Yes |* **Edit**: Modify the asset information by changing settings such as name, action, and parameter. The asset remains "Confirmed" after being modified.<br><br>* **Discard**: Discard the asset. The asset status will be updated to "Discarded." |
|Dismissed |* APIs in "Discovering" or "Discovered" status will be changed to "Dismissed" status if they are dismissed.<br><br>* The API will then be displayed in the "Dismissed" list.<br><br>* WAF will no longer conduct rule checks for this API. |No |* **Recover**: Recover the asset, after recovery the asset will switch to "Discovering" status. |
|Discarded |* APIs in the "Discovering," "Discovered," or "Confirmed" statuses will change to "Discarded" status after being discarded.<br><br>* The API will then be displayed in the "Discarded” list.<br><br>* WAF directly blocks requests related to this API. |No |* **Restore**: Once restoration is confirmed, you can edit the information including name, action, and API parameters. The asset status will change to "Confirmed" after being modified.<br><br>* **Delete**: Deletes the asset, but AI may discover the same one later. |


<span id="b867e52b"></span>
### Adding APIs manually


|Status |Decription |Whether the rule is performed |Next steps |
|---|---|---|---|
|Confirmed |* When APIs are added manually, their default status is set to "Confirmed."<br><br>* WAF will automatically monitor and block corresponding traffic based on predefined rules, even if you do not confirm the API details. |Yes |* **Edit**: Edit this asset, allowing modifications to the name, actions, and <参数\>Parameter</a\> configurations. The asset remains "Confirmed" after being modified.<br><br>* **Discarded**: Discard this asset, switching its status to "Discarded." |
|Discarded |* The APIs in "Confirmed" status will be changed to "Discarded" status after being discarded.<br><br>* The API will then be displayed in the "Discarded” list.<br><br>* WAF directly blocks requests related to this API. |No |* **Restore**: After confirming the restoration, the asset can be edited, supporting modifications to the name, action, and configuration of parameters, etc. After modification and submission, the asset switches to "Confirmed" status.<br><br>* **Delete**: Delete this asset, but AI may rediscover the same rule. |


<span id="03193541"></span>
## FAQ

<span id="aede8859"></span>
### Do I need to manually confirm APIs that are discovered automatically? When an API is automatically discovered for the first time, it is not validated or confirmed. If you do not manually confirm it, WAF will continue to identify the API using business traffic data.


* When the automatically discovered API is in the "Discovering" status, WAF will not perform rule detection.

* When an auto\-discovered API is in "Discovered" status, WAF will perform rule detection even if you do not manually confirm it.


<span id="4d63b03a"></span>
### How do I access APIs that have been dismissed or discarded? APIs that have been dismissed or discarded will not appear in the API protection policy list. To view them, proceed as follows:


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. Select the instance region in the top menu bar.

3. In the left navigation, select **Protection Policy \> API Protection**.

4. Select the target domain name.

5. Click **View.**  above the API rule list.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If there are no dismissed or discarded APIs under the current domain, this entry is not displayed.   </div>
   

6. View the dismissed or discarded APIs.

   * Discarded APIs: You can restore or delete them.

   * Dismissed APIs: You can restore them.
