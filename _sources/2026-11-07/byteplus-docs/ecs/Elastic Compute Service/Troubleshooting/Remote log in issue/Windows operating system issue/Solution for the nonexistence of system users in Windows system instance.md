---
title: "Solution for the nonexistence of system users in Windows system instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Solution_for_system_user_not_existing_in_Windows_system_instances"
---

This topic describes the issue where login to a Windows instance via the ECS Terminal fails because the Administrator account does not exist.

<span id=".6Zeu6aKY5Y6f5Zug"></span>
## **Causes**

The default Administrator username of the Windows instance is modified or disabled. This prevents login using the password of the Administrator account. Even after the password is reset by using the reset\-authentication plug\-in, login attempts by using the Administrator account still fail.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5b2T5pyJ5YW25a6D566h55CG5ZGY6LSm5oi35Y-v5Lul55m75b2VV2luZG93cw=="></span>
### When other administrator accounts can log in to Windows


1. Right\-click the lower\-left corner of the desktop and select "Computer Management".

2. Select "Local Users and Groups \> Users", and then troubleshoot and resolve related issues based on your needs.

   * Check whether the current account is disabled.

      1. Double\-click the name of the current account to check if it is disabled. If it is disabled, clear "Account is disabled".

      2. Click the "OK" button to complete the operation.

   * Check whether the account belongs to the Administrators group.

      1. Double\-click the name of the current Administrator account.

      2. Click the "Member Of" tab and check if it is in the Administrators group.

   * Check whether the current account name is Administrator. If not, right\-click the current account and rename it to Administrator.


<span id=".5b2T5peg5YW25a6D566h55CG5ZGY6LSm5oi35Y-v5Lul55m75b2VV2luZG93cw=="></span>
### When no other administrator accounts can log in to Windows

If there are no accounts that can log in to Windows, you will not be able to re\-enable the Administrator account or modify the name of the Administrator account.
