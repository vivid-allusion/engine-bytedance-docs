---
title: "Configuring operating system Single Sign-On (OS SSO)"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configuring-os-sso"
---

SealSuite allows you to implement Single Sign\-On (SSO) for macOS, Windows and Linux. By enabling this feature, employees can use their SealSuite credentials or third\-party identity provider (IdP) accounts to log directly into their computer's operating system, facilitating unified identity authentication and streamlined authorization management.

<span id="8a6d55f1"></span>
## Overview

Traditionally, enterprises relied on domain controllers exclusively for Windows environments. However, as organizations adopt a diverse range of devices and operating systems, the need for unified and convenient device management has grown. With SealSuite OS SSO, you can integrate your existing account infrastructure to provide:


* **Simplified Account Management**: Eliminates the need for separate credentials for different operating systems, significantly reducing administrative overhead and costs.

* **Enhanced Security**: Centralized authentication ensures that only authorized personnel can access corporate devices. When an employee leaves the company, administrators can instantly disable their account in the central identity source, revoking their access to all managed devices and mitigating data breach risks.


<span id="8df1546a"></span>
## Administrative Configuration


1. Log in to the SealSuite Admin Console.

2. In the left navigation pane, go to **Endpoint** \> **MDM** \> **System Login**.

3. On the **Overview** page, review the supported operating systems and click **Get Started**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4093d28aac40441c8587093207963981~tplv-goo7wpa0wc-image.image) </span>

4. Configure the functional parameters and click **Confirm**.

   
   |Section |Parameter |Description |
   |---|---|---|
   |**Authentication Source Configuration** |**Account password source** |Select the identity provider used for OS login.<br><br>The default source is **SealSuite**. You can also configure external sources (e.g., LDAP/Active Directory, RADIUS, OIDC, or CAS) under **Identity** \> **Account Setup** \> **Third\-Party Login**. |
   |**Client side binding prompt configuration** |**Box title** |Customize the title of the dialog box that appears on the SealSuite client when users are prompted to bind their passwords. Supports multi\-language configuration. |
   ||**Box description** |Provide detailed instructions or context within the binding dialog. |
   ||**Password Field Placeholder** |Customize the hint text displayed inside the password input field. |
   |**Scope** |**Effective Range** |Define the policy's reach by **User** (Department/Role) or **Device** (Group/OS/ID). |
   


<span id="042a2133"></span>
### Policy Removal Logic

If a user or device is removed from the target scope after the policy has been applied, the following logic applies:


* **If already bound**: The device will continue to use the synced IdP password. If the user subsequently changes their local password manually, that new local password will take precedence.

* **If not bound**: The device will continue to use its original local password.


<span id="82c1cc2a"></span>
## Client\-Side Password Binding

Once the administrator has deployed the OS SSO policy, users within the target scope will receive a prompt in their SealSuite client to bind their local OS password with their corporate identity password.


1. Log in to the SealSuite client.

2. A synchronization prompt will appear. The user must enter their current **Local OS Password** and their **Identity Source (IdP) Password**.

3. After successful binding, the user will use their **IdP Password** the next time they log in to the operating system.


*Note: If the user changes either their local password or their IdP password later, the SealSuite client will prompt them to perform the binding process again to maintain synchronization.* 

<span id="1fb78a44"></span>
## Monitoring and Management


1. Navigate to **Endpoint** \> **MDM** \> **System Login**.

2. Select the tab for the target platform (**macOS**, **Windows**, or **Linux**) to view the following:


<span id="acac50a1"></span>
### 1. Global Status

Check if the SSO policy is enabled for the specific platform. Disabling the global switch follows the same logic as removing an object from the target scope (see [Policy Removal Logic](https://docs.byteplus.com/docs/sealsuite/configuring-os-sso#042a2133)).

<span id="ab2438a7"></span>
### 2. Analytics Dashboard

Monitor deployment progress through key metrics:


* **Total Target Devices**: Number of devices assigned the policy.

* **Pending Setup**: Devices where the user has not yet completed the binding process.

* **Synchronized**: Devices where the local password matches the IdP password.

* **Inconsistent**: Devices where a password change has caused a mismatch.


<span id="30255ba8"></span>
### 3. Device Details

The device list provides granular status for each endpoint:


|Field |Description |
|---|---|
|**Device Name** |The name and unique DID of the endpoint. |
|**OS** |The specific version of the operating system. |
|**Employee** |The user associated with the device. |
|**Password Source** |* **Local Password**: The device is not successfully bound (pending setup or inconsistent).<br><br>* **SealSuite Password**: Successfully bound to SealSuite credentials.<br><br>* **Domain Password**: Successfully bound to a third\-party IdP (e.g., AD). |
|**Status** |Current state of synchronization (**Pending**, **Synchronized**, or **Inconsistent**). |
|**Last Modification** |Timestamps for the most recent local and IdP password updates. |


<span id="aa6ffde3"></span>
## FAQ

**1. What if an employee forgets their identity source (IdP) password?** 


* **Windows AD**: If downstream synchronization is configured, users may be able to reset their AD password via the SealSuite login interface. (LDAP reset is currently not supported via this method).

* **Other Platforms**: Reset the password on the original identity platform. SealSuite will detect the change and prompt the user to re\-bind.


**2. If an employee has multiple macOS devices, do they need to bind each one?** 

Yes. Password binding is device\-specific. The user must complete the binding process on each device after their initial SealSuite login.

**3. If an employee changes their IdP password** **on Device A, will it automatically sync to Device B?** 

No. Device B will initially require either the old IdP password or the local password to log in. Once the user logs into SealSuite on Device B, they will be prompted to bind the new password.

**4. How do I troubleshoot a failed password synchronization?** 

Check the **System Login** details for that specific platform and compare the "Last Modification" timestamps for the local and IdP passwords to identify where the mismatch occurred.
