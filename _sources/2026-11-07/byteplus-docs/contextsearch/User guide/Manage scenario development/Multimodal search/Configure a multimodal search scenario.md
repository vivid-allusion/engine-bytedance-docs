---
title: "Configure a multimodal search scenario"
product: "ContextSearch"
product_code: "contextsearch"
source: "https://docs.byteplus.com/en/docs/contextsearch/Configure_a_multimodal_search_scenario"
---

After completing the initialization of a multimodal search scenario, you can further configure scenario capabilities according to business needs, add files in the knowledge center, and verify scenario effects through the conversation feature. This topic describes how to configure multimodal search scenarios.

## Prerequisites

Created and initialized multimodal search scenarios. For detailed operations, see [Create a scenario](https://docs.byteplus.com/en/docs/contextsearch/Create_a_scenario) and [Initialize a multimodal search scenario](https://docs.byteplus.com/en/docs/contextsearch/Initialize_an_Agentic_Search_scenario).

## Procedure

### Scenario conversation

1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. In the left navigation pane, select **My Scene**, then click the target multimodal search scenario.

4. Select the operation mode from the dropdown menu to the left of the input box at the bottom.

   * Search: enter your question or upload an image in the dialog box, then click the send button. The system outputs results based on your configured knowledge center. For more actions regarding the knowledge center, refer to the following chapters.

   * Build: generate or configure a multimodal search scenario using natural language description (e.g., enter "help me generate a multimodal search scenario"), then click the send button. The system automatically completes the scenario build; you can view and manage the generated artifacts in the **Scene artifact** panel. For more actions regarding scene artifacts, refer to the following chapters.

### View and manage scene artifacts

The scene artifact panel centrally displays the dist artifact package generated after completing the current multimodal search scenario build.

1. Click on the right![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_90447d6097eb14aa598752950bf745f9.png)Click the icon to open the **Scene artifact** panel, which presents the complete project structure and source list in a file tree format.

2. Click any artifact package to preview its content online.

3. After confirming, click **Deploy immediately** to release the artifact to the runtime environment.

> **tip**

> After deploying a new artifact, previously deployed artifacts of the current scene will go offline and be archived.

### Add files to the knowledge center

The knowledge center manages data resources for multimodal search scenes in one place. You can upload text, pictures, and other files as knowledge data. The system parses and indexes the files to support later retrieval.

1. Click the![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_77957c2465a295f7c4c33f66bd77ad27.png) icon to open the **Scene configuration** panel, then select the **Knowledge center** tab.

2. Click **Add file** in the top right of the Knowledge center area, then choose **Local upload**, **Feishu upload**, **TOS upload**, or **API upload** as needed.

   **Local upload**

In the **Local upload** dialog, click the upload area to select files to upload or drag files to the upload area, then click **confirm**.

   > **tip**

   * > Supported file formats include PDF, TXT, DOC, DOCX, MD, HTML, PNG, JPEG, and JPG.

   * > The size of a single file must not exceed 100 MB.

   * > You can upload up to 50 files at a time.

   **Feishu upload**

1. In the **Feishu upload** dialog, select the target Feishu data source type from the **Data source** dropdown list. If a new data source is needed, click **Create a data source**. For detailed steps, refer to adding a data source.

   2. Select **I have carefully read and agree Authorization requirements**, then click **To authorize**.

   3. Authorize the Feishu data source to import on the pop\-up authorization page, then click **Import**.

   **TOS upload**

In the **TOS upload** dialog, enter the TOS address of the file to add, then click **Confirm**.

   > **tip**

   * > Only addresses starting with tos:// are supported.

   * > To upload multiple files, separate multiple addresses with spaces or line breaks.

   **API upload**

See [Adding TOS files via API](https://docs.byteplus.com/en/docs/contextsearch/Add_TOS_files_through_the_API).

#### Subsequent operations

* You can click **Task center** in the top right of the **Knowledge center** area to view file information and processing status.

* You can click the delete icon under the **Actions** column to remove added files.

* You can click **Slices** in the **Knowledge Center** area to view file slices after parsing.
