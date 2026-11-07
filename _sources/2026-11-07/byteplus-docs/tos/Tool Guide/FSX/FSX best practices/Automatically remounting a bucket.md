---
title: "Automatically remounting a bucket"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Set-up-automatic-bucket-mounting"
---

After a cloud server is shut down or restarted, the mount point becomes unmounted. In this case, you will need to use FSX to remount the bucket. You can create an auto\-start script that will cause FSX to start and remount the bucket automatically when the cloud server starts up. This topic describes the prerequisites and steps for enabling automatic remounting.

<span id="c55f4f56"></span>
## Prerequisites

You have installed FSX and mounted the bucket. For instructions, see [Configuration and mounting](https://docs.byteplus.com/docs/tos/FSX-configuration-and-mounting).

<span id="fc10e2b6"></span>
## Steps


1. Run this command to create the `script.sh` file in the `root` directory.

   ```JSON
   touch /root/script.sh
   ```
   

2. Open the `script.sh` file, insert the following content, and save it.

   ```JSON
   echo "start to mount fsx"
   # wait 5s for fusemonitor lazy loading to complete
   sleep 5 
   echo sleep done
   # Modify the mount parameters according to your actual needs
   mount -t fsx /tos/<bucket name>:/<bucket directory> <mount point> -o region="<your region>",endpoint="<your endpoint>",credential_filepath="<absolute path of credentials file>",no_writeback_cache,num_prefetch_threads=180   
   
   echo "end to mount $?"
   ```
   

   Modify the parameters `region`, `endpoint`, and `credential_filepath` in the `script.sh` file according to your environment. The descriptions are as follows:

   
   |**Flag** |**Description** |
   |---|---|
   |region |The region of the bucket that you want to mount. |
   |endpoint |The endpoint that follows the TOS protocol. Endpoints that follow the S3 protocol are not supported. Unless otherwise specified, HTTPS is used by default in the format `https://{host}:{port}`. |
   |credential_filepath |The absolute path of the credentials file used to load the required access credentials. You need to create the credentials file yourself. The file must have a `json` extension and contain the following content:<br><br>```Bash```<br>```{```<br>```    "VOLC_ACCESSKEY": "<ak_string>",```<br>```    "VOLC_SECRETKEY": "<sk_string>",```<br>```    "VOLC_SECURITY_TOKEN": "<sts_string>"```<br>```}```<br> |
   

3. Run this command to modify the access permissions of the `/root/script.sh` file. This will give the owner read, write, and execute permissions, and give others read and execute permissions.

   ```JSON
   chmod 755 /root/script.sh
   ```
   

4. Run this command to create the `fuse-fsx.service` file in the `/etc/systemd/system/` directory.

   ```JSON
   touch /etc/systemd/system/fuse-fsx.service
   ```
   

5. Open the `fuse-fsx.service` file, write the following content, and save it.

   ```JSON
   [Unit]
   Description=Mount FUSE filesystem
   # Must depend on fusemonitor.service
   After=multi-user.target fusemonitor.service 
   Wants=multi-user.target
   [Service]
   Type=oneshot
   ExecStart=/bin/bash /root/script.sh
   RemainAfterExit=yes
   [Install]
   WantedBy=multi-user.target
   ```
   

6. Run this command to load the `fuse-fsx.service` file.

   ```JSON
   systemctl daemon-reload
   ```
   

7. Run this command to set the `fuse-fsx.service` service to start on boot.

   ```JSON
   systemctl enable fuse-fsx.service
   ```
   

   Once you have finished configuring, reboot the ECS instance. After rebooting, the system will automatically mount the bucket.
