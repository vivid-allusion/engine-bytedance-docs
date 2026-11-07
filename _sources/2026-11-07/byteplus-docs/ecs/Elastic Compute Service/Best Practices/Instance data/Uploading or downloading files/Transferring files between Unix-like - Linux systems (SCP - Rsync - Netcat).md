---
title: "Transferring files between Unix-like/Linux systems (SCP/Rsync/Netcat)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Transferring_files_between_UNIX_Linux"
---

This topic describes how to transfer data between ECS instances running Unix\-like and Linux operating systems.

The primary tools for transferring file data include SCP, Rsync, and Netcat. The following sections will provide a detailed overview of the features and usage of each tool.

<span id="SCP"></span>
## SCP

SCP (Secure Copy) is a method for securely transferring files between two local servers, two remote servers, or a local server and a remote server. SCP is an application based on SSH login. Any machine involved in data transfer must support the SSH service.

<span id=".5L2_55So56S65L6L"></span>
### Usage example


|Applicable scenarios |Command |Example |
|---|---|---|
|Transfer files between two Linux servers |`scp <Username of the source host>@<IP address of the source host>:<Path of the file to be transferred> <Username of the destination host>@<IP address of the destination host>:<Destination file path>` |To transfer files from the ECS instance whose IP address is 192.168.1.104 to the /home/ directory on the ECS instance whose IP address is 192.168.1.105, execute the following command:<br><br>`scp root@192.168.1.104:/test.txt root@192.168.1.105:/home/` |
|Upload files from the local machine to a remote server |`scp <Local file path> <Username of the remote server>@<EIP of the remote server>:<File path on the remote server>` |To upload the local file /home/test.txt to the corresponding directory on the ECS instance whose EIP is 10.x.x.x, execute the following command:<br><br>`scp /home/test.txt root@10.x.x.x:/home/` |
|Download files from a remote server to the local host |`scp <Username of the remote server>@<EIP of the remote server>:<File path on the remote server> <Local file storage path>` |To download the /home/test.txt file from the ECS instance whose EIP is 10.x.x.x to the local /home/ directory, execute the following command:<br><br>`scp root@10.x.x.x:/home/test.txt /home/` |


You can execute the `man scp` command to learn more about the scp command syntax.

<span id="Rsync"></span>
## Rsync

Rsync is a data mirroring and backup tool for Linux and Unix\-like systems. It supports remote synchronization, local copying, and synchronization with other SSH or Rsync hosts, and provides high transfer efficiency.

The Rsync algorithm does not transfer entire files each time. Instead, it only transfers the differing parts between two files, which results in fast transfer speed.

<span id=".5Y-C5pWw6K-05piO"></span>
### Parameter description

The following table describes common Rsync parameters:


|The parameters​. |Description |
|---|---|
|\-v |Show details. |
|\-q |Ignore non\-error\-related output. |
|\-a |The archive mode, which specifies that files are transferred recursively and all file attributes are preserved, equivalent to \-rlptgoD (excluding \-H, \-A, and \-X). |
|\-r |Process subdirectories recursively. |
|\-l |Do not process symbolic links (retain symbolic links). |
|\-p |Retain permission. |
|\-t |Retain the modification time. |
|\-g |Retain the group information |
|\-o |Retain the file owner information. |
|\-D |Retain the device file information. |
|\-H |Retain hard links. |
|\-S |Apply special handling to sparse files to conserve space. |
|\-z |Compress data during transfer. |


<span id=".5a6J6KOF6K-05piO"></span>
### Installation description

This section uses the CentOS 7.9 operating system as an example to describe how to install and configure Rsync.

<span id=".5q2l6aqk5LiA77ya5a6J6KOFUnN5bmM="></span>
#### Step 1: Install Rsync


1. Execute the `rsync --version` command to check whether Rsync is installed.

   If the version information is returned, Rsync is installed.

2. If Rsync is not installed, install it by executing the appropriate command for your operating system.

   * CentOS/Fedora: `yum install rsync`

   * Debian/Ubuntu/veLinux: `sudo apt-get install rsync`

   * OpenSUSE: `zypper in rsync`


<span id=".5q2l6aqk5LqM77yaUnN5bmPmnI3liqHphY3nva7vvIjlj6_pgInvvIk="></span>
#### Step 2: Configure the Rsync service (optional)

To use the Rsync service to transfer files between two servers, you need to pre\-configure the Rsync service on the server and the client.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use SSH to transfer files, you do not need to pre\-configure the Rsync service and you can skip this step.</div>


<span id=".U2VydmVy56uv6YWN572u"></span>
##### Server configuration


1. Log in to the server.

2. Modify the /etc/rsyncd.conf file.

   1. Execute the `vim /etc/rsyncd.conf` command to open the file, press `i` to enter edit mode, and then add the following content to the end of the file:

      ```Plain Text
      uid = root
      gid = root
      use chroot = no
      max connections = 4
      exclude = lost+found/
      transfer logging = yes
      timeout = 900
      ignore nonreadable = yes
      dont compress = *.gz *.tgz *.zip *.z *.Z *.rpm *.deb .bz2
      [test]               #Custom module name
      path=/home/test/     #Specify the path for storing files
      comment=test
      ignore errors
      read only=no         #Set to no: clients can upload files; yes means read-only
      write only=no        #no means downloadable on the client; yes means not downloadable on the client
      list=no              #Use the module list when a client requests
      auth user=root       #Specify the username to use during transmission
      ```
      

   2. Press `Esc` to exit the edit mode, input `:wq` and press Enter.

3. Create the /etc/rsyncd.passwd file.

   1. Execute the `vim /etc/rsyncd.passwd` command to create the file.

   2. Press `i` to enter edit mode and add the username and login password to be used during transfer: `<auth user>:<password>`.

   3. Press `Esc` to exit the edit mode, input `:wq` and press Enter.

