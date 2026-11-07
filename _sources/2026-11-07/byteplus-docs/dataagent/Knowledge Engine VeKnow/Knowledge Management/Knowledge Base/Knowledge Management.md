---
title: "Knowledge Management"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Manage_Knowledge"
---

This article introduces how to manage the imported knowledge, configure the knowledge label and valid period, and test the effect.

# Prerequisite

You have completed the creation of the knowledge base and imported the knowledge, please refer to [Create a New Knowledge Base](https://docs.byteplus.com/docs/dataagent/Create_a_New_Knowledge_Base)and [Import Knowledge](https://docs.byteplus.com/docs/dataagent/Import_Knowledge).

# Manage Knowledge

* The knowledge base display form can switch between table view and card view.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/25ea46140aba4aca89c20f5b7c73988b~tplv-goo7wpa0wc-image.image)

* Support searching the authorized knowledge base according to keywords and precision searching the authorized knowledge according to the full text of the document.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/384294af0bc04f2a80cca12b5271f9ad~tplv-goo7wpa0wc-image.image)

* Knowledge base types are classified into generic content, Query cache, QA Q & A, and term. Different types of knowledge are managed differently.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9fb31a767a8b4e27a12cef9f84c661b5~tplv-goo7wpa0wc-image.image)

* Support setting filter conditions such as creator, update time, and creation time to filter knowledge bases.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e66e55efc294cf6907ed069b7d2627a~tplv-goo7wpa0wc-image.image)

## Generic content

Enter the generic content knowledge base, and you can configure information such as knowledge label, status and valid period on the **knowledge management** page to support batch operations.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9e74a0193f8462fbbecbffeac4da3f0~tplv-goo7wpa0wc-image.image)

|Parameter |Parameter description |
|---|---|
|Display name |1. Hover over the knowledge data name and click the edit button.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33d8e1e294204f0bb3dfb30bfc1c411e~tplv-goo7wpa0wc-image.image)<br><br>2. In the **Set knowledge display name** dialog box, set the knowledge display name.<br><br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e15b32f14f3e460ea3f5033a889a4d21~tplv-goo7wpa0wc-image.image) |
|Label Configuration |Click **Knowledge Tab Configuration** to enter Add Tab. Configuring knowledge labels can classify knowledge and improve the accuracy of knowledge retrieval. If you need to add a new knowledge label, please refer to the specific operation [Manage Knowledge Label](https://docs.byteplus.com/docs/dataagent/Manage_Knowledge#1a2acc32). |
|Enable/disable |Click **Enable/Disable** to manage the status of knowledge data, support disabling the specified knowledge data, and support re\-enabling. |
|Valid period configuration |Click **valid period configuration**, select permanent or set valid period. After the valid period is set, the knowledge will expire after 23:59:59 of the last valid date. If knowledge is not within the valid period range, it will no longer participate in the recall, but the system still saves the knowledge data. If there is a subsequent need to recall knowledge, you can modify the valid period of knowledge. |
|Move |Click **Move** to change the save path of the current knowledge. |
|Download |Click **Download** to view the download task on the **download record** page of the knowledge base, and download the file locally.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cda4792888ad4db1b3690465d0bbf603~tplv-goo7wpa0wc-image.image) |
|Delete |Click **Delete** to delete the document. |

After selecting multiple knowledge data, batch operations are supported, as shown in the figure below.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24f23986bcb544cd8228c04c5fa10634~tplv-goo7wpa0wc-image.image)

## Query Cache/QA/Term

Enter the Query cache/QA Q & A/terminology knowledge base, and support the following operations on the **knowledge management** page.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a53708837a9945eb93a62a1426dda3cb~tplv-goo7wpa0wc-image.image)

* Supports searching for knowledge by keywords.

* Support knowledge editing, enable/disable, delete operations.

* Support multi\-selection knowledge, batch deletion, enable/disable, download(support download to Excel, CSV format) operations.

   After downloading the knowledge, you need to enter the **download record** page of the knowledge base to view the download task and download the file locally.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d39fcd3167647b69418c199c070e1fa~tplv-goo7wpa0wc-image.image)

* The QA Q & A Knowledge Base supports configuration labels.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b3a730d52b846daa4f2c9867e807695~tplv-goo7wpa0wc-image.image)

   Support managing labels or adding labels on the label configuration page. For an introduction to label operations, see [Manage Knowledge Label](https://docs.byteplus.com/docs/dataagent/Manage_Knowledge#1a2acc32).

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/321bbd1a22b54c80ad917d83a9bf5806~tplv-goo7wpa0wc-image.image)

