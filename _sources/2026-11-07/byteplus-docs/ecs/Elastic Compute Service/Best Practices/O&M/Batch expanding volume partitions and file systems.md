---
title: "Batch expanding volume partitions and file systems"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Batch-extend-of-Volumes-partitions-and-file-systems"
---

This topic mainly describes how to use the cloud assistant feature to batch expand volume partitions and file systems without logging in to or restarting an instance.

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenario

As your business grows and application data increases, the current volume capacity is insufficient to store large amounts of business data. To solve this, you can expand your volume to increase storage capacity without losing existing data. By using the cloud assistant feature, you can batch expand file systems and partitions quickly without manually operating inside instances.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes

The expansion script provided in this practice only supports expanding volume partitions of the `MBR` type and the `ext4` file systems. You can follow the [guide for viewing partition and file system details](https://docs.byteplus.com/en/docs/ecs/Extend-volume-linux#.5q2l6aqk5LqM77ya5p-l55yL5YiG5Yy65ZKM5paH5Lu257O757uf5oOF5Ya1) to confirm the partition type and file system information of volumes mounted on your instances.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have [purchased an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) with the [cloud assistant Agent installed](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client).

* You have partitioned the target volume as well as formatted and mounted file systems on partitions. For detailed operations, see [Partitioning and formatting volumes](https://docs.byteplus.com/en/docs/ecs/Initialize-volume-overview).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5omp5a655LqR55uY"></span>
### Step 1: Expand volume


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).  

2. In the top menu bar, select the project and region of the target instance.

3. In the left\-side navigation pane, select "Instances & Images \> Instances".

4. On the Instances page, click the name of the target instance.

5. Select the "Volumes" tab.

6. On the right side of the target volume, select "... \> Extend" in the "Actions" column.

7. On the Expand volume page, confirm the current configuration information. For the "New capacity" parameter, enter the volume capacity after expansion. In the example provided in this topic, the volume capacity is expanded to 60 GiB.

8. Click the "Extend volume" button to submit the expansion application.

9. After the volume is expanded in the console, follow the steps below for expanding partitions and file systems.


<span id=".5q2l6aqk5LqM77ya5Yib5bu65omp5a655ZG95Luk"></span>
### Step 2: Create an expansion command


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).  

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> Cloud Assistant". 

3. In the top menu bar, select the region where your business is located. 

4. Select the "Custom commands" tab to enter the custom command list page.

5. Click the "Create a custom command" button to enter the Create a custom command page.

6. Enter the following job information as instructed.

   > This practice only describes necessary parameters. Other parameters remain with default values. For parameter details, refer to [Creating custom commands](https://docs.byteplus.com/en/docs/ecs/Managing-Custom-Commands#.5Yib5bu66Ieq5a6a5LmJ5ZG95Luk).   
   

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Command name |Set the command name. |Expand volume partition and file system |
   |Command type |Select "Shell". |Shell |
   |Command contents |Enter information accordingly, and copy the complete content of the following script.<br><br>```bash```<br>```#!/bin/bash```<br>```set -x```<br>```#Check whether the growpart command is installed```<br>```CHECK_STATUS=$(yum versionlock status)```<br>```if [[ -z CHECK_STATUS ]];then```<br>```   INSTALL_GROW_PART=$(yum install -y cloud-utils-growpart)```<br>```   if [[ $? -ne 0 ]]; then```<br>```      echo 'install cloud-utils-growpart failed'```<br>```      exit 0```<br>```   fi```<br>```fi```<br>``````<br>```#Specify the partition to be expanded```<br>```LC_ALL=en_US.UTF-8 growpart {{volume}} {{partitionNumber}}```<br>```if [[ $? -ne 0 ]]; then```<br>```   echo 'growpart failed'```<br>```   exit 0```<br>```fi```<br>``````<br>```#Synchronize the file system to the kernel based on the file system type```<br>```resize2fs {{volume}}{{partitionNumber}}```<br>```if [[ $? -ne 0 ]]; then```<br>```   echo 'resize2fs failed'```<br>```   exit 0```<br>```fi```<br>``````<br>```#View the result```<br>```df -Th```<br> |\- |
   |Use argument |Check "Enable" to enable "Use argument". |\- |
   

7. Click the "Confirm" button to save the custom command.


<span id=".5q2l6aqk5LiJ77ya5omp5a655YiG5Yy65LiO5paH5Lu257O757uf"></span>
### Step 3: Expand partition and file system


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).  

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> Cloud Assistant". 

3. In the top menu bar, select the region where your business is located. 

4. Select the "Job management" tab.

5. Click the "Create a job" button and then enter job information based on the following instructions.

   > This practice only describes necessary parameters. Other parameters remain with default values. For parameter details, refer to [Creating jobs](https://docs.byteplus.com/en/docs/ecs/Creating-a-job).   
   

   
   |Argument |Description |Sample value |
   |---|---|---|
   |Job name |Set the job name. |Expand volume partition and file system |
   |Command type |Select **Custom commands**. |\- |
   |Command |Select the expansion command created in step 2. |Expand volume partition and file system |
   |Parameter |Enter the information of the volume partition and file system to be expanded.<br><br><br>* `volume`: Enter the volume partition. For example, `/dev/vdb`.<br><br>* `partitionNumber`: Enter the volume partition number. For example, `1` . |\- |
   |Object |Select the instance associated with the target volume. |\- |
   

6. Click the "Confirm" button to complete the job creation.

7. After the job is created, the system automatically redirects you to the Job management page. The new job is then executed immediately.


<span id=".5p-l55yL5omp5a6557uT5p6c"></span>
## View expansion results


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).  

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> Cloud Assistant". 

3. In the top menu bar, select the region where your business is located. 

4. Select the "Job management" tab, and then find the target job in the job list.

5. Click the target job name or the number in the "Execution object" column to open the job details page.

6. Select the "Execute object" tab to view the command execution results on each instance.

7. If the job is in **Execution successful** status, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b01a7896cde10261316c3bb8df266172.png) </span> button to the left of the target instance name for details of the target partition.

   If the following output is displayed, the capacity of volume `/dev/vdb1` is successfully expanded to 60 GiB.
