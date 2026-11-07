---
title: "Configure API protection policies"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/docs-configuring-api-protection-policies"
---

To protect your API traffic from malicious requests, you can use Web Application Firewall (WAF) API protection policies. This guide provides step\-by\-step instructions on how to configure these policies. You will learn how to define rules for specific API paths and methods through manual registration, and how to use the API auto\-discovery feature to automatically record and manage potentially risky request behaviors. 

<span id="759cQks6"></span>
## Background information 


* Manual registration: By manually adding or uploading files, API request behaviors with fixed characteristics are recorded as detection rules. When an API request matches a rule, WAF executes the corresponding action. 

* API auto\-discovery (available only for Enterprise Edition and above): WAF uses intelligent detection and learning capabilities to record API request behaviors that may pose risks as API protection rules. Automatically added rules are set to the "discovered" status by default, and the default action is "observe". You can manually confirm rules and modify actions. After confirmation, the rule switches to the "confirmed" status. 

* Unregistered API execution actions: Unregistered APIs refer to API requests that are neither manually added nor included in the API automatic discovery list. You can set a unified execution action for these APIs, including observe, do not check, or block. 

   * Observe: Allow the request, but log the request in the attack log. 

   * Do not check: Allow the request and report the request behavior to the access log. 

   * Block: Block the request and report the request behavior to the attack log. If a custom block response page is configured, WAF returns the configured block response page information to the client. 


<span id="mkexIpmq"></span>
## Important notes 

API auto\-discovery is currently available only for Enterprise Edition and above. Enabling this feature incurs a feature activation fee, a QPS package add\-on fee, and an elastic QPS add\-on fee. 

<span id="EzA7EL4W"></span>
## Requirements 

You have connected the websites that require protection to the WAF instance.

<span id="4k7jP1Yb"></span>
## Manual registration 

You can add API protection rules manually or by uploading a JSON file. 


1. Log in to the [Web Application Firewall console](https://console.byteplus.com/waf/dashboard).

2. Select the region of the instance in the top menu bar. 

3. In the left navigation pane, select **Protection policy \> API protection**. 

   1. Select the domain name for which you want to add a policy. 

   2. (Optional) Confirm that the protection mode for the current domain is set to "Enable protection"; otherwise, click **Change protection mode** to modify it. 

   3. Enable the policy switch. 

4. You can add rules manually or by uploading a file. 

   * Manual addition: Set API protection policy parameters. 

      
      |**Parameter** |**Note** |Example configuration  |
      |---|---|---|
      |API name  |A unique name for the API. <br><br>tip <br><br><br>* Must start with a Chinese character, a letter, or a digit. <br><br>* Allows letters, digits, Chinese characters, period ".", underscore "_", and hyphen "\-". <br><br>* Length must be between 1 and 128 characters.  |Delete file  |
      |API description  |Enter a description for the API rule. <br><br>tip <br><br><br>* Must start with a Chinese character, a letter, or a digit. <br><br>* Allows letters, digits, Chinese characters, period ".", space, underscore "_", hyphen "\-", equals sign "=", English comma ",", Chinese comma "，", and Chinese period "。" <br><br>* Length must be between 0 and 255 characters.  |Used to protect against unauthorized delete operations  |
      |API path  |Enter the API path. Up to 128 characters. Must comply with the Swagger PATH format and not include domain name or parameters. For example: /waf/user.  |/api/v1/delete_project_file  |
      |Request method  |Select the API request method. Supported methods are GET, PUT, POST, DELETE, OPTIONS, HEAD, PATCH, and TRACE.  |DELETE  |
      |Action  |* Observe: Allow request traffic, but log the request in the attack log. <br><br>* Block: Block request traffic and report the request activity to the attack log. If a custom block response page is configured, WAF returns the configured block response page to the client.  |Block  |
      |Rule switch  |Enable or disable the current rule.  |Enable  |
      |API rule  |Enter detailed API rule information, including parameter name, parameter location, data type, and parameter range.  |* Parameter name: ID <br><br>* Parameter location: query <br><br>* Parameter format: string  |
      

   * File upload: Import API files in JSON format in bulk. 

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The file must be a JSON file in Swagger 3.0 format, and its size cannot exceed 500 KB.       </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If you import an API that already exists, its configuration will be overwritten.       </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">After the API is successfully imported, the policy switch is enabled by default and the action is set to Observe. You can change this after importing.       </div>
      

5. Click **OK** to complete rule configuration. 

   After configuration is complete, you can view rule information in the API protection list, and perform operations such as disabling/enabling, editing, deprecating, and viewing logs. 


<span id="Frt9sJ9P"></span>
## API auto\-discovery 

WAF leverages intelligent detection and learning capabilities to record potentially risky API request behaviors as API protection rules. 

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">API auto\-discovery is currently available only for Enterprise Edition and above. Enabling this feature incurs a feature activation fee, a QPS package add\-on fee, and an elastic QPS add\-on fee.</div>


<span id="mN97ZL6w"></span>
### Procedure 


1. Log in to the [Web Application Firewall console](https://console.byteplus.com/waf/dashboard). 

2. Select the region of the instance in the top menu bar. 

3. In the left navigation pane, select **Protection policy \> API protection**. 

4. Enable the auto\-discovery feature. 

   After enabling, if the WAF detects an API request with potential risk, it will automatically generate an API rule with the action set to "Observe". The status of this rule is "Discovered". 


<span id="5vnyUigI"></span>
### Automatic rule discovery instructions 

After an automatic discovery rule is generated, you can manually modify the action or confirm the rule.
