---
title: "Setting up GitLab"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Building-GitLab"
---

GitLab is an open\-source repository management system. It uses Git as its code management tool and provides a web service built on this foundation. This topic describes how to build and use a GitLab application on a Linux Elastic Compute Service (ECS) instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A Linux instance is purchased. For more information, see [Purchasing ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   > If the instance type is lower than 4 vCPU and 8 GiB memory, the installation may fail or take too long due to low configuration. We recommend upgrading the instance type before installing GitLab. [Learn more.](https://docs.byteplus.com/en/docs/ecs/Modifying-instance-types)   
   

* An EIP is associated with the Linux instance, enabling the instance to connect to the Internet. For information about how to associate an EIP with an ECS instance, see [Associating EIPs](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).

* In the security group associated with the instance, inbound TCP traffic on port 80 is allowed.


<span id=".56ys5LiA5q2l77ya5a6J6KOFR2l0bGFi"></span>
## Step 1: Install GitLab

<span id="4RJt7agB"></span>
### Community Edition GitLab


<Tabs>
<Tab zoneid="c3n5Bag1Vr" title="CentOS 7.x">
<TabTitle>CentOS 7.x</TabTitle>

1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to install the required dependencies.

   ```Plain Text
   sudo yum install -y curl policycoreutils-python openssh-server
   ```
   

3. Execute the following command to start the SSH service and configure auto\-start on boot.

   ```Plain Text
   sudo systemctl enable sshd
   sudo systemctl start sshd
   ```
   

4. Execute the following command to install Postfix, which is used to send emails.

   ```Plain Text
   sudo yum install -y postfix
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When installation options appear, make adjustments as needed and press the Enter key to confirm. This document maintains the default configuration.   </div>
   

5. Execute the following command to start Postfix and configure auto\-start on boot.

   ```Plain Text
   sudo systemctl enable postfix
   sudo systemctl start postfix
   ```
   

6. Execute the following command to add the GitLab repository.

   ```Plain Text
   curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
   ```
   

   If the following output appears, it indicates the GitLab repository has been successfully added.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f086c37438d7d89a374dda837aeddce3.png) </span>

6. Execute the following command to install GitLab.

   ```Plain Text
   sudo EXTERNAL_URL="<ECS instance Elastic IP (EIP) address>" yum install -y gitlab-ce
   ```
   

   If the following output is displayed, the installation is successful.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_edd05e8ed1423523c380cfb54d624994.png) </span>

8. Execute the following command to view and record the default login password for GitLab.

   ```Plain Text
   cat /etc/gitlab/initial_root_password
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This file will be automatically deleted in 24 hours.   </div>
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7650f61976094356574e75a7fc9a8d52.png) </span>


</Tab>
<Tab zoneid="X43AcR3dOJ" title="Ubutun">
<TabTitle>Ubutun</TabTitle>

1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to install the required dependencies.

   ```Plain Text
   sudo apt-get update
   sudo apt-get install -y curl openssh-server ca-certificates tzdata perl
   ```
   

3. Execute the following command to install Postfix for sending email.

   ```Plain Text
   sudo apt-get install -y postfix
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When installation options appear, make adjustments as needed and press the Enter key to confirm. This document maintains the default configuration.   </div>
   

4. Execute the following command to start Postfix and configure auto\-start on boot.

   ```Plain Text
   sudo systemctl enable postfix
   sudo systemctl start postfix
   ```
   

5. Execute the following command to add the GitLab repository.

   ```Plain Text
   sudo curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash
   ```
   

   If the following output appears, it indicates the GitLab repository has been successfully added.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f1e2dfa0f00dda177fb8ec94b6476f6d.png) </span>

6. Execute the following command to install GitLab.

   ```Plain Text
   sudo EXTERNAL_URL="<ECS instance Elastic IP (EIP)>" apt-get install -y gitlab-ce
   ```
   

   If the following output is displayed, the installation is successful.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e2f4cd3f50e88c538c5ff0f98df0f302.png) </span>

7. Execute the following command to view and record the default login password for GitLab.

   ```Plain Text
   cat /etc/gitlab/initial_root_password
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This file will be automatically deleted in 24 hours.   </div>
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7650f61976094356574e75a7fc9a8d52.png) </span>


</Tab>
</Tabs>


