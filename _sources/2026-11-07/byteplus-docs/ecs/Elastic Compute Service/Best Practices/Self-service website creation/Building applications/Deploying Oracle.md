---
title: "Deploying Oracle"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Building-Oracle"
---

Oracle is a database commonly used for online transaction processing (OLTP), data warehousing (DW), and hybrid (OLTP & DW) database workloads. This topic describes how to deploy Oracle.

## Prerequisites

* [Oracle officially](https://docs.oracle.com/en/database/oracle/oracle-database/21/ladbi/oracle-database-installation-checklist.html#GUID-E847221C-1406-4B6D-8666-479DB6BDB046) recommends using Linux operating systems version 7.4 or later.

* You have [purchased an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) and [associated an EIP with it](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).

* The ECS instance status is **Running**.

## Software versions

* Linux operating system: In the example provided by this topic, CentOS 7.6 is used.

* Oracle database: 19.3.0.0.

## Procedure

### Step 1: Download software

1. Download an installation package of Oracle database 19.3.

   1. From a local computer, access the [Oracle official website](https://www.oracle.com/database/technologies/oracle-database-software-downloads.html#19c) to download the LINUX.X64_193000_db_home.zip package.

      > You need to register for and log in to an Oracle account to download the package.

   2. Upload the local Oracle installation package to the `/home` directory on the Linux server. For detailed operations, refer to [Overview of local data upload](https://docs.byteplus.com/en/docs/ecs/Local-data-uploading-overview).

### Step 2: Install Oracle

#### Prepare the installation environment

1. Execute the following command to update CentOS system components to the latest version.

   ```Bash
   yum update -y
   ```

2. Execute the following command to install required components.

   ```Bash
   yum install -y \
     binutils.x86_64 \
     compat-libcap1.x86_64 \
     gcc.x86_64 \
     gcc-c++.x86_64 \
     glibc.i686 \
     glibc.x86_64 \
     glibc-devel.i686 \
     glibc-devel.x86_64 \
     ksh \
     compat-libstdc++-33 \
     libaio.i686 \
     libaio.x86_64 \
     libaio-devel.i686 \
     libaio-devel.x86_64 \
     libgcc.i686 \
     libgcc.x86_64 \
     libstdc++.i686 \
     libstdc++.x86_64 \
     libstdc++-devel.i686 \
     libstdc++-devel.x86_64 \
     libXi.i686 \
     libXi.x86_64 \
     libXtst.i686 \
     libXtst.x86_64 \
     make.x86_64 \
     sysstat.x86_64
   ```

3. Disable SELinux.

   Execute the `sestatus -v` command to view the SELinux status.

   > **tip**

   * > By default, SELinux is disabled in a CentOS public image provided by BytePlus.

   * > If SELinux is enabled, execute the `setenforce 0` command to disable it.

4. Disable firewall.

   Execute the `systemctl status firewalld` command to view the firewall status.

   > **tip**

   * > By default, the firewall is disabled in a CentOS public image provided by BytePlus.

   * > If the firewall is enabled, execute the `systemctl stop firewalld` command to disable it.

5. Execute the following commands to create the required operating system groups and users for the Oracle database, and set the password for the Oracle user.

   ```Bash
   groupadd oinstall
   groupadd dba
   groupadd asmdba
   groupadd backupdba
   groupadd dgdba
   groupadd kmdba
   groupadd racdba
   groupadd oper
   useradd -g oinstall -G dba,asmdba,backupdba,dgdba,kmdba,racdba,oper -m oracle
   passwd oracle
   ```

6. Edit the file `/etc/hosts` to configure the domain name resolution file.

   1. Execute the `hostname` command to view the hostname.

      A hostname refers to an internal computer name in the operating system. It identifies a computer on a network and differs from an instance ID.

   2. Execute the following command to open the `/etc/hosts` file.

      ```Bash
      vim /etc/hosts
      ```

   3. Press `i` key to enter edit mode and add the private IP address and hostname to the end.

      ```Plain Text
      192.xx.xx.xx hostname
      ```

      > **Description**

      > You can obtain the private IP address of the instance on the Instances page.

   4. Press `Esc`, enter `:wq`, and then press Enter to save the modifications and close the file.

7. Edit the `/etc/sysctl.conf` file to modify kernel parameters.

   1. Execute the following command to open the `/etc/sysctl.conf` file.

      ```Bash
      vim /etc/sysctl.conf
      ```

   2. Press `i` key to enter edit mode and add the following content at the end.

      ```Plain Text
      fs.aio-max-nr = 1048576
      fs.file-max = 6815744
      kernel.shmall = 16451328
      kernel.shmmax = 33692319744   #Half of the physical memory
      kernel.shmmni = 4096
      kernel.sem = 250 32000 100 128
      net.ipv4.ip_local_port_range = 9000 65500
      net.core.rmem_default = 262144
      net.core.rmem_max = 4194304
      net.core.wmem_default = 262144
      net.core.wmem_max = 1048576
      ```

   3. Press `Esc`, enter `:wq`, and then press Enter to save the modifications and close the file.

   4. Execute the `sysctl -p` command to make kernel modifications take effect.

8. Edit the `/etc/security/limits.conf` file to modify user limits.

   1. Execute the following command to open the `/etc/security/limits.conf` file.

      ```Bash
      vim /etc/security/limits.conf
      ```

   2. Press `i` key to enter edit mode and add the following content at the end.

      ```Plain Text
      @oinstall soft nofile 2048
      @oinstall hard nofile 65536
      @oinstall soft nproc 16384
      @oinstall soft stack 10240
      ```

   3. Press `Esc`, enter `:wq`, and then press Enter to save the modifications and close the file.

9. Edit the `.bash_profile` file to set environment variables.

   1. Execute the `su - oracle` command to switch to the oracle user.

   2. Execute the following command to open the `.bash_profile` file.

      ```Bash
      vim .bash_profile
      ```

   3. Press `i` key to enter edit mode and add the following content at the end.

      > **tip**

      > Replace the value of the ORACLE_HOSTNAME parameter with the hostname.

      ```Plain Text
      export ORACLE_BASE=/u01/app/oracle
      export ORACLE_HOME=/u01/app/oracle/product/19c
      export PATH=$PATH:$ORACLE_HOME/bin:/usr/local/bin
      export ORACLE_HOSTNAME=i-7grb71fftuhprqn9****   #Please modify it to your hostname
      export ORACLE_SID=test                          #Oracle System ID
      export LD_LIBRARY_PATH=$ORACLE_HOME/lib:$ORACLE_HOME/rdbms/lib:$ORACLE_HOME/network/lib:/lib:/usr/lib
      export CLASSPATH=$ORACLE_HOME/jlib:$ORACLE_HOME/rdbms/jlib:$ORACLE_HOME/network/jlib
      ```

   4. Press `Esc`, enter `:wq`, and then press Enter to save the modifications and close the file.

   5. Execute the `source .bash_profile` command to make file modifications take effect.

10. Execute the following command to switch to the root user.

   ```Bash
   su -
   ```

11. Execute the following commands to create an Oracle installation directory.

   ```Bash
   mkdir /u01
   chmod 777 /u01
   ```

#### Extract the installation package

1. Execute the following commands to extract the zip file of the Oracle database software.

   ```Bash
   mkdir -p /u01/app/oracle/product/19c
   yum install zip unzip -y
   unzip /home/LINUX.X64_193000_db_home.zip -d /u01/app/oracle/product/19c
   ```

2. Execute the following command to change the ownership of /u01.

   ```Bash
   chown -R oracle:oinstall /u01
   ```

#### Install software

You can choose silent command\-line installation or graphical interface installation. If you select the graphical interface installation, make sure that your instance has the [graphical interface installed](https://docs.byteplus.com/en/docs/ecs/Install-a-GUI-in-Linux).

##### Silent command\-line installation

1. Execute the `su - oracle` command to switch to the oracle user.

2. Execute the following commands to back up the response file.

   ```Bash
   cd /u01/app/oracle/product/19c/install/response
   cp db_install.rsp db_install.rsp.bak
   ```

3. Edit the `db_install.rsp` file to configure the response file.

   1. Execute the following command to open the `db_install.rsp` file.

      ```Bash
      vim db_install.rsp
      ```

   2. Press `i` key to enter edit mode. Only modify the parameter values displayed below; keep all other parameters at their default values.

      ```Plain Text
      oracle.install.option=INSTALL_DB_SWONLY
      UNIX_GROUP_NAME=oinstall
      INVENTORY_LOCATION=/u01/app/oraInventory
      ORACLE_HOME=/u01/app/oracle/product/19c
      ORACLE_BASE=/u01/app/oracle
      oracle.install.db.InstallEdition=EE
      oracle.install.db.OSDBA_GROUP=dba
      oracle.install.db.OSOPER_GROUP=oper
      oracle.install.db.OSBACKUPDBA_GROUP=backupdba
      oracle.install.db.OSDGDBA_GROUP=dgdba
      oracle.install.db.OSKMDBA_GROUP=kmdba
      oracle.install.db.OSRACDBA_GROUP=racdba
      oracle.install.db.rootconfig.executeRootScript=false
      ```

   3. Press `Esc`, enter `:wq`, and then press `Enter` to save the modifications and close the `db_install.rsp `file.

4. Execute the following commands to install Oracle.

   ```Bash
   cd /u01/app/oracle/product/19c
   ./runInstaller -silent -responseFile /u01/app/oracle/product/19c/install/response/db_install.rsp
   ```

   If the following output is returned, the installation succeeds.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_604adcb475fdf76f7d8e943123e14d7b.png)

5. Execute the following commands to run the scripts.

   ```Bash
   su -
   /u01/app/oraInventory/orainstRoot.sh
   /u01/app/oracle/product/19c/root.sh
   ```

   If the following output is returned, scripts have run successfully.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2c5b620cd2a5081e7fdea158798dca0c.png)

##### Graphical interface installation

1. [Log in to the Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) via VNC.

2. In the graphical interface, enter the Oracle user password, and then click "Applications \> System Tools \> Terminal" to open the terminal.

3. Execute the following commands to install Oracle.

   ```Bash
   cd /u01/app/oracle/product/19c
   ./runInstaller
   ```

4. In the "Select Configuration Option" window that pops up, select "Set Up Software Only", and click "Next".

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/ee34570648774a90bd5a0fce029190f7.png)

5. In the windows from Step 2 to Step 6, keep the default configurations and click "Next" in sequence.

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/a48e219f27ac4fea8fe4ce5eae7b0b03.png)

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/69d610047e18432697df2d8c935048fc.png)

   ![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_d6597df81d7d748088006e9917dc4c10.png)

   ![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1669e7b5cf295d21d833910cfab06228.png)

   ![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_5a228345da2889a9be4e559c7f1a5cd6.png)

