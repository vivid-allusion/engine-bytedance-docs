---
title: "Tag overview"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/efs_Tag_overview"
---

EFS supports tag\-based resource management. Tags help you categorize file systems by purpose, type, owner, environment or other criteria, making filtering and managing cloud resources easier.

<span id="PxTajoVc"></span>
## Feature introduction


* As cloud resources grow, management complexity increases. BytePlus offers tag\-based resource management, enabling customizable identification and classification of cloud service resources across various dimensions. You can use tags to organize cloud resources by business category, purpose, user, or other criteria. These tags allow for the quick querying and filtering of specific resource categories once applied.

* With tags, you can manage EFS resources at the file system level. A tag consists of a key\-value pair, where a tag key is associated with exactly one tag value. You can add multiple tags from different categories to each EFS file system. Additionally, each tag can be associated with multiple file systems.


<span id="mbPDFxaS"></span>
## Use cases

Tags are particularly useful in the following scenarios.


* **Classified management of cloud resources**: Managing and identifying cloud resources just by their file system names is challenging when there are many resources. In this case, you can group EFS file systems by business scenarios and tag those with the same scenario. After setting up tags, you can easily filter file systems by tag keys and values.

* **Billing and cost allocation**: If your business scenario requires cost allocation by different organizations or departments, you can use tags to classify cloud resources. Assign identical tags to cloud resources within the same organization or department to allocate costs during periodic billing.


<span id="f2gnFVBr"></span>
## Notes


* You can add multiple tags to each EFS file system. However, tag keys under the same file system cannot repeat. Each key can only have one value. For example, if you want to add the tag `filesystemowner:UserB` to EFS file system A, which already has the tag `filesystemowner:UserA`, you must first delete the tag `filesystemowner:UserA`.

* Tag information is not shared across regions. For example, tags created in the China (Beijing) region are not visible in the China (Shanghai) region.

* Each EFS file system can have up to 50 tags, but there is no global limit on total tags. For more information, see Tagging rules.


<span id="QZUxInvb"></span>
## Usage examples

For example, Company A purchased five EFS file systems on BytePlus. These file systems were assigned to the gaming, AI, and IoT departments and serve users in Beijing, Guangzhou, and Shanghai. Alice, Ben, and Carl maintain these file systems. To make management easier, Company A can tag these file systems:


* Set the following tags:

   
   |Tag key |Tag value |
   |---|---|
   |department |game, ai, iot |
   |region |beijing, guangzhou, shanghai |
   |owner |Alice, Ben, Carl |
   

* Assign these tags to each file system:

   
   |File system name |Tag |
   |---|---|
   |EFS file system A |* department:game<br><br>* region:beijing<br><br>* owner:Alice |
   |EFS file system B |* department:game<br><br>* region:guangzhou<br><br>* owner:Ben |
   |EFS file system C |* department:ai<br><br>* region:beijing<br><br>* owner:Ben |
   |EFS file system D |* department:ai<br><br>* region:shanghai<br><br>* owner:Carl |
   |EFS file system E |* department:iot<br><br>* region:beijing<br><br>* owner:Carl |