## Structured data

Enter the structured data type knowledge base, and on the **knowledge management** page, support the following management operations.

* Support for adding knowledge directories on the left.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2623804a7a5b4516bebf1ca6f0e6f9b2~tplv-goo7wpa0wc-image.image)

* In the folder, it supports setting list display fields.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/664c8754d94e49529fb170d0eb2852d3~tplv-goo7wpa0wc-image.image)

* In the knowledge list, enable/disable, move, delete, or download operations are supported for the specified knowledge.

   > **注意**

   > Once the data is deleted, it cannot be recovered. Please proceed with caution.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8615e95c18e4967be037ca4332136e3~tplv-goo7wpa0wc-image.image)

* Click to specify the name of the knowledge data to redirect to the knowledge details page. On the details page, it supports configuring table fields, manually adding data, editing existing field values, and deleting data.

   > **注意**

   > Once the data is deleted, it cannot be recovered. Please proceed with caution.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/37c0477ebc0b4ed7a56cd8fd1b6955e2~tplv-goo7wpa0wc-image.image)

# Manage Group Directory

On the left\-hand side of the knowledge management page of the knowledge base, the management group directory is supported.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aad0ea0b863747828d68a010ab41bd57~tplv-goo7wpa0wc-image.image)

The following administrative operations are supported:

|**Operation** |**Description** |
|---|---|
|New subfolder |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/348dae12d0304a29ae6b3789d90fe5f5~tplv-goo7wpa0wc-image.image) |
|Edit Folder |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/360fff3a894a46be9630e17ed63991ff~tplv-goo7wpa0wc-image.image)<br><br><br>* You can edit the folder name and folder path.<br><br>* The root directory does not support editing. |
|Delete |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1e7594b29474bef96a3db1ae47076f1~tplv-goo7wpa0wc-image.image)<br><br><br>* Once the folder is deleted, it cannot be restored. Please proceed with caution.<br><br>* The root directory does not support deletion. |

# Manage segmentation

After importing knowledge and segmenting it, you can go to the knowledge details page to manage segmentation.

1. Click on the document name to go to the knowledge segmentation details page.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/994e7e719f7746fe96a2857390a54f71~tplv-goo7wpa0wc-image.image)

2. On the **knowledge segment** details page, you can view the following information.

   * Knowledge segmentation details and support for:

      * Modify the content of the segment, including modifying the title and body (rich text editor, supports adding images, tables, bolding, underlining, ordered lists, unordered lists, withdrawing, etc.).

      * Delete the segment.

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88b29de9f761495585e75c2d8cc3c117~tplv-goo7wpa0wc-image.image)

   * View the total number of paragraphs, the total number of characters, the average number of characters in the current knowledge segment, and the ID, character, and chunk duration of each segment.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f9c4b524e3da41ed9219ae325b9b2e01~tplv-goo7wpa0wc-image.image)

   * Review the original text of the document, and click Segment to locate the matching content within the original text.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55a10322ac424bfd8234ceef6ef7991b~tplv-goo7wpa0wc-image.image)

3. Text segmentation details page, you can click **new segment** , fill in the chunk data, and add a chunk.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b0319417a804fba9b5cd36229710432~tplv-goo7wpa0wc-image.image)

4. If you are not satisfied with the current segment, you can click on the upper right corner **to re\-segment**, adjust the parameter configuration and re\-run, which will affect the subsequent retrieval accuracy after adjustment.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f4584e089127414f9f9218f12276a0c6~tplv-goo7wpa0wc-image.image)

5. Multiple segments support **merging with the next segment**.

   * When the headings of the upper and lower subparagraphs are the same, merging the subparagraphs will omit the title of the second paragraph.

   * When the headings of the upper and lower subparagraphs do not match, merging subparagraphs will merge the headings of the second paragraph into the content of the first paragraph.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a738f3565fc44e87937e95ad00a3b9c8~tplv-goo7wpa0wc-image.image)

6. Click the **Abnormal Details** tab to view the exception item, or click **Ignore** to ignore the exception item.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9cc4504b96d2436ebdc82cf9a5f5d7f8~tplv-goo7wpa0wc-image.image)

# Knowledge enhancement

Within the Common Content Type Knowledge Base details page, knowledge enhancement configuration is supported.

