---
title: "Solution for missing system accounts in Linux instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Solution_for_Non-existent_System_User_in_Linux_Instance"
---

This topic describes how to resolve login failures for a Linux instance caused by the loss of critical system user information. In a Linux system, if critical system user information (basic information and passwords) is lost, users may not be able to log in as expected. In such cases, it is necessary to restore the information in the `/etc/passwd` and `/etc/shadow` configuration files.


> * The `/etc/passwd` file stores the basic information of all users in the system.

> * The `/etc/shadow` file stores the password information of system users.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before you modify the configuration or data of an instance, we recommend that you [create a snapshot](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot) to improve fault tolerance and ensure data security.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Enter the Linux operating system in single\-user mode. For more information, see [Entering single-user mode](https://docs.byteplus.com/en/docs/ecs/Booting-in-single-user-mode).

2. Execute the following commands in sequence to back up the old `etc/passwd` and `/etc/shadow` files.

   ```Plain Text
   cp /etc/passwd /etc/passwd.bak
   cp /etc/shadow /etc/shadow.bak
   ```
   

3. Restore the /etc/passwd and /etc/shadow files.

   * **Restore from backup**:

      If you back up your instance on a regular basis (`/etc/passwd-` and `/etc/shadow-` are backed up), you can execute the following command to restore the two files from the backups.

      ```Plain Text
      cp /etc/passwd- /etc/passwd
      cp /etc/shadow- /etc/shadow
      ```
      

   * **Copy from other systems with the same configuration**:

      If you have another instance with the same configuration and know the lost user information, you can restore the lost user information by copying the relevant content from the `/etc/passwd` and `/etc/shadow` files of that instance.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">This method may introduce other issues. For example, the UID and GID allocations may differ between the two systems. We recommend that you do not use this method.      </div>
      

4. After the restoration is complete, restart the instance for the configuration to take effect.