<span id="y4tkRrbw"></span>
## Step 2: Log in to the GitLab management page

Using the community edition of GitLab as an example , this section introduces how to log in to the GitLab management page and perform necessary configuration.


1. Enter `http://<ECS instance Elastic IP (EIP) address>/` in the local browser and log in to GitLab using the root account and default Password.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aa86b45c168d950a58765084eb2a3626.png) </span>

2. Modify the Password for the root Account.

   1. Click the "Admin" button at the bottom of the left navigation pane.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9c6fb63eb8facde4584b71053f5f466c.png) </span>

   2. In the left navigation pane, select "Overview \> Users".

   3. Select the "User" tab.

   4. Click the "Edit" button to the right of the Administer user.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ebeaea7dd7cf656a485aae44dad10eb5.png) </span>

   5. Enter the new root Account login Password in the "Password" module.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6d4a0b1ecc3a95f17e420804f0dd35fe.png) </span>

3. If there is a new user request, you can approve the request by following the steps below.

   1. Click the "Admin" button at the bottom of the left navigation pane.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9c6fb63eb8facde4584b71053f5f466c.png) </span>

   2. In the left navigation pane, select "Overview \> Users".

   3. Select the "Users" tab, click the button to the right of the requesting user, and approve the request.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_babf3975ef3068b17262e78a75f0d6c2.png) </span>

5. For more management operation instructions, view [admin_area](https://docs.gitlab.com/ee/administration/admin_area.html).


<span id="L1rD1ziN"></span>
## Step 3: Register a new user and configure password\-free login


1. Input `http://<ECS instance Elastic IP (EIP)>/` in the local browser.

2. Click the "Register now" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8aca3cf96ed02251bbd231630d725251.png) </span>

3. After filling in the new user information, click the "Continue" button to Submit the application.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8aa7981b7a86d60f0a89ffde20f3d0a9.png) </span>

4. Contact the GitLab administrator to approve your new user application.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f2f41575bb872bc22fb5cbe593ca30a8.png) </span>

5. Once approved, you can log in to GitLab using the new user Account.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5136fefe963a017ef5a6e814dfd3d541.png) </span>

6.  **(Optional)**  Configure password\-free authentication.

   If you need to frequently interact with GitLab for actions such as pushing and pulling code in your local development environment, using SSH Key for password\-free login can improve efficiency and enhance security.

   1. Execute the following command in the PC that needs password\-free access to GitLab to get the SSH Key.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">This configuration only takes effect on the current PC, and reconfiguration is required after switching PCs.      </div>
      

      ```Plain Text
      ssh-keygen -t rsa
      ```
      

   2. Follow the instructions to configure the path where the Key is saved and the passphrase.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">This topic uses the default configuration. Press Enter at each step.       </div>
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_376bcb748cd9905356b8bb2c016e8579.png) </span>

   3. Execute the following command to view and record the SSH Key public key.

      ```Plain Text
      cat .ssh/id_rsa.pub
      ```
      

      Sample output:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a9d2aea99a2981c0bea15d137763ca9d.png) </span>

   4. Log in to GitLab using the target Account.

   5. Click on the Account avatar and select "Edit profile".

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d725ddc7015ad2fbd21b234b7f02cd03.png) </span>

   6. In the left directory tree, select "SSH Keys" and click the "Add new key" button.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dd9dfa96547c3c8caf9faed171d6c01c.png) </span>

   7. Paste the public key content obtained earlier into the "Key" module and click the "Add key" button to complete the action.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_77e39ec642a6cb1dfa562fb3924a7d2e.png) </span>


<span id="0j4yXGPB"></span>
## Step 4: Use GitLab

This section uses the same local PC as an example to introduce a common GitLab usage process. For more operation instructions, refer to [Get started with GitLab](https://docs.gitlab.com/user/get_started/).

<span id="6OZfJfef"></span>
### Create a remote repository


1. In the GitLab home page, click the "Create a project" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1eaa0d6a1132472499382240d67357aa.png) </span>

2. Click the "Create blank project" button to create a project.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4e855126bf65c05ac9686bc827a0810b.png) </span>

