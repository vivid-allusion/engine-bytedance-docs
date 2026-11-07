---
title: "Configure web content filtering policies"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configure-web-content-filtering-policies"
---

**Web content filtering** provides granular control over endpoint users' website access behavior. By creating policies, you can allow or block users from visiting specific categories of websites, helping your organization strengthen network security, maintain regulatory compliance, and improve employee productivity. Common use cases include:

* **Improving productivity**: Restricting or blocking access to non\-work\-related websites such as video streaming, social media, and gaming during work hours.

* **Strengthening security**: Preventing employees from visiting phishing, malware, botnet, and other high\-risk websites.

* **Ensuring compliance**: Blocking access to illegal or inappropriate content such as gambling and violence, in accordance with corporate or industry regulations.

## Prerequisites

Refer to [Configure traffic diversion policies](https://docs.byteplus.com/configure-traffic-diversion-strategy) and complete the following configurations:

1. **Configure a traffic routing policy**: Ensure that traffic from managed endpoints is routed through the SWG tunnel.

2. **Distribute the corporate root certificate**: Ensure that endpoints trust the corporate CA certificate, enabling the system to decrypt HTTPS traffic for content inspection.

> **注意**

> Deep inspection in web content filtering depends on SSL/TLS decryption.

* > **Automatic decryption**: If a policy references specific website categories or custom domains, the system automatically triggers decryption by default.

* > **SSL policy takes precedence**: If you have configured a "Do not decrypt" rule for a resource in the SSL decryption policy, the system will skip packet inspection because SSL policies have the highest priority. In this case, the web filtering module can only block access based on the domain name — it cannot filter based on specific URL paths or page content.

## Configure a filtering policy

Log in to the SealSuite Admin Console, choose **SWG** \> **Web Filtering**, and click **New Policy** on the **Policy Management** tab. On the **Add control policy** page, complete the following configurations in sequence.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b47125c6ced442209823c72671c497a8~tplv-goo7wpa0wc-topic.webp)

### Basic information

Set the policy name, priority, and website categories to control.

|Configuration item |Description |
|---|---|
|**Policy name** |Enter a custom name to identify the policy. Up to 60 characters are supported. |
|**Priority** |Set a value from 0–100. A higher value indicates a higher priority. When multiple policies conflict, only the policy with the highest priority is enforced. If priorities are equal, the policy with the higher action priority takes effect. |
|**Website category** |Select the website categories to control. Select preset categories from the **Built\-in website category library**, or select enterprise\-maintained categories from **Custom website categories**.<br><br><br>* **Built\-in website category library**: SealSuite provides a built\-in website category library covering dozens of dimensions, including social media, online games, illegal content, and recruitment. It covers tens of millions of resource sites. The system automatically identifies and matches the corresponding traffic.<br><br>* **Custom website categories**: To maintain custom categories, go to **System settings** \> **Resource management** \> **Resource library** \> **Website category library**. For more information, see [SWG Web resource library management](https://help.feilian.cn/help-center/swg-web-resource-library-management).<br><br><br>> **注意**<br><br><br>> Website addresses not included in the built\-in resource library are automatically classified as "**Unknown**" resources and centrally included in the "**Other**" category. When Administrators configure filtering policies, especially for highly sensitive user groups or critical devices, we recommend selecting this category as well. This ensures all long\-tail access traces are included in the control scope and prevents audit blind spots.<br><br><br>> If audit logs later show a large number of "Uncategorized" or "Unknown" website visits, the system also supports **batch categorization** in the **Statistical analysis** module. This quickly converts audited addresses into custom resource assets without adding them manually one by one. For more information, see [Batch categorize uncategorized websites](https://help.feilian.cn/help-center/configuring-website-content-filtering-policy#269665ab).<br> |

### Action

Select the corresponding enforcement action based on your control requirements:

|Action |Logic and expected behavior |
|---|---|
|**Access block** |Blocks employees from accessing the target website. The following block notification methods are supported:<br><br><br>* **No notification**: Terminates the connection immediately, with no redirect or message.<br><br>* **Use SealSuite built\-in information**: Redirects to the security warning page and supports custom text in multiple languages.<br><br>* **Use a custom redirect page**: Redirects to an enterprise\-specified address. HTTP, HTTPS, and IP address + port formats are supported. Only one address can be entered. |
|**Access warning** |Allows access but displays a risk warning page to the employee when the connection is established. This raises security awareness and generates an audit log stored in **Access Event Logs**. You must set the warning frequency and notification method:<br><br><br>* **Use SealSuite built\-in information**: Redirects to the security warning page and supports custom text in multiple languages.<br><br>* **Use a custom redirect page**: Redirects to an enterprise\-specified address. HTTP, HTTPS, and IP address + port formats are supported. Only one address can be entered. |
|**Access audit** |Allows employees to access the website without any interruption. The system only records the access time, frequency, and full URL in the background. Records are stored in **Access Event Logs**. |

### Scope

Select the employees or devices to which the policy applies. Configure exclusions for users or devices that do not need this policy. For example, after configuring a website access blocking policy for the sales department, exclude employees who need access for work.

* In the **Scope** area, select **User** or **Device** to set the policy scope. When you select employees, you can select by department, role, or member. When you select devices, you can set the scope based on the device conditions provided on the page.

* To exclude some objects, turn on **Exclude object**, select an object type, and then select the specific objects to exclude. To configure multiple object groups, click **Add Exclusion Object** and continue selecting the type and specific objects. For example, you can exclude specified employees and specified devices at the same time.

   You can exclude specified **Devices**, specified **Device groups**, specified **Departments** and employees in their subdepartments, specified **Roles**, or specified **Employees**.

> **注意**

> If the same object matches both the effective scope and the exclusion scope, the exclusion scope takes precedence. This policy does not apply to the object. Exclusion only skips the current policy, and the access request may still match other policies. If no excluded objects are configured, the policy is enforced based on the original effective scope.

### Advanced settings

Restrict the effective time and request methods of the policy as needed.

|Configuration item |Description |
|---|---|
|**Active period** |**All time periods by default** means no time limit is applied.<br><br>After you select **Specified time period**, configure the time when the policy applies. The policy is enforced only during the specified time period. |
|**Request method** |When you select **All**, HTTP request methods are not restricted.<br><br>After you select **Partial**, select the methods to match from the list. Standard HTTP methods and WebDAV extension methods are supported. |

After completing the configurations, click **Confirm** to save the policy.

## Manage filtering policies

Administrators can centrally operate and maintain created rules in the **Policy Management** list view:

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9e34dde190c4879a23f3025211cca77~tplv-goo7wpa0wc-topic.webp)

