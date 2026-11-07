---
title: "Creating file systems"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Creating_file_systems"
---

This topic explains how to create a Cache FileNAS file system.

<span id="46b35905"></span>
## Prerequisites


* You have created a BytePlus account and completed enterprise verification. For more information, see [Signing up for BytePlus accounts](https://docs.byteplus.com/byteplus-platform/docs/signing-up-your-account).

* You have created a project for the file system. For information on projects and how to create one, see [Creating a project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-project).


<span id="5298f84c"></span>
## Notes

Cache FileNAS automates capacity setup and can scale up to 10 PiB.

<span id="3aad2acf"></span>
## Steps


1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where you want to create the file system.

3. In the left navigation pane, select **File System** \> **File System list**.

4. On the **File System list** page, click **Create File System**.

5. Set the following parameters on the **Create File System** page.

   
   |Parameter |Required |Description |
   |---|---|---|
   |File System name |Yes |Enter a name for the file system. The name must:<br><br><br>* Not start with a number or a hyphen (\-).<br><br>* Contain only Chinese characters, letters, numbers, underscores (_), or hyphens (\-).<br><br>* Be between 1 and 128 characters long.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">File system names must be unique within the same region.</div><br> |
   |Description |No |Provide additional information about the file system. The description must:<br><br><br>* Start with Chinese characters, letters, or numbers.<br><br>* Contain only Chinese characters, letters, numbers, spaces, periods (.), underscores (_), hyphens (\-), equal signs (=), English commas (,), Chinese commas, or Chinese periods.<br><br>* Be no more than 255 characters long. |
   |Availability Zone |Yes |Select the availability zone for your file system.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">We recommend creating the file system in the same availability zone as the Elastic Compute Service (ECS) instance on which the file system is mounted. Otherwise, latency may increase, resulting in poorer performance.</div><br> |
   |File System type |Yes |Select **Cache FileNAS**. |
   |Provisioned Bandwidth |No |The amount of bandwidth allocated based on business needs, regardless of storage capacity. Higher bandwidth enables faster reading, writing, and access speeds. After turning on the provisioned bandwidth switch, you can set its **throughput limit**.<br><br>The minimum provisioned bandwidth is 700 MB/s, and the maximum is 60,000 MB/s, with increments of 100 MB/s. Please [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000244) if you require higher provisioned bandwidth. |
   |Burst Bandwidth |No |Temporary bandwidth boost. After enabling burst bandwidth, you can set an upper limit for how much extra bandwidth the system can use during performance spikes.<br><br>Burst bandwidth starts at 700 MB/s, with a maximum of 60,000 MB/s and increments of 100 MB/s. When provisioned bandwidth is turned on, burst bandwidth should be at least equal to provisioned bandwidth. For more information, see [Managing burst bandwidth](https://docs.byteplus.com/en/docs/nas/Managing_burst_bandwidth).  |
   |Tag |No |Click **Add Field** to add a tag to the file system. You can add up to 20 tags.<br><br>A tag is a key\-value pair that labels resources for easier searching and grouping. For more information, see [Tag overview](https://docs.byteplus.com/en/docs/nas/Overview1). |
   |Affiliated project |No |Select the project to which the file system belongs. The `default` project is selected by default.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can either select an existing project or click <strong>Create new projects</strong> to go to the <strong>Project</strong> page and create a new one. </div><br> |
   |Billing method |Yes |Only **pay\-as\-you\-go** is supported. |
   

6. After completing the settings, click **Confirm order**.

7. On the details page, read the terms and select **I have read and agree to The Terms of Storage Products and Service**. Then, click **Buy now**.

   Once you have made your purchase, click **Go to console** to view the created file system on the **File System list** page.
