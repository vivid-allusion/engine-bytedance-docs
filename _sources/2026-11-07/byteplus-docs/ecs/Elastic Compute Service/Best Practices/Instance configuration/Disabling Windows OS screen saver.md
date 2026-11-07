---
title: "Disabling Windows OS screen saver"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Disable_Windows_Screen_saver"
---

If the services running on your ECS instance require the screen to stay on, or if a locked screen may interrupt your normal workflow, refer to this topic to disable the screen saver on a Windows\-based ECS instance.

<span id="WuhXq2ug"></span>
## What is screen saver?

A screen saver is a program that displays images or animations when the computer is inactive. At first, it was designed to prevent the **burn\-in effect** on old\-fashioned CRT monitors, which refers to the permanent marks left by static images displayed on the screen for a long time. Modern liquid crystal displays (LCDs) and light\-emitting diode (LED) displays are largely unaffected by burn\-in.

<span id="Kh43Y3PD"></span>
## Usage note

To disable the screen saver, you can configure the "Personalize" settings or modify the Registry. Note the following:


|Method |Feature |Application scenarios |
|---|---|---|
|"Personalize" settings |Operate through a graphical user interface, which is more intuitive and secure. |Suitable for daily use by most users. |
|Registry |Directly edit system configurations. This method is suitable for scenarios that require more fine\-grained control, but it is complex and risky. |Applicable to scenarios that involve system\-level configurations or unified configurations in an enterprise. |


<span id="dysAgjnR"></span>
## Prerequisites


* You have [purchased an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances?LibVersion=markdown备份版本).

* The ECS instance status is **Running**.


<span id="9zBVOWLr"></span>
## Procedure

In the example provided in this topic, Windows Server 2022 Datacenter Edition 64 bit English image is used.


<Tabs>
<Tab zoneid="MkmodJyHSf" title="Via "Personalize" settings">
<TabTitle>Via "Personalize" settings</TabTitle>

1. [Log in to the target Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Right\-click the blank area of the server screen, and then click the "Personalize" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d32f47de6dc0d85164f3efa33c632db5.png) </span>

3. In the left directory tree, select "Lock screen", and in the right "Lock screen" module, click the "Screen saver settings" button at the bottom.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7ac3516c764be503bc4cd68d5f264f3f.png) </span>

4. Set "Screen saver" to "(None)", and uncheck the "On resume, display logon screen" option.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_10a91069501c8be9d412dd4505458718.png) </span>

5. Click the "Apply" button and the "OK" button in sequence. After this, the screen saver is disabled.


</Tab>
<Tab zoneid="EdkIOdWMbq" title="Via Registry">
<TabTitle>Via Registry</TabTitle>

1. [Log in to the target Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Click the "Windows" icon and then select "Windows System \> Run".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c2c44dff7e90b42224bea79fdf88b330.png) </span>

3. Fill in the following content in the dialog box and click the "OK" button to open the Task Scheduler dialog box.


```Plain Text
regedit
```



<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b7bbcadd118df6273b7268c386e1fd9a.png) </span>

4. In the left directory tree, select "HKEY_CURRENT_USER \> Control Panel \> Desktop".

5. Right\-click `ScreenSaveActive`, click the "Modify" button, and then specify `Value data` as `0`. Then, click the "OK" button to save the change.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_786152375ccf6b0e1ba1486ef3230ab7.gif) </span>

6. [Restart the instance](https://docs.byteplus.com/en/docs/ecs/Restarting-instances) to make the configuration take effect.


</Tab>
</Tabs>
