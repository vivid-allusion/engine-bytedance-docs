---
title: "Pull and push images"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/push-and-pull-images-in-an-enterprise-instance"
---

This document describes how to create a CR instance and use the Docker, Nerdctl, or Helm client to push and pull container artifacts (images/Helm Charts).

<span id="XPpbyM8Y"></span>
## Background

CR supports the following three client tools for pushing and pulling artifacts:


|Client |Purpose |
|---|---|
|Docker |Push and pull container images. |
|Nerdctl |Push and pull container images (containerd native tool). |
|Helm |Push and pull Helm Chart. |


<span id="9PXjBMP8"></span>
## Prerequisites

<span id="slpXisqV"></span>
### CR


* An instance has been created. For instructions, see [Create standard instance ](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance).

* A namespace has been created. For instructions, see [Create namespace ](https://docs.byteplus.com/en/docs/cr/create-a-namespace).

* The **IAM** **Public network access** switch has been turned on. For details, see [IAM](https://docs.byteplus.com/en/docs/cr/enable-public-network-access).


<span id="fNI5o2BX"></span>
### Client environment

The corresponding client tool has been installed on the business server, and the corresponding image or Chart file is prepared.


|Client |Installation method |Version requirements |
|---|---|---|
|Docker |[Install Docker](https://docs.docker.com/engine/install/). |1.19 and above |
|Nerdctl |[Install Nerdctl](https://github.com/containerd/nerdctl). |— |
|Helm |[Install Helm 3](https://helm.sh/docs/intro/install/), and execute `export HELM_EXPERIMENTAL_OCI=1` to turn on OCI support. |3.0 and above (3.13.0 and 3.13.1 are not supported) |


<span id="TBzinaKQ"></span>
## Procedure

The placeholders and corresponding examples in artifact management operation\-related code are described as follows:


|Parameter |Placeholder |Sample value |
|---|---|---|
|IAM username |User name |v\*\* |
|IAM user ID |User ID |1007\*\*\* |
|Instance |Instance |test1 |
|Region |Region Code |ap\-southeast\-1 |
|Namespace |Namespace |space |
|OCI artifact repository |Repository |* CR: mysql<br><br>* Chart repository: redis |
|Artifact repository tag |* Image tag<br><br>* Chart version |* Image tag: latest<br><br>* Chart version: 25.3.10 |



<Tabs>
<Tab zoneid="keYAGX1r" title="Push/Pull images (Docker)">
<TabTitle>Push/Pull images (Docker)</TabTitle>

<span id="HeBvwIOm"></span>
### Pushing Images


1. Execute the following command using the command\-line tool, enter the configured access password, and login to the CR instance.

   ```Bash
   docker login --username=[User name]@[User ID] [Instance]-[Region].cr.bytepluses.com
   ```
   

   Example:

   ```Bash
   docker login --username=v**@1007*** test1-ap-southeast-1.cr.bytepluses.com
   ```
   

2. Execute the following command to tag the local image.

   ```Bash
   docker tag [ImageId or Repository] [Instance]-[Region].cr.bytepluses.com/[Namespace]/[Repository]:[Image tag]
   ```
   

   Example:

   ```Bash
   docker tag mysql:latest test1-ap-southeast-1.cr.bytepluses.com/space/mysql:latest
   ```
   

3. Execute the following command to push the image to the CR instance.

   ```Bash
   docker push  [Instance]-[Region].cr.bytepluses.com/[Namespace]/[Repository]:[Image tag]
   ```
   

   Example:

   ```Bash
   docker push test1-ap-southeast-1.cr.bytepluses.com/space/mysql:latest
   ```
   

   If the system displays information similar to the following, it indicates that you have successfully pushed the image.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_07d67e8ab762ea98bc5fbdd2dac8bfe5.png) </span>


<span id="BGFIvXk7"></span>
### Pulling Images

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Public images can be pulled anonymously, which means you can directly pull public images without logging in to the Container Registry Instance.</div>



1. Execute the following command using the command\-line tool, enter the configured access password, and login to the CR instance.

   ```Bash
   docker login --username=[User name]@[User ID] [Instance]-[Region].cr.bytepluses.com
   ```
   

   Example:

   ```Bash
   docker login --username=v**@1007*** test1-ap-southeast-1.cr.bytepluses.com
   ```
   

2. Execute the following command to pull the image.

   ```Bash
   docker pull [Instance]-[Region].cr.bytepluses.com/[Namespace]/[Repository]:[Image tag]
   ```
   

   Example:

   ```Bash
   docker pull test1-ap-southeast-1.cr.bytepluses.com/space/mysql:latest
   ```
   

   The system displays similar information as below, indicating that you have successfully pulled the image from the Container Registry.

   ```Bash
   Status: Image is up to date for test1-ap-southeast-1.cr.bytepluses.com/space/mysql:latest
   ```
   





</Tab>
<Tab zoneid="TjWWO96P" title="Push/Pull images (Nerdctl)">
<TabTitle>Push/Pull images (Nerdctl)</TabTitle>

<span id="YSyKozUE"></span>
### Pushing Images


1. Use the command\-line tool to execute the following command, and enter the set access password to log in to the CR instance.

   ```Bash
   nerdctl login --username=[User name]@[User ID] [Instance]-[Region].cr.bytepluses.com
   ```
   

   Example:

   ```Bash
   nerdctl login --username=v**@1007*** test1-ap-southeast-1.cr.bytepluses.com
   ```
   

2. Execute the following command to tag the local image.

   ```Bash
   nerdctl tag [ImageId or Repository] [Instance]-[Region].cr.bytepluses.com/[Namespace]/[Repository]:[Image tag]
   ```
   

   Example:

   ```Bash
   nerdctl tag mysql:latest test1-ap-southeast-1.cr.bytepluses.com/space/mysql:latest
   ```
   

3. Execute the following command to push the image to the CR instance.

   ```Bash
   nerdctl push  [Instance]-[Region].cr.bytepluses.com/[Namespace]/[Repository]:[Image tag]
   ```
   

   Example:

   ```Bash
   nerdctl push test1-ap-southeast-1.cr.bytepluses.com/space/mysql:latest
   ```
   

   If the system displays information similar to the following, it indicates that you have successfully pushed the image.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_07d67e8ab762ea98bc5fbdd2dac8bfe5.png) </span>


<span id="B5H43jDB"></span>
### Pulling Images

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Public images can be pulled anonymously, which means you can directly pull public images without logging in to the Container Registry Instance.</div>



1. Use the command\-line tool to execute the following command, and enter the set access password to log in to the CR instance.

   ```Bash
   nerdctl login --username=[User name]@[User ID] [Instance]-[Region].cr.bytepluses.com
   ```
   

   Example:

   ```Bash
   nerdctl login --username=v**@1007*** test1-ap-southeast-1.cr.bytepluses.com
   ```
   

2. Execute the following command to pull the image.

   ```Bash
   nerdctl pull [Instance]-[Region].cr.bytepluses.com/[Namespace]/[Repository]:[Image tag]
   ```
   

   Example:

   ```Bash
   nerdctl pull test1-ap-southeast-1.cr.bytepluses.com/space/mysql:latest
   ```
   

   The system displays similar information as below, indicating that you have successfully pulled the image from the Container Registry.

   ```Bash
   Status: Image is up to date for test1-ap-southeast-1.cr.bytepluses.com/space/mysql:latest
   ```
   





</Tab>
<Tab zoneid="j536qgOb" title="Push/Pull Helm Chart (Helm version earlier than 3.7)">
<TabTitle>Push/Pull Helm Chart (Helm version earlier than 3.7)</TabTitle>

<span id="AvCZPQav"></span>
### Push a Chart


1. Use the command\-line tool to execute the following command, and enter the set access password to log in to the CR instance.

   ```Bash
   helm registry login --username=[User name]@[User ID] [Instance]-[Region].cr.bytepluses.com
   ```
   

   Example:

   ```Bash
   helm registry login --username=v**@1007*** test1-ap-southeast-1.cr.bytepluses.com
   ```
   

2. Execute the following command to package the Chart file.

   ```Bash
   helm chart save [Repository] [Instance]-[Region].cr.bytepluses.com/[Namespace]/[Repository]:[Chart version]
   ```
   

   Example:

   ```Bash
   helm chart save redis test1-ap-southeast-1.cr.bytepluses.com/space/redis:25.3.10
   ```
   

3. Execute the following command to push the Chart to the CR instance.

   ```Bash
   helm chart push [Instance]-[Region].cr.bytepluses.com/[Namespace]/[Repository]:[Chart version]
   ```
   

   Example:

   ```Bash
   helm chart push test1-ap-southeast-1.cr.bytepluses.com/space/redis:25.3.10
   ```
   


<span id="V0Q1jFq2"></span>
### Pull a Chart


1. Use the command\-line tool to execute the following command, and enter the set access password to log in to the CR instance.

   ```Bash
   helm registry login --username=[User name]@[User ID] [Instance]-[Region].cr.bytepluses.com
   ```
   

   Example:

   ```Bash
   helm registry login --username=v**@1007*** test1-ap-southeast-1.cr.bytepluses.com
   ```
   

2. Execute the following command to pull the Chart.

   ```Bash
   helm chart pull [Instance]-[Region].cr.bytepluses.com/[Namespace]/[Repository]:[Chart version]
   ```
   

   Example:

   ```Bash
   helm chart pull test1-ap-southeast-1.cr.bytepluses.com/space/redis:25.3.10
   ```
   

   If the system returns information similar to the following, it indicates that the Chart was pushed successfully.

   ```Bash
   Pulled: test1-ap-southeast-1.cr.bytepluses.com/space/redis:25.3.10
   Digest: sha256:d1055f45acf6f9******0d807264ff97e5d02d739d1be7bb3dd0bf03ad******
   ```
   


The **IAM** **Public network access** switch has been turned on. For detailed actions, see [IAM](https://docs.byteplus.com/en/docs/cr/enable-public-network-access).


</Tab>
<Tab zoneid="d582L686" title="Push/Pull Helm Chart (Helm version 3.7 and later)">
<TabTitle>Push/Pull Helm Chart (Helm version 3.7 and later)</TabTitle>

<span id="F5deKjM1"></span>
### Push a Chart


1. Execute the following command using the command\-line tool, and enter the access password that has been set to log in to the CR instance.

   ```Bash
   helm registry login --username=[User name]@[User ID] [Instance]-[Region].cr.bytepluses.com
   ```
   

   Example:

   ```Bash
   helm registry login --username=v**@1007*** test1-ap-southeast-1.cr.bytepluses.com
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
   helm push [[Repository]-[Chart version].tgz] oci://[Instance]-[Region].cr.bytepluses.com/[Namespace]
   ```
   

   Example:

   ```Bash
   helm push redis-25.3.10.tgz oci://test1-ap-southeast-1.cr.bytepluses.com/space
   ```
   

   If the system returns information similar to the following, it indicates that the Chart was packaged successfully.

   ```Bash
   Successfully packaged chart and saved it to: /Users/bytedance/redis-25.3.10.tgz
   ```
   


<span id="vbJhxduG"></span>
### Pull a Chart


1. Execute the following command using the command\-line tool, and enter the access password that has been set to log in to the CR instance.

   ```Bash
   helm registry login --username=[User name]@[User ID] [Instance]-[Region].cr.bytepluses.com
   ```
   

   Example:

   ```Bash
   helm registry login --username=v**@1007*** test1-ap-southeast-1.cr.bytepluses.com
   ```
   

2. Execute the following command to pull the Chart.

   ```Bash
   helm pull oci://[Instance]-[Region].cr.bytepluses.com/[Namespace] --version [Chart version]
   ```
   

   Example:

   ```Bash
   helm pull oci://test1-ap-southeast-1.cr.bytepluses.com/space/redis --version 25.3.10
   ```
   

   If the system returns information similar to the following, it indicates that the Chart was pushed successfully.

   ```Bash
   Pulled: test1-ap-southeast-1.cr.bytepluses.com/space/redis:25.3.10
   Digest: sha256:d1055f45acf6f9******0d807264ff97e5d02d739d1be7bb3dd0bf03ad******
   ```
   





</Tab>
</Tabs>
