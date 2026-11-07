---
title: "Setting Windows OS languages"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Configuring-a-display-language-for-an-ECS-instance"
---

Currently, the BytePlus platform only provides Chinese and English versions of Windows Server public images. If you need other system languages, such as French or Japanese, you can change the system language by following the guidance in this topic.

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenarios


* **Local technical support**

   For cross\-border businesses, switching the server language to the local language helps local team members quickly interpret error messages and perform system configuration tasks, thereby reducing O&M costs and improving troubleshooting efficiency.

* **Multilingual development and testing**

   Switching the server language helps developers and testers set up different language environments to perform functional and compatibility tests on software of different language versions. This ensures that the software runs correctly in the target language environment and improves software quality.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have [purchased an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) and [associated an EIP with it](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).

* The ECS instance status is **Running**.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="CKnxvJaFOh" title="Windows Server 2019 and later versions">
<TabTitle>Windows Server 2019 and later versions</TabTitle>

1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. On the server desktop, click "Start \> Settings" in the lower\-left corner, and then select "Time & Language".

3. In the left\-side navigation pane, select "Language".

4. Click the "Add a language" button.

5. After you select the target language, click the "Next" button.

6. On the Install language features page, configure features based on your needs, and then click the "Install" button. In the example provided in this topic, default settings are retained.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">By default, after you install a new language pack, the corresponding language is automatically set as the default system language. If you do not want to change the system language, uncheck "Install language pack and set as my Windows display language". Then, in the list of supported languages, click "Options" of the corresponding language for download and installation.   </div>
   

7. From the "Windows display language" dropdown menu, select a language based on your needs.

8.  **(Optional)**  Configure the language of the welcome screen and new user accounts.

   1. Select "Related settings \> Administrative language settings".

   2. Click the "Copy settings..." button.

   3. Check the "Welcome screen and system accounts" and "New user accounts" options based on your needs, and then click the "OK" button.

9. [Restart the instance](https://docs.byteplus.com/en/docs/ecs/Restarting-instances) to check whether the language has been changed.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7924df981118bd257adf0c196954a0f7.png) </span>


</Tab>
<Tab zoneid="oaBlp8oVoG" title="Windows Server 2012 & 2016">
<TabTitle>Windows Server 2012 & 2016</TabTitle>

1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. On the desktop of the Windows instance, click "Start \> Control Panel".

3. Under "Clock, Language, and Region", click the "Add a language" button.

4. Click the "Add a language" button.

5. Add the target language.



<Tabs>
<Tab zoneid="mryfsIlcv7" title="Languages not differentiated by regions">
<TabTitle>Languages not differentiated by regions</TabTitle>

   1. Click the target language.

   2. Click the "Add" button.


</Tab>
<Tab zoneid="HN11rJug5F" title="Languages differentiated by regions">
<TabTitle>Languages differentiated by regions</TabTitle>

   1. Click the target language.

   2. Click the "Open" button.

   3. Select the target language for the corresponding region, and then click the "Add" button.


</Tab>
</Tabs>



6. Select the target language, and then click the "Move up" button to move it to the top.

7. Click the "Options" button to the right of the target language.

8. After the availability check passes, click the "Download and install language pack" button and wait for the language to be downloaded and installed.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Do not interrupt the language installation to avoid system language exceptions.   </div>
   

9.  **(Optional) ** Configure the language of the welcome screen and new user accounts.

   1. Select "See also \> Location".

   2. Select the "Administrative" tab, and then click the "Copy settings..." button.

   3. Check the "Welcome screen and system accounts" and "New user accounts" options based on your needs, and then click the "OK" button.

10. [Restart the instance](https://docs.byteplus.com/en/docs/ecs/Restarting-instances) to check whether the language has been changed.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_adde215bfd77965c0cf994cfcef03f75.png) </span>


</Tab>
</Tabs>
