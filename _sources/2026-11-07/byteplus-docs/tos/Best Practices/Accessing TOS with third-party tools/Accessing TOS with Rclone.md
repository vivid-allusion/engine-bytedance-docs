---
title: "Accessing TOS with Rclone"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-accessing-tos-with-rclone"
---

Rclone is a powerful open source command\-line tool that supports interconnection with diverse cloud storage systems (including S3\-compatible object storage systems) for data upload, download, synchronization, management, and more. This topic describes how to use Rclone to access TOS, which is S3\-compatible.

<span id="03b899e5"></span>
## Background

For more information on Rclone, visit the [official website](https://rclone.org/).

<span id="5fb3e2f9"></span>
## Prerequisites


* You have created a BytePlus account and activated TOS.

* You have obtained the access key ID and secret access key of the current account.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can log in to the <a href="https://console.byteplus.com/home">BytePlus console</a>, click the profile photo in the upper\-right corner, and choose <strong>Key management</strong> to view the access key ID and secret access key.   </div>
   

* For more information on S3 endpoints for TOS, see [Regions and Endpoints](https://docs.byteplus.com/en/tos/docs/region-and-endpoint?version=1.0.0).


<span id="408f43af"></span>
## Step 1: Installation

This section describes how to install Rclone in different operating systems before accessing TOS.


* **macOS/Linux/BSD**

   In macOS, Linux, or BSD operating systems, run the following command to install Rclone:

   ```Plain
   curl https://rclone.org/install.sh | sudo bash
   ```
   

* **BytePlus ECS for Linux**

   In BytePlus ECS for Linux, run the following commands to install Rclone:

   ```Plain
   wget https://tos-tools.tos-cn-beijing.volces.com/third-party%2Frclone-current-linux-amd64.zip
   unzip rclone-current-linux-amd64.zip
   cd rclone-v1.58.0-linux-amd64
   
   sudo cp rclone /usr/bin/
   sudo chown root:root /usr/bin/rclone
   sudo chmod 755 /usr/bin/rclone
   
   rclone version
   ```
   

* **Other installation methods**

   For other installation methods, see [Install](https://rclone.org/install/).


<span id="5f02292b"></span>
## Step 2: Configuring the connection

Here, the North China 2 (Beijing) region of TOS is used as an example. Make sure that all the prerequisites are met.

```Plain
AccessKey ID：AKLTYTBjY*
AccessKey Secret：TVdaaFkyRTNNa*
Region：ap-southeast-1
Endpoint：tos-s3-ap-southeast-1.bytepluses.com 
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">S3 endpoints must be used. For more information, see <a href="https://docs.byteplus.com/en/tos/docs/region-and-endpoint?version=1.0.0">Regions and Endpoints</a>.</div>


* <div data-tips="true" data-tips-type="warning">Different endpoints are used over private and public networks. Using the latter incurs traffic fees over the public network.</div>


1. Run the following command to configure the TOS connection in Rclone.

   ```Plain
   rclone config
   ```
   

2. Select the options or type the information as follows.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Select the options based on the text description, as the numbers of options may vary by Rclone version.   </div>
   

   ```Plain
   n) New remote  
   
   name> volces-tos  
   
   5 / Amazon S3 Compliant Storage Providers including AWS, Alibaba, Ceph, Digital Ocean, Dreamhost, IBM COS, Minio, SeaweedFS, and Tencent COS
      \ "s3"   
   
   14 / Any other S3 compatible provider
      \ "Other"  
   
   1 / Enter AWS credentials in the next step
      \ "false"  
   
   access_key_id> AKLTYTBjY*******  // Press AK
   
   secret_access_key> TVdaaFkyRTNNa*****  //Press SK
   
   region> ap-southeast-1  //Press  Region ID
   
   endpoint> https://tos-s3-ap-southeast-1.bytepluses.com //Press  Endpoint
   
   location_constraint>    //Press Enter
   
   acl>  //Press Enter
   
   n) No (default) 
   
   y) Yes this is OK (default)  //Press y
   
   q) Quit config  
   ```
   

3. Then, run the following command to view existing connections.

   ```Plain
   rclone config show
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">By default, Rclone uses the path style to access object storage systems, which needs to be changed to the virtual\-hosted style to access TOS.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">By default, Rclone uses HTTP2 to access object storage systems, which needs to be disabled to access TOS.   </div>
   

4. Below are the detailed instructions.

   1. Run the following command to get the path of the configuration file.

      ```Plain
      rclone config file
      ```
      

   2. Open the configuration file and append the following to the connection configuration.

      
      |**Parameter** |**Required** |**Description** |
      |---|---|---|
      |force_path_style = false |Yes |Disables the path style to access object storage. |
      |disable_http2 = true |Yes |Disables HTTP2 to access object storage. |
      |list_version = 2 |No |Use API version 2 to list objects,as it has more parameters than version 1, with the timeout issue in version 1 handled.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default" data-wrapper-indent="0">If you do not include this parameter in the configuration file, add <code>--s3-list-version 2</code> when using the list command. For more information, see <a href="https://docs.byteplus.com/en/docs/tos/docs-accessing-tos-with-rclone#03c3a33b">Viewing buckets or directories</a>.</div><br> |
      

      Below is the modified configuration file.

      ```Plain
      [volces-tos]
      type = s3
      provider = Other
      access_key_id = AKLTYTBjY*
      secret_access_key = TVdaaFkyRTNNa*
      region = cn-beijing
      endpoint = https://tos-s3-ap-southeast-1.bytepluses.com
      force_path_style = false
      disable_http2 = true
      list_version = 2
      ```
      


<span id="1aec4a0d"></span>
## Common operations