4. Execute the `chmod 600 /etc/rsyncd.passwd` command to add read/write permissions.

5. Execute the `systemctl start rsyncd` command to enable the service.


<span id=".Q2xpZW5056uv6YWN572u"></span>
##### Client configuration


1. Log in to the client.

2. Create the /etc/rsyncd.passwd file.

   1. Execute the `vim /etc/rsyncd.passwd` command to create the file.

   2. Press `i` to enter edit mode and add the password corresponding to the server\-side auth user: `<password>`.

   3. Press `Esc` to exit the edit mode, input `:wq` and press Enter.

3. Execute the `chmod 600 /etc/rsyncd.passwd` command to add read/write permissions.


<span id=".5L2_55So56S65L6L"></span>
### Usage example


|Applicable scenarios |Command |Example |
|---|---|---|
|Copy local files |`rsync -avSH <Source file path> <Destination path>` |To copy the test.txt file from the /home directory to the /tmp directory, execute the following command:<br><br>`rsync -avSH /home/test.txt /tmp/` |
|Copy the contents of the local machine to the remote machine (by using Shell programs such as SSH) |`rsync -av <Local file path> <IP address of the remote machine>:<File storage path on the remote machine>` |To copy the test.txt file from the /home directory on the local machine to the /tmp directory on the remote machine whose IP address is 192.168.2.65, execute the following command:<br><br>`rsync -av /home/test.txt 192.168.2.65:/tmp/` |
|Copy the contents of the remote machine to the local machine (by using Shell programs such as SSH) |`rsync -av <IP address of the remote machine>:<File path on the remote machine> <File storage path on the local machine>` |For example, to copy the test.txt file from the /tmp directory on the remote machine whose IP address is 192.168.2.65 to the /home directory on the local machine, execute the following command:<br><br>`rsync -av 192.168.2.65:/tmp/test.txt /home/` |
|Copy files from the local machine to the remote Rsync server (Rsync transfer) |`rsync -av <Local file path> <auth user>@<IP address of the remote server>::<Module name>` |To upload the local test.txt file to the test module on the remote machine whose IP address is 192.168.2.65, execute the following command:<br><br>`rsync -av /root/test.txt root@192.168.2.65::test` |
|Copy files from the remote Rsync server to the local machine (Rsync transfer) |`rsync -av <auth user>@<IP address of the remote server>::<Module name> <Local file storage path>` |To copy files from the test module of the remote machine whose IP address is 192.168.2.65 to the /home directory of the local machine, execute the following command:<br><br>`rsync -av root@192.168.2.65::test /home/` |
|Display the file list of the remote machine (Rsync transfer) |`rsync -v rsync://<IP address of the remote server>/<Module name>` |To display the file list of the remote machine whose IP address is 192.168.2.65, execute the following command:<br><br>`rsync -v rsync://192.168.2.65/test` |


<span id="Netcat"></span>
## Netcat

Netcat (NC) is known as the "Swiss Army knife" of network tools. It is compact yet packs powerful functionality. Netcat establishes a TCP connection to conveniently transfer files between two hosts.

<span id=".5Y-C5pWw6K-05piO"></span>
### Parameter description

The following table describes common Netcat parameters:


|The parameters​. |Description |
|---|---|
|\-g<gateway\> |Specify the remote communication gateways of the router. You can specify up to eight remote communication gateways. |
|\-G<Number of pointers\> |Specify the number of source\-routing pointers. The value must be a multiple of 4. |
|\-h |Online help. |
|\-i<Latency in seconds\> |Specify the time interval for transferring information and scanning communication ports. |
|\-l |Use listen mode to control incoming data. This parameter must be used together with the \-p option. |
|\-n |Use the IP address instead of the domain name server. |
|\-p<Communication port\> |Specify the communication port used by the local host. |
|\-r |Specify the communication ports for the local and remote hosts. |
|\-s<Source address\> |Specify the IP address for outgoing data packets from the local host. |
|\-u |Use the UDP transport protocol. |
|\-v |Display the command execution process. |
|\-w<timeout duration in seconds\> |Specify the connection timeout period. |
|\-z |Use 0 input/output mode only for scanning communication ports. |


<span id=".5a6J6KOF6K-05piO"></span>
### Installation description


1. Execute the `nc --version` command to check whether Netcat is installed.

   If the version information is returned, Netcat is installed.

2. If Netcat is not installed, execute the following command to install it.

   ```Plain Text
   wget https://sourceforge.NET/projects/netcat/files/netcat/0.7.1/netcat-0.7.1.tar.gz
   tar zxvf netcat-0.7.1.tar.gz
   cd netcat-0.7.1
   ./configure
   make
   make install
   ```
   


<span id=".5L2_55So56S65L6L"></span>
### Usage example


|Applicable scenarios |Command |Example |
|---|---|---|
|Scan ports |`nc -v -w 2 <IP address of the target machine> -z <Port range>` |To scan ports 20 to 30 on the remote server whose IP address is 192.168.2.253, execute the following command:<br><br>`nc -v -w 2 192.168.2.253 -z 20-30` |
|Transfer files |* Enable listening on the receiver: `nc -l -p <listening port> > <output file>`<br><br>* Send a file from the sender: `nc <IP address of the receiver> < <file to be transferred>` |To copy the test.txt file from the machine whose IP address is 192.168.2.65 to the machine whose IP address is 192.168.2.253, execute the following command:<br><br><br>* receiver (192.168.2.253): `nc -l -p 1234 > test.txt`<br><br>* Sender (192.168.2.65): `nc 192.168.2.253 1234 < test.txt` |
