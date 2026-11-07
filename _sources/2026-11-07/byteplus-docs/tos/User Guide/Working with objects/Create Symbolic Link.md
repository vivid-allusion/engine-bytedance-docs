---
title: "Create Symbolic Link"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Create-Symbolic-link"
---

A symbolic link is an independent file that contains path information pointing to the target file, similar to a shortcut. You can quickly access frequently used target objects through a symbolic link object, which has a much smaller storage capacity compared to the target object and can be considered negligible, helping you save on storage costs. This article covers topics such as soft link behavior, billing information, and the steps to create a soft link.

<span id="582e37e2"></span>
## Behavior description

Soft link objects support version control, allowing different versions of the soft link objects to point to different target objects. When accessing a symbolic link object, different operations access different actual objects, and the returned object content also varies as described below:


|**Operation** |**The returned content** |
|---|---|
|[GetObject](https://docs.byteplus.com/docs/tos/reference--getobject) |When using GetObject to download symbolic link objects, different parameters return different content, as described below:<br><br><br>* `body`: Returns the specific content of the target object that the symbolic link object points to.<br><br>* `Content-Length`, `ETag`, `x-tos-storage-class` and `x-tos-hash-crc64ecma`: Returns information about the target object that the symbolic link object points to.<br><br>* `Last-Modified`: Returns the most recent modification date between the symbolic link object and the target object.<br><br>* Other parameters: Returns information about the symbolic link object. |
|[HeadObject](https://docs.byteplus.com/docs/tos/reference-headobject) |When using HeadObject to retrieve object metadata, different parameters return different content, as explained below:<br><br><br>* `ETag`, `x-tos-storage-class`, `x-tos-hash-crc64ecma`, and `x-tos-symlink-target-size`: Returns information about the target object that the symlink object points to.<br><br>* `Last-Modified`: Returns the latest update date between the symlink object and the target object.<br><br>* Other parameters: Returns information about the symlink object. |
|Operations other than GetObject and HeadObject. |Retrieves information about the symlink object, but not the target object. |


<span id="71aebec5"></span>
## Billing description

The billing method for symlink objects is the same as for regular objects. When accessing a symlink object, TOS charges for the symlink object, regardless of the target object. For example, when using the GetObject or HeadObject interfaces to retrieve information about a symlink object, or when processing a symlink object with data processing features, TOS charges for the number of requests and the data traffic fees for the symlink object. The PutSymlink and GetSymlink interfaces also charge for the request count according to the storage type of the symlink object.

<span id="cad85a0f"></span>
## Precautions


|**Category** |**Precautions** |
|---|---|
|Region |Symlink objects and target objects support being in the same region and same bucket or in the same region but different buckets; they are not supported in buckets located in different regions. |
|Permissions |When creating symbolic link objects, TOS does not check if the creator has access permissions to the target object. However, when accessing the target object via a symbolic link, TOS checks if the account has read permissions for both the symbolic link and the target object. You need to ensure the account has the appropriate permissions, otherwise access will fail. |
|Quantity |The number of symbolic link objects that can be created on the target object is unlimited. |
|Storage Type |Infrequency access storage,flashback archive and archive storage have minimum measurement unit restrictions. Individual files smaller than 64 KiB will be charged for storage capacity based on 64 KiB. Symbolic link object storage capacity is generally less than 64 KiB. To avoid unnecessary costs, it is recommended to set the storage type of symbolic link objects to standard storage. |
|Scope of Effect |Actions performed on symbolic link objects only affect the symbolic links themselves and do not apply to the target objects, such as changing storage types or deleting symbolic link objects. |


<span id="7aa66562"></span>
## Usage restrictions


|**Category** |**Instructions** |
|---|---|
|Creation Restrictions |* Soft links cannot be created for directories.<br><br>* Creating secondary links is not supported, which means you cannot create soft links to a soft link object. |
|Access Restrictions |* When accessing a target object via a soft link, if the target object's storage type is archive storage,cold archive,deep cold archive,the target object must be recovered first; otherwise, access will fail. For specific operations, please see [Restoring Files](https://docs.byteplus.com/docs/tos/docs-restoring-files).<br><br>* After moving, deleting, or renaming the target object, you will not be able to access the corresponding soft link object. |
|Feature Restrictions |Symbolic links do not support the following features, explained as follows:<br><br><br>* Cross\-region and same\-region copy functions are not supported for symbolic links, meaning you cannot use this feature to copy symbolic link objects.<br><br>* Server\-side encryption is not supported, meaning you cannot encrypt symbolic link objects.<br><br>* File recovery is not supported. If the storage type of the symbolic link is archive storage, you do not need to recover the symbolic link to download the object using the GetObject interface. |
|TOS Browser restrictions |Only versions 1.8.1 and above of TOS Browser support the download of soft link objects. |


<span id="0d0306d2"></span>
## Create a symbolic link


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. On the **Objects** page, click the  **...**  \> **Set Symlink** in the **Actions** column of the target file.

4. In the **Set Symlink** dialog, configure the following parameters.

   
   |**Parameters** |**Description** |
   |---|---|
   |Symlink Bucket |Select the storage bucket for the symbolic link; only buckets in the same region as the target file can be chosen. |
   |Symlink Path |Select the path location method and set the symbolic link object's storage path in the bucket as follows:<br><br><br>* **relative path:**  A path that is relative to the target file, for instance, if your current file is in `/test/` directory and the path is set to `data-symlink`, then the symlink’s path would be `/test/data-symlink`.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the target object and the symlink object are in different buckets, and the bucket containing the symlink object does not have the path of the target file, setting the path as a relative path will save the symlink object at a path starting from the root directory.   </div><br>   <br><br>* **absolute path:**  The full path starting from the root directory, for example, if your current file is in `/test/` directory, setting the path to `data1-symlink`, the path of the symlink would be `/data1-symlink`.<br><br><br>After selecting the path positioning method, enter the specific path, and adhere to the following specifications:<br><br><br>* Supports Chinese, English, numbers, and common characters.<br><br>* Supports using forward slashes (/) to quickly create subfolders.<br><br>* Does not support starting with a forward slash (/) or a backslash (\).<br><br>* Does not support using consecutive forward slashes (/).<br><br>* Directories named with consecutive dots (..) are not supported.<br><br><br>For example `aaa/bbb/filename`. |
   

5. After completing the setup, click **Ok**.

   After successfully creating a symbolic link object, you can hover your mouse over the link icon to the right of the symbolic link object name to view the path of the target object it points to.


<span id="61a4bef9"></span>
## Related documents


* [PutSymlink](https://docs.byteplus.com/docs/tos/Putsymlink)

* [GetSymlink](https://docs.byteplus.com/docs/tos/Getsymlink)
