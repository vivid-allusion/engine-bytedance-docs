---
title: "Managing the File Type Library"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/managing-the-file-type-library"
---

The File Type Library is a centralized resource for managing file extensions and their corresponding identification capabilities. It includes hundreds of pre\-defined formats—covering office documents, design files, source code, and images—and allows administrators to manually add proprietary custom extensions based on specific business needs.

<span id="03450f60"></span>
## Use Cases

The File Type Library is primarily used for security scenarios based on file extensions.


* **Bulk Management by Extension**: Apply unified control over specific categories of files, such as blocking the transmission of all images, source code, or design blueprints.

* **Support for Proprietary Formats**: Manually add specific engineering formats or development components used by your organization (e.g., `.data`, `.pck`).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">Resources in this library apply only to <strong>File Type</strong> identification. Ensure you select the correct criteria when creating classification and grading rules.</div>


2. <div data-tips="true" data-tips-type="tip">If you plan to audit specific formats using "Sensitive Words" or "Fingerprints," verify whether that extension <strong>supports content identification</strong> in this library.</div>



<span id="13f8ce77"></span>
## Prerequisites

The administrator must have the following permissions. See [Configuring Administrator Access](https://docs.byteplus.com/docs/sealsuite/docs-adding-administrator_1) for details.


* **Menu Permissions**: **Security** \> **DLP** \> **Data Identification** \> **File Type Library**.

* **Operation Permissions**: **DLP** \> **Data Identification Related Permissions**.


<span id="d5b5f1cd"></span>
## Navigation Path


1. Log in to the Admin Console.

2. In the left navigation bar, choose **DLP** \> **Data Identification**.

3. Click the **File Type Library** tab at the top of the page.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/471c5032a45b4ca7b62d6daa71c5c560~tplv-goo7wpa0wc-image.image) </span>

<span id="f0ed3cc6"></span>
## Understanding the Page Layout

The page consists of a **Category Tree** on the left and a **Details List** on the right, allowing you to quickly locate and manage hundreds of formats.

<span id="9d7e81ec"></span>
### Category Tree

The tree organizes extensions into a logical hierarchy for easier management.


* **Hierarchy**: Uses a two\-tier structure: **Primary Category** (e.g., Office Document) → **Secondary Type** (e.g., Office Word Document).

* **Management Rules**:

   * **Fixed Categories**: Built\-in categories are maintained by SealSuite and cannot be added or deleted by administrators.

   * **Dynamic Inheritance**: When configuring policies, if you select a Primary Category, all **current and future extensions** added to that category are automatically included in the scope of control.

* **Quick Search**: Use the search bar above the tree to find specific extensions (e.g., `pdf`) or category names.


<span id="8172d505"></span>
### Details List

The list provides in\-depth information and management options for extensions within the selected category.


* **Filtering and Search Area**

   Use the filtering dimensions at the top of the list to pinpoint specific file formats:

   * **Client Version**: Enter a version number to see which formats are supported from that specific release onwards.

   * **Creation Type**: Quickly distinguish between **Pre\-defined** system formats and **Custom** formats added by administrators.

* **List Details Area**

   This section displays specific extension information for the selected category.

   
   |**Field** |**Description** |
   |---|---|
   |**File** **Extension** |The file suffix (e.g., `.pdf`, `.zip`). |
   |**File MIME** |The Internet standard MIME type that identifies the file format (e.g., `application/json`).<br><br>When the **File type identification method** includes **File header**, the system can automatically obtain this type. The system uses the MIME type to track the file‘s flow across scenarios such as "Save As" and extension changes, ensuring continuous traceability across different operations. |
   |**Does it support content recognition?**  |Indicates whether the system can parse sensitive information (text, images, etc.) inside the file.<br><br><br>* **Support**: The system can analyze internal data.<br><br>* **Not supported**: The system can only identify the file by its extension; it cannot read internal content.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Custom extensions and some built\-in formats do not support content\-based identification.</div><br> |
   |**Does it support file transfer tracing?**  |Indicates whether the system can perform end\-to\-end tracking across the full lifecycle of the file, including creation, modification, and transfer.<br><br><br>* **Support**: In the **File Transfer Records** on the audit log details page, the system can fully display a visual end\-to\-end timeline of the file from download, creation, editing, and compression to transfer.<br><br>* **Not supported**: The system records only outbound file transfers and cannot trace its activity history on the endpoint. |
   |**File type identification method** |The technology used to determine the file's format.<br><br><br>* **Extension**: Identification based solely on the filename suffix. Supported for both built\-in and custom types.<br><br>* **File header**: Identification based on internal characteristic codes (magic numbers). It serves as the basis for the system to obtain an accurate MIME type and provides **anti\-spoofing** capabilities, ensuring the system can still identify the actual file type regardless of any extension changes made by employees. This method is only supported for some system\-built\-in extensions.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If a file type only supports identification based on file extension, be aware that users may bypass the policy by tampering with the file extension. It is recommended to add content\-based identification rules as a compensating measure.</div><br> |
   |**Minimum supported client version** |The minimum SealSuite client version required for the identification logic to take effect. |
   |**Supported OS** |The platforms where this identification is available. Most mainstream formats are supported across **Windows, macOS, and Linux**. |
   |**Creation Type** |* **Pre\-defined**: Industry\-standard formats provided by the system.<br><br>* **Custom**: Proprietary formats manually added by an administrator. |
   |**Actions** |* **Details**: View all supported attributes of the format.<br><br>* **Edit/Delete**: Available only for custom extensions.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Extensions referenced by a classification and grading rule cannot be deleted until the association is removed.</div><br> |
   


<span id="8ce5937a"></span>
## Adding Custom File Types

If the pre\-defined library does not meet your needs, you can manually expand it.

<span id="1c5d6804"></span>
### Before You Start


1. Search for the extension using the bar above the Category Tree to ensure it isn't already included.

2. **Limitations**: Custom extensions currently support **Extension Identification only**. They do not support **Content Identification** or **File Header Identification**. SealSuite will control these files based on their names but cannot inspect their internal content.

3. **Version Compatibility**: Any custom file types defined in your previous policies will be automatically moved to the **Other documents** category.


<span id="16f4363f"></span>
### Steps


1. On the **File Type Library** page, click  **+ Add File Type**.

2. In the popup window, configure the following:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3868ce89f02e4c8295478267db69bc43~tplv-goo7wpa0wc-image.image) </span>

   * **File extension**: Enter the suffix without a dot (e.g., enter `dwg`, not `.dwg`). Duplicate extensions are not allowed.

   * **File type**: Select the most appropriate category for the extension.

   * **Best Practice**: Assign custom extensions to categories with similar meanings. If no category fits, use **Other documents**. This ensures the extension is included when you select that "Primary Category" in a policy.

3. Click **Confirm**.


<span id="b6586956"></span>
## Next Steps

After configuring the File Type Library, you must link the extensions to a **Classification and Grading Rule**. Refer to [Managing classification and grading rules](https://docs.byteplus.com/docs/sealsuite/managing-classification-and-grading-rules) for details on using "File Type" as a detection criterion.