6. In the "Root script execution configuration" window, select "Automatically run configuration scripts", enter the root user password, and click "Next".

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/53103d623d644ac1b938ac79356fc340.png)

7. In the "Perform Prerequisite Checks" window, select "Ignore All" and then click "Next".

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/ce1b2d6d76c648869c79e713def84259.png)

8. In the prompt window that pops up, select "Yes".

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/8f34ae55fbc647c1844badd4af38f42d.png)

9. In the "Summary" window, click "Install".

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/387b1d3b9c864acc92c10199c0d225fd.png)

10. Wait for the Oracle installation to complete. When the pop\-up window appears, click "Yes" to complete the installation.

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/95f2c2b0eedd4653aaa3dc16b1eb5ec3.png)

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/5fe677ac6f1f4274a8d2133ad030813b.png)

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/1b0b4b86730845a2abb5514ec854c0e5.png)

### Step 3: Create a database

You can choose silent command\-line creation or graphical interface creation. If you choose graphical interface creation, make sure that your instance has [the graphical interface installed](https://docs.byteplus.com/en/docs/ecs/Install-a-GUI-in-Linux).

#### Silent command\-line creation

##### Create a Listener

1. Execute the `su - oracle` command to switch to the oracle user.

2. Execute the following commands to create a Listener.

   ```Bash
   netca /silent /responseFile /u01/app/oracle/product/19c/assistants/netca/netca.rsp
   lsnrctl status
   ```

   If the following output is returned, the creation succeeds.

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/23ab3c10887e4e33bb893d97eb9218d7.png)

