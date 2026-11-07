---
title: "What do I do if the root partition of the system disk does not expand automatically after I expand a volume of a Linux instance?"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/After_expanding_Volumes_partition_cannot_autom"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

After I expand the system disk of a Linux instance, the root partition of the system disk does not expand automatically.

<span id=".6Zeu6aKY5Y6f5Zug"></span>
## Causes

Automatic partition expansion for ECS instances on the platform is performed by Cloud\-init. The issue may stem from a lack of tools such as growpart in the Linux instance or incorrect configuration of the cloud.cfg file.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solutions


1. Execute the following command in the faulty instance to check whether growpart is installed.

   ```Plain Text
   which growpart
   ```
   

   * If no output is displayed, the tool is not installed. Execute the following command to install the automatic expansion dependency tool.

      
      <Tabs>
      <Tab zoneid="msWiS09y2Y" title="CentOS">
      <TabTitle>CentOS</TabTitle>
      
      ```Plain Text
      sudo yum -y install cloud-utils-growpart
      ```
      
      
      
      </Tab>
      <Tab zoneid="u9cwsEYdOJ" title="Debian/Ubuntu">
      <TabTitle>Debian/Ubuntu</TabTitle>
      
      ```Plain Text
      sudo apt -y install cloud-guest-utils
      ```
      
      
      
      </Tab>
      </Tabs>
      

   * If an output is displayed, the tool is installed. Continue with the follow\-up procedures.

2. Execute the following command to check whether information about the growpart and resizefs tools exists in the /etc/cloud/cloud.cfg file.

   ```Plain Text
   cat /etc/cloud/cloud.cfg
   ```
   

   Correct sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1cca8f1aa10682c21e651f794b7ebe51.png) </span>

   * If no relevant content is displayed in the output, follow the following steps to supplement the content.

      1. Execute the following command to open the Cloud\-init configuration file.

         ```Plain Text
         vim /etc/cloud/cloud.cfg
         ```
         

      2. In the `cloud_init_modules` module, add information about the growpart and resizefs tools (as shown in the preceding **Correct sample output**).

      3. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save and exit the file.

   * If relevant content is displayed in the output, the issue is resolved.
