---
title: "Setting up AD Domain Services with multiple domain controllers"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Setting_up_AD_Domain_Services_with_multiple_domain_controllers"
---

This topic uses the Windows Server 2022 Datacenter operating system as an example to describe how to deploy Windows Active Directory (AD) Domain Services with multiple domain controllers.

<span id="sMIGMaA6"></span>
## About AD Domain Services

AD Domain Services is a core directory service provided by Microsoft for the Windows Server operating system. Essentially, it is a centralized, hierarchical database designed to store and manage information about all resources in a network environment. Its core value lies in the unified management and authentication of users, computers, policies, and resources. This enables administrators and network users to easily locate and utilize such information, thereby achieving efficient and secure centralized management. [Learn more](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/get-started/virtual-dc/active-directory-domain-services-overview).

Scenarios suitable for deploying multiple domain controllers:


* Medium and large\-sized enterprises (with a large number of users or cross\-regional operations) that require load balancing and high availability.

* Businesses that require high continuity and need to avoid single points of failure (for example, if one domain controller fails, another can take over automatically).

* Multi\-site office scenarios, where deploying local domain controllers at different physical locations helps reduce authentication latency and network link load.


<span id="CFiVgCub"></span>
## Prerequisites


* Purchase three ECS instances running the Windows Server operating system (Windows Server 2022 Datacenter is used in this topic). Two of them will serve as domain controllers (DCs) and one as a client. [Learn more](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* Prepare the instance network environment

   * Network information: A VPC is adopted as the network type in this topic, with the CIDR block set to `192.168.0.0/24`.

   * Domain name information: Prepare the domain name information. `example.com` is used as the sample domain name in this topic.

   * Private IP addresses of instances:

      * Private IP address of the instance serving as the primary DC: `192.168.3.126`

      * Private IP address of the instance serving as the secondary DC: `192.168.3.127`

      * Private IP address of the instance serving as the client: `192.168.3.128`


<span id="77TLvTuE"></span>
## Procedure

<span id="pXqRTnQs"></span>
### Step 1: Deploy the primary domain controller


1. Follow the [domain controller deployment](https://docs.byteplus.com/en/docs/ecs/Building-a-Windows-AD-domain-for-an-ECS-instance#.5q2l6aqk5LiA77ya6YOo572yQUTln5_mjqfliLblmag=) guidelines to deploy the instance designated as the primary DC as a domain controller.

2. Modify the DNS server address.

   1. Click "Start \> Control Panel \> Network and Internet \> Network and Sharing Center". In the "Network and Sharing Center" window, click "network_0".

   2. In the "network_0 Status" window, click "Properties".

   3. In the "network_0 Properties" window, select "Internet Protocol Version 4 (TCP/IPv4)", and then click "Properties".

   4. In the "Internet Protocol Version 4 (TCP/IPv4) Properties" window, select "Use the following DNS server addresses" and enter the private IP address of the DNS server.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Set "Preferred DNS server" to the private IP address of the current instance. Set "Alternate DNS server" to the private IP address of the instance designated as the secondary domain controller.      </div>
      

   5. Click the "OK" button to save the changes and exit the "network_0" properties settings.


<span id="HCDawOKt"></span>
### Step 2: Deploy the secondary domain controller


1. [Log in to the instance serving as the secondary DC](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Windows-instance).

2. Modify the DNS server address.

   1. Click "Start \> Control Panel \> Network and Internet \> Network and Sharing Center". In the "Network and Sharing Center" window, click "network_0".

   2. In the "network_0 Status" window, click "Properties".

   3. In the "network_0 Properties" window, select "Internet Protocol Version 4 (TCP/IPv4)", and then click "Properties".

   4. In the "Internet Protocol Version 4 (TCP/IPv4) Properties" window, select "Use the following DNS server addresses" and enter the private IP address of the DNS server.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Set "Preferred DNS server" to the private IP address of the current instance. Set "Alternate DNS server" to the private IP address of the instance serving as another domain controller.      </div>
      

   5. Click the "OK" button to save the changes and exit the "network_0" properties settings.

3. Execute the following command in Windows PowerShell to check whether the instance serving as the client can ping the IP address of the DNS server.

   ```Plain Text
   ping example.com
   ```
   

4. Join the AD domain.

   1. Click "Start \> Control Panel \> System and Security \> System". In the "Related settings" section, click "Rename this PC".

   2. In the pop\-up "System Properties" window, click the "Change..." button.

   3. In the pop\-up "Computer Name/Domain Changes" window, modify the computer name as needed, select "Domain" under "Member of", enter the domain name configured in your DC instance (in this topic, the domain name is `example.com`), and then click "OK".

   4. In the pop\-up "Windows Security" window, enter the user name and login password of an account authorized to join the domain, then click "OK".

   5. If the window for confirmation pops up as below, this means that the instance has joined the domain.

   6. Click the "OK" button, and restart the instance to make the configuration take effect.

5. After logging in to the instance again, proceed to deploy AD Domain Services.

   1. Click "Start \> Server Manager".

   2. In the "Server Manager" window, click "Add roles and features".

   4. In the pop\-up window "Add Roles and Features Wizard", click the "Next" button to open the "Select installation type" page.

   5. On the "Select installation type" interface, select "Role\-based or feature\-based installation", and then click the "Next" button.

   6. On the "Select destination server" page, keep the default settings and click "Next".

   7. On the "Select server roles" page, select "Active Directory Domain Services" and "DNS Server" in sequence.

   8. On the "Confirm installation selections" page, click "Install" to start the installation process.

   9. After the installation is complete, click "Close" to exit the wizard.

   10. On the "Server Manager" page, click the triangle icon in the upper right corner, and in the pop\-up window, click "Promote this server to a domain controller".

   11. Proceed to the "Deployment Configuration" page of AD Domain Services.

      1. Select "Add a domain controller to an existing domain".

      2. Enter the domain name (in this topic, we use `example.com` as the domain to join).

      3. Click the "Change" button next to "Supply the credentials for this operation". Then in the pop\-up window, enter the user name and login password of an account authorized to join the domain.

      4. Click the "Next" button.

   11. On the "Domain Controller Options" page, configure "Type the Directory Services Restore Mode (DSRM) password", then click "Next".

   12. On the "DNS Options" page, click the "Next" button.

   13. On the "Additional Options" page, click the drop\-down menu next to "Replicate from" under "Specify additional replication options", select the primary domain controller, and then click "Next".

   14. Specify the path to store AD data, and then click the "Next" button. In the example provided in this topic, the default settings are retained.

   15. On the "Review Options" page, confirm the configuration information. Then, click the "Next" button.

   16. After the prerequisite check is passed, click the "Install" button to start installing the AD domain server. After the installation is complete, the instance will automatically restart.

6. After logging in to the instance again, execute the following command in Windows PowerShell to verify whether there are two domain controllers in the AD domain.

   ```PowerShell
   dsquery computer
   ```
   

   If the following output is displayed, two domain controllers are configured in the current AD domain.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_48e4ad339546af78003921dac51530f2.png) </span>


<span id="uQivzyS3"></span>
### Step 3: Configure the client instance and add it to the AD domain

Follow the guidelines for [modifying the client Security Identifier (SID)](https://docs.byteplus.com/en/docs/ecs/Building-a-Windows-AD-domain-for-an-ECS-instance#.5q2l6aqk5LqM77ya5L-u5pS55a6i5oi356uv55qE5a6J5YWo5qCH6K-G56ymU0lE) and [joining the client to the AD domain](https://docs.byteplus.com/en/docs/ecs/Building-a-Windows-AD-domain-for-an-ECS-instance#.5q2l6aqk5LiJ77ya5bCG5a6i5oi356uv5Yqg5YWlQUTln58=) to add the instance serving as the client to the AD domain.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Set "Preferred DNS server" of the client instance to the private IP address of the primary domain controller instance. Set "Alternate DNS server" to the private IP address of the secondary domain controller instance.</div>
