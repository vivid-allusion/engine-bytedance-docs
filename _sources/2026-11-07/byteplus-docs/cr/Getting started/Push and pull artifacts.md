---
title: "Push and pull artifacts"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/push-and-pull-images"
---

This article describes how to create a Container Registry instance and push and pull container artifacts (images or Helm Chart) using Docker, Nerdctl, or Helm client.

<span id="DHw6WTc1"></span>
## Background

The Container Registry supports the following three client tools for pushing and pulling artifacts:


|Client |Purpose |
|---|---|
|Docker |Push and pull container images. |
|Nerdctl |Push and pull container images (containerd native tool). |
|Helm |Push and pull Helm Chart. |


<span id="JeTJm9p3"></span>
## Prerequisites

<span id="m4dcTPIH"></span>
### Account and permissions


* Enterprise account real name authentication has been completed. For detailed instructions, see [Real name authentication](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* The Container Registry Product has been activated. If not activated yet, please log in to the [Container Registry Console](https://console.byteplus.com/cr) and follow the system prompts to activate the product.

* (Optional) If IAM users need to operate the Container Registry, ensure that Container Registry\-related policy and role authorization have been completed. For specific operating instructions, see [Authorization management](https://docs.byteplus.com/en/docs/cr/authorize-iam-users).


<span id="VupIEnx7"></span>
### Client environment

The corresponding client tool has been installed on the business server, and the corresponding image or Chart file is prepared.


|Client |Installation method |Version requirements |
|---|---|---|
|Docker |[Install Docker](https://docs.docker.com/engine/install/) |1.19 and above |
|Nerdctl |[Install Nerdctl](https://github.com/containerd/nerdctl) |— |
|Helm |[Install Helm 3](https://helm.sh/docs/intro/install/), and execute `export HELM_EXPERIMENTAL_OCI=1` to enable OCI support. |3.0 and above (not supported: 3.13.0 and 3.13.1) |


<span id="h8Y4J3ll"></span>
### Networking

The **IAM** **Public network access** switch has been turned on. For detailed instructions, see [IAM](https://docs.byteplus.com/en/docs/cr/enable-public-network-access).

<span id="S2O9UCtf"></span>
## Step 1: Create a Standard Edition Instance


1. Log in to the[ CR console](https://console.byteplus.com/cr).

2. Select the target region in the top navigation bar.

3. After clicking **List of instances** in the left navigation bar, click **Create instance** in the **List of instances** area on the right page.

4. On the **Create Registry Instance** page, fill in the **Purchase Information**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This step only describes the parameters related to this scenario. For more parameter descriptions, see <a href="https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance">Create instance</a>.   </div>
   

   
   |Parameter |Description |
   |---|---|
   |Name |The name of the Standard Edition instance. Ensure that the instance name is unique within the same region.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After the Standard Edition instance is created successfully, the instance name cannot be modified.</div><br> |
   |Billing type |This example selects **Pay\-as\-you\-go**. |
   

5. In **Specification**, click **Standard Edition**.

6. View the instance specification comparison and configuration costs. After confirming that everything is correct, click **Confirm Order**.

7. On the **Confirm order** page, confirm the order information again, carefully read and check **I have read and agree to the "Container Registry Service Terms"** .

8. Click **Confirm** to submit the order and start creating the Standard Edition instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can view the instance creation progress on the <strong>Instances</strong> page. When <strong>Instance status</strong> is <strong>Running</strong>, it indicates that the instance has been created successfully.   </div>
   

<span id="HIfuT1Uv"></span>
## Step 2: Initialize instance


1. In the left navigation bar, click **Instance list**. On the right\-side **Instance list** page, find the target Standard Edition instance, and click **Enter instance**.

2. On the **Initialize instance** page, configure the instance initialization information.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This step only introduces the parameters relevant to this scenario. For more parameter descriptions, please see <a href="https://docs.byteplus.com/en/docs/cr/initialize-an-instance">Initialize instance</a>.   </div>
   

   1. Configure network information.

      
      |Parameter |Description |
      |---|---|
      |Public NAT for internet endpoint |<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Enabling public network access may take 5 to 10 minutes. You can later check the status on the  <strong>Access control</strong> page.</div><br><br><br>Once public access is enabled, clients on the public internet can directly push images to and pull images from the Standard Edition instance. |
      

   2. Click **Next** to set the instance access password.

      
      |Parameter |Description |
      |---|---|
      |Set CR password |You can configure a fixed CR password. |
      

   3. Click **Next** to select or create the namespace to which the instance belongs. You can then generate and copy the commands for image login, push, and pull.

3. Click **Complete** to finish instance initialization.


<span id="f5HFyORf"></span>
## Step 3: Push and pull artifacts

In the related code for artifact management actions, the placeholders and corresponding examples are described as follows:


|Parameter |Placeholder |Sample value |
|---|---|---|
|IAM user |User name |v\*\* |
|IAM user ID |User ID |1007\*\*\* |
|Instance |Instance |test1 |
|Region |Region Code |cn\-beijing |
|Namespace |Namespace |space |
|OCI artifact repository |Repository |* CR: mysql<br><br>* Chart repository: redis |
|Artifact repository tag |* Image tag: Image tag<br><br>* Chart version: Chart version |* image tag: latest<br><br>* Chart version: 25.3.10 |



<Tabs>
<Tab zoneid="RwfHwcnp7U" title="Push/Pull images (Docker)">
<TabTitle>Push/Pull images (Docker)</TabTitle>

<span id="HeBvwIOm"></span>
### Pushing Images


1. Use the command\-line tool to execute the following command, and enter the configured password to log in to the CR instance.

   ```Bash
   docker login --username=[User name]@[User ID] [Instance]-[Region].cr.volces.com
   ```
   

   Example:

   ```Bash
   docker login --username=v**@1007*** test1-cn-beijing.cr.volces.com
   ```
   

2. Execute the following command to tag the local image.

   ```Bash
   docker tag [ImageId or Repository] [Instance]-[Region].cr.volces.com/[Namespace]/[Repository]:[Image tag]
   ```
   

   Example:

   ```Bash
   docker tag mysql:latest test1-cn-beijing.cr.volces.com/space/mysql:latest
   ```
   

3. Execute the following command to push the image to the CR instance.

   ```Bash
   docker push  [Instance]-[Region].cr.volces.com/[Namespace]/[Repository]:[Image tag]
   ```
   

   Example:

   ```Bash
   docker push test1-cn-beijing.cr.volces.com/space/mysql:latest
   ```
   

   If the system displays information similar to the following, it indicates that you have successfully pushed the image.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_07d67e8ab762ea98bc5fbdd2dac8bfe5.png) </span>


<span id="BGFIvXk7"></span>
### Pulling Images

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Public images can be pulled anonymously, which means you can directly pull public images without logging in to the Container Registry Instance.</div>



1. Use the command\-line tool to execute the following command, and enter the configured password to log in to the CR instance.

   ```Bash
   docker login --username=[User name]@[User ID] [Instance]-[Region].cr.volces.com
   ```
   

   Example:

   ```Bash
   docker login --username=v**@1007*** test1-cn-beijing.cr.volces.com
   ```
   

2. Execute the following command to pull the image.

   ```Bash
   docker pull [Instance]-[Region].cr.volces.com/[Namespace]/[Repository]:[Image tag]
   ```
   

   Example:

   ```Bash
   docker pull test1-cn-beijing.cr.volces.com/space/mysql:latest
   ```
   

   The system displays similar information as below, indicating that you have successfully pulled the image from the Container Registry.

   ```Bash
   Status: Image is up to date for test1-cn-beijing.cr.volces.com/space/mysql:latest
   ```
   





</Tab>
<Tab zoneid="WVKzUYrg4t" title="Push/Pull images (Nerdctl)">
<TabTitle>Push/Pull images (Nerdctl)</TabTitle>

<span id="YSyKozUE"></span>
### Pushing Images


1. Execute the following command using the command\-line tool, and enter the access password you have set to log in to the CR instance.

   ```Bash
   nerdctl login --username=[User name]@[User ID] [Instance]-[Region].cr.volces.com
   ```
   

   Example:

   ```Bash
   nerdctl login --username=v**@1007*** test1-cn-beijing.cr.volces.com
   ```
   

2. Execute the following command to tag the local image.

   ```Bash
   nerdctl tag [ImageId or Repository] [Instance]-[Region].cr.volces.com/[Namespace]/[Repository]:[Image tag]
   ```
   

   Example:

   ```Bash
   nerdctl tag mysql:latest test1-cn-beijing.cr.volces.com/space/mysql:latest
   ```
   

3. Execute the following command to push the image to the CR instance.

   ```Bash
   nerdctl push  [Instance]-[Region].cr.volces.com/[Namespace]/[Repository]:[Image tag]
   ```
   

   Example:

   ```Bash
   nerdctl push test1-cn-beijing.cr.volces.com/space/mysql:latest
   ```
   

   If the system displays information similar to the following, it indicates that you have successfully pushed the image.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_07d67e8ab762ea98bc5fbdd2dac8bfe5.png) </span>


<span id="B5H43jDB"></span>
### Pulling Images

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Public images can be pulled anonymously, which means you can directly pull public images without logging in to the Container Registry Instance.</div>



1. Execute the following command using the command\-line tool, and enter the access password you have set to log in to the CR instance.

   ```Bash
   nerdctl login --username=[User name]@[User ID] [Instance]-[Region].cr.volces.com
   ```
   

   Example:

   ```Bash
   nerdctl login --username=v**@1007*** test1-cn-beijing.cr.volces.com
   ```
   

2. Execute the following command to pull the image.

   ```Bash
   nerdctl pull [Instance]-[Region].cr.volces.com/[Namespace]/[Repository]:[Image tag]
   ```
   

   Example:

   ```Bash
   nerdctl pull test1-cn-beijing.cr.volces.com/space/mysql:latest
   ```
   

   The system displays similar information as below, indicating that you have successfully pulled the image from the Container Registry.

   ```Bash
   Status: Image is up to date for test1-cn-beijing.cr.volces.com/space/mysql:latest
   ```
   





</Tab>
<Tab zoneid="ZJOx6WoR1t" title="Push/Pull Helm Chart (Helm versions before 3.7)">
<TabTitle>Push/Pull Helm Chart (Helm versions before 3.7)</TabTitle>

<span id="AvCZPQav"></span>
### Push a Chart


1. Use the command\-line tool to execute the following command, and enter the configured password to log in to the CR instance.

   ```Bash
   helm registry login --username=[User name]@[User ID] [Instance]-[Region].cr.volces.com
   ```
   

   Example:

   ```Bash
   helm registry login --username=v**@1007*** test1-cn-beijing.cr.volces.com
   ```
   

2. Execute the following command to package the Chart file.

   ```Bash
   helm chart save [Repository] [Instance]-[Region].cr.volces.com/[Namespace]/[Repository]:[Chart 版本号]
   ```
   

   Example:

   ```Bash
   helm chart save redis test1-cn-beijing.cr.volces.com/space/redis:25.3.10
   ```
   

3. Execute the following command to push the Chart to the CR instance.

   ```Bash
   helm chart push [Instance]-[Region].cr.volces.com/[Namespace]/[Repository]:[Chart 版本号]
   ```
   

   Example:

   ```Bash
   helm chart push test1-cn-beijing.cr.volces.com/space/redis:25.3.10
   ```
   


<span id="V0Q1jFq2"></span>
### Pull a Chart


1. Use the command\-line tool to execute the following command, and enter the configured password to log in to the CR instance.

   ```Bash
   helm registry login --username=[User name]@[User ID] [Instance]-[Region].cr.volces.com
   ```
   

   Example:

   ```Bash
   helm registry login --username=v**@1007*** test1-cn-beijing.cr.volces.com
   ```
   

2. Execute the following command to pull the Chart.

   ```Bash
   helm chart pull [Instance]-[Region].cr.volces.com/[Namespace]/[Repository]:[Chart 版本号]
   ```
   

   Example:

   ```Bash
   helm chart pull test1-cn-beijing.cr.volces.com/space/redis:25.3.10
   ```
   

   If the system returns information similar to the following, it indicates that the Chart was pushed successfully.

   ```Bash
   Pulled: test1-cn-beijing.cr.volces.com/space/redis:25.3.10
   Digest: sha256:d1055f45acf6f9******0d807264ff97e5d02d739d1be7bb3dd0bf03ad******
   ```
   





</Tab>
<Tab zoneid="EtAWHyfRMX" title="Push/Pull Helm Chart (Helm version 3.7 and later)">
<TabTitle>Push/Pull Helm Chart (Helm version 3.7 and later)</TabTitle>

<span id="F5deKjM1"></span>
### Push a Chart


1. Use the command\-line tool to execute the following command, enter the set password, and log in to the CR instance.

   ```Bash
   helm registry login --username=[User name]@[User ID] [Instance]-[Region].cr.volces.com
   ```
   

   Example:

   ```Bash
   helm registry login --username=v**@1007*** test1-cn-beijing.cr.volces.com
   ```
   

2. Execute the following command to package the Chart file.

   ```Bash
   helm package [Repository] --version [Chart version]
   ```
   

   Example:

   ```Bash
   helm package redis --version 25.3.10
   ```
   

3. Execute the following command to push the Chart to the CR instance.

   ```Bash
   helm push [[Repository]-[Chart version].tgz] oci://[Instance]-[Region].cr.volces.com/[Namespace]
   ```
   

   Example:

   ```Bash
   helm push redis-25.3.10.tgz oci://test1-cn-beijing.cr.volces.com/space
   ```
   

   If the system returns information similar to the following, it indicates that the Chart was packaged successfully.

   ```Bash
   Successfully packaged chart and saved it to: /Users/bytedance/redis-25.3.10.tgz
   ```
   


<span id="vbJhxduG"></span>
### Pull a Chart


1. Use the command\-line tool to execute the following command, enter the set password, and log in to the CR instance.

   ```Bash
   helm registry login --username=[User name]@[User ID] [Instance]-[Region].cr.volces.com
   ```
   

   Example:

   ```Bash
   helm registry login --username=v**@1007*** test1-cn-beijing.cr.volces.com
   ```
   

2. Execute the following command to pull the Chart.

   ```Bash
   helm pull oci://[Instance]-[Region].cr.volces.com/[Namespace] --version [Chart version]
   ```
   

   Example:

   ```Bash
   helm pull oci://test1-cn-beijing.cr.volces.com/space/redis --version 25.3.10
   ```
   

   If the system returns information similar to the following, it indicates that the Chart was pushed successfully.

   ```Bash
   Pulled: test1-cn-beijing.cr.volces.com/space/redis:25.3.10
   Digest: sha256:d1055f45acf6f9******0d807264ff97e5d02d739d1be7bb3dd0bf03ad******
   ```
   





</Tab>
</Tabs>
