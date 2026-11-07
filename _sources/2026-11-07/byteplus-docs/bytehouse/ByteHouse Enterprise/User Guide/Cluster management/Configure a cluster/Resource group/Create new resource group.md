---
title: "Create new resource group"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/create-resource-group"
---

Users can create one or more resource groups on the ByteHouse Console and restrict the resource usage of each group to achieve tenant isolation.

<span id="ae9f1dd0"></span>
## Prerequisites


* Cluster administrator or system administrator permissions are required during operations.

* Cluster resources must be enabled in advance.


<span id="16c04666"></span>
## Steps


1. Access **ByteHouse Console \> Manage clusters \> Cluster List \> Cluster details**, and then click the "Load & Resource Groups" tab.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e55ddb030e344f03bf6a898f701ae9f8~tplv-goo7wpa0wc-image.image) </span>

2. In the "Resource Group" section, click the "+ New Resource Group" button on the right.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54fde30f7a6548cd88b838f127932a4a~tplv-goo7wpa0wc-image.image) </span>

3. In the pop\-up window, fill in the following information sequentially:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f816a314d8494cd487bb4811f139a774~tplv-goo7wpa0wc-image.image) </span>



|Param |Configuration Description |
|---|---|
|Group Name |It cannot start with a number and can only contain letters, numbers, and underscores. |
|CPU Usage Limits |Select the type of CPU limit for the current resource group, currently supporting hard and soft limits.<br><br><br>* Hard limit: Limits the number of CPU cores that the current resource group can use.<br><br>* Soft limit: Limits the maximum percent of total CPU use for the current resource. |
|Max CPU usage proportion / CPU cores |* If a hard limit is selected for CPU usage, set the maximum CPU cores that the resource group can use here.<br><br>* If a soft limit is selected for CPU usage, set the resource group's **maximum CPU usage proportion** here. |
|Max Memory Usage Proportion |Select the max memory usage proportion for this resource group **Max Memory Usage Proportion**. |
|Maximum concurrency |Fill in **the maximum concurrency**. You may adjust according to the "remaining allocable" number below. If the number of concurrent users exceeds the limit during use, the system will display an error message. |
|Maximum wait queue number |Select **the maximum wait queue number**. If the number of wait queues is exceeded during use, the system will report an error. |
|Maximum wait duration |(Optional) Fill in the **maximum wait duration** in the queue. If the maximum duration is exceeded, the search will report an error. |
|Associated resource groups correspond to users |Associated resource groups correspond to users (multiple choices), and subsequent **user usage will be restricted by this resource group**. |



4. Click "Confirm" to complete the resource group settings.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61c24808e3c244cba6495689b24ed0fa~tplv-goo7wpa0wc-image.image) </span>
