---
title: "Managing the File Fingerprint Library"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/managing-the-file-fingerprint-library"
---

The File Fingerprint Library is designed for deep content modeling of core corporate assets, such as standardized contracts, design blueprints, and financial templates. Unlike basic keyword matching, file fingerprinting uses advanced algorithms to extract unique digital characteristics. This allows the system to accurately identify sensitive data even if the file is partially modified, restructured, or renamed.


* **Unified Management**: A dedicated portal for entering and maintaining the fingerprints of your most critical assets.

* **High Transparency**: The system visualizes the specific keywords extracted from sample files, allowing administrators to understand and fine\-tune the detection logic.

* **Strong Resilience**: Adjustable "Similarity Thresholds" allow the system to detect leaks even when document content has been tampered with or edited.


<span id="d02d2feb"></span>
## Use Cases

File fingerprinting is ideal for identifying documents that follow a specific template, contain proprietary secrets, or are difficult to define using simple keywords or regex.


* **Standard Contracts and Bids**: Prevents employees from leaking contracts even after modifying clauses or changing filenames.

* **Technical Specifications and Blueprints**: Protects core R&D assets, ensuring they are recognized even after being reformatted or partially edited.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">File fingerprints are applied exclusively to <strong>file content</strong> scanning. They cannot be used for rules based on external attributes like filenames or extensions. Ensure you select the correct criteria when creating classification and grading rules.</div>


<span id="b16b7d54"></span>
## Prerequisites

The administrator must have the following permissions. See [Configuring Administrator Access](https://docs.byteplus.com/docs/sealsuite/docs-adding-administrator_1) for details.


* **Menu Permissions**: **Security** \> **DLP** \> **Data Identification** \> **File Fingerprint Library**.

* **Operation Permissions**: **DLP** \> **Data Identification Related Permissions**.


<span id="dbdf7962"></span>
## Navigation Path


1. Log in to the Admin Console.

2. In the left navigation bar, choose **DLP** \> **Data Identification**.

3. Click the **File Fingerprint Library** tab at the top of the page.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/518d3f5164bb4a02be33c400393d5538~tplv-goo7wpa0wc-image.image) </span>

<span id="f100b309"></span>
## Adding a File Fingerprint

Upload your organization's standard documents as samples for the system to learn their unique characteristics.


1. On the **File Fingerprint Library** page, click  **+ Add File Fingerprint**.

2. Configure the following settings in the popup window and click **OK**.


<span id="1b2cfcb3"></span>
### File Fingerprint Generation


|**Setting** |**Description** |
|---|---|
|**File fingerprint name** |Provide a clear name for the fingerprint (e.g., `R&D-Core Algorithm Spec-V1.0`). This helps in identifying protected assets in classification rules and audit logs. |
|**Upload Samples** |Drag and drop sample files to serve as the baseline for the fingerprint model.<br><br><br>* **How it works**: SealSuite automatically extracts representative word groups to build a unique digital fingerprint. Once established, the system can detect the asset even if an employee:<br><br>   * **Renames the file** (e.g., changing "Core_Plan.pdf" to "Notes.pdf").<br><br>   * **Changes the format** (e.g., copying Word content into a TXT or PDF file).<br><br>   * **Modifies the content** (e.g., deleting paragraphs or inserting filler text).<br><br>* **Requirements**:<br><br>   * **Supported Formats**: Word (.doc, .docx), TXT, and PDF.<br><br>   * **Limits**: Individual file size ≤ 20MB; up to 5 files per upload.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Best Practices</strong>: Ensure samples are unique and contain substantial business content. Using generic templates with common industry clauses may reduce identification accuracy.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Data Privacy</strong>: The system only stores encrypted feature vectors. <strong>Original files are never saved or backed up</strong>; they are cleared from the cache immediately after the scanning process.</div><br> |
|**Manage labels** |Associate the current file fingerprint with specific tags (optional). The drop\-down list only displays tags that the current administrator has been granted. By associating tags, you can enforce permission isolation between administrators of different regions or business lines. To add or adjust the visible tag options in the drop\-down list, a super administrator must modify the **Managed tag scope** for your administrator role under **Settings** \> **Admin Access**. |


<span id="0023f3bc"></span>
### File Fingerprint Configuration


|**Setting** |**Description** |
|---|---|
|**Keywords** |These extracted keywords act as the "digital DNA" of the file. The system determines similarity based on the presence of these high\-weight word combinations.<br><br><br>* **Remove Noise**: Deselect common terms (e.g., your company name or general industry jargon) to prevent false positives.<br><br>* **Keep Core Terms**: Ensure professional terminology or unique descriptions specific to the document remain selected. |
|**Similarity Threshold** |Defines the detection sensitivity (Default: 60%).<br><br><br>* **High (80%\-90%)** : Strict matching. Only triggers when the file is nearly identical to the original. Best for official, static documents like final financial reports.<br><br>* **Medium\-Low (50%\-60%)** : Loose matching. Catches files even after restructuring or partial edits. Best for dynamic content like design drafts or code documentation.<br><br>* **Recommendation**: Start with the 60% default and adjust based on your audit results. |


<span id="558bc64e"></span>
## Managing the File Fingerprint List

On the **File Fingerprint Library** list page, you can quickly search and manage all existing fingerprint assets in the system.


|**Field** |**Description** |
|---|---|
|**File fingerprint name** |The identifier for the fingerprint asset. |
|**File fingerprint keywords** |High\-similarity terms identified by the algorithm. Hover over the field to view the full list. |
|**File fingerprint similarity** |The minimum match percentage required to trigger a detection. |
|**Action** |You can view **Details**, **Edit**, or **Delete** an asset.<br><br>*Note: Fingerprints currently used in a classification rule cannot be deleted until the association is removed.*  |


<span id="e530ee2f"></span>
## Next Steps

Once configured, you must link the fingerprint to a **Classification and Grading Rule**. By referencing the fingerprint model and assigning a data level (L1–L4), the identification logic will be applied to your file transfer control or blocking policies. For more details, see [Managing classification and grading rules](https://docs.byteplus.com/docs/sealsuite/managing-classification-and-grading-rules).
