---
title: "Creating file systems"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/efs_Creating_file_systems"
---

This topic explains how to create a file system.

<span id="0IiHKsXF"></span>
## Prerequisites

Before creating a file system, make sure you have completed the following:


1. You have created a BytePlus account and completed enterprise verification. For more information, see [Signing up for BytePlus accounts](https://docs.byteplus.com/byteplus-platform/docs/signing-up-your-account).

2. You have created a project for the file system. For information on projects and how to create one, see [Creating a project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-project).

3. You have created a virtual private cloud (VPC). If you have not created a VPC or want to create a new one, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).


<span id="HF88mneR"></span>
## Steps


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region where you want to create the file system.

3. In the left navigation pane, select **File System**.

4. On the **File System** page, click **Create File System**.

5. Set the following parameters on the **Create Elastic File System** page.

   * **Basic information**

      
      |Parameter |Description |
      |---|---|
      |File System name |Enter the name of the file system. File system names must:<br><br><br>* Start with Chinese characters or English letters.<br><br>* Contain only Chinese characters, letters, numbers, periods (.), underscores (_), or hyphens (\-).<br><br>* Be between 1 and 128 characters long. |
      |Description |Provide additional information about the file system to help you identify it later. Descriptions must:<br><br><br>* Start with Chinese characters, letters, or numbers.<br><br>* Contain only Chinese characters, letters, numbers, spaces, periods (.), underscores (_), hyphens (\-), equal signs (=) and English commas (,), Chinese commas, enumaration commas, or Chinese periods.<br><br>* Be between 0 and 255 characters long. |
      |Billing type |EFS currently only supports **pay\-as\-you\-go** billing. For more information, see [Billing overview](https://docs.byteplus.com/en/docs/nas/Billing_overview). |
      |Availability Zone |Select the availability zone for the file system.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">For optimal performance, deploy your file system and ECS instance in the same availability zone.</div><br> |
      

   * **Instance configuration**

      
      |Parameter |Description |
      |---|---|
      |Instance type |Select the product specification that best fits your needs. For more information, see [Product specifications](https://docs.byteplus.com/en/docs/nas/Product_specifications).<br><br><br>* **Premium**: Uses solid state drives (SSD) to deliver high\-performance with lower latency. You can access your stored data after mounting the file system with NFS and FSX.<br><br>* **Basic**: Uses hard disk drives (HDD) to offer high\-capacity file storage at a lower cost. You can access your stored data after mounting the file system with NFS and FSX. |
      

   * **Bandwidth configuration**

      
      |Parameter |Description |
      |---|---|
      |Bandwidth mode |Choose the bandwidth mode that best fits your needs. The options are:<br><br><br>* **Provisioned Bandwidth mode** (Recommended): This mode is ideal for predictable workloads. It supports up to 20,000 MB/s of read bandwidth and 1,800,000 IOPS. Configure the provisioned bandwidth according to your needs. Once you have selected this option, you will only be charged for bandwidth that exceeds the baseline bandwidth.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To ensure optimal performance when you begin using this service, we recommend configuring a higher initial bandwidth in this mode.   </div><br>   <br><br>* **Baseline Bandwidth mode**: This mode provides scalable bandwidth based on storage capacity for workloads with basic performance requirements. It supports up to 30,000 MB/s of read bandwidth and 900,000 IOPS. |
      |Provisioned Bandwidth |When you set the **Bandwidth mode** to **Provisioned Bandwidth mode**, you must set the size of the provisioned bandwidth. Provisioned bandwidth starts at 100 MB/s, with a maximum of 20,000 MB/s and increments of 100 MB/s. |
      |Estimated Capacity |Enter a value to estimate the performance of the file system once the storage capacity is reached. The valid range is 0 to 10 PiB. |
      |Estimated result |Displays the estimated performance of the file system at the specified storage capacity, including:<br><br><br>* **100% read**<br><br>* **100% write**<br><br>* **Billable capacity**<br><br>* **Billable Provisioned Bandwidth**<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The <strong>Billable Provisioned Bandwidth</strong> parameter only appears when <strong>Provisioned Bandwidth mode</strong> is selected.   </div><br>    |
      |Burst Bandwidth |This mode is designed for workloads that have high bursts of short\-duration, unpredictable peak traffic.<br><br>This feature is disabled by default. When enabled, it dynamically allocates idle cluster bandwidth resources. Performance automatically scales with workload pressure, and you only pay for bandwidth used beyond the baseline and provisioned amounts, allowing for flexible cost management. |
      |Burst Bandwidth limit |When you select to enable **burst bandwidth**, set the cap for the burst bandwidth. The burst bandwidth limit starts at 100MB/s, with a step size of 100MB/s, and can burst up to a maximum of 60,000MB/s read bandwidth and 1,800,000 read IOPS. |
      

   * **Advanced configuration**

      
      |Parameter |Description |
      |---|---|
      |Tag |A tag is a key\-value pair. Click **Add tag** to create a tag for this file system to make identification, searching, and grouping easier.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">A file system can have up to 20 tags.</div><br> |
      |Affiliated project |Select or create a project to which the file system belongs.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">A project is a resource grouping mechanism provided by BytePlus that helps you achieve logical resource isolation. Projects can be used for authorization and cost allocation. </div><br> |
      

6. Click **Next** **step**.

7. Verify your configurations. Then, check the box that says **I have read and agree to** **The Terms of Storage Products and Service** **and** **Service Level Agreement for Elastic File Storage**.

8. Click **Submit**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Creating a file system takes time. After submitting your order, click <strong>Go to the console</strong> on the File System page to check the progress of the creation. Once the file system <strong>Status</strong> shows <strong>Running</strong>, it means that the file system has been successfully created.   </div>
