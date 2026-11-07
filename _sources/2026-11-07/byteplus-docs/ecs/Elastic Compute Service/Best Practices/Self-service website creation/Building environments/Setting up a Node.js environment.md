---
title: "Setting up a Node.js environment"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Building-a-Node-js-environment"
---

Node.js is a JavaScript runtime environment built on the Chrome V8 engine. It leverages an event\-driven, non\-blocking I/O model, enabling the seamless development of responsive and scalable network applications. This topic describes how to deploy this environment on a Linux instance.

<span id=".6L2v5Lu254mI5pys"></span>
### Software versions


* Operating system: In the example provided in this topic, CentOS 8.3 is used.

* Node.js: In the example provided in this topic, v6.9.5 and v10.14.2 are used.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A Linux instance is purchased. For more information, see [Purchasing ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* An EIP is associated with the Linux instance, enabling the instance to connect to the Internet. For information about how to associate an EIP with an ECS instance, see [Associating EIPs](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).


<span id=".5q2l6aqk5LiA77ya5a6J6KOFTm9kZS5qcw=="></span>
## Step 1: Install Node.js


1. Remotely connect to and log in to the ECS instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. You can select one of the following installation methods based on your business requirements.

   
   |Installation method |Description |
   |---|---|
   |NVM |Node Version Manager (NVM) is a version management tool for Node.js. If you use NVM to install Node.js, you can quickly switch between different Node.js versions. |
   |Binary files |Use the platform (recommended) or the Node.js official website binary files to install a specific version. Version switching is not supported. |
   

   * Use NVM to install multiple versions

      1. Execute the following command to install Git.

         ```Plain Text
         yum install -y git
         ```
         

      2. Execute the following commands to clone the source code into your local ~/.nvm directory by using Git, and check for the latest version.

         ```Plain Text
         git clone https://github.com/cnpm/nvm.git ~/.nvm && cd ~/.nvm && git checkout `git describe --abbrev=0 --tags`
         ```
         

      3. Execute the following command to activate NVM and write it to the profile file.

         ```Plain Text
         echo ". ~/.nvm/nvm.sh" >> /etc/profile
         ```
         

      4. Execute the following command to make the environment variables take effect.

         ```Plain Text
         source /etc/profile
         ```
         

      5. Execute the following command to view all versions of Node.js.

         ```Plain Text
         nvm list-remote
         ```
         

      6. Execute the following commands to install multiple required Node.js versions.

         ```Plain Text
         nvm install v6.9.5
         nvm install v10.14.2
         ```
         

      7. Execute the following command to view the installed Node.js versions.

         ```Plain Text
         nvm ls
         ```
         

         If the following output is displayed, the installation is successful and the current version in use is v10.14.2.

         <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/ce35f11952ed4ec6b6368343edfeacbd.png) </span>

      8. Execute the following command to switch versions.

         ```Plain Text
         nvm use v6.9.5
         ```
         

         If the following output is displayed, the switch is successful.

         <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/ff335f8c9f454444afdcd395af8b32fa) </span>

   * Use platform binary files to install Node.js

      1. Execute the following command to download the Node.js installation package.

         ```Plain Text
         wget https://mirrors.ivolces.com/nodejs-release/v6.9.5/
         dnf -y install nodejs
         ```
         

      2. Execute the following command to view the Node.js and npm versions.

         ```Plain Text
         node -v
         ```
         

   * Use binary files from the Node.js official website to install Node.js

      1. Execute the following command to download the Node.js installation package. You can visit [the official Node.js website](https://nodejs.org/zh-cn/download/) to download more installation packages.

         ```Plain Text
         wget https://nodejs.org/dist/v6.9.5/node-v6.9.5-linux-x64.tar.xz
         ```
         

      2. Execute the following command to extract the installation package.

         ```Plain Text
         tar xvf node-v6.9.5-linux-x64.tar.xz
         ```
         

      3. Execute the following commands to create symbolic links for node and npm. After you create symbolic links, you can use the node and npm commands in any directory within the instance.

         ```Plain Text
         ln -s /root/node-v6.9.5-linux-x64/bin/node /usr/local/bin/node
         ln -s /root/node-v6.9.5-linux-x64/bin/npm /usr/local/bin/npm
         ```
         

      4. Execute the following command to view the Node.js and npm versions.

         ```Plain Text
         node -v
         npm -v
         ```
         


<span id=".5q2l6aqk5LqM77ya6YOo572y56S65L6L6aG555uu"></span>
## Step 2: Deploy a sample project


1. Execute the following command to enter the home directory of the instance.

   ```Plain Text
   cd
   ```
   

2. Execute the following command to create and open the project file test.js.

   ```Plain Text
   vim test.js
   ```
   

3. Press the `i` key to enter edit mode, and then paste the following content into the file.

   * const port: You can specify a port number based on your business requirements.

      ```Plain Text
      const http = require('http'); 
      const hostname = '0.0.0.0'; 
      const port = 3500; 
      const server = http.createServer((req, res) => {
          res.statusCode = 200; 
          res.setHeader('Content-Type', 'text/plain'); 
          res.end('Hello World\n'); 
      }); 
      server.listen(port, hostname, () => {
          console.log(`Server running at http://${hostname}:${port}/`); 
      });
      ```
      

4. Press the `Esc` key to exit edit mode, enter `:wq`, and then press `Enter` to save and exit the file.

5. Execute the following command to run the project.

   ```Plain Text
   node ~/test.js
   ```
   


<span id=".5q2l6aqk5LiJ77ya5pS-6YCa5Lia5Yqh56uv5Y-j5bm25rWL6K-V"></span>
## Step 3: Allow and test service ports


1. In the inbound rules of the instance security group, allow "const port" and the IP address of the host intending to access the project.

   1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).  

   2. Click the instance name. On the "Overview" tab, click "Security Group". The "Security Group" tab is displayed.

   3. Click the "Edit rule" button. On the "Access rules \> Inbound rules" tab, add a rule. Set "Strategy" to "Allow", select "TCP" for "Protocol type", set "Port range" to "const port", and set "Source" to the IP address of the host intending to access the project, as shown in the following figure. For more information, see [Security group overview](https://docs.byteplus.com/en/docs/ecs/Security-group-overview).

2. In the local browser, enter `http://<ECS instance EIP>:port number` to access the test.js project.
