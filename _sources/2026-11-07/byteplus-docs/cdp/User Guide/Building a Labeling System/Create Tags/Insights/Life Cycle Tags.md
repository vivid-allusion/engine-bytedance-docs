---
title: "Life Cycle Tags"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Life_Cycle_Tags"
---

<span id="_1-产品概述"></span>
# 1. Product Overview

Lifecycle tags are efficient marketing models provided to users by CDP, including common models such as the AIPL model and the 5A model.

In this function module, companies can flexibly create lifecycle tags, gain insights into user lifecycles based on model tags, develop marketing strategies, enhance brand awareness and interest among users, then export crowd packages based on user stages for refined operations, promote user purchase decisions, and continuously improve user brand loyalty.

<span id="_2-名词解释"></span>
# 2. Term Explanation

<span id="_2-1-aipl模型"></span>
## **2.1 AIPL Model** is a means of quantifying and operating brand audience assets in a linked manner.


* A (Awareness): Represents the brand\-aware audience, generally referring to the audience that passively interacts with the brand, such as those reached by brand advertising and those searching for category keywords.

* I (Interest): Represents the brand's interested audience, generally referring to the audience actively engaging with the brand. For example, those who click on ads, browse the brand/store homepage, participate in brand interactions, view product details, search for brand keywords, claim trials, subscribe/follow/join, and add items to the cart or favorites.

* P（Purchase）: Represents the group of people who purchased the brand, including those who have made a purchase.

* L (Loyalty): Represents the brand loyalists, such as those who have repurchased or given positive feedback and shared about the brand within the purchasing group.


<span id="_2-2-5a模型"></span>
## 2.2 5A Model

The 5A model is a marketing model proposed by marketing master Philip Kotler in "Marketing 4.0".


* A1 Aware: Refers to customers passively receiving information, such as brand advertising exposure and category keyword searches.

* A2 Appeal: refers to customers who increase their brand impression, such as those who click on ads, engage in brand interactions, browse product detail pages, and search for brand keywords.

* A3 (Ask): Refers to customers who are driven by curiosity to proactively search for information, such as guiding the number of people entering the store.

* A4 Act: Refers to customers who take action, such as collecting, purchasing, as well as those who use and receive after\-sales services after purchasing.

* A5 (Advocate): Refers to customers who are loyal to the brand and promote it, such as becoming fans.


<span id="_3-操作步骤"></span>
# Step 3. Operating Steps


|Process |Explanation |Operating documents |
|---|---|---|
|Step one |Create user lifecycle model tags, such as AIPL, 5A, and other model tags |[Lifecycle tags](https://www.volcengine.com/docs/7139/191750#_3-1-%E5%88%9B%E5%BB%BA%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E6%A0%87%E7%AD%BE%EF%BC%88%E4%BB%A5aipl%E4%B8%BA%E4%BE%8B%EF%BC%89) |
|Step two |Insights into user lifecycle based on model tags |[Life Cycle Analysis](https://www.volcengine.com/docs/7139/191784) |
|The third step |Exporting audience packages according to user stage for refined operations |/ |


Below, we will use the AIPL tag as an example to explain the actual functions based on user operations:

<span id="_3-1-创建生命周期标签（以aipl为例）"></span>
## 3.1 Create a Lifecycle Tag (Using AIPL as an Example)

**Step 1**: Go to the **Tagging System** module, click on the **Create New Tag** button, select **Lifecycle Tag** to enter this functional module.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_26947a8ff783ea695b3a2eb30354b049.png) </span>

**Step 2**: Configure basic information.


* Tag Name: The name of the new tag (up to 100 characters; under the same project, tag names cannot be repeated)

* Path: Select the folder category where the tag is located.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A new tag has been created \- the path involves two switches:</div>



1. <div data-tips="true" data-tips-type="tip">Group Switch: In the Project Center \- Group Configuration \- Function Configuration, there is a switch for <strong>Tag Catalog Permission Control</strong>, which is off by default. When turned on, strict permission control will be applied to "catalog" when creating tags, allowing only those without <strong>Tag Tree Editing</strong> permission to place tags under "Uncategorized".</div>


   <div data-tips="true" data-tips-type="tip">2）Module switch: Tag Directory Access Control switch, when turned on, users without Edit Tag Tree permissions will default to the "Uncategorized" path when creating a new tag (project administrators can authorize users in Project Center\-Permissions).   </div>
   

* Description: Enter a tag description for reference by other tag users.

* Calculation Type: Choose between Offline Calculation or Real\-time Calculation.

* Update Type: Choose between Scheduled Update or Manual Update.

* Update frequency: When scheduled updates are required, set the update frequency and time, supporting daily/weekly/monthly synchronization.

* Storage rule for calculation results: When scheduled updates are enabled, you can set the number of historical versions to retain. Excess versions beyond the limit will be deleted the next day.

   * If you select **unlimited quantity** here, it will follow the configuration in the group [标签系统表TTL长度](https://docs.byteplus.com/docs/undefined/672484e558c46e0316c8988a).

   * If you choose **custom TTL** here, it will follow the number of recent versions to retain (when the **custom TTL** for a single tag exceeds the TTL length of the group's tag system table, the group's tag system table TTL length will apply)；


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">TTL (Time To Live): The data lifecycle, which refers to the time that data stored becomes invalid;</div>


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ac602783a699e4e922c5cde835ba753f.png) </span>

**Step Three:**  Select the type of model to create, taking the AIPL model as an example;

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_d1fc1b298d780b7dfcb62b3b01732bbd) </span>

**Step Four:**  Configure information for each stage of labels. Display default awareness, interest, purchase, and loyalty label values.


* At the position shown in 1, users can construct rules for this stage by adding tags, behaviors, detailed data, and user data under each tag value.

* At the position shown in 2, users can rename, copy, or delete the current tag values.

* At the position shown in 3, users can add new tag values as needed.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Number limit: A maximum of eight tag value rules can be added</div>


* <div data-tips="true" data-tips-type="tip">Tag value name: Does not support English single quotes', English double quotes'', English parentheses(), English ellipses`</div>



<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ca41ca228ddf45a9d33d58b33ec71d00.png) </span>

Step 5: Click "Estimated Number" in the upper right corner to view the number of people covered in each stage; click "Create Completed" to generate an AIPL lifecycle tag.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_56e1c07fe4cbf41ed97f5c7034bb6b52) </span>

Step 6: You can view tag details on the redirected tag page.


* At the location shown in 1, you can preview the tag page, including tag distribution (showing the number of people in different tag value partitions under the latest time zone), tag history details (showing the trend of people distribution for the selected time period under the tag), and tag rules.

* At the location shown in 2, you can view tag operation records, showing detailed current tag operation records within a specific date range, including date, operation status, duration, etc., supporting batch operation.

* At the location shown in 3, you can authorize the tag to other members under the project.

* At the location shown in 4, you can jump to the User Insight module to gain insights into the user lifecycle based on model tags.

* At the location shown in 5, you can re\-edit the rules of this tag.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_80f3cd6374e429ae98efceb5f6ecdb15.png) </span>

<span id="_3-2-洞察用户生命周期"></span>
## 3.2 Insight into User Lifecycle

Click **Analyze Insight\> Lifecycle Analysis** or **Life Cycle Analysis** on the Lifecycle Tag page to enter this module.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_66d81bff52b96534efc65aa32041a0ce.png) </span>Click to view detailed operation instructions on [Life Cycle Analysis](https://www.volcengine.com/docs/7139/191784)
