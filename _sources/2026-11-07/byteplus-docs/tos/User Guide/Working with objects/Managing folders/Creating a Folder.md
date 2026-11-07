---
title: "Creating a Folder"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-creating-a-folder"
---

You can use the folder feature to categorize and manage files stored in TOS. This topic describes how folders work and how to create a folder.

<span id="732a9491"></span>
## **Prerequisites**

You have created a bucket as instructed in [Creating a Bucket](https://docs.byteplus.com/en/tos/docs/create-a-bucket?version=1.0.0).

<span id="524284ef"></span>
## **Background**

TOS stores files in a flat structure, which does not involve the concept of folders. To facilitate categorization and management of files, TOS displays files ending with a forward slash ( / ) as folders by default. Essentially, such a folder is a 0 KiB file with characteristics of a regular file. It can be uploaded and downloaded. You can also operate it as a folder in the TOS console.

<span id="3f2930e3"></span>
## **Procedure**


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. On the **Objects** page, click **Create folder**.

4. In the pop\-up dialog box, type the folder name and click **Create**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The folder name should conform to the following rules:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It can contain Chinese characters, letters, digits, and common symbols.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can quickly create a subfolder by entering a name with both the folder and subfolder names separated by a forward slash ( / ). The subfolder name cannot start with a forward slash ( / ) or backslash ( \ ) and cannot contain consecutive forward slashes ( / ).   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You cannot name a folder <code>..</code> .   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Folder names must be unique in the same bucket.   </div>
