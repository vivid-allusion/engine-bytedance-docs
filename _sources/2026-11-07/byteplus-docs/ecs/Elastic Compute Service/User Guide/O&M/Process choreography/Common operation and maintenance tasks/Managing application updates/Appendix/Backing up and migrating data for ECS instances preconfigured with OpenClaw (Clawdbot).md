---
title: "Backing up and migrating data for ECS instances preconfigured with OpenClaw (Clawdbot)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Back_up_data"
---

For existing ECS instances preconfigured with OpenClaw (Clawdbot), you may need to reinstall the operating system to upgrade the version and fix system faults, and retain application memory data (such as conversation history and user preferences). In such cases, you can follow the instructions in this topic to back up data and migrate data after the operating system is reinstalled.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Make sure that your ECS instance is stopped before you perform any operations. Otherwise, data being written may be lost.</div>


<span id="HIqb2cN3"></span>
## Steps

The following instructions use an OpenClaw instance as an example. For a Clawdbot instance, simply replace `/root/.openclaw/workspace` with `/root/clawd`.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">OpenClaw instance: The workspace directory is <code>/root/.openclaw/workspace</code>.</div>


* <div data-tips="true" data-tips-type="default">Clawdbot instance: The workspace directory is <code>/root/clawd</code>.</div>



<span id="vzm8A55R"></span>
### **Step 1: View application memory**

Verify the integrity, validity, and completeness of the application memory data to be backed up by viewing the application memory.


* Execute the following command to view the full content of the workspace directory.

   ```Bash
   ls -l /root/.openclaw/workspace
   ```
   

   An output similar to the following is displayed:

   ```Bash
   total 40
   -rw-r--r-- 1 root root 7869 Feb  1 19:00 AGENTS.md
   -rw-r--r-- 1 root root 1470 Feb  1 19:00 BOOTSTRAP.md
   -rw-r--r-- 1 root root  168 Feb  1 19:00 HEARTBEAT.md
   -rw-r--r-- 1 root root  248 Feb  3 11:43 IDENTITY.md
   drwxr-xr-x 2 root root 4096 Feb  3 11:45 memory
   drwxr-xr-x 6 root root 4096 Jan 29 17:36 skills
   -rw-r--r-- 1 root root 1673 Feb  1 19:00 SOUL.md
   -rw-r--r-- 1 root root  860 Feb  1 19:00 TOOLS.md
   -rw-r--r-- 1 root root  481 Feb  1 19:00 USER.md
   ```
   

* Execute the following command to view IDENTITY.md (agent identity configuration).

   ```Bash
   cat /root/.openclaw/workspace/IDENTITY.md
   ```
   

   An output similar to the following is displayed:

   ```Bash
   # IDENTITY.md - Who Am I?
   
   - **Name:** jiaxx (Jarxx)
   - **Creature:** Operating System Intelligent Butler
   - **Vibe:** A capable and precise intelligent assistant with a sense of technology, efficiently solving various system and daily tasks 
   - **Emoji:** 🤖
   - **Avatar:** (can be supplemented later )
   ```
   

* View the memory directory

   ```Bash
   ls -l /root/.openclaw/workspace/memory/
   ```
   

   An output similar to the following is displayed:

   ```Bash
   total 4
   -rw-r--r-- 1 root root 277 Feb  3 11:45 2026-02-03.md
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">total 4: Indicates the total size of all files in this directory is 4 KB.   </div>
   

* View the memory file

   ```Bash
   cat /root/.openclaw/workspace/memory/2026-02-03.md 
   ```
   

   An output similar to the following is displayed:

   ```Bash
   # 2026-02-03 work record
   
   1. Initialize identity information: Set the name to Jia, the identity to Operating System Intelligent Butler, and save it to IDENTITY.md
   2. Query and return the current operating system information: Ubuntu 24.04 LTS, kernel version 6.8.0-55-generic
   3. Record today's work tasks to the memory file
   ```
   


<span id="8lJueLKF"></span>
### Step 2: Package the workspace and transfer it to the local computer


1. Execute the following command to package the core work data of the workspace into a compressed package named `workspace.tar.gz` for easy backup, transfer, and migration.

   
   <Tabs>
   <Tab zoneid="oLys6ZRqvx" title="OpenClaw">
   <TabTitle>OpenClaw</TabTitle>
   
   &nbsp;
   
   ```Bash
   cd ~
   tar -zcvf workspace.tar.gz -C /root/.openclaw/ workspace
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="etWIeNeRUz" title="Clawdbot">
   <TabTitle>Clawdbot</TabTitle>
   
   &nbsp;
   
   ```Bash
   cd ~
   tar -zcvf workspace.tar.gz /root/clawd
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
   

2. Execute the following command to securely transfer the packaged OpenClaw/Clawdbot backup archive `workspace.tar.gz` from the ECS instance to the current working directory of your local terminal. This achieves off\-site storage of the backup archive, moving it from the server side to your local computer.

   ```Bash
   # Run the following code locally.
   scp root@{EIP of your instance}:/root/workspace.tar.gz .
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>{EIP of your instance}</code> with the actual address of the target server used for storing ECS instance files.   </div>
   

<span id="Ujz35RI9"></span>
### Step 3: Create an application update task

Perform operating system reinstallation in Orchestration, reconfigure the model, and integrate Telegram. [Learn more](https://docs.byteplus.com/en/docs/ecs/Creating_application_update_tasks).

<span id="wSC43xEm"></span>
### Step 4: Migrate backup data to the instance with the reinstalled operating system


1. After the instance with the reinstalled operating system starts, execute the following command locally to copy the local backup archive `workspace.tar.gz` to the instance.

   ```Bash
   # Run the following code locally.
   ssh-keygen -R {EIP of your instance}
   scp ./workspace.tar.gz root@{EIP of your instance}:/root
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>{EIP of your instance}</code> with the actual address of the target server used for storing ECS instance files.   </div>
   

2. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) and perform the following operations:

   1. Execute the following command to decompress the local backup archive `workspace.tar.gz` to `/root`.

      ```Bash
      cd /root
      tar -xzvf workspace.tar.gz
      ```
      

   2. Overwrite the original workspace directory with the decompressed one and restart the Gateway service.

      1. Execute the following command to rename the original OpenClaw workspace directory to workspace.bak to avoid conflicts with the restored backup directory.

         ```Bash
         mv /root/.openclaw/workspace /root/.openclaw/workspace.bak
         ```
         

      2. Execute the following command to move the decompressed backup workspace directory from the `/root` directory to the official deployment path of OpenClaw `/root/.openclaw/`. This ensures that the application can read the restored data.

         ```Bash
         mv workspace /root/.openclaw/
         ```
         

      3. Execute the following command to restart the OpenClaw Gateway service. This allows the application to reload the workspace directory data restored to the official path and ensures all historical configurations, memory, and other information take effect.

         ```Bash
         openclaw gateway restart
         ```
         


<span id="lQ4fEYhk"></span>
### Step 5: Verify memory data

Check whether the backed up memory files are restored as expected with complete and valid content, and confirm that OpenClaw can read the memory data as expected. This section uses Lark application integration as an example:


1. In Lark, enable "Open Platform Assistant" message notifications, and click "Open App".

2. Enter the `/new` command and use the relevant features as prompted on the interface.
