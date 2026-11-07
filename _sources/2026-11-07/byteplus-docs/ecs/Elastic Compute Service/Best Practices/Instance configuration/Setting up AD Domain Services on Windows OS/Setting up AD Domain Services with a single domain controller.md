---
title: "Setting up AD Domain Services with a single domain controller"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Building-a-Windows-AD-domain-for-an-ECS-instance"
---

This topic uses the Windows Server 2022 Datacenter operating system as an example to describe how to deploy Windows Active Directory (AD) Domain Services with a single domain controller.

<span id=".5YWz5LqOQUQ="></span>
## About AD Domain Services

AD Domain Services is a core directory service provided by Microsoft for the Windows Server operating system. Essentially, it is a centralized, hierarchical database designed to store and manage information about all resources in a network environment. Its core value lies in the unified management and authentication of users, computers, policies, and resources. This enables administrators and network users to easily locate and utilize such information, thereby achieving efficient and secure centralized management. [Learn more](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/get-started/virtual-dc/active-directory-domain-services-overview).

Scenarios suitable for deploying a single domain controller:


* Small\-sized organizations (such as teams with fewer than 50 members) that require low costs and minimal maintenance efforts.

* Testing/experimental environments used for functional verification or short\-term projects.

* Temporary branch offices that do not demand high availability and can restore services via domain service backups from the headquarters.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Purchase two ECS instances running the Windows Server operating system (Windows Server 2022 Datacenter is used in this topic). One of them will serve as a domain controller (DC) and the other one as a client. [Learn more](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* Prepare the instance network environment

   * Network information: A VPC is adopted as the network type in this topic, with the CIDR block set to `192.168.0.0/24`.

   * Domain name information: Prepare the domain name information. `example.com` is used as the sample domain name in this topic.

   * Private IP addresses of instances:

      * Private IP address of the instance serving as the DC: `192.168.3.126`

      * Private IP address of the instance serving as the client: `192.168.3.128`


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Make sure that both instances support the DNS service and the TCP/IP protocol.</div>


* <div data-tips="true" data-tips-type="warning">After you set up an AD domain, make sure that the IP address associated with the ECS instance is fixed all the time. Otherwise, you may fail to access the ECS instance.</div>


* <div data-tips="true" data-tips-type="warning">We recommend that you do not create a custom image from an existing domain controller instance and then deploy new domain controller instances using this custom image. If this method has to be used, make sure that the hostname of the newly created instance is the same as that of the original domain controller instance. Otherwise, an error message "The security database on the server does not have a trust relationship for this workstation" may appear. Or, after you create the instance, change its hostname to the existing instance hostname to avoid this issue.</div>



<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YOo572yQUTln5_mjqfliLblmag="></span>
### Step 1: Deploy DC for the AD domain


1. [Log in to the instance serving as the DC](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Windows-instance).

2. Click "Start \> Server Manager".

3. In the "Server Manager" window, click "Add roles and features".

4. In the pop\-up "Add Roles and Features Wizard" window, click the "Next" button to enter the "Select installation type" page.

5. On the "Select installation type" interface, select "Role\-based or feature\-based installation", and then click the "Next" button.

6. On the "Select destination server" page, keep the default settings and click "Next".

7. On the "Select server roles" page, select "Active Directory Domain Services" and "DNS Server" in sequence.

8. On the "Confirm installation selections" page, click "Install" to start the installation process.

9. After the installation is complete, click "Close" to exit the wizard.

10. On the "Server Manager" page, click the triangle icon in the upper right corner, and in the pop\-up window, click "Promote this server to a domain controller".

11. On the "Deployment Configuration" page of AD Domain Services, select "Add a new forest", enter the AD domain name (`example.com` is used in this topic), and then click the "Next" button.

11. On the "Domain Controller Options" page, configure "Type the Directory Services Restore Mode (DSRM) password", then click "Next".

12. On the "DNS Options" page, click the "Next" button.

13. On the "Additional Options" page, retain the default setting and click the "Next" button.

14. Specify the path to store AD data, and then click the "Next" button. In the example provided in this topic, the default settings are retained.

15. On the "Review Options" page, confirm the configuration information. Then, click the "Next" button.

16. After the prerequisite check is passed, click the "Install" button to start installing the AD domain server. After the installation is complete, the instance will automatically restart.

17. After logging in to the instance again, click "Start \> Control Panel \> System and Security \> System". In the "Related settings" section, click "Rename this PC" to view the installation result.


<span id=".5q2l6aqk5LqM77ya5L-u5pS55a6i5oi356uv55qE5a6J5YWo5qCH6K-G56ymU0lE"></span>
### Step 2: Modify the Security Identifier (SID) of the client


1. [Log in to the instance serving as the client](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Windows-instance).

2. Access the official website of the [sidchg](https://www.stratesave.com/html/downloads.html) tool via a browser and download sidchg.

4. Execute the following command in Windows PowerShell to run sidchg.

   ```PowerShell
    C:\Users\Administrator\Downloads\sidchg64-3.0n.exe /R
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>C:\Users\Administrator\Downloads\sidchg64-3.0n.exe</code> with the actual path where sidchg is located.   </div>
   

2. Follow the on\-screen instructions to input the license key or trial key and press "Enter" to confirm. 

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can go to the <a href="https://www.stratesave.com/html/sidchg.html">Stratesave official website</a> to obtain a trial key.   </div>
   

3. If the sidchg tool is blocked by Windows Security Center and cannot run, add the sidchg tool process to the exclusion list in Security Center based on the error message.

   1. Click "Start \> Windows Security".

   2. In the left directory tree, select "Virus & threat protection". Then in the "Virus & threat protection settings" section, click "Manage settings".

   3. In the "Exclusions" section, click "Add or remove exclusions".

   4. Click "Add an exclusion" and select "Process". Enter the process name of the sidchg tool specified in the error message (in the example provided in this topic, `C:\Windows\Temp\sidchg64_.exe` is used), and then click "Add".

4. Follow the on\-screen instructions to enter `Y` and press "Enter" to confirm SID resetting.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">During the reset, the system is restarted.   </div>
   

5. Log in to the instance again, and execute the following command in Windows PowerShell to check whether the SID is modified.

   ```PowerShell
   whoami /user
   ```
   

   If the following output is displayed, the SID is modified.


<span id=".5q2l6aqk5LiJ77ya5bCG5a6i5oi356uv5Yqg5YWlQUTln58="></span>
### Step 3: Add the client to the AD domain


1. [Log in to the instance serving as the client](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Windows-instance).

2. Modify the DNS server address.

   1. Click "Start \> Control Panel \> Network and Internet \> Network and Sharing Center". In the "Network and Sharing Center" window, click "network_0".

   2. In the "network_0 Status" window, click "Properties".

   3. In the "network_0 Properties" window, select "Internet Protocol Version 4 (TCP/IPv4)", and then click "Properties".

   4. In the "Internet Protocol Version 4 (TCP/IPv4) Properties" window, select "Use the following DNS server addresses" and enter the private IP address of the DNS server.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Since both AD Domain Services and the DNS server are installed on the instance serving as the DC in Step 1, the address here should be set to the private IP address of the DC instance. In this topic, <code>192.168.3.126</code> is used as an example.      </div>
      

   5. Click the "OK" button to save the changes and exit the "network_0" properties settings.

3. Execute the following command in Windows PowerShell to check whether the instance serving as the client can ping the IP address of the DNS server.

   ```Plain Text
   ping example.com
   ```
   

4. Click "Start \> Control Panel \> System and Security \> System". In the "Related settings" section, click "Rename this PC".

5. In the pop\-up "System Properties" window, click the "Change..." button.

6. In the pop\-up "Computer Name/Domain Changes" window, modify the computer name as needed, select "Domain" under "Member of", enter the domain name configured in your DC instance (in this topic, the domain name is `example.com`), and then click "OK".

7. In the pop\-up "Windows Security" window, enter the username and login password of the DC, and click the "OK" button.

8. If the window for confirmation pops up as below, this means that the instance has joined the domain.

9. Click the "OK" button, and restart the instance to make the configuration take effect.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you create an ECS instance serving as the client, avoid using the custom image created based on an instance that has joined an AD domain. Otherwise, in the newly created instance using such a custom image, an error is reported as "The security database on the server does not have a trust relationship for this workstation". If you need to create a custom image based on an AD\-associated instance, we recommend removing the instance from the domain before using it to create a new custom image.   </div>
