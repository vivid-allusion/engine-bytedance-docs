---
title: "Creating key pairs"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Creating-key-pairs"
---

This topic describes how to create an SSH key pair in the console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Key pairs are isolated by region. You can only associate an instance with a key pair in the same region.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the top menu bar, select the region and project.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you select a specific project in the top menu bar, any newly created key pair is associated with that project by default. If you select "All Resources," any newly created key pair can be associated with any project in the current account.   </div>
   

3. Click "Key Pair \> Create key pair".

4. On the "Create key pair" page, configure the parameters described in the following table.

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |Key pair name |Enter the key pair name. |SSH |
   |Creation type |* **Auto\-create**: The system automatically creates a key pair. After the key pair is created, the private key file is automatically downloaded to your local device. The default file name is <key\-pair\-name\>.pem. You have only one opportunity to download the private key. BytePlus does not store your private key. Make sure that you keep your private key safe.<br><br>* **Import**: Paste your existing public key into the public key text box. You can obtain your public key by referring to [Viewing public key information](https://docs.byteplus.com/en/docs/ecs/Viewing-public-keys). |Auto\-create |
   |Project |(Optional) Select a project for the key pair.<br><br><br>* A key pair can belong to only one project.<br><br>* After a project is selected, the created key pair can only be used by users who have permission on that project.<br><br>* When you go to the "Create key pair" page, if you have already selected a specific project in the top menu bar, the newly created key pair is associated with that project by default. To associate the key pair with a different project, change the project in the top menu bar to "All Resources" or the target project.<br><br>* For more information about projects, see [Project management](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management). |projectA |
   |Tag |A tag is a key\-value pair used to identify cloud resources. Tags help you categorize cloud resources based on different dimensions, such as purpose, owner, or environment. This allows you to search and aggregate your cloud resources.<br><br>Click the "+ Add tags" button, select existing tags or enter new tags, and then associate the tags with the key pair. For more information, see [Tag overview](https://docs.byteplus.com/en/docs/resourcemanagement/Tag_Overview). |k1:v1 |
   

5. Click "Create" to complete the operation.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After the key pair is created, the system automatically downloads the private key file (KeyName.pem) to the local device. If the private key file is lost, it cannot be recovered. Store it securely.   </div>
   

<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operation

After you create a key pair, you need to [associate the key pair with your Linux instance](https://docs.byteplus.com/en/docs/ecs/Binding-key-pairs-to-instances). This way, you can use the private key of the key pair to [log in to the instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[CreateKeyPair](https://docs.byteplus.com/en/docs/ecs/CreateKeyPair)
