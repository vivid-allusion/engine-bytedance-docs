---
title: "How do I resolve the hanging issue of the df -H command in a Linux instance?"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/resolve-command-becomes-stuck"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

When I execute the `df -H` command in a Linux instance to view file system disk usage, the command remains in progress and does not return any output.

<span id=".6Zeu6aKY5Y6f5Zug"></span>
## Causes

The command may hang during execution due to the failure of the NFS shared disk mounted to the instance.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solutions


1. Execute the following command to monitor the execution status of the `df -H` command.

   ```Plain Text
   strace df -H
   ```
   

   In this example, the command hangs at /data/nfs.

   ```Plain Text
   stat("/", {st_mode=S_IFDIR|0755, st_size=4096, ...}) = 0
   stat("/sys/kernel/security", {st_mode=S_IFDIR|0755, st_size=0, ...}) = 0
   stat("/dev/shm", {st_mode=S_IFDIR|S_ISVTX|0777, st_size=40, ...}) = 0
   stat("/data/nfs",
   ```
   

2. Execute the following command to view the mount information of the /data/nfs directory.

   ```Plain Text
   mount -l | grep /data/nfs
   ```
   

   In this example, /data/nfs is an NFS directory and has expired.

   ```Plain Text
   192.168.xx.xx:/home/data/nfs on /data/nfs type nfs4 (rw,relatime,vers=4.0,
   rsize=1048576,wsize=1048576,namlen=255,hard,proto=tcp,port=0,timeo=600,retrans=2,sec=sys,
   clientaddr=192.168.xx.xx,local_lock=none,addr=192.168.xx.xx)
   ```
   

3. Execute the following command to check whether any processes are using the directory.

   ```Plain Text
   fuser -cu /data/nfs
   ```
   

   In this example, the chrony process is using this directory.

   ```Plain Text
   /data/nfs:  579(chrony) 
   ```
   

4.  **(Optional)**  If there are processes using a directory that has become unresponsive, you can execute the following command to stop all processes running in that directory.

   > Before you stop the process, make sure that data will not be affected.   
   

   ```Plain Text
   fuser -ck /data/nfs
   ```
   

5. Execute the following command to unmount the invalid directory.

   ```Plain Text
   umount -v /data/nfs
   ```
   

6. Execute the `df -H` command again and check whether the command can be executed as expected.
