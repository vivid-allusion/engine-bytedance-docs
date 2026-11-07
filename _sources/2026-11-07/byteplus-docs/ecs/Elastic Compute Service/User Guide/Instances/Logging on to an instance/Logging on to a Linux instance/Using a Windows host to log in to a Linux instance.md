---
title: "Using a Windows host to log in to a Linux instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Using-a-Windows-host-to-log-on-to-a-Linux-instance"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenarios

This topic describes how to log in to a Linux ECS instance from a Windows host.


|Operating system of the local host |Operating system of the ECS instance |Login tool on local host |Login authentication method |
|---|---|---|---|
|Windows |Linux |Command Prompt\-\-SSH command or PuTTY |Password and key |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Make sure that the ECS instance you log in to meets the conditions in the [Login restrictions](https://docs.byteplus.com/en/docs/ecs/Overview-1).

* Make sure that the ECS instance [is associated with an EIP](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP), and can communicate with the Internet.

* If you need data transfer, refer to [Transferring files from a local Windows system to a Linux instance (WinSCP)](https://docs.byteplus.com/en/docs/ecs/Using-WinSCP-to-upload-files-from-a-local-Windows-to-a-Linux-instance).


<span id=".5a-G56CB55m75b2V5q2l6aqk"></span>
## Password login procedure


<Tabs>
<Tab zoneid="pDobEUPj5h" title="Use SSH">
<TabTitle>Use SSH</TabTitle>

1. On the local host, click "Start" and open the "Command Prompt" terminal.

2. Enter the following SSH command.

   ```Plain Text
   ssh <root>@<The EIP address of the Linux ECS instance>
   ```
   

3. Input the password of the root user and press the `Enter` key to log in to the Linux ECS instance.


</Tab>
<Tab zoneid="FHbZBvvrTo" title="Use PuTTY">
<TabTitle>Use PuTTY</TabTitle>

1. Access [PuTTY](https://the.earth.li/~sgtatham/putty/0.76/w64/putty.exe) with the browser on your local host, and then download and install it.

2. Double\-click the putty64.exe file and configure the following parameters.

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_e573ab45a62b174ef8c6989f958d060a.png) </span>

   
   |Parameter |Description |
   |---|---|
   |Host Name |Enter the EIP address of the ECS instance. |
   |Port |Specify the port of the ECS instance. In this case, set the port to 22. |
   |Connection type |Select SSH. |
   |Saved Sessions |Name this session based on your needs, and then click "Save". This can help you record this connection for easy logins afterwards. |
   

3. Click "Open" to open the PuTTY terminal window. Follow the prompts to enter "root" and the password of the root user. Then, you can log in to the Linux ECS instance.

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_c8cb7ff3abf46fb2626427f9d812ba27.png) </span>


</Tab>
</Tabs>


<span id=".5L2_55SoU1NI5bel5YW3"></span>
### Password login procedure


<Tabs>
<Tab zoneid="tlWEukSQNl" title="Use SSH">
<TabTitle>Use SSH</TabTitle>

1. On the local host, click "Start" and open the "Command Prompt" terminal.

2. Run the following commands in sequence to make the private key file readable to the current logged\-in user.

   ```Plain Text
   icacls <The absolute path of the .pem private key file on the local host> /grant <The username of the local host>:F
   icacls <The absolute path of the .pem private key file on the local host> /inheritancelevel:r
   ```
   

3. Run the following command to log in to the instance.

   ```Plain Text
   ssh -i <The file path of .pem private key file on the local host> <Username of the Linux instance>@<EIP address of the Linux instance>
   ```
   

4. Press the `Enter` key to log in to the instance.


</Tab>
<Tab zoneid="ZUMxngnBw2" title="Use PuTTY">
<TabTitle>Use PuTTY</TabTitle>

1. Access [PuTTY](https://the.earth.li/~sgtatham/putty/0.76/w64/putty.exe) and [PuTTYgen](https://the.earth.li/~sgtatham/putty/0.76/w64/puttygen.exe) with the browser on your local host, and then download and install them.

2. Double\-click the puttygen.exe file.

   1. Select "Type of key to generate \> RSA". Then, click "Load".

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_683a55d3c3fee5c35c908345180f3cd2.png) </span>

   2. Select "All Files", and then select the target private key file. Then click "Open".

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0197bcad79d35af60afb764c88edcb8a.png) </span>

   3. In the confirmation dialog box that pops up, click "OK", and then select "Save private key" in the following figure.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_068ec11f461f43c143a3c5586427286a.png) </span>

   4. In the confirmation dialog box that pops up, click "Yes".

   5. Specify a name for the .ppk file, and click "Save".

3. Double\-click the putty64.exe file.

   1. In the left\-side navigation pane, select "Connection \> SSH \> Auth". In the right\-side pane, click "Browse".

      <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_8b84834ca4658e01eed06e8e1aa08bc6.png) </span>

   2. Select the .ppk private key file and then click "Open".

   3. In the left\-side navigation pane, click "Session" and configure the following parameters.

      <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_e573ab45a62b174ef8c6989f958d060a.png) </span>

      
      |Parameter |Description |
      |---|---|
      |Host Name |Input the EIP address of ECS instance. |
      |Port |Specify the port for the ECS instance. In this case, the port is set to 22. |
      |Connection type |Select SSH. |
      |Saved Sessions |Name this session based on your needs, and click "Save". This saves the connection so that you can log in more easily next time. |
      

4. Click "Open" to go to the run page of "PuTTY". Follow the prompts to enter "root". Then, the system automatically identifies the private key. After this, you can log in to the Linux ECS instance.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_300f92436ffde6191dd4e226f2f883d4.png) </span>


</Tab>
</Tabs>