After you have installed the tool and configured the TOS connection, you can perform operationssuch as viewing directories, uploading files, and viewing the directory size. This section describes common commands for these operations. For more information, see [Rclone Commands](https://rclone.org/commands/).

<span id="03c3a33b"></span>
### Viewing buckets or directories

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">We recommend that you use API version 2 to list objects,as it has more parameters than version 1, with the timeout issue in version 1 handled. You can use API version 2 in the following ways:</div>



* <div data-tips="true" data-tips-type="tip">Set <code>list_version = 2</code> in the configuration file.</div>


* <div data-tips="true" data-tips-type="tip">Append <code>--s3-list-version 2</code> to your command.</div>


* Run the following command to list all buckets under the current account.

   ```Plain
   rclone lsd volces-tos: --s3-list-version 2 //volces-tos is the configured name for the remote connection.
   ```
   

* Run the following command to list first\-level folders in a bucket.

   ```Plain
   rclone lsd volces-tos:bucket-demo --s3-list-version 2 //bucket-demo is the name of the storage bucket.
   ```
   


<span id="b1184481"></span>
### Uploading local files

Run `rclone copy` to copy data from the source to the destination. The command structure is as follows.

```Plain
rclone copy source:sourcepath dest:destpath
```



* Run the following command to copy all files from local folder "testdir" to the root directory of bucket "bucket\-demo".

   ```Plain
   rclone copy testdir volces-tos:bucket-demo
   ```
   

* Run the following command to copy local folder "testdir" to bucket "bucket\-demo" and make it a first\-level directory.

   ```Plain
   rclone copy testdir volces-tos:bucket-demo/testdir
   ```
   

* Run the following command to call for shard upload if the original file is larger than 5 GiB (in TOS, you can upload a file of up to 5 GiB by calling a common API) or if you want to speed up the upload of large files.

   ```Plain
   rclone copy  testdir  volces-tos:bucket-demo/testdir -P  --s3-upload-cutoff 1G --s3-upload-concurrency 8 --s3-chunk-size 16M
   ```
   

   Below are the shard upload parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |\-\-s3\-upload\-cutoff |Any files larger than this value will be uploaded in shards. The default value is 200 MiB, and the maximum value is 5 GiB. |
   |\-\-s3\-upload\-concurrency |Specifies the number of shards uploaded concurrently. The default value is 4. If you are uploading a small number of large files, increasing this value can increase the bandwidth. The maximum value is 16. |
   |\-\-s3\-chunk\-size |Specifies the shard size. The default value is 5 MiB. The maximum value is 32 MiB. |
   

* Increasing the concurrency speeds up data transfers but consumes more host resources. We recommend that you run the following command to flexibly adjust the concurrency.

   ```Plain
   rclone copy  testdir  volces-tos:bucket-demo/testdir --transfers=32 --checkers=32   -P
   ```
   

   Below are the parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |\-\-transfers |Specifies the number of files to be transferred concurrently. The default value is 4, and the maximum value is 128. |
   |\-\-checkers |Specifies the number of files to check. The default value is 8, and the maximum value is 128. |
   

* If there are many files at the destination, run the following command to search for the target file without traversing the destination.

   ```Plain
   rclone copy  testdir  volces-tos:bucket-demo/testdir --no-traverse
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>--no-traverse</code>indicates not to traverse the destination.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can run the following command to save log files of data transfers. Supported log levels are DEBUG, INFO, NOTICE (default), and ERROR.   </div>
   

   ```Plain
   rclone copy  testdir  volces-tos:bucket-demo/testdir  --log-file /root/rclone.log  --log-level DEBUG
   ```
   

   Below are the parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |\-\-log\-file |Specifies the log path. |
   |\-\-log\-level |Specifies the log types. |
   


<span id="fcd60d04"></span>
### Synchronizing a local directory

Run `rclone sync` to synchronize incremental data (including new and modified files) to the destination.

```Plain
rclone sync source:path dest:path [flags]
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This command updates the destination to match the source, that is, some destination data may be deleted. Proceed with caution.</div>


Run the following command to update folder "testdir" in the bucket to match local folder "testdir".

```Plain
rclone sync testdir volces-tos:bucket-demo/testdir
```


<span id="7e6ea76e"></span>
### Viewing the directory size

Run `rclone size` to get the total number and size of files in a bucket or directory.

```Plain
rclone size remote:path [flags]
```



* Run the following command to get the total number and size of files in bucket "bucket\-demo".

   ```Plain
   rclone size volces-tos:bucket-demo
   ```
   

* Run the following command to get the total number and size of files under folder "testdir" in bucket "bucket\-demo".

   ```Plain
   rclone size volces-tos:bucket-demo/testdir
   ```
   


<span id="b4af8e27"></span>
### Comparing files

Run `rclone check` to compare data at the source and destination.

```Plain
rclone check source:path dest:path [flags]
```


Below are the optional parameters:


* `--size-only`: compares only file sizes.

* `--download`: downloads remote files and compares them.


<span id="12d60017"></span>
## FAQs


* What should I do if Rclone does not speed up object upload?

   Rclone may be used improperly. Check if the upload is faster by using `--no-check-dest` and `--no-traverse` to skip data check. For more information on Rclone parameters, see [Global Flags](https://rclone.org/flags/).

* What should I do if `Forbidden path to access server` is reported when uploading an object using Rclone?

   TOS does not support path style access. Use virtual\-hosted style instead. This issue is due to the fact that path style is the default option for third\-party SDKs. Path and virtual\-hosted styles mainly differ in the position of the bucket name in the HTTP URL, as shown below:

   ```Plain
   # Path access method
   https://tos-s3-cn-beijing.bytepluses.com.cn/{bucketname}
   
   # VirtualHost access method
   https://{bucketname}.tos-s3-cn-beijing.bytepluses.com.cn
   ```