3. After the project is configured, click the "Create project" button to complete the creation process. For more remote repository management operations, refer to [Organize work with projects](https://docs.gitlab.com/user/project/organize_work_with_projects/).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_16abc7bcb70a273aca386cf12cd93810.png) </span>


<span id="sec9RSUR"></span>
### Clone a remote repository


1. Log in to the local PC.

2. Execute the following commands to install Git.

   
   <Tabs>
   <Tab zoneid="OogcM2zMuN" title="CentOS">
   <TabTitle>CentOS</TabTitle>
   
   &nbsp;
   
   ```Plain Text
   sudo yum update
   sudo yum install -y git
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="PfaDALQkxQ" title="Ubutun">
   <TabTitle>Ubutun</TabTitle>
   
   &nbsp;
   
   ```Plain Text
   sudo apt update
   sudo apt install -y git
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
   

3. Execute the following command to configure the user name for the Git repository.

   ```Plain Text
   git config --global user.name "testname"
   ```
   

3. Execute the following command to configure the user email for the Git repository.

   ```Plain Text
   git config --global user.email "xxx@example.com"
   ```
   

4. Go to the home page of the target GitLab project, and copy the project address.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_df939bb50936915545eb8044f91f5dd9.png) </span>

5. Execute the following command to clone the project.

   ```Plain Text
   git clone <remote repository address> <local directory>
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you have not configured password\-free authentication, follow the prompts to enter your GitLab username and password.   </div>
   

   If the following is echoed, the cloning was successful.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_283d72f0d7bd564099ac403e17b70d7c.png) </span>

6. Execute the following command to enter the project directory.

   ```Plain Text
   cd <project directory>
   ```
   

7. Execute the following command to view the current branch of the project.

   ```Plain Text
   git branch
   ```
   

   If the following is echoed, you are on the main branch `main`.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_720c0b7110f4a62cbbaad60b8b9ab4d3.png) </span>


<span id="sYOrCphj"></span>
### Modify project content.


1. Execute the following command to enter the project directory.

   ```Plain Text
   cd <project directory>
   ```
   

2. Execute the following command to create and switch to branch `test`, then modify the project content.

   ```Plain Text
    git checkout -b test
   ```
   

3. Execute the following command to create a test file and write content into it.

   ```Plain Text
   echo "test" > test.sh
   ```
   


<span id="HoVPZXM1"></span>
### Push the local branch to the remote repository.


1. Execute the following command to enter the project directory.

   ```Plain Text
   cd <project directory>
   ```
   

2. Execute the following command to switch to branch `test`.

   ```Plain Text
    git checkout test
   ```
   

3. Execute the following command to add the changes to the staging area.

   ```Plain Text
   git add test.sh
   ```
   

4. Execute the following command to submit the changes in the staging area to the local repository.

   ```Plain Text
   git commit -m "<remark>"
   ```
   

   The following output indicates the submission was successful.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_547b5cfc4e8acd9859b65d4abb654724.png) </span>

6. Execute the following command to push the local branch to the remote repository.

   ```Plain Text
   git push -u origin test
   ```
   

   The following output indicates the push was successful.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0bcdf0aa8c43ac0ffb661844f762f1c0.png) </span>

7. After a successful push, other users with permission for the project can also view the branch content on GitLab.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2a59d86850b36fed667a0066bfefe0ed.png) </span>


<span id="Qom4HdOo"></span>
### Merge changes and push to the remote repository.


1. Execute the following command to enter the project directory.

   ```Plain Text
   cd <project directory>
   ```
   

2. Execute the following commands to switch to the main branch `main`.

   ```Plain Text
    git checkout main
   ```
   

3. Execute the following command to pull the main branch of the remote repository to ensure that the content of the local main branch is consistent with it.

   ```Plain Text
   git pull origin main
   ```
   

4. Execute the following commands to merge the changes of the newly created branch `test` into the main branch.

   ```Plain Text
   git merge test
   ```
   

   The following output indicates that the merge was successful  and there are no conflicts.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6502e45bf8ae6c55ab4c6d298355fbe3.png) </span>

5. Execute the following commands to push the local branch to the remote repository.

   ```Plain Text
   git push
   ```
   

   The following output indicates a successful push.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_94361ef37696f4d0b1992926eb939a10.png) </span>

6. After a successful push, the changes in the local main branch are synchronized to the main branch of the remote repository.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ba5f540239c3e7bc7b528da97b618abd.png) </span>
