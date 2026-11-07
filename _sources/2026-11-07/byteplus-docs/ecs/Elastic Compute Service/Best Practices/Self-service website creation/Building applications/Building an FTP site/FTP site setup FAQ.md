---
title: "FTP site setup FAQ"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/FTP_site_setup_FAQ"
---

This topic describes typical issues that you may encounter when setting up an FTP site and corresponding solutions. This facilitates efficient troubleshooting to ensure the stable and uninterrupted operation of FTP services and the security of data transfer.

<span id="xIYNaC4s"></span>
## **How to resolve file download failure from an FTP server using IE browser?** 

Refer to the following steps to enable the download permission in the IE browser.


1. Open the IE browser on the client host where files cannot be downloaded.

2. Click the Settings icon in the upper right corner of the browser, and click "Internet options".

3. Select the "Security" tab, and in the "Select a zone to view or change security settings" section, select "Internet".

4. In the "Security level for this zone" section, click the "Custom level" button.

5. Select "Downloads \> File download \> Enable" and click the "OK" button.

6. Back to the "Internet Options" page, click the "Apply" and "OK" buttons in sequence to apply and save the change.


<span id="FmRnICN5"></span>
## **What do I do if an error is reported during FTP server connection?** 

You can manually troubleshoot based on the specific FTP error or log information. For example, you can view the log file specified by the `xferlog_file` parameter in the FTP server instance. If troubleshooting fails, we recommend using a third\-party FTP client tool, such as [FileZilla](https://filezilla-project.org/).

<span id="ftxfQcdZ"></span>
## How to create a server certificate?


2. In the "Server Manager" window, select "Dashboard \> Tools \> Internet Information Services (IIS) Manager".

2. In the "Internet Information Services (IIS) Manager" window that pops up, select a server in the left navigation pane, and then double\-click "Server Certificates" in the right pane.

3. Select "Create Self\-Signed Certificate" in the "Actions" bar on the right.

4. In the "Create Self\-Signed Certificate" window that pops up, set a certificate name and certificate store type, and then click "OK" to complete the creation process.

   In the example provided in this topic, an SSL certificate of the "Personal" store type is created.

   After the creation succeeds, you can view the created certificate on the Server Certificates page.


<span id="ao7uaoFB"></span>
## How to handle FTP connection failure?


* **Check whether "Use Passive FTP (for firewall and DSL modem compatibility)" is enabled on the Windows instance**

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In the example provided in this topic, the passive mode FTP connection is used. This requires that the Windows instance IE browser have the "Use Passive FTP" feature enabled.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">By default, this setting is enabled in Windows public images provided by BytePlus. If the "Use Passive FTP" feature is not enabled in your Windows instance, follow steps below to enable it in your IE browser first. Then, try accessing the FTP site again.   </div>
   

   1. [Log in to the ECS instance that hosts the FTP site](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance), and open the IE browser.

   2. Click the Settings icon in the upper right corner of the browser, and click "Internet options".

   3. Select the "Advanced" tab, and in the "Settings" section, check the "Use Passive FTP (for firewall and DSL modem compatibility)" option.

   4. Click the "Apply" and "OK" buttons in sequence to complete the configuration.

* **Check whether "Use Passive FTP (for firewall and DSL modem compatibility)" is enabled on the Windows client**

   This topic uses an FTP connection in passive mode as an example. If you access FTP via a Windows client, you need to enable the "Use Passive FTP" feature in the IE browser of your client. Specific steps are as follows:

   1. Open the IE browser on the client host where FTP server connection failed.

   2. Click the Settings icon in the upper right corner of the browser, and click "Internet options".

   3. Select the "Advanced" tab, then in the "Settings" section, check the "Use Passive FTP (for firewall and DSL modem compatibility)" option.

   4. Click the "Apply" and "OK" buttons in sequence to complete the configuration.

* **Set the firewall to add svchost.exe to allowed programs**

   If you still cannot connect to FTP after performing the above configuration, configure svchost.exe for the ECS instance that hosts the FTP site. After this, restart the FTP service and try accessing the FTP site from the client again.

   1. [Log in to the ECS that hosts the FTP site](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

   2. Click "Start \> Control Panel".

   3. In the "Control Panel" window, click "System and Security."

   4. On the "System and Security" page, click "Windows Defender Firewall".

   5. On the "Windows Defender firewall" page, click "Allow an app or feature through Windows Defender firewall".

   6. On the "Allowed apps" page, click the "Allow other app" button.

   7. On the "Add an app" page, click the "Browse" button.

   8. On the "Browse" page, input `svchost.exe`, and click the "Open" button.

   9. On the "Add an app" page, click the "Add" button.

   10. On the "Allowed apps" page, click the "OK" button to complete adding the svchost.exe program.


<span id="SOZBk7kM"></span>
## Port range configuration recommendations in FTP passive mode

In FTP passive mode (PASV), the server dynamically assigns ports from a specified range for data connections, and the client actively connects to these ports for data transfer. Therefore, a proper port range is critical for service performance, concurrent processing capability, and security.

<span id="MzUsIPVv"></span>
### Applicable scenario


* **Concurrent connection support**

   In high\-concurrency scenarios, each concurrent data transfer requires a dedicated port.

* **Connection isolation**

   This prevents data crossover caused by port reuse, ensuring data integrity.

* **Session management**

   Associating a port with a session state can enhance session stability.

* **Load Balancer**

   Utilizing multiple ports facilitates load distribution and improves data transfer performance.


<span id="kw5JCevq"></span>
### Configuration recommendations


* **Port selection principles**

   * Avoid system ports. A port range greater than **1024** is recommended.

   * Avoid conflicts with ports used by known services.

* **Estimate concurrent connections**

   * For small businesses/departments (approximately 10–50 users), a port range of **2 x the maximum number of concurrent users** is typically sufficient.

   * For medium businesses (approximately 50–200 users), a port range of **2.5 x the maximum number of concurrent users ** is typically sufficient.

   * For large enterprises/IDCs (approximately 200+ users), a port range of **3 x the maximum number of concurrent users + a buffer ** is typically sufficient.

   * For high\-concurrency download sites (such as publicly accessible sites), a port range of **2000–5000** is typically sufficient.

* **Security enhancement**

   * Only open the necessary port range, use firewall rules to restrict access to the specified port range, and accept connections only from trusted hosts or networks.

   * Prefer FTPS (FTP over TLS/SSL) or SFTP protocols to ensure the confidentiality and integrity of data transfers, especially over public networks or in sensitive data scenarios.

* **Monitoring and audit**

   * Implement real\-time monitoring of network port usage. Use tools and log analysis to detect activities and traffic patterns with exceptions.

   * Enable detailed connection logging for real\-time monitoring of connection patterns with exceptions. Establish a security incident response process to ensure compliance and traceability.

* **Automated O&M**

   * Automate port settings and security policy deployment using configuration management tools (such as Ansible and Puppet) for standardized deployment and rapid iteration.

   * For critical business scenarios, consider deploying an FTP cluster and combining it with Load Balancer. This enables pooled management of port resources, enhancing service reliability.
