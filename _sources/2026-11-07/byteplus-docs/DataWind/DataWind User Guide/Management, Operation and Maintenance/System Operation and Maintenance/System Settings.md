---
title: "System Settings"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/System_Settings"
---

This article provides a detailed introduction to the core features of the "System settings" module in system management, including security settings, copy and download permissions, network zone access control, third\-party service authorization, and configuration methods and application scenarios for message push channels.

<span id="18001d43"></span>
# Feature overview

System management includes the system settings module. This module allows project administrators to configure security settings (watermark settings, system control), copy and download permissions, network zone access control, third\-party service authorization, and message push channel settings.

By configuring watermark settings, a personal information watermark is added to images when users take screenshots.

Through system control, system administrators can configure accounts to automatically join the product upon login or manage them manually, and grant permissions to members outside the project.

By configuring copy and download permissions, users are prevented from bulk copying data or directly copying and downloading data, restricting them from transferring data to other platforms.

By configuring network zone access, users can only use the system within intranet or similar network environments.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c183611239b4460b3e21c78ff4d1a88~tplv-goo7wpa0wc-image.image) </span>

<span id="492ea6a2"></span>
# Feature introduction

<span id="6fdccf15"></span>
## Security settings

<span id="a61aa2ad"></span>
### Watermark settings

Supports configuration of watermarks for PC and mobile devices. Administrators can configure visible watermarks for both desktop and mobile devices, and adjust watermark content (username, last four digits of phone number, IP address, current time), watermark style (single line, line break), watermark color, and watermark font size.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6d598fa84a5489eae5199710546560e~tplv-goo7wpa0wc-image.image) </span>

<span id="d5b39621"></span>
### System control

In system control, administrators can set the license control method and restrict resource administrators to authorize only users within this project.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b46fbbdd9f145b3973c50605d893aab~tplv-goo7wpa0wc-image.image) </span>


* License control methods:

   * "System users automatically join upon logging into this product": After system users log in to this product, they are automatically added to the license list without the need for administrators to configure the list again. This is suitable for scenarios where account resources are not limited and resources can be shared, offering greater convenience.

   * System administrator configures license allowlist: The resource administrator must manually configure the license allowlist. System users who are not on the allowlist will not be able to access resources after logging in. License usage can be controlled to avoid the “first come, first served” issue; manage DataWind users to meet resource isolation requirements.

* Resource administrators can only authorize users under this project: If enabled, the resource administrator can only authorize users under this project; if disabled, all users can be authorized.


<span id="b634d7ba"></span>
## Copy and download

Supports configuring system\-wide copy and download permissions. When the “Allow data download/copy” button is disabled, all projects in the system will not support data download or copy, which can effectively reduce the likelihood of data dissemination; administrators can also limit the maximum number of rows that can be downloaded at one time to restrict users from downloading data in bulk.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1835ba1efb8a447fb56ee6b17f158ea3~tplv-goo7wpa0wc-image.image) </span>

<span id="0dd6fc9e"></span>
## Network zone access control

<span id="bbd8be6b"></span>
### **Basic introduction**

In industries and enterprises with strict data security controls, there are usually multiple network environments, such as production network (intranet), office network, and internet. In different network environments, the openness of data and operations on production data are controlled to varying degrees. This feature supports usage in different scenarios:

**Scenario 1**: In the production environment, viewing raw data is supported, and processing data is also supported.

**Scenario 2**: In the office network environment, data viewing is supported, but data must undergo data masking, and data development actions (such as dataset creation) are not supported.

**Scenario 3**: In the internet environment (mobile devices), only some data assets are open, and access via mobile devices is supported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85e854c7e09a4edeb5312aedca675a05~tplv-goo7wpa0wc-image.image) </span>

All of the above scenarios can be implemented through **network zone access control + data masking capability**.

<span id="b04f7f58"></span>
### **Scenario examples**

<span id="60c3fe96"></span>
#### **Restrict network access**

For scenarios where the system is used only in the office network or certain networks, proceed as follows:


1. In System Management \- Security Settings \- Network Zone Access Control, enable “Multiple Network Zones” and add a new network zone.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a12f1aa3f45a453ba66c6d807e43cc23~tplv-goo7wpa0wc-image.image) </span>


2. Enter basic information such as name, domain, and ID, configure accessible endpoints, accessible modules, push method, and the scope of data masking application, then click Save.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52e6fbda943b4b4cb6627beec6b8d325~tplv-goo7wpa0wc-image.image) </span>

You can add multiple network zones to configure differentiated access control settings for different networks.

3. In addition to multiple network zones, you can also perform global configuration on the right side to set the default access network.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c574e70d678b4d34b80955f7c6ccf7af~tplv-goo7wpa0wc-image.image) </span>

**Short link encryption for links**

For scenarios where embedded links are encrypted into short links, the specific steps are as follows:


1. The system administrator needs to check "Encrypt embed" in System Management \> Security Settings \> Network Zone Access Control.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08a9becef752421e9ae1041cb823292f~tplv-goo7wpa0wc-image.image) </span>


2. The project administrator needs to check "Include encrypted embed" in the Embedded Project Resources section under Project Center \> Project Information.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/393299a6ad31406e849d1b16b74b1205~tplv-goo7wpa0wc-image.image) </span>


3. Users in the project can enable encrypted processing of embedded links when embedding charts or dashboards.


<span id="9e0de93a"></span>
# Third\-party service authorization

The third\-party service authorization feature is used to configure external services that can be integrated into the project, clarify the linkage permissions between the project and third\-party tools, and ensure that external service usage is compliant and controllable. It includes information such as project name, available third\-party services, default third\-party authorization, and default third\-party authorization services.
