---
title: "Configure traffic routing policies"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configure-traffic-routing-policies"
---

When you use SealSuite Secure Web Gateway (SWG) to control employee internet access, traffic routing policies let you specify the employees or devices to control and configure traffic that does not need to pass through SWG.

## Feature description

After a traffic routing policy is enabled, traffic from the target objects passes through SWG by default, except VPN traffic and traffic that matches exclusion rules. Traffic that enters SWG is inspected and processed based on the security policies you configure, such as website content filtering and cloud application control. Excluded traffic does not pass through SWG and is not inspected by SWG. Therefore, we recommend excluding only traffic that is confirmed to require no control.

Applicable scenarios:

* **Enable internet access control in batches**: An enterprise wants to pilot SWG in some departments before rolling it out gradually. The Administrator can set the pilot departments as target objects for the traffic routing policy. After verifying access and control results, the Administrator can expand the target scope.

* **Exclude business traffic that requires no control**: An enterprise wants to inspect employee internet traffic while keeping confirmed websites or applications connected directly to their destinations. The Administrator can exclude this traffic from SWG control by using IP, domain, or process exclusion rules.

Before adding a traffic routing policy for the first time, configure the enterprise certificate and the certificate auto\-installation scope. Enterprises that have completed the configuration can add policies directly.

## First\-time setup

Before adding a traffic routing policy for the first time, configure the enterprise self\-signed root certificate and the certificate auto\-installation scope. If the configuration is incomplete, Strategy Center displays the message "SWG traffic routing policies depend on the client certificate decryption capability. Configure the certificate auto\-installation scope."

Client trust in the enterprise CA certificate is required for SWG to decrypt and inspect HTTPS traffic. The certificate auto\-installation scope specifies which objects' clients receive and install the certificate. The target objects of the traffic routing policy specify which objects the policy applies to.

Most web access and cloud applications transmit data over the HTTPS encryption protocol. By default, SWG cannot obtain information inside encrypted traffic, such as request paths, webpage keywords, and uploaded file content. Therefore, you must configure and trust the enterprise CA certificate before SWG can identify content and filter HTTPS traffic for security.