##### Create the database

1. Execute the following commands to back up the response file.

   ```Bash
   cd /u01/app/oracle/product/19c/assistants/dbca
   cp dbca.rsp dbca.rsp.bak
   ```

2. Edit the `dbca.rsp` file to configure the response file.

   1. Execute the following command to open the `dbca.rsp` file.

      ```Bash
      vim dbca.rsp
      ```

   2. Press `i` key to enter edit mode. Only modify the parameter values displayed below; keep all other parameters at their default values.

      ```Plain Text
      gdbName=test
      sid=test
      databaseConfigType=SI
      templateName=General_Purpose.dbc
      sysPassword="password" //Please customize the password
      systemPassword="passowrd" //Please customize the password
      emConfiguration=DBEXPRESS
      dbsnmpPassword="password" //Please customize the password
      datafileDestination=/u01/app/oracle/oradata
      characterSet=AL32UTF8
      totalMemory=8192
      ```

   3. Press `Esc`, enter `:wq`, and then press Enter to save the modifications and close the file.

3. Execute the following command to install the database.

   ```Bash
   dbca -silent -createDatabase -responseFile /u01/app/oracle/product/19c/assistants/dbca/dbca.rsp
   ```

   If the following output is returned, the creation succeeds.

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/dea22c235118496db55431b7268d9621.png)

