---
title: "Creating an ObjectSet"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Creating-an-ObjectSet"
---

After initializing the ObjectSet feature, you can create an ObjectSet and add tags to manage it. This topic explains how to create an ObjectSet.

<span id="M2mNWt2G"></span>
## Prerequisites

You have initialized the ObjectSet feature. For more information, see [Initializing ObjectSet](https://docs.byteplus.com/en/docs/tos/Initializing-ObjectSet?lang=en).

<span id="B5iTMJ9J"></span>
## Notes

You cannot modify the hierarchy depth or custom delimiter if there is an existing ObjectSet in the bucket. Make sure these two settings are correct before creating an ObjectSet.

<span id="biL3xyKF"></span>
## Steps


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**.

3. In the top menu bar, select the project of the bucket you want to manage.

4. On the **Buckets** page, click the name of the bucket.

5. In the left navigation pane, select **ObjectSet \> ObjectSet management**.

6. Click **Create ObjectSet** on the right side. Then, configure the ObjectSet parameters **.** 

   
   |Parameter |Description |
   |---|---|
   |ObjectSet name |Enter a name for your ObjectSet.<br><br>Requirements:<br><br><br>* The ObjectSet name must be between 3 and 256 characters long.<br><br>* The ObjectSet name must start with a lowercase letter or number.<br><br>* The ObjectSet name must meet the configured hierarchy depth requirement for the bucket.<br><br>* Multi\-level directories are separated by a delimiter, and a trailing delimiter is automatically added.<br><br>* Using the root directory (`/`) as the path prefix is not permitted. |
   |Initial binding Tags |Add one or more tags to your ObjectSet.<br><br>Follow these guidelines when adding tags:<br><br><br>* Tag keys must be unique.<br><br>* Tag keys can be up to 128 characters long, and tag values can be up to 256 characters long.<br><br>* Tag keys and values cannot contain Chinese characters.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can add up to 10 tags.</div><br> |
   

7. Click **Confirm create**.


<span id="zZeHKPXB"></span>
## Other operations

From the **ObjectSet management** page, you can perform the following operations on your ObjectSets.


* **Edit an ObjectSet**: Click **Details** in the **Actions** column of the ObjectSet. This will allow you to modify its **Binding Tags** and **QoS traffic control**.

* **Delete an ObjectSet**: Click **Delete** in the **Actions** column of the ObjectSet. In the box that appears, click **Confirm delete** to delete the ObjectSet.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Deleting an ObjectSet only removes its configuration metadata, such as capacity limits, independent domains, and tag associations, but does not delete the objects contained within it. These objects will then be considered orphaned.   </div>
