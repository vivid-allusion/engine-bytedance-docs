---
title: "Integration of crash logs and recovery with Torch Log Service"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Integration_of_crash_logs_and_recovery_with_Torch_Log_Service"
---

App Monitoring retains monitoring data for up to 90 days. By integrating crash logs and recovery logs into Torch Log Service, you can query logs over a longer period. Additionally, you can correlate and process these logs with other log types in Torch Log Service, enabling deeper log analysis.

<span id="8951c8fd"></span>
## Prerequisites

Activate Torch Log Service, create log projects, and log topics For details.

<span id="8ce88bf0"></span>
## Step 1: Create an account and authorize

Both the root user and IAM user can view the entry point for cloud product integration. When the root user or IAM user accesses cloud product integration for the first time, the interface will prompt them to activate the TLS service. After following the prompt to activate the service, the respective root user or IAM user will be granted the TLSFullAccess permission.


* If TLS permission is first activated by the root user, all IAM users will be unable to view the Torch Log Service list when accessing cloud product integration, because they do not have TLS permission. The root user must, based on business requirements, grant the TLSFullAccess policy or the TLSReadOnlyAccess policy to the IAM user in the Identity and Access Management interface.

* If TLS permission is first activated for IAM user A, the root user is not affected because it has TLSFullAccess permission by default. However, except for IAM user A, other IAM users will be unable to view the Torch Log Service list during cloud product integration because they do not have TLS permission. The root user needs to grant the TLSFullAccess or TLSReadOnlyAccess policy to these IAM users in the Identity and Access Management interface, based on business requirements.

1. Use the root user account to log in to the [Identity and Access Management console](https://console.byteplus.com/iam/identitymanage/user).

2. In the left navigation bar, click **User management** \> **User**.

3. On the **User** page, click **Create User**. 

4. In the list on the **User** page, click the **Manage** button in the Actions column to the right of the newly created user.

5. On the **user details** page, click the **permission** tab, and then click **add permission**.

6. On the **add permission** page, check either the **TLSFullAccess** policy or the **TLSReadOnlyAccess** policy, then click **confirm**.


<span id="6a6cf118"></span>
## Step 2: Create import rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only accounts with Application Performance Management Plus administrator permission can create import rules. For details, refer to <a href="https://docs.byteplus.com/en/docs/apmplus/Client_permissions_management">Client permission management</a>.</div>



1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client) using the root user.

2. In the left navigation bar, click **Cloud Product Linkage**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When accessing for the first time, you need to perform cross\-service authorization between APMPlus and Torch Log Service, and activate the TLS service.   </div>
   

3. Click **Create import rule**.

4. On the **Create import rule** page, configure as follows, and then click **Confirm**.

   Parameter description:

   
   |Parameter |DescriptionS |
   |---|---|
   |Rule name |Custom rule name, used to identify the rule. |
   |Client type |Currently, only **App Monitoring** is supported. |
   |Region |Select the corresponding region for Torch Log Service. |
   |Log entries |Select a log item This project was created within the permission control module. |
   |Log topics |Select a log topic The topic is one created in Torch Log Service.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">A log topic can only store data of one log type. Because different log types have different formats and indexes, storing crash logs and recovery logs together can result in log format disorder and retrieval failure.</div><br> |
   |log type |Currently, only **crash log** and **recovery log** are supported. |
   |Log scope |* Application ID: Select an application that has already been integrated.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Do not create duplicate rules for the same application ID, otherwise there is a risk of importing duplicate data.   </div><br>   <br><br>* Log conditions: Add filter conditions. |
   |Import mechanism |* Import existing logs: Import data generated before the import rule is created into Torch Log Service.<br><br>* Import new logs: Import data generated after the import rule is created into Torch Log Service. |
   |Index configuration |Automatic configuration key\-value pair.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Ensure that the index configuration for the selected log topic is set to enable key\-value indexing; otherwise, automatic configuration will not work.</div><br> |
   


<span id="021f0d1f"></span>
## Step 3: Verify results


1. After the import is complete, you can view the import rules that have been created in the Torch Log Service list on the Cloud Product Integration page. The import status will be displayed as **Importing**.

2. Click **Go to Torch Log Service**.

3. In the **Torch Log Service** console, click **Torch Log Service** \> **Log Project Management**.

4. In the log project list, click the target log project name.

5. In the log topic list, click **Search and analyze** in the Actions column on the right of the target log topic.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Importing existing data takes a long time. If no data is found during retrieval and analysis, you can increase the search time range.   </div>
   

   * Crash log format description:

      
      |Field name |Field type |Meaning |
      |---|---|---|
      |aid |int64 |Application ID. |
      |crash_type |string |Crash types.<br><br><br>* crash<br><br>* anr<br><br>* oom_crash<br><br>* launch<br><br>* extension<br><br>* watch_dog<br><br>* native<br><br>* java |
      |time |int64 |Log occurrence timestamp, unit: milliseconds. TLS built\-in field. |
      |os |string |App\-side operating system<br><br><br>* iOS<br><br>* Android |
      |os_version |string |OS version. |
      |app_version |string |The app version. |
      |apm_version |string |APM SDK Version. |
      |sdk_version |string |SDK version (exclusive to channel mode). |
      |update_version_code |striing |APP minor version number. |
      |device_model |string |Device model. |
      |channel |string |Download channels |
      |is_jailbroken |int |Jailbreak status. |
      |rom |string |ROM information. |
      |process_name |string |Process name. |
      |device_manufacturer |string |Manufacturer. |
      |device_id |string |Device ID. |
      |net_access |string |Network type. |
      |isp |string |Internet service providers. |
      |country |string |Country name. |
      |province |string |Provinces. |
      |city |string |The city name. |
      

   * Recovery log format description:

      
      |Field name |Field type |Meaning |
      |---|---|---|
      |aid |int64 |Application ID. |
      |device_id |string |Device ID. |
      |level |string |Log level. |
      |identify |string |Identification. |
      |process_info |string |Process: the thread information. |
      |time |int64 |Timestamp of the log event (unit: milliseconds). This is a built\-in field in TLS. |
      |log_info |string |Log details. |
      


<span id="cb556234"></span>
## Other operations


* For rules being imported, only accounts with Application Performance Management Plus administrator permission can **edit**, **disable**, **enable**, and **delete** them.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The editing rules should be used with caution.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Rules for importing incremental logs: After the rules are updated, only data generated after update operations will be imported.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Rule for importing existing log data: After the rule is updated, data from before the update action will be imported, which may result in duplicate data being imported.   </div>
   

* Only accounts with Application Performance Management Plus administrator permission can **delete** rules that have been imported.
