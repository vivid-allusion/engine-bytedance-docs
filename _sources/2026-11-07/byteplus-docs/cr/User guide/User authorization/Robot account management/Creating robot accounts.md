---
title: "Creating robot accounts"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Create-robot-accounts"
---

Robot accounts are only associated with the instance status and are not affected by changes to IAM users. This topic describes how to create a robot account.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This action applies only to Standard Edition instances.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Usage limits

Up to 20 robot accounts can be created under each root user. Exceeding this limit will result in robot account creation failure.

<span id="Gk2ZxlYr"></span>
## Background

The availability of accounts associated with individual users (such as IAM users) can be affected by personnel changes. Events like employee departure or role changes can cause the corresponding IAM user to be unavailable, leading to failures in related tasks. One example is an image pull task in a CI/CD automation system that relies on an IAM user.

Using robot accounts created at the instance level, which are not associated with IAM users, can effectively prevent issues in such scenarios.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When you push or pull images via Docker, ensure you use Docker version 1.19 or later to avoid failures.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances.** 

2. In the left navigation bar of the instance page, click **robot account**.

3. On the  ** Robot account** page, click **Create robot account**.

4. Configure robot account parameters.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">It is recommended to set a specific expiration time or regularly reset the password to prevent account leaks.   </div>
   

   
   |Configuration item |Description |
   |---|---|
   |username |The custom name of the robot account. |
   |Password |Set the login password of the robot account. You can use an auto\-generated password or enter one manually.<br><br><br>* **Automatic generation**: After you complete the configuration and click ** Confirm**, the password is automatically generated. The automatically generated password is displayed only once. Save it properly.<br><br>* **Manual input**: Enter a password manually. The password must contain upper and lower case letters, and at least one digit or special character. The length must be 8 to 20 characters. |
   |Description |The custom description of the robot account. |
   |Expiration time |Set the valid period of the robot account.<br><br><br>* **Never expire**: No expiration time. The account will not expire.<br><br>* **Specified days**: The account expires after the specified number of days. Unit: day(s). |
   |Permission configuration |Configure permissions of the robot account by namespace or project.<br><br><br>* Permission scopes:<br><br>   * **Specify namespace**: Select the namespace to be authorized.<br><br>   * **Specify project**: Select the project to be authorized. The namespace associated with the project will be authorized.<br><br>   * **All namespaces (including new ones)** : Both existing and new namespaces are authorized.<br><br>* Authorization level:<br><br>   * **Read only**: Allows viewing resources but no operations in the target namespace. The account can pull images from, but cannot push images to, the target namespace.<br><br>   * **Read\-write**: Allows all read and write operations in the namespace. The account can push images to and pull images from the namespace. |
   

5. Click **confirm** to complete the operation.


<span id="RdC7b6DL"></span>
## Subsequent operations

<span id="8WT1d96S"></span>
### Use robot account to push and pull images

After creating a robot account, you can use the account and password of the robot account to log in to the CR instance in CI/CD pipelines, automation scripts, or container clusters, and perform image push and pull operations. This document provides example commands for reference. For complete operating instructions, see [Push and pull artifact](https://docs.byteplus.com/en/docs/cr/push-and-pull-images?lang=en).


1. Use a robot account to log in to the CR instance.

   ```Bash
   docker login [instance-name]-[region].cr.volces.com --username [robot-account-name] --password [robot-account-password]
   ```
   

2. Push or pull images.

   
   <Tabs>
   <Tab zoneid="KBXVx47uPS" title="Pushing Images">
   <TabTitle>Pushing Images</TabTitle>
   
   After logging in successfully, execute the following command to push the local image to the CR instance.
   
   ```Bash
   # Tag the local image
   docker tag [local-image-name]:[tag] [instance-name]-[region].cr.volces.com/[namespace]/[repository]:[tag]
   # Push image
   docker push [instance-name]-[region].cr.volces.com/[namespace]/[repository]:[tag]
   ```
   
   
   If the system displays information similar to the following, it indicates that you have successfully pushed the image.
   
   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_07d67e8ab762ea98bc5fbdd2dac8bfe5.png) </span>
   
   
   </Tab>
   <Tab zoneid="sazxw3aVTn" title="Pulling Images">
   <TabTitle>Pulling Images</TabTitle>
   
   After logging in successfully, execute the following command to pull the image from the CR instance.
   
   ```Bash
   docker pull [instance-name]-[region].cr.volces.com/[namespace]/[repository]:[tag]
   ```
   
   
   The system displays similar information as below, indicating that you have successfully pulled the image from the Container Registry.
   
   ```Bash
   Status: Image is up to date for test1-cn-beijing.cr.volces.com/space/mysql:latest
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
