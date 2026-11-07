---
title: "Quick start"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Quick-start"
---

This article introduces the initialization steps and common operations required before using the tosutil tool.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The tosutil tool must be downloaded and installed. For detailed steps, see [Download and Installation](https://docs.byteplus.com/docs/tos/Download-and-install).

* Obtain the Region and Endpoint information. For supported Region and Endpoint details, see [Regions and Access Domains](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* Obtain the access keys (Access Key ID and Secret Access Key). For steps to view AK and SK information, see [View AKSK Information](https://docs.byteplus.com/docs/byteplus-platform/docs-managing-an-accesskey).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

All commands in this guide use Linux or macOS as examples. For Windows command formats, see [Command Format](https://docs.byteplus.com/docs/tos/Command-format).

<span id=".5q2l6aqk5LiA77ya5Yid5aeL5YyW6YWN572u"></span>
## Step 1: initialize configuration


1. (Optional) On Linux or macOS systems, run the following command to grant execution permissions.

   Windows systems can skip this step and proceed directly to the initialization setup.

   ```Plain
   chmod +x tosutil
   ```
   

2. Use the `config` command for initialization configuration. Refer to the use cases to choose the appropriate initialization method:

   * Use permanent access keys

      ```Plain
      # -i specifies the access key for the account/sub-account
      # -k specifies the secret key for the account/sub-account
      # -e specifies the access endpoint
      # -re specifies the access region
      ./tosutil config -i <access key> -k <secret key> -e <endpoint> -re <region>
      ```
      

   * Use temporary access keys

      ```Plain
      # -i specifies temporary access key\n# -k specifies temporary secret key\n# -t specifies temporary security token\n# -e specifies access endpoint\n# -re specifies access region\n./tosutil config -i <access key> -k <secret key> -t <security token> -e <endpoint> -re <region>
      ```
      

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Ensure the configured Endpoint is a TOS protocol domain, not an S3 protocol domain. For supported Regions and Endpoint information of TOS, see <a href="https://docs.byteplus.com/docs/tos/docs-region-and-endpoint">Regions and Access Domains</a>.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">After running the access key configuration command, a configuration file named <a i=2\>.tosutilconfig</a\> will be automatically generated in the user directory of the operating system (macOS or Linux operating systems)<code>~</code>directory, and in Windows operating systems, in the <code>C:\\Users\\<username></code> directory. This file contains all tosutil configuration information. To ensure key security and prevent leakage, tosutil automatically encrypts your information.      </div>
      

   * Anonymous access

      tosutil supports anonymous access functionality. When you access a bucket anonymously, you can read public data and write data to buckets set for public write.

      When initializing configuration with the `config` command, you do not need to specify key information; just set the key parameters to `-i=`, `-k=`, and `-t=`.

      ```Plain
      # clear -i parameter\n# clear -k parameter\n# clear -t parameter\n# specify the endpoint with -e parameter\n# specify the region with -re parameter\n./tosutil config -i= -k= -t= -e <endpoint> -re <region>
      ```
      


<span id=".5q2l6aqk5LqM77ya5qOA5p-l54mI5pys5ZKM6L-e6YCa5oCn"></span>
## Step 2: check version and connectivity

After initialization, you can check the tosutil tool's version and connectivity as follows.


* Use the `version` command to check the tool version:

   ```Plain
   # check tool version\n./tosutil version
   ```
   

   The result is as follows:

   ```Plain
   tosutil version: v1.1.0
   operating system: darwin, arch: amd64
   ```
   

* Use the `ls` command to check connectivity:

   ```Plain
   # this command returns the bucket list of the current account\n./tosutil ls
   ```
   

   The result is as follows:

   ```Plain
   Start at 2022-10-27 09:29:45.79638 +0000 UTC
   Bucket                   CreationDate                  Location       
   tos://db-storage         2022-07-28T06:53:37Z          cn-beijing     
    
   tos://tosutil            2022-07-05T09:40:35Z          cn-beijing     
   
   Bucket number is: 2
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After running the <code>ls</code> command, you can determine the configuration result based on the command output:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the result includes <code>Bucket number is:</code>, it indicates the configuration is correct.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the result contains <code>Http status [403]</code>, it indicates the access key is incorrectly configured or lacks permission.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the result contains <code>A connection attempt failed</code>, it means TOS cannot be connected; please check if the network environment is normal.   </div>
   


<span id=".5q2l6aqk5LiJ77ya5b-r6YCf5L2_55So"></span>
## Step three: quick start

This article introduces common commands for creating buckets, uploading files, downloading files, and deleting files using the tosutil tool.


1. Run the following command to create a bucket named **bucketname**.

   ```Plain
   # create bucket\n./tosutil mb tos://bucketname
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The default region for creating buckets is the region set when initializing the tool. To create a bucket in another region, use the <code>-re</code> command. For details, see <a href="https://docs.byteplus.com/docs/tos/Command-format#.6YCa55So5Y-v6YCJ5Y-C5pWw">general parameters</a>.   </div>
   

2. Run the following command to upload the file **file.txt** to the bucket **bucketname**.

   ```Plain
   # upload a single object\n./tosutil cp /temp/file.txt tos://bucketname/file.txt
   ```
   

3. Run the following command to download the file **file.txt** from the bucket **bucketname** to your local machine.

   ```Plain
   # download a single object\n./tosutil cp tos://bucketname/file.txt /temp/file.txt
   ```
   

4. Run the following command to delete the file **file.txt** from the bucket **bucketname**.

   ```Plain
   # delete a single object\n./tosutil rm tos://bucketname/file.txt
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When deleting an object using the <code>rm</code> command, the tool prompts for <code>y/n</code> confirmation. To force deletion, add the <code>-f</code> parameter. For more details, see <a href="https://docs.byteplus.com/docs/tos/Delete-a-bucket-object-or-shard-upload-task-rm">rm command</a>.   </div>
   

5. Run the following command to upload the **test_folder** folder to the **bucketname** bucket.

   ```Plain
   # upload folder\n./tosutil cp /temp/test_folder tos://bucketname -r
   ```
   

6. Run the following command to download the **test_folder** folder from the **bucketname** bucket to your local device.

   ```Plain
   # download folder\n./tosutil cp tos://bucketname/test_folder /temp -r
   ```
   

7. Run the following command to delete the **test_folder** folder from the **bucketname** bucket.

   ```Plain
   # Delete folder
   ./tosutil rm tos://bucketname/test_folder -r
   ```
   


<span id=".5biu5Yqp5paH5qGj"></span>
## Help documentation


* tosutil includes help documentation. You can view it using the `help` command.

   ```Plain
   # View help documentation
   ./tosutil help
   ```
   

* The help documentation supports both Chinese and English. You can refer to the following commands to change the language of the help documentation.

   ```Plain
   # Change the language of the help documentation
   vim ~/.tosutilconfig
   # Modify the helpLanguage enum to support the following values:
   # Chinese
   # English
   ```
