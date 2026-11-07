---
title: "Remote connection to Dev boxes via SSH"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Remote_connection_to_Dev_boxes_via_SSH"
---

After the Dev boxes are successfully created, they will be `in the running`state. At this time, you can connect to the Dev boxes through WebIDE (new version) and SSH

<span id="使用前提"></span>
## Premise of use


* Dev boxes status is `running`

* Only creator operations are supported


<span id="操作步骤"></span>
## Procedure

You can connect the Dev boxes by clicking Connect on the list page or details page, and choosing WebIDE or SSH connection. The following will introduce the operation steps of the two methods respectively

<span id="配置-ssh-公钥"></span>
### Configuring SSH Public Key


1. Generate key pair

   a. Generate public and private keys on the local machine, you can generate a new public and private key file with the `ssh-keygen`command

   b. Get the public key of the local machine through the `cat~/.ssh/id_rsa.pub`command

2. On the Dev boxes editing page, open `SSH remote development`and fill in the public key. Please enter multiple public keys through line wrapping (please make sure that the local private key file and the filled public key file are a pair, otherwise the connection will fail)

   a. Only supports `running`and `shutdown`state on/off SSH remote development

   b. Support updating SSH remote development listening ports only in `shutdown`state

   <div style="text-align: right">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1fdb8eb47b684b1387e27ccd13cd8da0~tplv-goo7wpa0wc-image.image" width="1648px" />   </div>
   


<span id="连接"></span>
### Connect


1. When the Dev box is running, click [Connect] to operate.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ddf960ddc624d98a7398fc1d91df4c7~tplv-goo7wpa0wc-image.image) </span>

2. After clicking Connect, connect the Dev boxes according to the public network command and the private network command. When logging in using a public or private network, please note the following information:

   1. Public network login: On any machine connected to the public network, you can use the SSH public network command to log in to Dev boxes.

   2. Private network login: When you need to log in to the Dev boxes through the SSH private network command, please ensure that the machine entering the login command is in the corresponding private network

   3. If the access configuration information is not filled in, you can edit the operation through the Dev boxes to complete the SSH access configuration.

3. How to connect Dev boxes via local VSCode

   1. Operation method one

      1. In the Dev boxes details page \- [Connection method] or click [Connect] to view the public/private network login instructions.

      2. In the local VSCode development environment, install the plug\-in Remote Explorer. Next, click the Remote Explorer button on the left, select "SSH TARGETS" in the drop\-down list above, and then click the Settings button on the page, the SSH profile path will appear

      3. Click the SSH path button that appears in the list, open the config file, and configure. The JSON configuration content is as follows

      ```Bash
      ssh -p 12345 root@123.123.123.12HOST DevInstance test
          HostName 123.123.123.12    Port 12345    User root
      ```
      

      5. After configuring JSON, go back to the SSH Targets page, right\-click the Dev boxes and click the [Connect to Host in New Window] button to connect the Dev boxes.

   2. Operation mode 2

      1. In the Dev boxes details page \- Connection method or click [Connect] to view the public network login instructions.

      2. Copy public network instructions

      3. In the local VSCode development environment, install the plug\-in Remote Explorer. Click the Remote Explorer button on the left, select "SSH TARGETS" in the drop\-down list above, click "+", and paste the public network command. The configuration of config will be automatically completed according to the public network instructions.

4. How to connect Dev boxes via Terminal

   1. Open the Terminal on the machine that generated the SSH public key and enter the public network command/private network command to connect to the remote computing node
