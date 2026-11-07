---
title: "Manually setting up Palworld servers"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Manually_build_the_Palworld_server"
---

This topic mainly describes how to manually set up a Palworld server on Windows\-based and Linux\-based instances, respectively.

<span id=".5LuA5LmI5piv5bm75YW95biV6bKB"></span>
## What is Palworld?

Palworld is an open\-world game developed by Pocketpair. It combines survival and construction, exploration and combat, creature catching, training, and business manufacturing. This game supports multiplayer online play. Players need to collect mysterious "Pals" in a vast world, use "Pals" for combat, construction, farming, and other tasks, and build their dream bases.

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenario

Palworld is an open\-world game that allows you to set up a dedicated server using an ECS instance. You and your friends can log in for better playing experience. The dedicated server can offer better privacy and help avoid issues like game crashes caused by overcrowding on official servers.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have [created an ECS instance](https://docs.byteplus.com/en/docs/ecs/Overview-of-methods-for-buying-ECS-instances).

* We recommend that you use Ubuntu 22.04 or Windows Server 2022 Data Center Edition as the operating system for the target instance.

* The target instance must be associated with an EIP. For information about how to associate an EIP with an ECS instance, see [Associating EIPs](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YWN572u5a6J5YWo57uE"></span>
### Step 1: Configure a security group

Since the Palworld server uses `UDP` port `8211` for data transmission, you need to allow inbound traffic on UDP port 8211 in the security group.


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

<span id=".5ZyobGludXjmk43kvZzns7vnu5_kuK3mkK3lu7o="></span>
#### Set up the Palworld server in a Linux\-based instance


1. Log in to the target instance. For more information, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command in the instance to create a user named `steam`, which will be used to install and run SteamCMD.

   ```Plain Text
   sudo useradd -m -s /bin/bash steam 
   ```
   

3. Install SteamCMD.

   1. Execute the following command to install the command\-line version of Steam.

      ```Plain Text
      sudo add-apt-repository multiverse -y; sudo dpkg --add-architecture i386; sudo apt update -y;apt-get remove needrestart -y
      sudo apt install steamcmd -y
      ```
      

   2. Press `Tab`, select `<ok>`, and press Enter to complete reading the agreement.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_83d67fdff4a8f22de1a281c0b6e6ca41.png) </span>

   3. Press the `↓` key to select `I AGREE`, and then press Enter to agree to the agreement.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4d677530f6a55488616f051cd60d818d.png) </span>

4. Execute the following commands to create a directory and download the SDK.

   ```Plain Text
   sudo -u steam mkdir -p ~steam/.steam/sdk64/
   sudo -u steam $(which steamcmd)  +login anonymous +app_update 1007 +quit
   sudo cp ~steam/Steam/steamapps/common/Steamworks\ SDK\ Redist/linux64/steamclient.so ~steam/.steam/sdk64/
   ```
   

   If the following output is displayed, SDK is downloaded. If the download fails, execute the commands again.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_db6c92098443afbc59dd9e429125ae5a.png) </span>

5. Execute the following command to download the Palworld server.

   ```Plain Text
   sudo -u steam $(which steamcmd)  +login anonymous +app_update 2394010 validate +quit
   ```
   

   If the following output is displayed, the Palworld server is downloaded.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_26ddbe8b0aa33c323e3a1662c6db6ef0.png) </span>

6. Create the Palworld server process as a custom service.

   1. Execute the following command to create and open the Palworld service file.

      ```Plain Text
      vim /etc/systemd/system/pal-world-server.service
      ```
      

   2. Press `i` key to enter the edit mode, and then copy and paste the following content into the file.

      ```Plain Text
      [Unit]
      Description=Customize Palworld Service
          
      [Service]
      Type=simple
      User=steam
      Restart=on-failure
      RestartSec=30s
      ExecStart=/home/steam/Steam/steamapps/common/PalServer/PalServer.sh -useperfthreads -NoAsyncLoadingThread -UseMultithreadForDS
      
      [Install]
      WantedBy=multi-user.target
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bc2921ad6be28bf3e1b349cbb4c3503f.png) </span>

   3. Press `Esc`, enter `:wq`, and then press Enter to save and exit the file.

   4. Execute the following command to specify that the Palworld server automatically starts upon instance startup.

      ```Plain Text
      sudo systemctl enable pal-world-server.service
      ```
      

   5. Execute the following command to restart the Palworld server and apply the configuration.

      ```Plain Text
      sudo systemctl restart pal-world-server.service
      ```
      

   6. Execute the following command to view the running status of the Palworld server.

      ```Plain Text
      sudo systemctl status pal-world-server.service
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_50a0c7927064933ecdb524d5cc0b36fc.png) </span>

7. At this point, the Palworld server has been set up.

8. To manage the Palworld server, you can execute the following commands in your instance.

   ```Plain Text
   # Start the Palworld server
   sudo systemctl start pal-world-server.service
      
   # Restart the Palworld server
   sudo systemctl restart pal-world-server.service
      
   # Stop the Palworld server
   sudo systemctl stop pal-world-server.service
      
   # Check the Palworld server status
   sudo systemctl status pal-world-server.service
   ```
   


<span id=".5ZyoV2luZG93c-aTjeS9nOezu-e7n-S4reaQreW7ug=="></span>
#### Set up the Palworld server in a Windows\-based instance


1. Log in to the target instance. For more information, refer to [Logging in to Windows instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Windows-instance).

2. Log in to the instance, right\-click the "Start" button, and select "Windows PowerShell (Admin)" to open PowerShell.

