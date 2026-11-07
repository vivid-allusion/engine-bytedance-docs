---
title: "OpenClaw FAQ"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/OpenClaw_deployment_FAQ"
---

This topic summarizes common issues encountered during the deployment of OpenClaw and integration of AI assistants on ECS instances, along with their corresponding solutions.


|Type |FAQ |
|---|---|
|Use OpenClaw |* [An error "404 The model or endpoint xxx does not exist or you do not have access to it." is reported when OpenClaw deployed on an instance calls a model in the Coding Plan. How do I resolve it?](https://docs.byteplus.com/en/docs/ecs/OpenClaw_deployment_FAQ#6ToHic3L)<br><br>* [How do I open the WebUI after I deploy OpenClaw on an ECS instance?](https://docs.byteplus.com/en/docs/ecs/OpenClaw_deployment_FAQ#Lw6xz8ZI)<br><br>* [Why does the error "The requested model does not support function calling, please switch to a different model or contact with administrator if you believe this model should support function calling." occur when I make a function call?](https://docs.byteplus.com/en/docs/ecs/OpenClaw_deployment_FAQ#ATpjbhMn)<br><br>* [After OpenClaw is integrated, the error "400 Input length xxxx exceeds the maximum length xxxx." occurs when I chat with the bot. How do I resolve this issue?](https://docs.byteplus.com/en/docs/ecs/OpenClaw_deployment_FAQ#R7ThxT5T)<br><br>* [How do I handle chat lag or situations where an ECS instance becomes unresponsive when I use OpenClaw?](https://docs.byteplus.com/en/docs/ecs/OpenClaw_deployment_FAQ#vRxfVwdX) |


<span id="KPY49UZZ"></span>
## Use OpenClaw

<span id="6ToHic3L"></span>
### An error "404 The model or endpoint xxx does not exist or you do not have access to it." is reported when OpenClaw deployed on an instance calls a model in the Coding Plan. How do I resolve it?

The 404 error indicating "the model does not exist or you do not have access" is usually caused by the following reasons:


* Incorrect model activation status

   The Coding Plan package must be subscribed to before the relevant models can be used. Log in to the [Model activation page](https://console.byteplus.com/ark/region:ark+cn-beijing/openManagement) and verify whether the model specified in the error message has been activated.

* Incorrect model name

   Make sure that the used model name is completely accurate. You can obtain the model name by referring to [Via configuration file](https://docs.byteplus.com/en/docs/ModelArk/1928261#model-selection).

* Incorrect Base URL configuration

   As a Claude\-like tool, OpenClaw should use the Base URL compatible with the Anthropic interface protocol:

   ```Plain Text
   https://ark.cn-beijing.volces.com/api/coding
   ```
   

   For tools compatible with the OpenAI interface, use the following URL:

   ```Plain Text
   https://ark.cn-beijing.volces.com/api/coding/v3
   ```
   

* Invalid API key used

   Check whether the `ARK_API_KEY` parameter is configured correctly and the configured key has not expired.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If the issue persists after the above checks, we recommend that you refer to the <a href="https://docs.byteplus.com/en/docs/82379/1299023">error code documentation</a> for further troubleshooting guidance or contact technical support for assistance.</div>


<span id="Lw6xz8ZI"></span>
### How do I open the WebUI after I deploy OpenClaw on an ECS instance?


1. Allow inbound traffic on port 18789 in the security group of the instance.

   1. Log in to the [Instances console](https://console.byteplus.com/ecs/region:ecs+cn-shanghai/instance), and click the name of the target instance to enter its details page.

   2. Select the "Security Group" tab, and click the "Configure rule" button to the right of the target security group (Default is used as an example in this topic).

   3. Select the "Access rules \> Inbound rule" tab, and click the "Add rule" button.

   4. Allow access to port 18789 via the TCP protocol.

2. Confirm the OpenClaw version.

   1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

   2. Execute the following command to confirm the currently deployed OpenClaw version.

      ```Bash
      openclaw --version
      ```
      

3. Open the WebUI.

   
   <Tabs>
   <Tab zoneid="NkTzKoAMT4" title="Linux">
   <TabTitle>Linux</TabTitle>
   
   Remotely access the WebUI from a local PC.
   
   
   1. Execute the following command to obtain the OpenClaw authorization token.
   
      ```Bash
      openclaw dashboard
      ```
      
   
      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
      
   
      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Securely keep the returned token. Leakage of the token may lead to serious security risks.   </div>
      
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_928b51872dab7c0a97d75d60dcb2e958.png) </span>
   
   2. Execute the following command to map port 18789 of the local PC to port 127.0.0.1:18789 of the OpenClaw server.
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Make sure that the terminal window where the command is executed remains open during WebUI access.   </div>
      
   
      <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Adjust the parameters based on your actual situation:   </div>
      
   
      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code><user_name></code> with the login username of the instance where the OpenClaw service is deployed.   </div>
      
   
      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code><public_ip></code> with the EIP of the instance where the OpenClaw service is deployed.   </div>
      
   
      ```Bash
      ssh -N -L 18789:127.0.0.1:18789 <user_name>@<public_ip>
      ```
      
   
   3. In the browser on the current PC, visit `http://127.0.0.1:18789?token=<your_token>` to open the OpenClaw WebUI interface.
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code><your_token></code> with the OpenClaw authorization token obtained in Step 1.   </div>
      
   
   
   </Tab>
   <Tab zoneid="aBfI1hVoXA" title="Windows">
   <TabTitle>Windows</TabTitle>
   
   Open the WebUI on the instance where OpenClaw is deployed.
   
   
   1. Execute the following command in PowerShell to obtain the OpenClaw authorization token.
   
      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
      
   
      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Securely keep the returned token. Leakage of the token may lead to serious security risks.   </div>
      
   
      ```PowerShell
      openclaw dashboard
      ```
      
   
   2. Subsequently, you can open a browser on the current instance and visit `http://127.0.0.1:18789?token=<your_token>` to access the OpenClaw WebUI.
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code><your_token></code> with the OpenClaw authorization token obtained in the previous step.   </div>
      
   
   
   </Tab>
   </Tabs>
   


<span id="ATpjbhMn"></span>
### Why does the error "The requested model does not support function calling, please switch to a different model or contact with administrator if you believe this model should support function calling." occur when I make a function call?

This issue occurs because the model you are using does not support function calling. We recommend that you switch to a model that supports function calling. [Click here to view the list of models supporting function calling](https://docs.byteplus.com/en/docs/82379/1330310).

<span id="R7ThxT5T"></span>
### After OpenClaw is integrated, the error "400 Input length xxxx exceeds the maximum length xxxx." occurs when I chat with the bot. How do I resolve this issue?

During conversational inference, the model incorporates the full context as input parameters into a single inference request to implement session memory. This error occurs and interrupts inference when the context length exceeds the maximum input limit of the model. We recommend that you reset the session regularly to avoid excessively long context:


* Clear via the IM dialog box

   If you have integrated OpenClaw with IM tools such as Feishu, enter the `/new` or `/reset` command in the OpenClaw bot chat window of the IM tool to start a new conversation and clear the context of the previous one.

* Clear via the WebUI

   If you chat with OpenClaw through its WebUI, [open the WebUI](https://docs.byteplus.com/en/docs/ecs/OpenClaw_deployment_FAQ#Lw6xz8ZI), go to the Chat page, and click the "New session" button to start a new conversation and clear the context of the previous one.


<span id="vRxfVwdX"></span>
### How do I handle chat lag or situations where an ECS instance becomes unresponsive when I use OpenClaw?

When you interact with OpenClaw through multiple channels, or perform updates, restarts, log queries, and other operations, OpenClaw may create a new process for each task. If multiple processes compete for instance resources simultaneously, it may result in issues such as chat lag or instance unresponsiveness. In this case, you can:


1. Optimize memory usage configuration.

   1. [Log in to the ECS instance where OpenClaw is deployed](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

   2. Execute the following command to create a script file.

      ```Bash
      vim /root/config_swap.sh
      ```
      

   3. Press the `i` key to enter edit mode, and then copy and paste the following content into the file.

      ```Bash
      #!/bin/bash
      set -e
      # If /swapfile already exists on the current system, skip the setting
      if [ -f /swapfile ]; then
          echo "The swapfile already exists..."
      else
          fallocate -l 2G /swapfile
          # First, modify the file permissions to grant read and write access only to the root user
          chmod 600 /swapfile
          # Set as swap file
          mkswap -f /swapfile
          # Finally, enable the swap file
          swapon /swapfile
      fi
      # To enable swap permanently, add the entry after the line for the root partition.
      if ! grep -q "^/swapfile" /etc/fstab; then
          echo "/swapfile  swap     swap    defaults      0       0" >> /etc/fstab
      fi
      # Permanently configure swappiness
      if grep -q '^vm\.swappiness' /etc/sysctl.conf ;then
          sed -i 's/^vm\.swappiness[[:space:]]*=[[:space:]]*[0-9]\+$/vm.swappiness = 20/' /etc/sysctl.conf
      else
          echo 'vm.swappiness = 20' >> /etc/sysctl.conf
      fi
      sysctl -w vm.swappiness=20
      ```
      

   4. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save and exit the file.

   5. Execute the following command to run the script file and optimize memory usage configuration.

      ```Bash
      bash /root/config_swap.sh
      ```
      

      If the output is as shown below, it indicates that memory usage optimization is completed.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8acd775192d32688e878d062b5960421.png) </span>

2. If the issue persists after you optimize memory usage configuration, we recommend that you:

   *  **(Recommended) ** Upgrade the instance configuration and deploy OpenClaw on a higher\-specification instance (such as 4 vCPUs, 8 GiB). [Learn more.](https://docs.byteplus.com/en/docs/ecs/Modify-instance-type)

   * Restart the target instance in the ECS console. [Learn more.](https://docs.byteplus.com/en/docs/ecs/Restarting-instances)
