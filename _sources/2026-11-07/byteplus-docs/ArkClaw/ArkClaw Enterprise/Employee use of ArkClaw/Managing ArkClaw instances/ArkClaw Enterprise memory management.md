---
title: "ArkClaw Enterprise memory management"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_Enterprise_memory_management__"
---

ArkClaw supports a visualized memory management feature that is based on LanceDB, providing you with more accurate memory storage, retrieval, and application solutions. You can access the **memory management ** feature from the **Settings** sidebar in the upper right corner of the ArkClaw console. This topic describes the overall capabilities of memory management and how to use **daily memory ** and **long\-term memory**.

<span id="5s6LSc4H"></span>
# Feature overview

**Memory management** is a set of capabilities provided by ArkClaw for automatically generating, viewing, and maintaining conversation memory. It centrally stores important information, preferences, and decisions accumulated during your use of ArkClaw, making subsequent conversations more closely aligned with your actual needs.


<card mode="container" href="" img="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d41a9889e8a7747e5c146aef0e51f215.png" iconSet="1" icon="" horizontal="0" iconSize="" >

LanceDB\\-based storage and retrieval


* All memories are centrally stored in a LanceDB vector database for more accurate retrieval and reference when needed.

* With LanceDB, the system can search memories by keyword or retrieve them through semantic association. This ensures higher relevance even for complex queries.

</card>




<card mode="container" href="" iconSet="1" iconSize="" icon="" horizontal="0" img="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_534cbaa148ec9f7ad39011fd8e3b5d2e.png" >

Daily memory and long\\-term memory

The memory management feature supports two types of memory, allowing you to manage your conversation memories at two levels: daily summaries and long\\-term memory assets.


* **Daily memory**: The system automatically saves these memories by date ** and ** records the highlights of your daily conversations with ArkClaw **.** 

   * The system automatically generates daily memories, and you cannot add them manually. Each daily memory is limited to 2,000 characters. Any content exceeding this limit is not displayed.

   * To maintain content accuracy and privacy compliance, you can view, edit, and delete existing daily memories in the list.

* **Long\\-term memory**: The system retains these memories long\\-term by topic and allows you to back up and restore them.

   * Five major long\\-term memory categories are preset, including behavioral preference, business common sense, decision\\-making reference, core project, and inspiration fragments. During persistence, the model automatically identifies and categorizes the memory based on its content.

   * You can manage long\\-term memories by editing, deleting, backing up, and restoring them.

</card>



You can access the **Memory management ** page via the **Settings ** sidebar on the right side of the ArkClaw console. This feature allows you to centrally view and manage the memory for the current ArkClaw instance. If you have enabled ArkClaw in Feishu, you can also configure a **Memory management ** quick entry in the lower left corner of the chat box for easy access at any time during a conversation.

<span id="qgQPXZYo"></span>
# Daily memory

**Daily memory** automatically records the highlights of your daily conversations with ArkClaw. The system automatically summarizes conversations when the conversation reaches a certain length or pauses for a period of time. This enables valuable information to be stored in the daily memory without manual intervention.

<span id="yYCYlHkl"></span>
## View daily memory


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter to access the ArkClaw conversation page.

2. Click the "Settings" button in the upper\-right corner of the page, then click the "Memory management" button in the Settings section.

3. Click the "Daily memory" option, locate the specific date in the list, and view the daily memory details.


<span id="sqACJTBk"></span>
## Edit daily memory

Click the Edit icon in the daily memory list, modify the content on the details page, and save your changes. This causes the original memory to be immediately overwritten.

<span id="ltp62DmS"></span>
## Delete daily memory

To delete a specific daily memory, click ** Delete** on the corresponding item or details page. The deleted content will no longer be used for searches and answers in subsequent conversations.

<span id="xfNX7P4I"></span>
# Long\-term memory

**Long\-term memory** is used to save information that remains valuable over an extended period across multiple sessions, such as your common workflows, important project backgrounds, or fixed preferences. Unlike daily memories archived by day, long\-term memory focuses more on stable knowledge and patterns, making it suitable as a prioritized "knowledge base" when ArkClaw answers questions.


* Five major long\-term memory categories are preset by the system, including behavioral preference, business common sense, decision\-making reference, core project, and inspiration fragments. During persistence, the model automatically identifies and categorizes the memory based on its content.

* You can switch to the **Long\-term memory ** tab on the **Memory management ** page to view all long\-term memory items. After selecting an item, you can add, edit, or delete memories in the details section.


<span id="kVBCNX1f"></span>
## View long\-term memory


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter to access the ArkClaw conversation page.

2. Click the "Settings" button in the upper\-right corner of the page, then click the "Memory management" button in the Settings section.

     &nbsp;

3. Click "Long\-term memory" and select the category you want to view. You can then view the long\-term memory list under the corresponding category.

   <div style="text-align: center">
      </div>
   


<span id="sXo3rwdq"></span>
## Add new long\-term memory


1. In the Long\-term memory section, click "Memory operation", and then click "Add memory" in the pop\-up box.

2. Select the corresponding memory type, edit the content, and then click Confirm. The new memory is displayed in the long\-term memory list.


<span id="ka6Zwk5n"></span>
## Edit long\-term memory

Click the Edit icon in the long\-term memory list to edit the memory content. After clicking Confirm, the modified content will be saved immediately.

<span id="S8tUzKuL"></span>
## Delete long\-term memory

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Once you delete a memory, the operation takes effect immediately and is irreversible. Proceed with caution.</div>


Click the Delete icon in the long\-term memory list to delete the corresponding memory.

<span id="Rcy6f3PR"></span>
## Backup and restoration

To prevent important memories from being lost due to accidental deletion or large\-scale adjustments, long\-term memory supports backups and restoration.

<span id="JOCgdPEl"></span>
### Memory backup


1. In the upper right corner of the Long\-term memory section, click "Memory operation", and then click "Back up memory" in the pop\-up box.

   Then, you can view the current backup list. The update time indicates when the memory in each backup version was last updated.

2. Click the "Create backup" button to back up the long\-term memory for the current ArkClaw instance.

3. Click the "Details" button to view the long\-term memory content stored in each backup version.


<span id="kdrOBr6h"></span>
### Memory restoration

Select "Memory operation \> Back up memory" to access the backup list and view historical backups in chronological order. You can click "Restore" on a specific backup to revert the current long\-term memory to that version.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Restoring a backup causes the current long\-term memory to be overwritten. Ensure that you have backed up your current memory before confirming the restoration, preventing it from being lost after restoration.</div>
