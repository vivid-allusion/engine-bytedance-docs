---
title: "Configure cloud application control policies"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configure-cloud-application-control-policies"
---

Cloud application control manages employee access to services such as personal cloud drives, collaboration tools, AI applications, and AI model relay services. Based on enterprise requirements, administrators can configure access block or access audit policies for specified employees or devices to restrict unapproved services and understand application usage.

## Feature description

Employees may use different external services during work, such as sharing files through cloud drives, collaborating with online tools, or calling large language models through AI model relay services. administrators can select the control scope by application and set corresponding access requirements for different employees or devices.

SealSuite identifies access targets through the application identification library. administrators can select built\-in applications or maintain custom application resources. Built\-in resources are organized by category, covering applications such as enterprise management, development tools, and generative AI. The AI model relay service category includes relay services. Each relay service is treated as one application, and access is identified by its associated domains. For information about viewing and maintaining application resources, see [SWG Web resource library management](https://docs.byteplus.com/en/docs/sealsuite/swg-web-resource-library-management?lang=en).

When employee access traffic passes through SWG, the system checks conditions such as the access target, employee or device, and access time. If a policy is matched, the system applies the corresponding action:

|Action |Effect |
|---|---|
|**Access block** |Blocks employee access to controlled applications and logs the event. Access block applies to the access behavior itself. Sensitive content does not need to be detected first. |
|**Access audit** |Allows access and records who accessed which application and when, so administrators can understand usage and trace access behavior. |

For example, if an enterprise requires employees to use specified file sharing and AI services, administrators can include unapproved personal cloud drives, AI applications, or model relay services in the control scope, and set **Access block** for relevant employees. To understand usage first, set **Access audit**, review access records, and then adjust the control method.

> **注意**

* > The configuration entry for **application protection policies** in the original cloud application control has been migrated to **DLP \> Strategy Center \> Control Strategy \> Network DLP**. Use it to configure auditing or blocking for sensitive text outbound transfer, file uploads, and file downloads. For details, see [Configure Web Data Protection policies](https://docs.byteplus.com/en/docs/sealsuite/configuration-web-data-protection-policy?lang=en).

* > Prompts sent to AI applications or large language model APIs are configured in **GenAI Data Protection** under the same path. For details, see [Configure GenAI Data Protection policies](https://docs.byteplus.com/en/docs/sealsuite/configure-genai-data-protection-policy?lang=en).

## Prerequisites

* A traffic diversion policy has been configured so that traffic from controlled endpoints passes through SWG. For details, see [Configure a traffic diversion policy](https://docs.byteplus.com/en/docs/sealsuite/configure-traffic-routing-policies?lang=en).

* If HTTPS traffic decryption is involved, the enterprise root certificate has been configured, and Endpoints trust the certificate. SSL decryption policies affect identifiable access content. Check whether "Do not decrypt" is configured for the target application. For details, see [Configure an SSL decryption policy](https://docs.byteplus.com/en/docs/sealsuite/configure-ssl-decryption-policies?lang=en).

## Configure a control policy

### Step 1: Enter basic information

1. Log in to the SealSuite Admin Console.

2. In the left navigation pane, choose **SWG** \> **Cloud App Control**.

3. Confirm that cloud application control is enabled, switch to the **Policy Management** tab, and click **Add Policy**.

4. On the **Add access control policy** page, complete the following settings.

|Configuration item |Description |
|---|---|
|**Policy name** |Identifies the policy and supports up to 150 characters. For example, "Block access to unapproved AI services". |
|**Priority** |The value ranges from 0–100. A larger value indicates a higher priority. If multiple policies have conflicting effective applications and effective objects, the policy with the highest priority is applied. If priorities are the same, the most recently added or modified policy is applied. |
|**Application scope** |Select the applications to control. Search by application name or domain, select by category in **Built\-in application**, or select enterprise\-configured resources in **Custom resource**.<br><br>When controlling AI applications, select the target applications under the **Generative AI** category. When controlling AI model relay services, select the target applications under the **AI Model Relay Services** category. Access control for AI applications and AI model relay services is scoped to the associated domains of the selected application or relay service. It does not distinguish between specific models provided by the same service.<br><br>To view built\-in applications or add custom applications, see [SWG Web resource library management](https://docs.byteplus.com/en/docs/sealsuite/swg-web-resource-library-management?lang=en). |

### Step 2: Select an action

Select an action based on business requirements:

* **Access block**: Applies to applications or services that the enterprise has explicitly prohibited. After a policy is matched, the system blocks access and logs the event.

* **Access audit**: Applies to applications or services whose usage needs to be understood. The system allows access and logs the event, so administrators can later evaluate and adjust policies.

When you select **Access block**, you must also set **Disabled access prompt information**:

|Prompt method |Description |
|---|---|
|**No prompt** |Blocks access without displaying a prompt page to employees. |
|**Use SealSuite built\-in information** |Uses the SealSuite prompt page. Customize the **Notification title** and **Notification content**, configure text in different languages through **Add language**, and view a preview. We recommend explaining the blocking reason and how to contact an Administrator in the prompt. |
|**Use a custom redirect page** |Redirects employee access to an enterprise\-specified page.<br><br><br>* Supports HTTP, HTTPS, or IP plus port formats, such as `http://www.test.com` or `127.0.0.1:8080`.<br><br>* Only one redirect page address is supported. |

When you select **Access audit**, disabled access prompt information is not required. Continue to set effective objects and advanced conditions. Access behavior that matches the policy is recorded in **Access Event Logs**.

### Step 3: Set effective objects

In the **Scope** area, select the employees or devices to which the policy applies, and configure exclusions as needed. For example, block the sales department from accessing a personal cloud drive, while excluding employees who need to use the cloud drive for business.

1. Select **User** or **Device** to set the effective scope.

   * When you select employees, search and select by department, role, or member.

   * When you select devices, select specified devices, or select an operating system or device group.

2. To configure exceptions, turn on **Exclude object**, then select the object type and specific objects.

   You can exclude **Device**, **Device group**, **Department** (including users in subdepartments), **Role**, or **User**.

   To add more exclusions, click **Add Exclusion Object**. After the configuration is complete, continue to set advanced conditions and save the policy.

   > **注意**

   > If the same object matches both the effective scope and the exclusion scope, the exclusion scope takes precedence, and the policy does not apply to this object. Exclusion only skips the current policy. The access request may still match other policies. If no excluded objects are configured, the policy runs based on the original effective scope.

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/swg-en-20261013/cloud-scope-en.png)

### Step 4: Set advanced conditions and save

In the **Advanced Settings** area, restrict the effective time and request methods of the policy as needed.

|Configuration item |Description |
|---|---|
|Active period |**All time period** indicates no time restriction. After you select **Specified**, set by time period or day of week. The policy runs only within the specified time period. |
|Request method |* **All** indicates no restriction on HTTP request methods.<br><br>* After you select **Restricted**, select the HTTP methods to match from the list. |

After you confirm the application scope, action, effective objects, and advanced conditions, click **Confirm** to save the policy. Return to the list and check **Status**. Policy changes may take effect with a delay due to client network connection and installation status.

## Manage control policies

On the **Policy Management** tab, search for policies by policy name, employee, device, associated application, effective status, and policy type. Then perform the following maintenance operations.

* **View status**: View policy statistics at the top of the list and the effective status of a single policy to confirm the currently enabled control scope.

* **Enable or disable**: Control the policy through the **Status** switch. To pause a policy temporarily, disable it and keep the configuration. Restore it later as needed.

* **Edit**: Adjust applications, actions, effective scope, excluded objects, or advanced conditions. For example, before changing audit to disable access, review access records to confirm the involved employees and applications.

* **Copy**: Create a similar policy based on an existing policy. The exclusion configuration of the original policy is also retained. Before saving, check the name, application scope, effective objects, and excluded objects to avoid reusing inapplicable configurations.

* **Delete**: Remove policies that are no longer used. Before deletion, confirm the access requirements covered by the policy to avoid missing applications or employees that still need control.

## View related logs

Events generated by the access control policies described in this document are recorded in **SWG \> Cloud App Control \> Access Event Logs**. View which employees accessed controlled applications and which disable access or audit access policy was matched.

1. In **SWG** \> **Cloud App Control**, switch to **Access Event Logs**.

2. Filter records by employee, device, software, matched policy, trigger time, and policy type.

3. View the trigger time, employee, accessed application, device, matched policy, and policy type in the list, and verify the control result of this access. For further investigation, view details in the **Actions** column.

### Data outbound logs

If you have also configured a Web Data Protection policy migrated to the new entry, separately view its text outbound transfer, Outbound file transfer, and file download records. Go to **DLP** \> **Investigation Audit** \> **Audit Log** \> **Network DLP**. For details, see [View Web data outbound logs](https://docs.byteplus.com/en/docs/sealsuite/view-web-data-outbound-logs?lang=en).

For prompt outbound records matched by GenAI Data Protection policies, switch to **GenAI data protection** under the same path. For details, see [View GenAI data outbound logs](https://docs.byteplus.com/en/docs/sealsuite/genai-data-outgoing-logs-view?lang=en).
