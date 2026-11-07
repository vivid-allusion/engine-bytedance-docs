---
title: "What do I do if the \"As a security precaution, the user account has been locked because there were too many logon attempts or password change attempts.\" error message is displayed?"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/resolve-account-locked"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

When I am using an ECS instance running the Windows operating system, the "As a security precaution, the user account has been locked because there were too many login attempts or password change attempts. Wait a while before trying again, or contact your system administrator or technical support" error message is displayed.

<span id=".6Zeu6aKY5Y6f5Zug"></span>
## Causes

The security mechanism of the system is triggered when an incorrect password is entered too many times during a Remote Desktop login to the instance.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solutions

In this example provided in this topic, the Windows Server 2022 Datacenter Edition 64 bit operating system is used.


1. Use VNC to log in to the instance. For more information, see [Using the console to log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

   > If you are unable to use VNC to log in to the instance, [reset the login password](https://docs.byteplus.com/en/docs/ecs/Resetting-passwords) and then try again.   
   

2. Right\-click the "Start" icon, and then click the "Run" button to open the "Run" dialog box.

3. Enter the following command in the dialog box, and click the "OK" button.

   ```Plain Text
   gpedit.msc
   ```
   

4. In the "Local Group Policy Editor" window, select "Computer Configuration \> Windows Settings \> Security Settings \> Account Policies \> Account Lockout Policy".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6c51971f90bb704a882197fa8dbadd6e.png) </span>

5. Double\-click "Account lockout threshold" to open the account lockout threshold window.

6. Modify the number of consecutive incorrect login password attempts required to lock the account based on your needs, and then click the "OK" button to complete the modification.

   > If `0` is specified, there is no limit on the number of consecutive incorrect password attempts.   
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_47e4b2d8768304baa9ebde89780b3f0a.png) </span>

7. Use Remote Desktop to connect to the instance again and check whether you can log in to the instance as expected.
