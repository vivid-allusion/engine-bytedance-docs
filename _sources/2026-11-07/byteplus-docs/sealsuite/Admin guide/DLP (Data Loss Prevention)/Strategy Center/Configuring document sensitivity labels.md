---
title: "Configuring document sensitivity labels"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configuring-document-sensitivity-labels"
---

To prevent accidental data leaks due to a lack of awareness, you can visually tag files on employee devices with sensitivity labels. This guide shows you how to enable and configure the file labeling feature, including setting the policy scope and customizing the label icons for Windows, macOS, and Linux.

 &nbsp;

<span id="important-notices"></span>
## Important Notices

Before enabling this feature, read and evaluate the following risks and compatibility requirements:


* Once enabled, this feature will automatically apply sensitivity labels to all relevant files on user devices within the policy's scope. Employees will see these labels, and on macOS, the "Finder Extensions" permission will be automatically enabled. Given the significance of this feature, we recommend a thorough evaluation and clear communication to all affected personnel before activation. The following image shows the result after the file is labeled.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5dd6c7f76cbe4e98a88997f28d6ec72c~tplv-goo7wpa0wc-topic.webp) </span>

* **Risk Prevention Advisory:**  To mitigate potential reputational risks, we advise enabling appropriate security measures on company\-owned devices. This helps protect the company's reputation by preventing unnecessary disputes arising from improper information disclosure.

* **Product Liability Disclaimer:**  SealSuite provides technical products and solutions and is not liable for any risks that may arise from their use. You are responsible for evaluating and assuming all associated risks.

* **System and version requirements**:

   * **Windows**: Windows 7 or later; SealSuite client `3.0.19` or later.

   * **macOS**: macOS 11 or later; SealSuite client `3.0.19` or later.

   * **Linux**: Ubuntu 18.04 or later; SealSuite client `3.3.13` or later.


 &nbsp;

<span id="procedure"></span>
## Procedure


1. Log in to the Admin Console.

2. In the left navigation bar, go to **DLP** \> **Strategy Center** \> **Label Management**.

3. Click **Edit** in the upper\-right corner, configure the following parameters, and then click **Save**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4467c3d88f8c44fd83e0efeaf62bd6f5~tplv-goo7wpa0wc-topic.webp) </span>

&nbsp;

   
   |**Setting** |**Description** |
   |---|---|
   |**Switch** |Enables or disables the sensitivity label feature. When enabled, files matching sensitive data rules will be automatically labeled, and users will not be able to modify these labels. |
   |**Scope** |Defines the scope of the policy by **employees** or **devices**.<br><br>You can also exclude certain employees or roles. The final effective scope is **Assigned Scope \- Excluded Scope**.<br><br><br>1. Enable the **Exclude object** toggle.<br><br>2. Add objects by device, device group, department, role, or employee. You can add multiple exclusions. |
   |**Marking Range** |Configure which sensitivity levels will be labeled. For example, you can choose to label files with L4 (Confidential) and L3 (Secret) sensitivity levels. |
   |**Client Side Presentation Style** |You can use the default SealSuite styles or create custom ones. To customize:<br><br><br>1. Click **Configure** next to Windows, macOS, and Linux.<br><br>2. Upload the corresponding image files for each level.<br><br>   * **Windows**: Requires `.ico` format.<br><br>   * **macOS**: Requires `.icns` format.<br><br>   * **Linux**: Requires `.png` format.<br><br><br>Before a large\-scale rollout, use the preview tool to ensure the icons appear as intended. If an icon obscures too much of the original file thumbnail, consider reducing the image content size within the file while maintaining the overall canvas dimensions, as shown in the following picture.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07c5664913b14cc493569607c3b406db~tplv-goo7wpa0wc-topic.webp) </span> |
