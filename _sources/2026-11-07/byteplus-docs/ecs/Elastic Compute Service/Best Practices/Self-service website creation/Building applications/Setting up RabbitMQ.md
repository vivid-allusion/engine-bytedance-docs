---
title: "Setting up RabbitMQ"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Building-RabbitMQ"
---

RabbitMQ is an open\-source message broker that implements the Advanced Message Queuing Protocol (AMQP). It supports multiple clients, including Python, Ruby, .NET, Java, JMS, C, PHP, and ActionScript, and offers ease of use, high scalability, and high availability.

<span id=".6L2v5Lu254mI5pys"></span>
## Software versions


* Operating system: In the example provided in this topic, CentOS 7.6 is used.

* Erlang: In the example provided in this topic, Erlang 24.1 is used.

* RabbitMQ: In the example provided in this topic, RabbitMQ 3.9.7 is used.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A Linux instance is purchased. For more information, see [Purchasing ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* An EIP is associated with the Linux instance, enabling the instance to connect to the Internet. For information about how to associate an EIP with an ECS instance, see [Associating EIPs](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).

* The security group associated with the instance has inbound rules that allow TCP traffic on ports 80, 5672, and 15672. The source address is set to 0.0.0.0/0 or the IP address of the host that needs to access the Linux instance.


<span id=".56ys5LiA5q2l77ya5a6J6KOFRXJsYW5n"></span>
## Step 1: Install Erlang


1. Remotely connect to and log in to the ECS instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to install the dependency packages required for Erlang.

   ```Plain Text
   yum -y install make gcc gcc-c++ m4 ncurses-devel openssl-devel unixODBC-devel
   ```
   

3. Visit the [official Erlang website](http://erlang.org/download/) to get the download link for the required version of Erlang. This topic uses version 24.1 as an example. Execute the following command to download the Erlang installation package.

   ```Plain Text
   wget http://erlang.org/download/otp_src_24.1.tar.gz
   ```
   

4. Execute the following command to decompress the Erlang installation package.

   ```Plain Text
   tar -zxvf otp_src_24.1.tar.gz
   ```
   

5. Execute the following commands to navigate to the Erlang directory and create the folder `/usr/local/erlang`.

   ```Plain Text
   cd otp_src_24.1
   mkdir /usr/local/erlang
   ```
   

6. Execute the following commands to compile and install Erlang.

   ```Plain Text
   ./configure --prefix=/usr/local/erlang
   make && make install
   ```
   

7. Execute the following commands to configure the environment variables for Erlang and make them take effect.

   ```Plain Text
   echo 'export PATH=$PATH:/usr/local/erlang/bin' >> /etc/profile
   source /etc/profile
   ```
   

8. Execute the following commands to return to the root directory and check whether Erlang is installed.

   ```Plain Text
   cd
   erl -version
   ```
   

   If the following output is displayed, Erlang is installed.

   ```Plain Text
   Erlang (SMP,ASYNC_THREADS) (BEAM) emulator version 12.1
   ```
   


<span id=".56ys5LqM5q2l77ya5a6J6KOFUmFiYml0TVE="></span>
## Step 2: Install RabbitMQ


1. Check the [RabbitMQ Erlang Version Requirements](https://www.rabbitmq.com/which-erlang.html?spm=a2c4g.11186623.0.0.69717241rPMLMQ) to confirm the compatible versions of RabbitMQ and Erlang. Then, select a RabbitMQ version that meets the requirements. This topic uses version 3.9.7 as an example.

2. Visit [the official RabbitMQ website](https://www.rabbitmq.com/versions.html) to get the download link for the installation package.

3. Execute the following command to download the RabbitMQ installation package.

   ```Plain Text
   wget https://github.com/rabbitmq/rabbitmq-server/releases/download/v3.9.7/rabbitmq-server-generic-unix-3.9.7.tar.xz
   ```
   

4. Execute the following command to decompress the installation package.

   ```Plain Text
   tar -xvf rabbitmq-server-generic-unix-3.9.7.tar.xz
   ```
   

5. Execute the following commands to configure the environment variables for RabbitMQ and make them take effect.

   ```Plain Text
   echo 'export PATH=$PATH:/root/rabbitmq_server-3.9.7/sbin' >> /etc/profile
   source /etc/profile
   ```
   

6. Execute the following command to start RabbitMQ in the background.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This operation only starts RabbitMQ when the operating system is running. This means RabbitMQ will not start automatically after the instance restarts.   </div>
   

   ```Plain Text
   rabbitmq-server -detached
   ```
   

7. Execute the following command to start the RabbitMQ web management page.

   ```Plain Text
   rabbitmq-plugins enable rabbitmq_management
   ```
   

8. Enter `http://<ECS instance EIP>:15672` in the local browser to access RabbitMQ.

   If the following output is displayed, RabbitMQ is set up successfully.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/acbd7f3d6ba04c138e591f4d78d66859.png) </span>


<span id=".56ys5LiJ5q2l77ya55m75b2VUmFiYml0TVE="></span>
## Step 3: Log in to RabbitMQ


1. Execute the following command to delete the default RabbitMQ account "guest".

   ```Plain Text
   rabbitmqctl delete_user guest
   ```
   

2. Execute the following command to create a new user.

   ```Plain Text
   rabbitmqctl add_user Username Password
   ```
   

3. Execute the following command to set the new user as an administrator.

   ```Plain Text
   rabbitmqctl set_user_tags Username administrator
   ```
   

4. Execute the following command to grant all permissions to the administrator.

   ```Plain Text
   rabbitmqctl set_permissions -p / Username ".*" ".*" ".*"
   ```
   

5. Enter `http://<ECS instance EIP>:15672` in the local browser to access RabbitMQ. After logging in with your username and password, you are directed to the RabbitMQ management page.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/ebbb717e05284c1988aaf1633f64a42a.png) </span>
