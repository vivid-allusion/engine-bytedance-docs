---
title: "Creating custom images by using Tailor"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-with-Tailor"
---

Tailor is a custom image building tool developed by the platform for the Linux and macOS operating systems. You can use Tailor to create a custom image based on a specific image.

This topic describes how to use Tailor to create a custom image.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An [ECS instance is purchased](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) and the [snapshot](https://docs.byteplus.com/en/docs/ecs/Overview-of-snapshots) service is enabled.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* You cannot use Tailor to create Windows custom images.

* You can create a custom image only for your system volume. The time required to create a custom image varies based on the actual size of the system volume.

* When you create a custom image, pay\-as\-you\-go cloud resources, such as temporary ECS instances and EIPs are automatically created. After the custom image is created, the cloud resources are automatically deleted. You are charged for the cloud resources that are automatically created when you create a custom image. For more information, see [Pay-as-you-go billing method](https://docs.byteplus.com/en/docs/ecs/Pay-as-you-go).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5a6J6KOFVGFpbG9y"></span>
### Step 1: Install Tailor


1. Log in to the instance where you want to run Tailor. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Run the following command to install Tailor in the /usr/local/bin directory.

   > /usr/local/bin/ is a directory for environment variables. If you install Tailor in this directory, you can use Tailor from any directory without the need to specify the installation directory of Tailor.   
   

   * Installation on Linux:

      ```Plain Text
      wget https://tailor.tos-cn-beijing.volces.com/Tailor.tar.gz && tar zxf Tailor.tar.gz -C /usr/local/bin/
      ```
      

   * Installation on macOS:

      ```Plain Text
      wget https://tailor.tos-cn-beijing.volces.com/Tailor_mac.tar.gz && tar zxf Tailor_mac.tar.gz -C /usr/local/bin/
      ```
      

3. You can run the following command to view the Tailor usage instructions and verify whether Tailor is installed.

   ```Plain Text
   Tailor --help
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fbc990c1c49a7334ee20fd8d1ce1f9d9.png) </span>


<span id=".5q2l6aqk5LqM77ya5Yib5bu65a6a5Yi26ZWc5YOP6ISa5pys77yI5Y-v6YCJ77yJ"></span>
### Step 2: Create a custom image script (optional)

You can write a Shell script that includes the operations you want to specify for a custom image, such as software and driver installation and CVE fixing. You can specify that the script is automatically executed when you use Tailor to create the custom image.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">You can include the instance restart operation in each script file that is specified by the script parameter. Tailor continues to execute the script tasks after the instance is restarted.</div>


* <div data-tips="true" data-tips-type="warning">Tailor supports the following script path formats. You can specify script paths in the following formats based on your business requirements.</div>


   * <div data-tips="true" data-tips-type="warning"><strong>Local directory</strong>. Example: /tmp/update/.</div>


   * <div data-tips="true" data-tips-type="warning"><strong>Local script</strong>. Example: /tmp/a.sh.</div>


   * <div data-tips="true" data-tips-type="warning"><strong>Network script</strong>. Example: http://install/a.sh.</div>


   * <div data-tips="true" data-tips-type="warning"><strong>Script in compression format</strong>. Currently, the <code>.tar</code>, <code>.gzip</code>, and <code>.zip</code> formats are supported. Example: centos_shell.zip.</div>


* <div data-tips="true" data-tips-type="warning">For a collection of <strong>scripts in compression format</strong> or <strong>scripts in local directory format</strong>, the following requirements must be met:</div>


   * <div data-tips="true" data-tips-type="warning">You need to specify buildx.sh script files, such as build1.sh and build3.sh as the entry points for executing the custom image script. Tailor automatically executes the buildx.sh scripts based on the value of <code>x</code>  in ascending order. Each time a buildx.sh script is executed, Tailor restarts the instance.</div>


   * <div data-tips="true" data-tips-type="warning">In the script collection, buildx.sh files cannot be stored in level\-2 directories, such as temp/temp_1/build3.sh. There are no restrictions on the location of other scripts and files.</div>



<span id=".5qCH5YeG55qE6ISa5pys6ZuG5ZCI56S65L6L"></span>
#### Example of a standard script collection

```Plain Text
centos_shell.zip          
  ├── 00_extra_pkg.sh
  ├── build1.sh
  ├── build5.sh
  ├── centos_zip.zip
  ├── cleanup.sh
  └── cve.sh
```


Example of the contents of the buildx.sh script:


* build1.sh

   ```Plain Text
   #!/bin/bash
   
   set -x
   
   BASE_PATH=$(cd "$(dirname "$0")";pwd)
   
   source ${BASE_PATH}/config
   
   scripts=(
       "00_extra_pkg.sh"
       "cve.sh"
   )
   for file in ${scripts[@]}
   do
       source ${BASE_PATH}/${file}
   done
   ```
   

* build5.sh

   ```Plain Text
   #!/bin/bash
   
   set -x
   
   BASE_PATH=$(cd "$(dirname "$0")";pwd)
   
   source ${BASE_PATH}/config
   
   scripts=(
       "cleanup.sh"
   )
   for file in ${scripts[@]}
   do
       source ${BASE_PATH}/${file}
   done
   ```
   


<span id=".5q2l6aqk5LiJ77ya5Yib5bu65Y-C5pWw6YWN572u5paH5Lu277yI5Y-v6YCJ77yJ"></span>
### Step 3: Create a parameter configuration file (optional)

When you use Tailor to create a custom image, you can specify the name and size of the custom image and the type of the temporary instance used during the creation process by using parameters in a YAML configuration file.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you do not create a parameter configuration file, you need to pass in parameters and their values when you execute the commands.</div>


* <div data-tips="true" data-tips-type="tip">The temporary instance is automatically created by the platform and automatically deleted after the custom image is created.</div>


1. Run the following command to view the parameters supported by Tailor.

   ```Plain Text
   Tailor build --help
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9568c49710bb418a21ac7160e9d6eba5.png) </span>

   **Parameters**:

   
   |Parameter |Required |Description |Sample value |
   |---|---|---|---|
   |base |Yes |The ID of the base image. Tailor creates a custom image based on the base image.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can use any public image, custom image, or shared image in your account as a base image.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can obtain the ID of the base image in the <a href="https://console.byteplus.com/image/images">Image console</a>.</div><br> |image\-yc6gg6s0nvl8j17XXXXX |
   |region |No |The region of the temporary instance used when you create the custom image. The default region is China (Beijing) (**cn\-beijing)** . For more information about regions, see [Regions and availability zones](https://docs.byteplus.com/en/docs/ecs/Regions-and-Availability-Zones).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The custom image that you create is also located in the region.</div><br> |cn\-beijing |
   |zone |No |The availability zone of the temporary instance used when you create the custom image. The default availability zone is **a** (availability zone A). For more information about regions and availability zones, see [Regions and availability zones](https://docs.byteplus.com/en/docs/ecs/Regions-and-Availability-Zones).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You do not need to include the region prefix when you specify the availability zone. For example, the zone ID for the Beijing availability zone A is <code>cn-beijing-a</code>. You only need to pass in <code>a</code>.</div><br> |a |
   |spec |No |The type of the temporary instance used when you create the custom image. The default instance type is **ecs.g2i.xlarge** (General\-purpose g2i). For more instance types, see [Instance type overview](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types). |ecs.g2a.xlarge |
   |disksize |No |The size of the image in GB. The default size is **20 GB**. |20 |
   |script |No |The script for creating the custom image. You can specify multiple scripts for creating the custom image. You can view the script description in [Creating custom scripts](https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-with-Tailor#.5q2l6aqk5LqM77ya5Yib5bu65a6a5Yi26ZWc5YOP6ISa5pys77yI5Y-v6YCJ77yJ). |\- |
   |name |No |The name of the custom image that you want to create. The default name of the custom image is in the format of **image type\-version\-architecture\-boot mode\-timestamp**. Example: centos\-7.8\-amd64\-legacy\-20220511_031740. |CentOS7.9 |
   

2. Create a YAML file that includes the parameters.

   1. Run the following command to create a configuration file.

      ```Plain Text
      vim config.yml
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>config</code> with the name of your configuration file.      </div>
      

   2. Press the `i` key and enter the parameter information that you want to specify in the following structure.

      ```Plain Text
      base: image-yclxxxxxx
      region: cn-beijing        
      zone: a
      script:
          - /temp/centos_shell.zip
          - http://install/update.sh
          - /temp/download.sh
      spec: ecs.g2a.xlarge
      disksize: 20
      name: CentOS7.9
      ```
      

   3. Press the `Esc` key to exit the edit mode, enter `:wq`, and then press the Enter key to save and exit the file.


<span id=".5q2l6aqk5Zub77ya5Yib5bu66Ieq5a6a5LmJ6ZWc5YOP"></span>
### Step 4: Create a custom image


1. When Tailor executes the custom image creation task, the task information and cache files are stored in the directory where you run the command. For more information, see [Creation result](https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-with-Tailor#.5q2l6aqk5LqU77ya5p-l55yL5Yib5bu657uT5p6c).

   Run the following command to navigate to the directory where you want to store the relevant content.

   ```Plain Text
   cd /etc/Tailors/
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>/etc/Tailors/</code> with your directory path.   </div>
   

2. Run the following command to import the AccessKey ID and AccessKey secret in the AccessKey pair. For more information, see [About access keys](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-keys).

   ```Plain Text
   export VOLC_AK=xxx
   export VOLC_SK=xxx
   ```
   

3. Run the following command to create a custom image.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you create a custom image, Tailor automatically displays <code>FATAL</code> and <code>ERROR</code> severity logs in the console. For information about log description and how to adjust displayed log information, see <a href="https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-with-Tailor#.5pel5b-X6K-05piO">Log description</a>.   </div>
   

   * Specify parameter values by using the parameter configuration file.

      ```Plain Text
      Tailor build config.yml
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">For information about how to create a parameter configuration file, see <a href="https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-with-Tailor#.5q2l6aqk5LiJ77ya5Yib5bu65Y-C5pWw6YWN572u5paH5Lu277yI5Y-v6YCJ77yJ">Creating parameter configuration files</a>.      </div>
      

   * Specify parameter values in the command.

      ```Plain Text
      Tailor build -base=image-ybqi99s7aayq8rx7xxxxx -script=/tmp/update.sh -script=/tmp/centos_shell.tgz
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">For information about the parameters that you can configure, see <a href="https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-with-Tailor#.5q2l6aqk5LiJ77ya5Yib5bu65Y-C5pWw6YWN572u5paH5Lu277yI5Y-v6YCJ77yJ">Creating parameter configuration files</a>.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">You can use the script parameter multiple times to specify information about multiple scripts.      </div>
      

4. After the custom image creation task is executed, Tailor displays the ID and name of the generated custom image. The custom image is automatically added to the region where the temporary instance resides.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d48b662246c7c879c783fd4c8233f9e1.jpeg) </span>


<span id=".5q2l6aqk5LqU77ya5p-l55yL5Yib5bu657uT5p6c"></span>
### Step 5: View the creation result

<span id=".5p-l55yL6Ieq5a6a5LmJ6ZWc5YOP"></span>
#### View the custom image


1. Log in to the [Image console](https://console.byteplus.com/image/region:image+ap-southeast-1/images?tab=2).

2. In the top menu bar, select the region and project where the target custom image is located.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The region of the image is the same as the region of the temporary instance. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-with-Tailor#.5q2l6aqk5LiJ77ya5Yib5bu65Y-C5pWw6YWN572u5paH5Lu277yI5Y-v6YCJ77yJ">Creating parameter configuration files</a>.   </div>
   

3. Select the "Custom Image" tab.

4. If the status of the target image is **Available** in the "State" column, the custom image is created.

5. You can also click the image name to go to the image details page, select the "Associative snapshot" tab, and view the IDs of the snapshots associated with the volumes in the image, the volume types, and the capacity of the volumes. For more information about snapshots, see [Snapshot overview](https://docs.byteplus.com/en/docs/ecs/Overview-of-snapshots).


<span id=".5p-l55yL5Lu75Yqh"></span>
#### View the task

When you run the `Tailor build` command, Tailor creates a workspace directory in the current directory to store intermediate artifacts generated during the custom image creation task. This makes it easier for you to troubleshoot any issues that occur during the creation process.

For each custom image creation task, a task directory is created in the workspace directory in the "ImageName\-Timestamp" format. The task directory stores the cache files and HTTP files related to the task.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If a custom image creation task is executed as expected, no task information is stored in the task directory.</div>


Sample structure of the workspace directory

```Plain Text
workspace
 └── centos-7.8-amd64-legacy-20220511_031740    
  ├── cache
  ├── http
  ├── log
  └── packer.json  
```



|File name |Description |
|---|---|
|cache |The directory for cache files. |
|http |The directory for intermediate files pulled over the network. Example: the directory for custom image scripts. |
|log |The directory for log files. |
|packer.json |The template file of the Packer builder. |


<span id=".5pel5b-X6K-05piO"></span>
## Log description

When you use Tailor to create a custom image, Tailor displays the task log information in the console. When you execute the image creation command, you can specify the log level based on your business requirements. This way, you can specify the level of detail for displayed logs.

<span id=".5pel5b-X57qn5Yir"></span>
### Log level

The following items describe the log levels and the content displayed at specific log levels.


* **0**: Display `FATAL` severity logs.

* **1**: Display `ERROR` and lower severity logs. This is the default log level.

* **2**: Display `WARN` and lower severity logs.

* **3**: Display `DEBUG` and lower severity logs.

* **4**: Display `INFO` and lower severity logs.


<span id=".6YWN572u6K-05piO"></span>
### Configuration description

When you execute the `Tailor build` command to create a custom image, you can pass in the `TAILOR_LOG_LEVEL` parameter to specify the log level for the task. Example:

```Plain Text
TAILOR_LOG_LEVEL=4 Tailor build -base=image-ybqi99sxxxxxx -spec=ecs.g2a.large
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_21f6a23778bc4f4c3a282a177b092466.png) </span>