1. Select knowledge in the knowledge base to enter the knowledge details page, and support **knowledge enhancement** in the upper right corner of the page.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/56c5914b87114ba1928e8dbd129a0891~tplv-goo7wpa0wc-image.image)

   Knowledge enhancement supports the following capabilities:

   |**Parameter** |**Parameter description** |
   |---|---|
   |Document summary |A paragraph summarizes the document's themes and core conclusions for document\-level coarse screening. |
   |Document guide |A detailed summary of the core points of the document, such as background, findings, and conclusions, makes it easy to quickly grasp the content of the document, and is mainly used by users to browse the key information of the document. |
   |Segmented summary |Condenses the chunk core in one sentence, which is used for fast and accurate retrieval of segmentation, which can improve the accuracy of retrieval recall. |
   |Segmented key issues |The high\-frequency questions that can be answered by segmentation can enhance the semantic distance between Query and chunk, and improve the accuracy of retrieval recall. |
   |Segmented keywords |Easy\-to\-retrieve labels for keyword filtering can enhance the accuracy of retrieval recalls. |

2. After selecting the desired capability, click **Regenerate Summary** and wait for the system to complete processing to view the enhancement results.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc95567b10f2486ab1068168caa3869d~tplv-goo7wpa0wc-image.image)

# Knowledge classification

Classify different knowledge based on labeling capabilities to improve knowledge management efficiency. The current database types that support marking include generic content and QA Q & A.

## Manage Knowledge Label

Before classifying the various types of knowledge in the knowledge base, you need to configure the knowledge labels.

1. Log in to the Marketing Agent platform.

2. Enter Enterprise Knowledge Engine in the left navigation bar.

3. In the left navigation bar of the Enterprise Knowledge Engine, select **Knowledge Management** \> **Knowledge Base**.

4. Select the Knowledge Base for the generic content type and proceed to the details page.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d101e9f594e4bdf93844b5af2ab2269~tplv-goo7wpa0wc-image.image)

5. Go to the Knowledge Label management page.

   The entry description of the management page is as follows:

   * On the **Knowledge Management** tab, select the specified knowledge data, and in the **Knowledge Label column** field, click the settings icon.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a3b01056c9bd4159a8f1831b5ca84ccf~tplv-goo7wpa0wc-image.image)

   * On the **Knowledge Management** tab, select the specified knowledge data, click **Knowledge Label Configuration** in the **Operation** column, and click the **Management Knowledge Label** in the pop\-up interface.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50af3b1b719b4eb1a514857af6a4c5d7~tplv-goo7wpa0wc-image.image)

   * On the **Knowledge Label** tab, click **Automatic Marking** and click the **Manage label** in the pop\-up interface.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23129cfce0554ff0bb1feec7eaf4c67c~tplv-goo7wpa0wc-image.image)

6. On the **Management Knowledge Label** page, the following management actions are supported.

   * **New Knowledge Label**

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee4bdcfffa7f4ae1b3132e3832516271~tplv-goo7wpa0wc-image.image)

      Description of each configuration item when creating a new one:

      * **Knowledge label name:**  Required, custom name, identifies the current label.

      * **Value Type:**  Required.

         * **Single\-value text:**  Only one value can be selected for subsequent marking.

         * **Multi\-Valued Text:**  Multiple values can be selected for subsequent marking.

      * **Label value:**  Required, sets the value of the current label, supports setting multiple, separated by commas, spaces or newlines.

      * **Knowledge label description:**  Optional, the description information of the current label, such as purpose, rules, etc.

   * **Delete knowledge label**

      In the list of knowledge labels, it is supported to remove labels that are no longer needed.

      > **注意**

      > Once the label is deleted, it cannot be recovered. Please proceed with caution.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/751465544a9743d8b6b913e2f5ab659f~tplv-goo7wpa0wc-image.image)

## Automatic marking

Once the labels are built, the Enterprise Knowledge Engine supports automatic marking of knowledge.

1. Log in to the Marketing Agent platform.

2. Enter Enterprise Knowledge Engine in the left navigation bar.

3. In the left navigation bar of the Enterprise Knowledge Engine, select **Knowledge Management** \> **Knowledge Base**.

4. Select the Knowledge Base for the generic content type and proceed to the details page.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e669ba6af36e41c4a759f8b0ae62015d~tplv-goo7wpa0wc-image.image)

5. Select the **Knowledge Label** tab and click **Automatic Marking**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f414317b000a4531b50e2284c00a7f05~tplv-goo7wpa0wc-image.image)

6. On the Automatic Marking Configuration page, complete the following configuration and click **Start Marking**.

   1. Please be sure to read the **marking logic description**.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e4a6d104b264ee3be9f7be46de5b11e~tplv-goo7wpa0wc-image.image)

   2. In the **Added** list, add one or more labels.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa4199ab9583426c96a6c70a6eb77965~tplv-goo7wpa0wc-image.image)

   3. Configure the following switches.

      * Turn on **historical knowledge automatically matches the above label** switch. After turning on, the system will automatically mark historical knowledge.

      * Turn on **new knowledge automatically matches the above label** switch. After turning on, the system will automatically mark each new knowledge.

