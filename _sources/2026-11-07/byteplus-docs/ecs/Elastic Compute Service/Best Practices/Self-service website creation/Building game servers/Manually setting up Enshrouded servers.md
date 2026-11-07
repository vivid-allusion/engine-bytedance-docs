---
title: "Manually setting up Enshrouded servers"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Manually_build_an_Enshrouded_server"
---

This topic mainly describes how to quickly set up an Enshrouded server on a Windows\-based instance.

<span id=".5LuA5LmI5piv6Zu-6ZSB546L5Zu9"></span>
## What is Enshrouded?

Enshrouded is a cooperative survival action RPG developed by Keen Games GmbH.

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenario

You can set up a dedicated server using an ECS instance, which allows you and your friends to log in for better playing experience. The dedicated server can offer better privacy and help avoid issues like game crashes caused by overcrowding on official servers.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have [created an ECS instance](https://docs.byteplus.com/en/docs/ecs/Overview-of-methods-for-buying-ECS-instances).

* Currently, you can set up an Enshrouded server only on a Windows operating system. We recommend using the Windows Server 2022 operating system for your instance.

* The target instance must be associated with an EIP. For information about how to associate an EIP with an ECS instance, see [Associating EIPs](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YWN572u5a6J5YWo57uE"></span>
### Step 1: Configure a security group


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the region and project where the target instance resides.

4. On the Instances page, find the target instance, and click the instance name to go to the instance details page.

5. Select the "Security Group" tab, and then click the "Edit rule" button.

6. On the security group details page, select "Access rules \> Inbound rules". Then, on the "Inbound rules" tab, configure a security rule as follows.

   1. Click the "Add rule" button.

   2. On the "Add Inbound rule" page:

      1. Specify "Protocol type" as `TCP`, copy `15636, 15637` into the "Port range" field, and copy `0.0.0.0/0` into the "Source" field.

      2. Click the "Add rule" button. Then, specify "Protocol type" as `UDP`, copy `15636, 15637` into the "Port range" field, and copy `0.0.0.0/0` into the "Source" field. Click the "Confirm" button to complete the configuration.


<span id=".5q2l6aqk5LqM77ya5pCt5bu66Zu-6ZSB546L5Zu95pyN5Yqh5Zmo"></span>
### Step 2: Set up an Enshrouded server


1. Log in to the target instance. For more information, refer to [Logging in to Windows instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Windows-instance).

2. Right\-click the "Start" button and select "Windows PowerShell (Admin)" to open PowerShell.

3. In PowerShell, execute the following commands to allow users to access your ECS instance through ports `15636` and `15637`.

   ```Plain Text
   New-NetFirewallRule -DisplayName "Allow UDP 15636" -Protocol UDP -LocalPort 15636 -Action Allow 
   New-NetFirewallRule -DisplayName "Allow TCP 15636" -Protocol TCP -LocalPort 15636 -Action Allow 
   New-NetFirewallRule -DisplayName "Allow UDP 15637" -Protocol UDP -LocalPort 15637 -Action Allow 
   New-NetFirewallRule -DisplayName "Allow TCP 15637" -Protocol TCP -LocalPort 15637 -Action Allow
   ```
   

   If the following output is displayed, configuration succeeds.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_38fd48d5a83237cf836a83720c60e6f6.png) </span>

4. In PowerShell, execute the following commands to download and update SteamCMD.

   ```Plain Text
   Invoke-WebRequest -Uri 'https://steamcdn-a.akamaihd.net/client/installer/steamcmd.zip' -OutFile 'C:\Users\Administrator\Downloads\steamcmd.zip'
   cd .\Downloads\
   New-Item -ItemType Directory -Name Steam
   Expand-Archive -LiteralPath 'C:\Users\Administrator\Downloads\steamcmd.zip' -DestinationPath 'C:\Users\Administrator\Downloads\Steam'
   Start-Process 'C:\Users\Administrator\Downloads\Steam\steamcmd.exe'
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4fdcff337e496e39ccfbedf8eb4be494.png) </span>

5. In PowerShell, execute the following command to download and install the Enshrouded server.

   ```Plain Text
   C:\Users\Administrator\Downloads\Steam\steamcmd.exe +login anonymous +app_update 2278520 validate +quit
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eb3a42c1164006a25113f9cc5ee91c61.png) </span>

