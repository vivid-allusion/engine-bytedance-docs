---
title: "Creating accounts to log in to ECS instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Self-building-users-log-in-to-the-ECS"
---

Linux instances use the root administrator account for login by default, and Windows instances use the Administrator account. Both have the highest administrative privileges of the operating system. To enhance instance security and manage user permissions hierarchically, you can create accounts in the instance by following this guide.

<span id=".TGludXjoh6rlu7rnlKjmiLc="></span>
## Create account in Linux instance

In the example provided in this topic, CentOS Stream 8 is used.


<Tabs>
<Tab zoneid="HmbsnmcRDW" title="Login with password">
<TabTitle>Login with password</TabTitle>

1. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance#.5pON5L2c5q2l6aqk) as the root administrator account.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can create new accounts only as the root account or an account with sudo permissions.   </div>
   

2. Execute the following command to create the new account.

   ```Bash
   useradd <new account name>
   ```
   

3. Execute the following command to set the new account password, and enter the password twice as prompted to confirm the password.

   ```Bash
   passwd <new account name>
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can also execute this command to change the password by resetting the password.   </div>
   

4. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance#.5pON5L2c5q2l6aqk) again as the new account via password.

5. Click "Confirm". If the following information is returned, you have logged in to the instance as the new account.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c724c442727327e862c42f75ef18b007.png) </span>


</Tab>
<Tab zoneid="aM1ZliTSrv" title="Login with key">
<TabTitle>Login with key</TabTitle>

1. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance#.5pON5L2c5q2l6aqk) as the root administrator account.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can create new accounts only as the root account or an account with sudo permissions.   </div>
   

2. Execute the following commands for creating a new account, switching to the directory of the new account, and viewing the directory path, respectively.

   ```Bash
   useradd <new account name>
   su - <new account name>
   pwd
   ```
   

3. Execute the following commands to create the .ssh directory for storing the key pair and grant the appropriate permissions to it.

   ```Bash
   mkdir .ssh
   chmod 700 .ssh
   ```
   

4. Execute the following command to log out of the new account.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Switch to the root user by default.   </div>
   

   ```Bash
   exit
   ```
   

5. Add the public key information[ into the instance](https://docs.byteplus.com/en/docs/ecs/Adding-or-replacing-key-pairs-for-instances).

6. Execute the commands to copy the "authorized_keys" file to the ".ssh" directory of the new account, and switch to the ".ssh" directory, respectively.

   ```Bash
   cp /root/.ssh/authorized_keys /home/<new account name>/.ssh/
   cd /home/<new account name>/.ssh
   ```
   

7. Execute the following command to view which user and group the "authorized_keys" file is associated with.

   ```Bash
   ls -al
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the associated group does not belong to the new account, execute the <code>chown <new user name>:<new user name> authorized_keys</code> command to modify accordingly.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9d83e59180636afd50aa84143c8beddc.png) </span>

8. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance#.5pON5L2c5q2l6aqk) again as the new account via key.

9. Click "Confirm". If the following information is returned, you have logged in to the instance as the new account.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_84d45e942ab79b81a9b0ce72af4abaf3.png) </span>


</Tab>
</Tabs>


<span id=".V2luZG93c-iHquW7uueUqOaItw=="></span>
## Create account in Windows instance

In the example provided in this topic, the Chinese edition of Windows Server 2022 is used.


1. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance#.5pON5L2c5q2l6aqk) with the Administrator account.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can create new accounts only with the Administrator account or an account granted administrator permissions.   </div>
   

2. Select "Start \> Settings \> Accounts".

3. Select "Other people \> Add someone else to this PC".

4. Select "Users \> More Actions \> New user...".

5. Enter the username and password of the new account.

6. Click the "Create" button to close the current window. Then, you can view the newly created account.

7. Click "Groups", find the three groups in the picture below, and then perform as follows in sequence.

   1. Select the item, right\-click, and then choose "Add to Group...".

   2. Click "Add...", enter the name of the newly created account, and click "Check Names". Then, the information of the new account appears.

   3. Click "OK" twice. Then, the new account is created.

8. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance#.5pON5L2c5q2l6aqk) again as the new account via password.

9. Click "Confirm" to log in to the instance as the new account.
