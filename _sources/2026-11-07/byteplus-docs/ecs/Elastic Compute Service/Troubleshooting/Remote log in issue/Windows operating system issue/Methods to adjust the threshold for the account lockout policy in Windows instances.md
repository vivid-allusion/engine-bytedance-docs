---
title: "Methods to adjust the threshold for the account lockout policy in Windows instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Method_for_adjusting_the_account_lockout_policy_threshold_for_Windows_instances"
---

This topic describes how to resolve the issue where the "As a security precaution, the user account has been locked because there were too many logon attempts or password change attempts" error message is displayed when you use Remote Desktop to connect to a Windows\-based ECS instance.

In the example provided in this topic, the Windows Server 2016 operating system is used. The operation steps for other operating systems are similar.

<span id=".6Zeu6aKY5Y6f5Zug"></span>
## Causes

A user account lockout policy is configured in the Local Group Policy of the Windows\-based ECS instance. If an incorrect password is entered too many times during login, the account will be locked, preventing Remote Desktop login.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance. For more information, see [Using the console to log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

   > Use VNC to log in to the Windows instance in the console.   
   

2. In the search box at the bottom\-right corner of the desktop, enter "Run" and select the "Run" application.

3. In the "Run" dialog box, enter the `gpedit.msc` command, and then click the "OK" button to open the Local Group Policy Editor.

4. On the "Local Group Policy Editor" page, select "Computer Configuration \> Windows Settings \> Security Settings \> Account Policies \> Account Lockout Policy".

5. On the "Account Lockout Policy" page, double\-click "Account lockout threshold" to open the "Account lockout threshold Properties" window.

6. In the "Account lockout threshold Properties" window, change the threshold ("Account will lock out after \* invalid logon attempts") from its current value to 0, and then click the "OK" button to complete the operation. The settings take effect immediately.