6. Modify the Enshrouded server configuration file.

   1. In PowerShell, execute the following command to open the configuration file.

      ```Plain Text
      Start-Process notepad.exe -FilePath "C:\Users\Administrator\Downloads\Steam\steamapps\common\EnshroudedServer\enshrouded_server.json"
      ```
      

   2. Adjust the values of the `name` and `password` parameters in the file. If you need to change the maximum number of players allowed to join a room, adjust the value of the `slotCount` parameter.

   * name: Required. Enter a name for the server room you create.

   * password: Required. Enter a password to access your server room.

   * slotCount: Required. Configure the maximum number of players allowed to join the room (upper limit: `16`). The value for slotCount must be an integer.

   3. After configuration is complete, press `Ctrl`+`s` to save changes and close the file.

7. In PowerShell, execute the following commands to specify that the Enshrouded server automatically starts upon instance startup.

   ```Plain Text
   Register-ScheduledTask -TaskName "AutoStartEnshroudedServer" -Action $(New-ScheduledTaskAction -Execute"C:\Users\Administrator\Downloads\Steam\steamapps\common\EnshroudedServer\enshrouded_server.exe") -Trigger $(New-ScheduledTaskTrigger -AtStartup) -Principal $(New-ScheduledTaskPrincipal -UserID "NT AUTHORITY\SYSTEM" -LogonType ServiceAccount -RunLevel Highest)  -Force
   Start-ScheduledTask "AutoStartEnshroudedServer"
   ```
   

8. Execute the following command to check whether the Enshrouded server has started.

   ```Plain Text
   Get-Process | Where-Object{$_.ProcessName -eq "enshrouded_server"}
   ```
   

   If the following output is displayed, the server is started.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bfab6c276f8d20c3cd918ccc9baaa907.png) </span>


<span id=".5q2l6aqk5LiJ77ya55m75b2V6Zu-6ZSB546L5Zu95LiT5bGe5pyN5Yqh5Zmo"></span>
### Step 3: Log in to the Enshrouded dedicated server


1. You and your friends can start Enshrouded on Steam.

2. On the game home page, click the "Join (join an online game)" button.

3. On the "Online game" page, search the room by the `name` parameter value you configured (your room name).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Since this game only supports search by room name, the searching process may take longer. Please wait patiently.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you forget the room name or password, you can find the information in the enshrouded_server.json file located at <code>C:\Users\Administrator\Downloads\Steam\steamapps\common\EnshroudedServer\</code> on your ECS instance.   </div>
   

4. After you find the room, click the "Join" button, and enter the value of the `password` parameter you configured (the password for entering the room). After this, you can join the game.


<span id=".55u45YWz5pON5L2c"></span>
## Related operations

<span id=".5pu05paw5ri45oiP"></span>
### Update the game

During a game update, you can log in to an ECS instance, open PowerShell as an administrator, and execute the following commands to update and restart an Enshrouded server.

```Plain Text
taskkill /f /im enshrouded_server.exe
C:\Users\Administrator\Downloads\Steam\steamcmd.exe +login anonymous +app_update 2278520 validate +quit
Start-Process 'C:\Users\Administrator\Downloads\Steam\steamapps\common\EnshroudedServer\enshrouded_server.exe'
```


<span id=".6LCD5pW05pyN5Yqh5Zmo6YWN572u"></span>
### Adjust server configurations

You can adjust the name, password, and player number of the game.


1. After you log in to an ECS instance, execute the following commands in PowerShell as an administrator.

   ```Plain Text
   taskkill /f /im enshrouded_server.exe
   Start-Process notepad.exe -FilePath "C:\Users\Administrator\Downloads\Steam\steamapps\common\EnshroudedServer\enshrouded_server.json"
   ```
   

2. Adjust values of the following parameters in the file as needed.

   * name: Required. Enter a name for the server room you create.

   * password: Required. Enter a password to access your server room.

   * slotCount: Required. Configure the maximum number of players allowed to join the room (upper limit: `16`). The value for slotCount must be an integer.

3. Press `Ctrl`+`s` to save changes and close the file.

4. In PowerShell, execute the following commands to start the Enshrouded server.

   ```Plain Text
   Start-ScheduledTask "AutoStartEnshroudedServer"
   Get-Process | Where-Object{$_.ProcessName -eq "enshrouded_server"}
   ```
   

   If the following output is displayed, the server is started.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5094ba0f6f5d8c924863ebd8739cf162.png) </span>
