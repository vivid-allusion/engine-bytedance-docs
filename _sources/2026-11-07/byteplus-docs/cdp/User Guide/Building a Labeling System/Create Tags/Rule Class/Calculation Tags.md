---
title: "Calculation Tags"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Calculation_Tags"
---

<span id="_1-产品概述"></span>
# 1. **Product Overview**

Supports the creation of calculation tags, allowing users to create new tags based on existing tags for secondary calculations.

<span id="c3ec1a62"></span>
# 2. **Common Use Cases**


1. Dynamic Amount Proportion, calculated as follows: Dynamic Amount Proportion = Loan Amount / Credit Amount (Loan and Credit are existing tag events)

2. Shopping Intent, obtains a total score by summing scores from multiple tags and then stratifies the scores.


<span id="8f11a39b"></span>
# 3. **Operating Steps**

Go to the **Labeling System** module, click the **Create New Tag** button, select **Calculation Tags** to access this functional module.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_426417d4acf9e5a9dd5ebd91ebe66eda.png) </span>

<span id="56ba7f79"></span>
## **3.1 Configure Basic Information**


* Tag Name: The name of the new tag (up to 100 characters; tag names cannot be the same within the same project)

* Path: Select the folder category for the tag


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Create a new tag \- the path involves two switches:</div>



1. <div data-tips="true" data-tips-type="tip">Group switch: In the Project Center \- Group Configuration \- Functional Configuration, there is a <strong>tag directory access control</strong> switch, which is off by default. When turned on, strict permission control over "directory" will be applied when creating tags, allowing only users with no <strong>label tree editing</strong> permission to place them in "Uncategorized."</div>


2. <div data-tips="true" data-tips-type="tip">Module switch: After turning on the <strong>tag directory access control</strong> switch, users without <strong>label tree editing</strong> permission will default to the "Uncategorized" path when <strong>creating a new tag</strong> (project administrators can authorize users in Project Center\-<strong>Authorization</strong>).</div>


* Input tag description for reference

* Calculation Type: offline calculation or real\-time calculation

* Update type: Optional scheduled updates or manual updates

* Frequency of Execution: When scheduled updates are necessary, both the update frequency and time must be set to support daily/weekly/monthly synchronization.

* Calculation result storage rule: When updating regularly, you can set the number of historical versions to retain and exceed the limit will be deleted the next day.

   * If you choose **unlimited quantity** here, it will follow the [标签系统表TTL长度](https://docs.byteplus.com/docs/undefined/66cd3eaa66e3df0303ac680e#_3-4-%E6%A0%87%E7%AD%BE%E7%B3%BB%E7%BB%9F%E8%A1%A8ttl%E9%95%BF%E5%BA%A6)configuration in the group settings

   * If **customized TTL** is selected here, the number of recently reserved versions set here will be followed (when the single tag's **customized TTL** exceeds the TTL length of the enterprise's tag system table, the TTL length of the enterprise's tag system table will prevail);


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">TTL (Time To Live): Data lifespan, meaning the time to make the stored data invalid.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d857871b15c24ca68b9d713b8c5feded~tplv-goo7wpa0wc-image.image) </span>

After completing the basic information configuration, click Next to select fields.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3fead223ced19f9bcc4ab60eddda4d08.png) </span>

<span id="b882f00c"></span>
## 3.2 Selecting Fields


1. Click the **add** button to either select only the tag, just the attribute, or both the tag and the attribute. After completion, click the **OK** button.

   1. When selecting attributes, ensure that the attribute fields are all from the same attribute table.

   2. You can choose up to 10 fields for tags and attributes.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7847ebc6000daa58bc7deaee88967012.png) </span>


2. Click the **Assign** button on the right side of the field, configure the corresponding numerical calculation standard, and click the **OK** button after completion.

   1. Text Type: Displays all tag values in a flat layout.

   2. Numeric Type: Segmented/uses the original numeric values, which can be modified by the user.

   3. Date and Time Type: Segmented/Use the original numerical value, which users can modify, assign values in order, such as 10 points in the last 6 months, 40 points in the last 1 month


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_750d4bdc158a44d899aa6fae1e977ba9.png) </span>

<span id="0215f593"></span>
## **3.3 Editing Expressions**


1. Click on the selected tags and arithmetic operators to generate an operation tag expression.

* The system supports addition (+), subtraction (\-), multiplication (\*), and division (/) operations, and provides bracket support for users to nest more complex operations;

* Users can complete expressions by selecting tags and operators at intersections;

* Users can also directly input arithmetic operators into the editing box using the keyboard to complete the tag expression.

* Operational tags support decimal calculations.

> Application Scenario Example: Proportional calculation:

> Scenario Description: Calculate the user's proportion, the ratio of the loan amount to the credit amount.

> Solution: Now you can calculate the proportion after the decimal point more accurately. For example, the loan amount is 1500.50 yuan, the credit amount is 2000 yuan, the proportion = 1500.50 / 2000 = 0.75025.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eae692fc720340eebc4907870f2e0eeb~tplv-goo7wpa0wc-image.image) </span>


2. Support users to set upper and lower limits for the values and results of tags involved in operations, this setting is optional.

* Result Value of the Operation Tag: Limit the upper and lower limits of the **result value** of this operational tag.

* Field Value Settings: Limit the upper and lower values of the **tags involved in the calculation**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f19f8d840b942168395941e0384a74a~tplv-goo7wpa0wc-image.image) </span>


* Value Acquisition Method:

   When the field involved in the calculation is empty, the value acquisition method is:

   **Assign 0**: For instance, in addition or subtraction operations, an empty field should not result in an empty result.

   **Discard**: For example, in multiplication or division operations, if the denominator is empty, it will cause a calculation error, so it is recommended to discard it.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b37c082cec144c28b2a33bec4f734e4b~tplv-goo7wpa0wc-image.image" width="815px" />   </div>
   

3. Operation Display Settings

* Divided by Statistical Values: Display label calculation results according to the actual calculation result enumeration values.

* Divided by Numerical Intervals: Display label calculation results based on the set numerical intervals.

   * During initial configuration, support setting infinite intervals of [\-∞, empty], [empty, +∞]; when the infinite intervals are deleted, these default interval values can be automatically restored by clicking the add layer operation.

   * Names in the hierarchical column cannot be duplicated


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/29e35f023fd94e268c232e7e7a9391a3~tplv-goo7wpa0wc-image.image) </span>

<span id="01b64bb5"></span>
## **3.4 View Tag Details**

Click to preview the estimated number of people and calculate the tag results. If everything is set correctly, click **Complete Creation** to finish creating the current tag.

You can view the current tag's distribution of people, historical details, and operation records on the tag details page.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_76e93619eb71797123b2131abff52b4d.png) </span>

<span id="21b2ac85"></span>
## 3.5 Calculation Tag Assignment Logic

When a user is not labeled in any **arbitrary** field (tag/attribute) (i.e., the corresponding value is null), the final calculation result for that user will be null.

**Application Scenarios**


* **If the calculated tag C=Tag A (age) \* Tag B (total platform visits in 30 days)** 

   * **Little John**: A=10 years old, B=2, calculation result C=20

   * **Little Jane**: A (null), B=1, calculation result C=null

   * Xiao Bing: A=2 years old, B(null), operation result C=null


When editing in the expression interface, if the user calculates that any selected field is not labeled (i.e., the corresponding value is null), the final output result for the user will be null.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a399166de00250ebbd46863bec78d7cd.png) </span>
