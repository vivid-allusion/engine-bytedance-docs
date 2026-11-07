---
title: "Creating and using live templates"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/live-templates"
---

When you need to create multiple live rooms with the same or similar configurations, you can first create a live template. Then, use the template to create live rooms, which will save you from repeating complex configurations and improve work efficiency.

<span id="e17d1aaa"></span>
## Prerequisites

A BytePlus account or an IAM user with Live template \> Edit permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

<span id="8b5ad7e2"></span>
## Creating a live template


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. In the top navigation bar, click **Account center**.

3. In the left navigation bar, click **Live templates**.

4. Click **Create template** or one of the system templates to create a live template copy.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f97306f24a34539a566168d39c76202~tplv-goo7wpa0wc-image.image) </span>

5. (Optional) If you click **Create template**, refer to the table below to complete or modify the basic information of the template and click **Save**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ea63cc1dee064ce0a69cd8d3b5f51565~tplv-goo7wpa0wc-image.image) </span>

   
   |**Basic information** |**Description** |
   |---|---|
   |**Template name** |Enter the name of the template, which cannot exceed 64 characters. |
   |**Template description** |Enter the description of the template, which cannot exceed 64 characters. |
   |**Cover** |Upload the cover image for live rooms in landscape or portrait mode. |
   |**Live stream latency** |Choose the type of live stream latency.<br><br><br>* **Normal latency**: Viewers can watch the live stream with a latency of 5 to 10 seconds.<br><br>* **Ultra\-low latency**: The ultra\-low latency feature will be automatically enabled for the first live source in the live room. Viewers selecting the first live source can watch the live stream with an ultra\-low latency of 1 to 2 seconds. See [Ultra-low latency live streaming](https://docs.byteplus.com/docs/byteplus-livesaas/ultra-low-latency-live-streaming). |
   

6. Continue to configure the live template. The configurations of the live template are the same as those of a live room. For more information, search and see the corresponding documentation.

7. After saving the configurations, click **Release** in the top right corner of the page.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Up to 10 live templates can be released.   </div>
   

8. (Optional) Click **Set as default template** in the top right corner of the page to set this template as the default one under the current BytePlus account and its IAM users. When creating a live room on the console or by calling [CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2) later, the configurations of this template can be used by default.

9. (Optional) In the live template list, you can click the more icon at the bottom right of a template to release or delete it, or set it as the default template as needed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c8fc4e943bf47b2b46e7e049e9d6c8b~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Only one default template is allowed under the same BytePlus account and its IAM users at the same time.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You cannot withdraw the default template. To withdraw the template, unset it as the default template first.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After setting an unreleased template as the default template, the template will be automatically released.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The default template is displayed as the first one in the live template list.   </div>
   

10. To modify the template configurations, withdraw the template first before making changes.


<span id="d4a8f815"></span>
## Using live templates

In the following scenarios, a new live room will inherit all configurations from a specific template:


* The default template is set: A new live room will inherit all configurations from the default template.

* Only one template is released: A new live room will inherit all configurations from the released template.


If multiple templates are released and you want a new live room to inherit all configurations from a non\-default template, you can create the live room using the following steps.


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. Click **Create live room**.

3. On the **Create live room** page, you can view all the released live templates under the current BytePlus account and its IAM users. Click a target live template.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2bda37dfa274268a2504302f0bf8f20~tplv-goo7wpa0wc-image.image) </span>

4. Complete the relevant configurations and click **Save**. The new live room will inherit all configurations from the live template. You can also make corresponding changes according to business needs.