7. In the label list, view the labeling of labels and label values.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a96265a4ac7f4da298d29dc56c1074b9~tplv-goo7wpa0wc-image.image)

## Manual marking

You can add labels to the specified knowledge data.

1. Log in to the Marketing Agent platform.

2. Enter Enterprise Knowledge Engine in the left navigation bar.

3. In the left navigation bar of the Enterprise Knowledge Engine, select **Knowledge Management** \> **Knowledge Base**.

4. Select the Knowledge Base for the generic content type and proceed to the details page.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00dc73bb39c14f6db4b78230e3a7314a~tplv-goo7wpa0wc-image.image)

5. On the **Knowledge Management** tab, find the knowledge data that needs to be marked, and in the **Operation** column click **Knowledge Label Configuration**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c00402ea682f4d1690b5ae650c0a2b1d~tplv-goo7wpa0wc-image.image)

6. In the knowledge label configuration that pops up on the right, click **Add knowledge label**, select label and label value, and support adding multiple labels.

   > **说明**

   > In the Added Knowledge Label \*\*Operation \*\*column, support for removing labels that are no longer needed.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ecf08f792ee41e19cc05acc34c8e917~tplv-goo7wpa0wc-image.image)

7. Click **Save** in the lower right corner of the page.

   After saving, the label information of the knowledge data can be viewed in the list.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94e072a5b9984d19bf276a3bbfcf8b2c~tplv-goo7wpa0wc-image.image)

# Manage version

In the knowledge base of common content type, if the same knowledge data is updated, the knowledge data can be iterated through version management.

1. Go to a generic content type knowledge base details page.

2. On the **Knowledge Management** tab, find the knowledge data you need to manage versions of, and select **More** \> **Version Management** in the **Operation** column.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59a5c2be76f24a92bd08b0f1a0c33724~tplv-goo7wpa0wc-image.image)

3. On the **Version Management** page, view and configure version parameters.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62df7f3ff818464bb04aac8fdd1af22d~tplv-goo7wpa0wc-image.image)

   * View version number information, including version name, creator, and version number rules, which support manual settings.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f4f0c657cff429db91774cccdc2d446~tplv-goo7wpa0wc-image.image)

   * Set **version Add type**:

      * **New version number:**  When a new version is added, historical version data is preserved and a new version is generated.

      * **Overwrite the original document:**  When a new version is added, the historical version data is directly replaced, and the historical version is not retained.

4. For knowledge added for the first time, the default version number is V1. Click **Add new version** and complete the following configuration to upload new version knowledge.

   * **Version date:**  System default fill date, support custom modification.

   * **Sharding Settings**:

      * **Synchronize the original version configuration:**  The knowledge segmentation settings are consistent with the original version configuration.

      * **Automatic sharding settings:**  Segment using the system's default automatic segmentation rules.

   * **Import Knowledge Selection:**  Import local files into the platform as new version knowledge.

5. When the configuration is complete, click **OK**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6943e8bace844b888701231342eb58ad~tplv-goo7wpa0wc-image.image)

6. Wait for the new version of knowledge to be uploaded and parsed. You can view the new version of knowledge in the version list.

   The version number and addition method will be implemented according to your configuration in version management. If it is a new version number, the latest version of knowledge is enabled by default, and manual switching to enable other versions of knowledge is supported. The same knowledge only supports enabling one version number.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33942245cc0640a69a4579f4e997869c~tplv-goo7wpa0wc-image.image)

7. (Optional) Manual deletion is supported for versions that are not in effect.

   > **注意**

   > It cannot be restored after deletion, please proceed with caution.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8899e154d4d477e82707d05ad611fcf~tplv-goo7wpa0wc-image.image)

# View run record

In the **run record** page of the knowledge base, the details of the knowledge import task are supported.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a5491d8f3c545a9a350624a09ab418d~tplv-goo7wpa0wc-image.image)

* The list displays information such as task name, task source, update method, status, and running time.

* Hover the mouse to the percentage of progress in the **status** column to view progress details.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70328332f1e3402faedfbe55285b87a4~tplv-goo7wpa0wc-image.image)

* For the tasks which **update method** is **automatically updated**, support in the **operation** column view running details, running logs, and manual operation.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/769ed8bd89b240f98c50a91a9c547fac~tplv-goo7wpa0wc-image.image)