* **Status monitoring**: View the distribution of each policy type and the total number of policies from the statistics at the top of the list.

* **Filter and search**: Query by combining dimensions such as policy name, effective object, and application scope.

* **Status switching**: Use the **Status** switch to enable or disable a specific rule in one click. Disabled policies do not participate in traffic matching.

* **Operations**:

   * **Edit**: Modify policy parameters, the action, the effective scope, or excluded objects.

   * **Copy**: Quickly create a rule from an existing policy template. The exclusion configuration of the original policy is retained. Check the effective scope and excluded objects before saving.

   * **Delete**: Remove policies that are no longer needed. After deletion, the corresponding control logic in the web content filtering policy may change. Proceed with caution.

## Audit analysis and continuous optimization

### View audit logs

Administrators can review employees' web browsing activity on the **Access Event Logs** page:

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e4388840f5b4c35ba5b7ef3d68df4ed~tplv-goo7wpa0wc-topic.webp)

* **Filter and analyze**: Use the filters at the top to perform combined queries by trigger time, user, device, or specific access address.

* **View details**: Click **View details** in the **Action** column to see the full event profile:

   * **Triggering event details**: Includes the matched policy name, action taken, and the specific access URL.

   * **User details**: Shows the employee's account status and department.

   * **Device details**: Records the endpoint's operating system version and SealSuite client version.

### Batch\-categorize uncategorized websites

If auditing reveals a large number of "Uncategorized" sites that share the same business attributes, administrators can batch\-categorize them into a specified custom category for more precise filtering control.

1. Go to **SWG** \> **Statistical Analysis**.

2. Click **Batch add categories** in the upper\-right corner of the access domain list.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb6d035549d741459be67f4af6b847e5~tplv-goo7wpa0wc-topic.webp)

3. Perform the categorization:

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e722e1fc18e4764b6467fc60e0986b5~tplv-goo7wpa0wc-topic.webp)

   * **Select websites**: Filter and select the "Uncategorized" website addresses you want to reclassify.

   * **Select category**: Choose an existing target custom category from the dropdown list. To create a new category, go to **System settings** \> **Resource management** \> **Resource library** \> **Website category library**. For details, see [SWG Web resource library management](https://docs.byteplus.com/swg-web-resource-library-management).

4. Click **Confirm** to complete the configuration.