#### Graphical interface creation

##### Configure the Listener

1. In the terminal, execute the `netca` command to open the "Oracle Net Configuration Assistant: Welcome" window. Then, select "Listener configuration" and click "Next" twice.

   > **tip**

   > In this step, you need to log in to the ECS via VNC and execute the command as the oracle user.

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/b152b4e38f3941709d85180ed922273c.png)

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/03c72eea8c6643af96e5b610896b58fc.png)

2. In the "Oracle Net Configuration Assistant: Listener Configuration, Listener" window, set the Listener name. In the example provided in this topic, the default name is used. Click "Next".

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/a638ea5b522e4eb3b8b45d207c2bbc92.png)

3. In the "Oracle Net Configuration Assistant: Listener Configuration, Select Protocols" window, select the protocol you need to add. In the example provided in this topic, TCP is selected. Click "Next".

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/c118e30bbc5d44bf8ae05742535def4f.png)

4. Keep the default configurations, and click "Next" three times in a row.

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/f42cdeca09564cb8afcc603443676bf1.png)

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/dec8a9d43b5149f1aec8b0f57bdd6a7a.png)

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/4261bcf7cb98418c99735a4893ec4348.png)

5. In the "Oracle Net Configuration Assistant: Welcome" window, click "Finish" to complete the Listener configuration.

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/0db54fdd77aa4a30a1e9a3736c02d86a.png)

##### Create the database

1. In the terminal, execute the `dbca` command to open the "Database Operation" window, select "create a database", and then click "Next".

   > **tip**

   > In this step, you need to log in to the ECS via VNC and execute the command as the oracle user.

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/970174abcc7d432cae1609f33951a032.png)

2. In the "Select Database creation Mode" window, select "Advanced configuration", and then click "Next".

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/eff3cf1bc55245359bc41e74720c5845.png)

3. In the windows from Step 3 to Step 8, keep the default configurations and click "Next" in sequence.

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/784ad60b5e5a4b2c82e489bcf2c82d45.png)

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/653190f81e0b4b8a9d2c93874fa00968.png)

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/e91e6ffa1d82490f883be4757dc47db5.png)

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/1bbed105e3c24f9e854543152d0af2d9.png)

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/cf11fa94f7634afd9fcc9f4160fa5597.png)

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/76343112159d427ba5dc64e6b192a0e1.png)

4. In the "Specify Configuration Options" window, configure memory and character set in sequence as needed. This topic uses the default configuration as an example. After configurations are completed, click "Next".

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/82d3325760eb48db918dc54f496a540d.png)

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/84b3f519da5846138e5921d58dd122c8.png)

5. In the "Specify database user credentials" window, select "Use the same administrative password for all accounts", set the password, and then click "Next".

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/7b7962a913f04defaf69e1d9d3399685.png)

6. In the "Select Database Creation option" window, keep the default configuration, and then click "Next".

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/8f3966fc20154a32af6ac9b25cee67e8.png)

7. In the "Summary" window, click "Finish" to start creating the database.

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/fd5a4685ad83491fb441c09de90ee0cf.png)

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/690323abf71a4457a261362e33090e9b.png)

8. In the "Finish" window, click "Close" to complete the creation process.

   ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/6646607874ac4adaa534e7cf709cacec.png)

### Step 4: Verify the database

Execute the `sqlplus / as sysdba` command as the oracle user to connect to the database.

> You can execute the `su - oracle command` to switch to the oracle user.

If the following output is returned, the database is created.

![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/fc1e0355d1d84566ae2a5913049ab957.png)
