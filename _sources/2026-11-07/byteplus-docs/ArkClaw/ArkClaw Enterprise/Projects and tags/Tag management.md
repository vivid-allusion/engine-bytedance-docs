---
title: "Tag management"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Tag_management"
---

As the number of ArkClaw instances continuously increases, management becomes more difficult. In this case, you can add different tags to Claw instances of different types and employees to identify and categorize employee Claw instances and shared Claw instances. A tag consists of a key\-value pair. You can use tags to categorize and aggregate Claw instances from different dimensions. This is suitable for batch filtering and management of Claw instances.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">By default, IAM users have no permission to use the tagging feature. For IAM users who need to use the tagging feature, contact the root user. The root user will create a custom policy and attach it to the IAM users. For more information, see <a href="https://docs.byteplus.com/en/docs/6257/1158323">Creating custom policies</a> and <a href="https://docs.byteplus.com/en/docs/6257/94013">Granting permissions to IAM users</a>.</div>


<span id="izcNlVCR"></span>
## Tag type


* **System tag**: Tags automatically added to resources are system tags. System tags usually start with `volc:` or `sys:`. They can only be viewed and cannot be edited.

* **Custom tag**: Tags manually added by users to resources are called custom tags. Custom tags cannot start with `volc:` or `sys:` in any case.


<span id="nuODcRNk"></span>
## Usage notes


* All tags in ArkClaw are **custom tags**. You can add tags to employee Claw instances and shared Claw instances in ArkClaw.

* If the tag key that you want to associate with the Claw instance is the same as an existing tag key, the new tag value overrides the original value. Proceed with caution.

* A tag consists of a tag key (Key) and a tag value (Value), both of which are case\-sensitive. Value can be empty.

* Keys of multiple tags for the same resource must be unique, and each Key can have only one Value.

* You can add up to 20 tags each time and up to 50 tags to a Claw instance.


<span id="QQffWfBb"></span>
## Tag principles

When associating tags with Claw instances, refer to the following guidelines to create tags.


* **Comprehensive plan**

   This principle means that when planning resources, you need to plan tags comprehensively (with priority given to the design of tag keys). Then, associate the planned tag keys and their corresponding tag values with resources. This helps you group and retrieve resources by tag subsequently.

* **Mutual exclusion**

   This principle means that using two or more tag keys for the same attribute should be avoided. For example, if you use `key=owner` to mark a resource owner, do not use other tag keys with the same meaning (such as own, belonger, or the Chinese term "Owner").

* **Simplified design**

   This principle means the simplified use of tag keys. When you plan tags, use tag keys with fixed dimensions. This reduces errors during operations due to an excessive number of tag keys.

* **Limited value**

   This principle mainly applies to the design of tag values. Remove redundant tag values from resources and retain only core ones. This helps to simplify processes, such as resource management, access control, and automatic O&M.

* **Consider future changes**

   Changing tags may cause changes in tag\-based processes, such as resource management, access control, and automatic O&M. When you plan tags, consider the impact of adding or removing tag values on existing processes in future work to change tags more flexibly.


<span id="VQcRIia5"></span>
## Manage tags

<span id="CrlbsAaQ"></span>
### **Associating or dissociating tags for a Claw instance**


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation bar, click "Claw Management \> Claws".

3. On the "Claws" page, you can view the list of Claw instances that enterprise employees have created.

4. In the "Tag" column that corresponds to the target Claw instance, click<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_90b3301bba3246a37a6cfdbb72efa16a.png) </span>.

5. In the "Edit tag" dialog box, associate tags with or dissociate tags from the Claw instance as needed.

   * **Associate tag**: Click "Add tag". Specify the key\-value pair of the tag, and then click "Confirm".

   * **Dissociate tag**: Next to an existing tag, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_82b6c404d7ab7b58a5a99165a0727444.png) </span>icon and then click "Confirm".

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">A single Claw instance can be associated with up to 20 tags.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Tag keys and values are case\-sensitive. In addition, tag keys cannot start with <code>volc:</code> or <code>sys:</code> in any case. Tag values can be empty.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When you associate multiple tags with the same Claw instance, each tag key must be unique, and can have only one value.   </div>
   

6. Return to the "Claws" page. Hover the pointer over the tag icon of the target Claw instance to view all tags associated with the instance.


<span id="Von1Tt3J"></span>
### Associating or dissociating tags for multiple Claw instances


1. On the "Claws" page, select multiple instances.

2. Click `...` \> "Associate tag" or "Disassociate tag" in the lower\-left corner.

4. Add the tags to be associated or disassociated, and click "Confirm".

   * **Batch associate tags**: In the pop\-up window, click "Add tag" and specify custom tag keys and values.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the "Key" of the newly associated tag matches an existing tag "Key" of the selected instance, the new tag "Value" will override the original one. Exercise caution when performing this operation. You can add up to 20 tags at a time.   </div>
   

   * **Batch dissociate tags**: Click "Add the tag key to be dissociated" in the pop\-up window, and enter the tag key. The system will display the number of Claw instances matched by the tag key.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Enter the tag "Key" you want to disassociate. All tags with the tag "Key" will be disassociated. Exercise caution when performing this operation. You can disassociate up to 20 tag keys at a time.   </div>
   

<span id="FcNbUXdg"></span>
### Filter Claw instances by tag


1. In the "Tag" column that corresponds to the target Claw instance, click<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8213f9608913fdf429fcf33dcd6db887.png) </span>.

2. In the pop\-up window, click "Add tag". Enter the target tags and then click "Confirm" to filter Claw instances.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You can add up to 10 tags when using tags to filter Claw instances.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you add multiple tags to filter Claw instances, the AND logic applies. This means only resources associated with all tags are returned​.   </div>
