---
title: "Managing Server-side IAM permissions"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Server_side_IAM_permission_management"
---

Server\-side Monitoring uses Identity and Access Management (IAM) to control access permissions of different identities.

<span id="ca29a7a4"></span>
## Background

The  IAM service provides fine\-grained access control capabilities for resources. You can log in as a  root user to create IAM users and assign them permission policies to enable multi\-user collaboration or secure access in various scenarios. For example, you can assign maintenance engineers permissions to manage all resources and assign operations specialists permissions to view specific resources. 

<span id="10915db5"></span>
## Prerequisites

An IAM user has been created. 

<span id="117d2a04"></span>
## Scenario 1: Grant permissions using preset policies

<span id="f38a7697"></span>
### Preset policies

Server\-side Monitoring provides the following preset policies, which are directly available for IAM user authorization.


|**Policy** |**Description** |
|---|---|
|APMPlusServerFullAccess |Grants full management permissions for Server\-side Monitoring. |
|APMPlusServerReadOnlyAccess |Grants read\-only access to Server\-side Monitoring. |


<span id="1a3ebc78"></span>
### **Grant permissions to the IAM user**


1. Log in to the [IAM console](https://console.byteplus.com/iam) as a  root user.

2. In the left navigation pane, select **User management** \> **User**. Find the target user and then click the username.

3. On the **Policy** tab of the user details page, click **Authorize**.

4. On the **Add authorization** page, search for preset policies of the **apmplus_server** service, select the desired policies, and click **Submit**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To enable fine\-grained permission control at the project level, select the target project.   </div>
   

<span id="3f1dfc6a"></span>
## Scenario 2: Grant permissions using custom policies

If the preset policies do not meet your permission granularity requirements in your actual scenario, you can create custom policies and assign them to IAM users. For example, you may allow or prohibit access to a specific API.

The content of custom policies follows the policy syntax, with key elements including Action and Resource. The Action element indicates a list of actions. The Resource element indicates the resources to which the actions apply. 

<span id="9d3d030d"></span>
### Create a custom policy


1. Log in to the [IAM console](https://console.byteplus.com/iam) as a  root user.

2. Click **Permission policy** in the left navigation pane and click **Create Policy**.

3. Set the policy name and policy content, and click **Submit**.

   * For this example, the policy name is `APMPlus-server-NotifyGroupManagement`.

   * The JSON content is as follows. You can add or remove specific actions and resources as needed.

   ```JSON
   {
     "Statement": [
       {
         "Effect": "Allow",
         "Action": [
           "apmplus_server:NotifyGroupCreate",
           "apmplus_server:NotifyGroupDelete",
           "apmplus_server:NotifyGroupUpdate",
           "apmplus_server:NotifyGroupDetail",
           "apmplus_server:NotifyGroupList"
         ],
         "Resource": [
           "*"
         ]
       }
     ]
   }
   ```
   


<span id="9c6bd5da"></span>
### Grant permissions to the IAM user


1. Go back to the **Permission policy** page, filter for the newly created custom policy, and then click **Authorization** to the right of the policy.

2. Select the IAM users to which you want to attach the policy and then click **Submit**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To enable fine\-grained permission control at the project level, select the target project.   </div>
   

<span id="30629fb9"></span>
### Validate results

After you authorize a user to access a specific API, you can test the calls to the API using Postman or other tools.