* **Enable deep protection**: Certificate configuration is required to enable HTTPS traffic decryption ([SSL inspection](https://help.feilian.cn/help-center/configure-ssl-decryption-policy?lang=zh)). After certificate configuration is complete and related detection rules are enabled in the corresponding modules, such as website filtering, SWG automatically decrypts and deeply scans HTTPS traffic that matches the rules.

* **Ensure a seamless experience**: SealSuite automatically distributes and trusts the root certificate. This prevents risk warnings such as "Your connection is not private" caused by an untrusted enterprise CA certificate when employees access HTTPS websites.

> **注意**

* > **Enterprises that have completed the configuration can skip this section and add a traffic routing policy directly**.

* > Automatic certificate distribution takes effect only on PC desktop clients. If automatic distribution fails, install the certificate manually. For details, see "FAQ" in this document.

1. Log in to the SealSuite Admin Console and choose **SWG \> Strategy Center \> Traffic Routing**.

2. In the **Configure automatic certificate installation** guide at the top of the page, click **Configure enterprise self\-signed root certificate** to go to **Enterprise Settings \> Company General \> General Settings**.

3. In the **Root Certificate Management** area, enter **Root CA information**. If a root certificate already exists, do not enter it again.

   * **Root CA certificate name**: Enter a custom name for backend identification, such as Corporate Root CA.

   * **Parent root CA certificate file (PEM)** : Paste the certificate content, or click the upload area to upload the certificate file. The content must include the complete PEM block identifiers, including the start line and end line.

   * **Parent root CA certificate private key (PEM)** : Paste the private key content that matches the certificate, or click the upload area to upload the private key file. The content must include the complete PEM block identifiers, including the start line and end line.

4. Configure **Sub CA information**. To ensure security, we recommend issuing a subordinate CA from the root CA specifically for SWG real\-time decryption.

   * **Sub CA certificate name**: Enter a name used to identify the subordinate CA.

   * **Sub CA certificate file**: Follow the same entry method as the root CA. Paste or upload the subordinate CA certificate in PEM format, and keep the complete start line and end line.

   * **Sub CA certificate private key**: Paste or upload the PEM\-format private key that matches the subordinate CA certificate, and keep the complete start line and end line.

5. In the **Certificate Auto\-Installation Scope** area, click **Configure**, then click **Add User**, and select the scope that must automatically trust this certificate. We recommend selecting all employees.

6. Click **Confirm** to complete the configuration.

7. Return to **SWG \> Strategy Center \> Traffic Routing** and continue adding a policy.

After the configuration is saved, the SealSuite client automatically downloads the **CA certificate (public key)**  and imports it into the **trusted root certificate store** of the endpoint system. No manual action is required from employees. You can check the installation status as described in "Verify the configuration result" in this document. If automatic installation fails, install the certificate manually as described in "FAQ".

## Add a traffic routing policy

1. Log in to the SealSuite Admin Console.

2. In the left navigation pane, choose **SWG** \> **Strategy Center** \> **Traffic Routing**.

3. Click **Add Policy** in the upper\-right corner of the page, and complete the following configuration based on your business requirements.

### Basic information

Set the policy name and policy status.

|Configuration item |Description |
|---|---|
|**Policy name** |Enter a custom policy name. We recommend naming it based on the business scenario, such as "Allow office software traffic". |
|**Strategy status** |* **Enable**: This policy takes effect. The system takes over internet traffic from target objects and applies the exclusion rules configured below.<br><br>* **Disable**: This policy does not take effect. If a controlled object does not match any other enabled traffic routing policy, its traffic connects directly by default and does not enter the SWG tunnel. |

### Exclude content

Define the content that does not require SWG protection. Select and configure different resource exclusion types as needed.

|Configuration item |Description |
|---|---|
|**IP address** |Specify IP addresses that do not need to pass through SWG. Traffic to these addresses bypasses SWG and is transmitted directly through the local network.<br><br>You can add IP addresses in the following two ways. You can add up to 1,000 IP addresses. If this limit is exceeded, the policy cannot be saved.<br><br><br>* **Add manually**: In the **IP address** area, click **Add address** to open the **Add IP address** window, and enter or paste the addresses to exclude.<br><br>   When pasting in batches, use line breaks or Chinese or English commas as separators. The system automatically splits the input into multiple address entries. We recommend entering one address per line. Do not use spaces to separate multiple addresses.<br><br>* **Import file**: In the **IP address** area, click **Import** to upload the completed `.xls` or `.xlsx` file. You can also drag the file to the upload area, and then click **Confirm**. The file uses only column A: enter the header in the first row, and enter one IP address per row starting from the second row. Do not put multiple addresses in the same cell or in other columns. |
|**Domain address** |Specify domain addresses that do not need to pass through SWG. Traffic to these addresses bypasses SWG and is transmitted directly through the local network.<br><br>You can add domain addresses in the following two ways. You can add up to 1,000 domain addresses. If this limit is exceeded, the policy cannot be saved.<br><br><br>* **Add manually**: In the **Domain address** area, click **Add address** to open the **Add domain** window, and enter or paste the addresses to exclude.<br><br>   When pasting in batches, use line breaks or Chinese or English commas as separators. The system automatically splits the input into multiple address entries. We recommend entering one address per line. Do not use spaces to separate multiple addresses.<br><br>* **Import file**: In the **Domain address** area, click **Import** to upload the completed `.xls` or `.xlsx` file. You can also drag the file to the upload area, and then click **Confirm**. The file uses only column A: enter the header in the first row, and enter one domain address per row starting from the second row. Do not put multiple addresses in the same cell or in other columns. |
|**URL category exclusion** |Reference custom website categories to exclude access traffic to websites in the same category. If no custom website category has been added, go to **System Settings** \> **Resource Management** \> **Resource Library** \> **Website Category Library** to add one. For details, see [Maintain custom website categories](https://help.feilian.cn/help-center/swg-web-resource-library-management#bb2b1bdc). |
|**Process** |Exclude traffic based on endpoint applications (processes). Click **Select process** to add specific process rules for Windows or macOS platforms.<br><br><br>* **Configuration recommendation**: To ensure accurate traffic routing exclusion, if the target program is a signed process, enter the complete **process name + file digital signature**.<br><br>* **Platform\-specific notes**:<br><br>   * Windows: Avoid configuring an overly broad path range. If only a root drive such as `C:\` is configured, the system automatically excludes traffic from **all** processes under that drive. Use it together with the process name or signature information, or set the path to the exact application installation directory.<br><br>   * macOS: Note the signature differences across software distribution channels. For the same software, the file digital signatures of the **official website download** and the **App Store download** are usually different. To ensure that the software can be excluded successfully in all installation scenarios, we recommend entering the signature rules for both channels, or confirming that users use a unified installation source. |
|**Network location** |Define the network environments where traffic does not enter the SWG tunnel.<br><br><br>* Not configured (keep empty): Default behavior. In all environments, traffic is controlled through the SWG tunnel.<br><br>* Any network area: In all environments, traffic keeps a direct connection.<br><br>* Specific network area: When an Endpoint is located **inside** a selected area, traffic connects directly and does not enter the tunnel. For the network area configuration method, see [Network area management](https://help.feilian.cn/help-center/network-area-management).<br><br>* Unknown network area: When an endpoint is located **outside** the selected area, traffic connects directly and does not enter the tunnel.<br><br>> Configuration examples:<br><br>> * If you want employee traffic to be controlled through the SWG tunnel **regardless of location, whether in the office or at home**, **do not configure this item**. Keep it empty by default.<br><br>> * If you want employee traffic to skip the SWG tunnel **on the corporate intranet** because the intranet is secure, but require control **at home or in public places**, select **Specific network area** and select the area that represents the corporate intranet. |

### Scope

In the **Scope** area, select the employees or devices to which the policy applies, and configure excluded objects as needed.

> **注意**

> Target objects must be within the **certificate auto\-installation** distribution scope so their clients can receive the certificate required for SWG. Click **View Distribution Scope** to check the certificate distribution scope.

* **Target scope**: Select the departments, members, roles, or specific endpoint devices (groups) to which the policy applies.

   * When **User** is selected, use the search box to find departments, roles, or members, or select them on the **Department** or **Role** tab. To view lower\-level departments or members, click **Lower** and continue selecting.

   * When **Device** is selected, search for and select specific devices on the **Device** tab, or select device groups on the **Group** tab.

* **Exclude object**: Further remove objects that do not need this policy from the selected target scope. Turn on the **Exclude object** switch, select **Device**, **Device group**, **Department**, **Role**, or **User**, and then select the corresponding specific objects. To add more exclusions, click **Add Exclusion Object** to continue adding. For example, you can enable traffic routing for a department while excluding specified employees or devices that do not need this policy.

Click **Confirm** to create the policy.

## Verify the configuration result

After a traffic routing policy is enabled, the client network page for objects within the target scope displays the SWG module, and the status is **Connected**.

1. **Check the certificate installation result**. On the **SWG \> Access Devices** page, filter by **Certificate status** to check whether the target endpoint has installed the certificate successfully.

2. **Check the client connection**. On the network page of the SealSuite client on the target endpoint, check the SWG module and connection status. If the connection is abnormal, check whether the traffic routing policy is enabled, whether the target object is within the target scope, and whether the certificate was installed successfully.

After a traffic routing policy takes effect, endpoint users cannot manually disconnect SWG directly. To temporarily remove protection, users must request a release passcode from the administrator.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa75f88bfe8448a689943629194d949a~tplv-goo7wpa0wc-topic.webp)

To hide the client SWG module or change the module name, see [Customize client feature display](https://help.feilian.cn/help-center/custom-client-function-display).

## Manage traffic routing policies

Manage created policies on the **SWG \> Strategy Center \> Traffic Routing** page.

|Operation |Description |
|---|---|
|Query |Search for policies by **policy name**, **personnel**, and other conditions. Click **Expand filters** to view additional filter conditions. |
|Enable or disable |Adjust the policy status by using the status switch in the operation column. |
|**Edit** |If business requirements change, such as adding excluded IP addresses, adjusting effective departments or excluded objects, click **Edit** in the operation column. The system opens the policy configuration page and pre\-fills all parameters. After you complete the changes, click **Confirm** to apply them. |
|**Copy** |Click **Copy** to quickly create a new policy with the same configuration. The system opens the policy configuration page and pre\-fills all parameters. Modify them as needed, then click **Confirm** to apply the policy. |
|**Delete** |Click **Delete** and complete the secondary confirmation to remove policies that are no longer needed. To delete policies in batches, select multiple policies and click the **Delete** button above the list. After a policy is deleted, traffic that was previously excluded for direct connection may be redirected to the SWG tunnel. Confirm that related business is not affected before the operation. |

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3bebdcf7868b41d7abb699757b8d171c~tplv-goo7wpa0wc-topic.webp)

## FAQ

**Why is the add policy button unavailable**?

If the page prompts you to configure the certificate auto\-installation scope, click **Configure enterprise self\-signed root certificate** to go to the **General Settings** page under **Company General**. Check whether the enterprise self\-signed root certificate and certificate auto\-installation scope are configured. After completing the configuration, return to Strategy Center and continue adding a policy.

**What do I do if automatic certificate installation fails**?

In the **Root Certificate Management** area of **Enterprise Settings \> Company General \> General Settings**, click **Download Public Key** to download the certificate file in `.crt` format. Distribute the file to target employees and guide them to install it manually. After installation, check the certificate status of the target endpoint again.
