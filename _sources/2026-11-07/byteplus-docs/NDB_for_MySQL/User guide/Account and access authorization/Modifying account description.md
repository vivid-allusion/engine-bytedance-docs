---
title: "Modifying account description"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_account_description"
---

This article describes how to modify the account description information.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance).

* An account has been created. For more information on specific operations, refer to [Creating an account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_and_deleting_accounts).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click **Accounts**.

5. On the **Accounts** tab, click the <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png)<sub> </sub></span> icon in the description column of the target account and modify the description in the pop\-up text box.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The description content length is 0~256 characters. It can contain numbers, Chinese characters, English characters, underscores (_) and hyphens (\-).   </div>
   

6. Click OK.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[ModifyDBAccountDescription](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBAccountDescription) |Call ModifyDBAccountDescription to modify the account description information. |
