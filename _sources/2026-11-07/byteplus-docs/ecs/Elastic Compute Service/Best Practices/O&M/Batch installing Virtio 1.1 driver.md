---
title: "Batch installing Virtio 1.1 driver"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Batch-install-the-Virtio1-1-driver"
---

This topic describes how to use the cloud assistant feature to batch install Virtio 1.1 drivers on Linux ECS instances.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Cloud assistant Agent is installed on the instance. For operation details, refer to [Installing cloud assistant Agent](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client).

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenario

For instances of certain types (refer to [Installing Virtio driver](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.5a6J6KOFVmlydGlvMS4x6amx5Yqo) for type details), you need to install the Virtio 1.1 driver first to run them normally. To batch install drivers on multiple instances, you can use the cloud assistant feature.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [cloud assistant console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/invocations). 

2. In the top menu bar, select the region where your business is located.

3. Click the "Create a job" button to enter the Create a job page.

4. Enter the following job information as instructed.

   > This practice only describes necessary parameters. Keep other parameters with default values. For parameter details, refer to [Creating jobs](https://docs.byteplus.com/en/docs/ecs/Creating-a-job).   
   

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |Job name |Set the job name. |Install the Virtio driver. |
   |Command type |Select "Manual input". |\- |
   |Command contents |Select "Shell", and copy the [command for installing Virtio 1.1 driver](https://docs.byteplus.com/en/docs/ecs/Batch-install-the-Virtio1-1-driver#.5a6J6KOF5ZG95Luk) into the content box.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Replace the driver installation command in the red box based on the actual image and its kernel version of the instance. For installation command details, see <a href="https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.5a6J6KOFVmlydGlvMS4x6amx5Yqo">Installing Virtio 1.1 driver</a>.</div><br> |\- |
   |Object |Select the instances on which you want to install the Virtio 1.1 driver. You can select multiple instances at a time.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">For the target instance, both the operating system and kernel version used are required to meet the requirements of the driver installation command.</div><br> |\- |
   

5. Click the "Confirm" button to complete the job creation.

6. After the job is created, the system automatically redirects you to the Job management page. The new job is then executed immediately.


<span id=".5p-l55yL5ZG95Luk5omn6KGM57uT5p6c"></span>
## View job execution results


1. Log in to the [cloud assistant console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/invocations). 

2. In the top menu bar, select the region where your business is located.

3. Find the target job in the job list or search by "Job name".

4. Click the target job name or the number in the "Execution result" column to open the job details page.

5. Select the "Execute object" tab to view the command execution results on each instance.

6. When the job status is **Execution successful**, it indicates that the script has been successfully executed on all instances. You can also click the "Run log" button in the "Action" column on the right side of the target instance to view the command output during execution on this instance.

   If the following output is displayed, the Virtio 1.1 driver is installed.

    &nbsp;


<span id=".5a6J6KOF5ZG95Luk"></span>
## Installation command

In this practice, a CentOS 7.9 64\-bit image (kernel version: 3.10.0\-1160.102.1.el7.x86_64) is used as an example. For more operating system and kernel version installation commands, see [Installing Virtio 1.1 driver](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.5a6J6KOFVmlydGlvMS4x6amx5Yqo).

```Bash
#!/bin/bash

wget -O virtio_tool https://virtio11-drivers.tos-cn-beijing.volces.com/virtio_tool_1.1.2
chmod +x ./virtio_tool
output=$(./virtio_tool -check)

if grep -q "Support virtio 1.1" <<< "$output"; then
    echo "No need to install Virtio1.1 driver"
    
elif grep -q "Not support virtio 1.1" <<< "$output"; then
    echo "Attempting to install Virtio1.1 driver"

    #Replace the installation command accordingly based on operating system and kernel version
    yum -y install rpm-build redhat-lsb-core
    yum -y install epel-release

    sed -e 's!^metalink=!#metalink=!g' \
        -e 's!^#baseurl=!baseurl=!g' \
        -e 's!//download\.fedoraproject\.org/pub!//mirrors.volces.com!g' \
        -i /etc/yum.repos.d/epel.repo /etc/yum.repos.d/epel-testing.repo
  
    yum -y install --enablerepo=epel dkms

    ./virtio_tool -install

else
    echo "Script execution failed"
fi
```