3. In PowerShell, execute the following command to allow users to access your purchased instance through port `8211`.

   ```Plain Text
   New-NetFirewallRule -DisplayName "Allow Port 8211" -Protocol UDP -LocalPort 8211 -Action Allow 
   ```
   

4. In PowerShell, execute the following command to download and install the C++ Runtime Library.

   ```Plain Text
   Invoke-WebRequest -Uri 'https://aka.ms/vs/17/release/vc_redist.x64.exe' -OutFile 'C:\Users\Administrator\Downloads\vc_redist.x64.exe'
   Start-Process 'C:\Users\Administrator\Downloads\vc_redist.x64.exe'
   ```
   

   Follow the installation prompts to complete the installation.

5. In PowerShell, execute the following command to download and install the DirectX support library.

   ```Plain Text
   Invoke-WebRequest -Uri 'https://download.microsoft.com/download/1/7/1/1718CCC4-6315-4D8E-9543-8E28A4E18C4C/dxwebsetup.exe' -OutFile 'C:\Users\Administrator\Downloads\dxwebsetup.exe'
   Start-Process 'C:\Users\Administrator\Downloads\dxwebsetup.exe'
   ```
   

   Follow the installation prompts to complete the installation.

6. In PowerShell, execute the following commands to download and update SteamCMD.

   ```Plain Text
   Invoke-WebRequest -Uri 'https://steamcdn-a.akamaihd.net/client/installer/steamcmd.zip' -OutFile 'C:\Users\Administrator\Downloads\steamcmd.zip'
   cd .\Downloads\
   New-Item -ItemType Directory -Name Steam
   Expand-Archive -LiteralPath 'C:\Users\Administrator\Downloads\steamcmd.zip' -DestinationPath 'C:\Users\Administrator\Downloads\Steam'
   Start-Process 'C:\Users\Administrator\Downloads\Steam\steamcmd.exe'
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7f42d636a9540f42f2ffb0b9726f17e6.png) </span>

7. In PowerShell, execute the following command to download and install Palworld.

   ```Plain Text
   C:\Users\Administrator\Downloads\Steam\steamcmd.exe +login anonymous +app_update 2394010 validate +quit
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0694b15d3e237359e8f6c57d1864c432.png) </span>

8. In PowerShell, execute the following commands to start the Palworld server and specify that the server automatically starts upon instance startup.

   ```Plain Text
   Register-ScheduledTask -TaskName "AutoStartPalServer" -Action $(New-ScheduledTaskAction -Execute "C:\Users\Administrator\Downloads\Steam\steamapps\common\PalServer\PalServer.exe") -Trigger $(New-ScheduledTaskTrigger -AtStartup) -Principal $(New-ScheduledTaskPrincipal -UserID "NT AUTHORITY\SYSTEM" -LogonType ServiceAccount -RunLevel Highest)  -Force
   Start-ScheduledTask "AutoStartPalServer"
   ```
   

   After you execute the commands, if the following dialog box is displayed, the Palworld server has been started.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d9ab011f8a251d8e6d4412f5f8cddfee.png) </span>

9. Execute the following command to check whether the Palworld server has started.

   ```Plain Text
   Get-Process | Where-Object{$_.ProcessName -eq "PalServer-Win64-Test-Cmd"}
   ```
   

   If the following output is displayed, the Palworld server is started.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_45abb6d5815cfc0269e55b2438cccdec.png) </span>


<span id=".5q2l6aqk5LiJ77ya5byA5aeL5ri45oiP"></span>
### Step 3: Start the game


1. Start Palworld in Steam.

2. On the game home page, click the "Join multiplayer game (dedicated server)" button.

3. On the start page, select "Community server", and at the bottom of the page, input the `ECS instance EIP:8211`. Click the "Contact" button to enter the dedicated server and start the game.


<span id=".5pu05paw5ri45oiP"></span>
## Update the game

<span id=".5ZyoTGludXjmk43kvZzns7vnu5_kuK3mm7TmlrA="></span>
### Update the game in a Linux\-based instance


1. Execute the following commands on the instance to update the game.

   ```Plain Text
   sudo systemctl stop pal-world-server.service
   sudo -u steam $(which steamcmd)  +login anonymous +app_update 2394010 validate +quit
   ```
   

   If the following output is displayed, the game server is updated.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_850398d2cf1b786a58a21772a2aa7a6d.png) </span>

2. Execute the following commands on the instance to start the game server and view its running status.

   ```Plain Text
   sudo systemctl start pal-world-server.service
   sudo systemctl status pal-world-server.service
   ```
   

   If the following output is displayed, the game server is started.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5d46ef05031a42fc5a81e1288651068c.png) </span>


<span id=".5ZyoV2luZG93c-aTjeS9nOezu-e7n-S4reabtOaWsA=="></span>
### Update the game in a Windows\-based instance


1. In the PowerShell dialog box of the instance, execute the following command to update the Palworld server.

   ```Plain Text
   Stop-Process -Name PalServer-Win64-Test-Cmd
   C:\Users\Administrator\Downloads\Steam\steamcmd.exe +login anonymous +app_update 2394010 validate +quit
   ```
   

2. In the PowerShell dialog box, execute the following commands to start the server and view its running status.

   ```Plain Text
   Start-ScheduledTask "AutoStartPalServer"
   Get-Process | Where-Object{$_.ProcessName -eq "PalServer-Win64-Test-Cmd"}
   ```
   

   If the following output is displayed, the Palworld server is started.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_33f75f2b4f1b3bc224ce6db728c5d1eb.png) </span>
