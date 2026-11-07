---
title: "Setting up a Java web environment"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Building-a-Java-web-environment"
---

Tomcat is currently a widely used Java web application server. This topic uses Tomcat as an example to describe how to deploy a Java web environment on a Linux instance.

<span id=".6L2v5Lu254mI5pys"></span>
### Software versions


* Operating system: In the example provided in this topic, CentOS 7.6 is used.

* Tomcat: a web application server. In this topic, Tomcat 10.1.41 is used.

* JDK: The Java Development Kit. In the example provided in this topic, JDK 18.0.2.1 is used.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A Linux instance is purchased. For more information, see [Purchasing ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* An EIP is associated with the Linux instance, enabling the instance to connect to the Internet. For information about how to associate an EIP with an ECS instance, see [Associating EIPs](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).


<span id=".5q2l6aqk5LiA77ya5LiL6L296L2v5Lu2"></span>
## Step 1: Download software


1. Remotely connect to and log in to the ECS instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Download the JDK. Go to the [Java SE](https://www.oracle.com/java/technologies/downloads/) page to obtain the download link for the required Java SE version. In the example provided in this topic, JDK 18.0.2.1 is downloaded.

   1. Method 1: First, download the JDK to your local machine, and then upload the JDK to your ECS instance. For more information, see [Overview of local data upload](https://docs.byteplus.com/en/docs/ecs/Local-data-uploading-overview).

   2. Method 2: Run the following command to download JDK 18.0.2.1 to the ECS instance.

      ```Plain Text
      wget https://download.oracle.com/java/18/archive/jdk-18.0.2.1_linux-x64_bin.tar.gz
      ```
      

3. Execute the following command to download Tomcat. This topic uses Tomcat 10.1.41 as an example. Please visit the [Apache official website](https://tomcat.apache.org/index.html) to obtain the download link for the required version.

   ```Plain Text
   wget https://dlcdn.apache.org/tomcat/tomcat-10/v10.1.41/bin/apache-tomcat-10.1.41.tar.gz
   ```
   


<span id=".5q2l6aqk5LqM77ya5a6J6KOFSkRL"></span>
## Step 2: Install the JDK


1. Execute the following command to create a new directory.

   ```Plain Text
   mkdir /usr/java
   ```
   

2. Execute the following command to extract the JDK installation package to the `/usr/java` directory.

   ```Plain Text
   tar xzf jdk-18.0.2.1_linux-x64_bin.tar.gz -C /usr/java
   ```
   

3. Execute the following command to enter the `/usr/java` directory.

   ```Plain Text
   cd /usr/java
   ```
   

4. Execute the following command to modify the `profile` file.

   ```Plain Text
   vi /etc/profile
   ```
   

6. Press the `i` key to enter edit mode and add the following content at the end.

   ```Plain Text
   JAVA_HOME=/usr/java/jdk-18.0.2.1
   JRE_HOME=$JAVA_HOME
   PATH=$JAVA_HOME/bin:$PATH
   CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JRE_HOME/lib/tools.jar
   export JAVA_HOME JRE_HOME PATH CLASSPATH
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6d83b08fda172e60539d14d5a174f4d5.png) </span>

7. Press `Esc`, enter `:wq`, and then press Enter to save and exit the file.

8. Execute the following command to make the newly added configuration in the `profile` file take effect.

   ```Plain Text
   source /etc/profile
   ```
   

9. Execute the following command to verify whether the JDK is installed.

   ```Plain Text
   java -version
   ```
   

   If the following output is displayed, the installation is successful.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3b206895a7f90b544420f1ff72c4eb32.png) </span>


<span id=".5q2l6aqk5LiJ77ya5a6J6KOFVG9tY2F0"></span>
## Step 3: Install Tomcat


1. Execute the following commands in sequence to create a new directory.

   ```Plain Text
   mkdir /usr/tomcat
   ```
   

2. Execute the following command to extract the Tomcat installation package to `/usr/tomcat`.

   ```Plain Text
   tar xzf /root/apache-tomcat-10.1.41.tar.gz -C /usr/tomcat
   ```
   

3. Execute the following command to enter the `bin` directory.

   ```Plain Text
   cd /usr/tomcat/apache-tomcat-10.1.41/bin
   ```
   

4. Execute the following command to modify the `setclasspath.sh` script.

   ```Plain Text
   vi setclasspath.sh
   ```
   

5. Press the `i` key to enter edit mode, and then add the following content.

   ```Plain Text
   JAVA_HOME=/usr/java/jdk-18.0.2.1
   JRE_HOME=$JAVA_HOME
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bc5269aed79905d418da33fdd86fe6c2.png) </span>

6. Press `Esc`, enter `:wq`, and then press Enter to save and exit the file.

7. Execute the following command to start Tomcat.

   ```Plain Text
   ./startup.sh
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4775c6bb1c49134f41ae4c5101285dad.png) </span>


<span id=".5q2l6aqk5Zub77ya5pS-6YCa5Lia5Yqh56uv5Y-j5bm25rWL6K-V"></span>
## Step 4: Allow and test service ports


1. In the inbound rules of the instance security group, allow the port required by the Java web environment. In the example provided in this topic, HTTP port 8080 is allowed.

   1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).  

   2. Click the instance name, select the "Security Group" tab, and click the "Edit rule" button. The security group details are displayed.

   3. On the "Access rules \> Inbound rules" tab, click the "Add rule" button. Set "Priority" to "1", set "Strategy" to "Allow", select "TCP" for "Protocol type", set "Port range" to "8080", and set "Source" to "0.0.0.0/0", as shown in the following figure. Click the "Confirm" button.

2. Enter `http://<ECS instance EIP>:8080` in the local browser to access the Java web environment.

   If the following output is displayed, the Java web environment is set up successfully.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_853b40b0fe4fcdfa4b66ba63610c03e5.png) </span>
