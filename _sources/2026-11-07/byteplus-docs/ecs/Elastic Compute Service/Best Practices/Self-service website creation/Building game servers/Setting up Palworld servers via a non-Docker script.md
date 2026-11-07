---
title: "Setting up Palworld servers via a non-Docker script"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Building_the_Palworld_server_using_a_script"
---

This topic mainly describes how to quickly set up a Palworld server by using a script on a Linux\-based instance.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Currently, you can set up a Palworld server using a non\-Docker script only on Linux\-based instances. We recommend using the Ubuntu 22.04 operating system for your instance.</div>


* <div data-tips="true" data-tips-type="warning">This script downloads and installs a Palworld server via the public network. As a result, Palworld server installation may fail. If an installation failure occurs, rerun the script to complete the installation.</div>



<span id=".5LuA5LmI5piv5bm75YW95biV6bKB"></span>
## What is Palworld?

Palworld is an open\-world game developed by Pocketpair. It combines survival and construction, exploration and combat, creature catching, training, and business manufacturing. This game supports multiplayer online play. Players need to collect mysterious "Pals" in a vast world, use "Pals" for combat, construction, farming, and other tasks, and build their dream bases.

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenario

Palworld is an open\-world game that allows you to set up a dedicated server using an ECS instance. You and your friends can log in for better playing experience. The dedicated server can offer better privacy and help avoid issues like game crashes caused by overcrowding on official servers.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have [created an ECS instance](https://docs.byteplus.com/en/docs/ecs/Overview-of-methods-for-buying-ECS-instances).

* The target instance must be associated with an EIP. For information about how to associate an EIP with an ECS instance, see [Associating EIPs](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YWN572u5a6J5YWo57uE"></span>
### Step 1: Configure a security group

Since the Palworld server uses `UDP` port `8211` for data transmission, you need to allow inbound UDP traffic on port 8211 in the security group of the target instance.


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the region and project where the target instance resides.

4. On the Instances page, find the target instance, and click the instance name to go to the instance details page.

5. Select the "Security Group" tab, and click the "Edit rule" button.

6. On the security group details page, select "Access rules \> Inbound rules" tab. Then, on the "Inbound rules" tab, complete the following configurations.

   1. Click the "Add rule" button.

   2. On the "Add Inbound rule" page, perform the following operations in sequence: specify "Protocol type" as `UDP`, copy `8211` into the "Port range" field, and copy `0.0.0.0/0` into the "Source" field. Then, click the "Confirm" button to complete the configuration.


<span id=".5q2l6aqk5LqM77ya5pCt5bu6UGFsd29ybGTmnI3liqHlmag="></span>
### Step 2: Set up a Palworld server


1. Log in to the target instance. For more information, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command on the instance to set up a Palworld server via a script.

   ```Plain Text
   wget -O script.sh  https://palworld.tos-cn-beijing.volces.com/install_palworld.sh && chmod +x script.sh && ./script.sh
   ```
   

   If the following output is displayed, the Palworld server is set up and started. If the setup fails, rerun the script.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b48730e795456d8f943d02e9b5bd6954.png) </span>

3. At this point, the Palworld server has been set up.


<span id=".5q2l6aqk5LiJ77ya5byA5aeL5ri45oiP"></span>
### Step 3: Start the game


1. Start Palworld in Steam.

2. On the game home page, click the "Join multiplayer game (dedicated server)" button.

3. On the start page, select "Community server", and at the bottom of the page, input `the ECS instance EIP:8211`. Click the "Contact" button to enter the dedicated server and start the game.


<span id=".5pu05paw5ri45oiP"></span>
## Update the game


1. Execute the following commands on the ECS instance to update the game.

   ```Plain Text
   sudo systemctl stop pal-world-server.service
   sudo -u steam $(which steamcmd)  +login anonymous +app_update 2394010 validate +quit
   ```
   

   If the following output is displayed, the game server is updated.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b51173df98618397be656568bb463f12.png) </span>

2. Execute the following commands on the instance to start the game server and view its running status.

   ```Plain Text
   sudo systemctl start pal-world-server.service
   sudo systemctl status pal-world-server.service
   ```
   

   If the following output is displayed, the game server is started.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1323700af1b7525739356fd75db13cb8.png) </span>
