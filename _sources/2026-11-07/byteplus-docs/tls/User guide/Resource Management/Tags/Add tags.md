---
title: "Add tags"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Add_tags"
---

Torch Log Service (TLS) allows you to attach tags to projects and topics. You can use tags to classify cloud resources, then search for or aggregate cloud resources by tag. This topic describes how to attach tags to projects and topics.

<span id=".5qCH562-6K6-572u6KeE5YiZ"></span>
## Rules for setting tags

The following table describes the rules for setting tags:


|Limited Item |Description |
|---|---|
|Tag Key |* A tag key can consist of letters and characters in multiple languages such as Chinese and English, digits, spaces, and the following special characters `_ . : / = + - @`. It cannot start or end with a space.<br><br>* `volc:` is a tag key reserved by the system. When you add a tag, the tag key cannot start with `volc:` in any combination of uppercase and lowercase letters.<br><br>* A tag key can be 1 to 128 characters in length. |
|Tag Value |* A tag key can consist of letters and characters in multiple languages such as Chinese and English, digits, spaces, and the following special characters `_ . : / = + - @`. It cannot start or end with a space.<br><br>* A tag key can contain 0 to 256 characters, that is, a tag value can be null. |
|the number of tags |* The total number of tags within your account is unlimited. However, you can attach up to 50 tags to one project or topic.<br><br>* You can add up to 20 tags at a time. |


<span id=".5Li65p-Q5Liq5pel5b-X6aG555uu6K6-572u5qCH562-"></span>
## Adding a tag to a project


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the Region where the projects that you want to view are located.

3. In the left\-side navigation pane, choose **Resource management** \> **Project**.

4. Find the target project, then click the Edit icon in the **tag** row.

   You can also click the name of the project. In the **Basic information** area of the page that appears, click the Edit icon in the **Tag** row.

5. Configure **Tag Key** and **Tag Value**. Follow the tag setting rules to set a tag. For more information, refer to [Rules for setting tags](https://docs.byteplus.com/docs/tls/Add_tags#.5qCH562-6K6-572u6KeE5YiZ).

6. Click **OK**.


<span id=".5Li65p-Q5Liq5pel5b-X5Li76aKY6K6-572u5qCH562-"></span>
## Adding a tag to a topic


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the Region where the projects that you want to view are located.

3. In the left\-side navigation pane, choose **Resource management** \> **Project**, then click the name of the project to which the target topic belongs.

4. Find the target topic and click the Edit icon in the **Tag** column.

5. Configure **Tag Key** and **Tag Value**.

   Follow the tag setting rules to set a tag. For more information, refer to [Rules for setting tags](https://docs.byteplus.com/docs/tls/Add_tags#.5qCH562-6K6-572u6KeE5YiZ).

6. Click **OK**.


<span id=".5om56YeP6K6-572u5qCH562-"></span>
## Adding tags to multiple resources at a time

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the tag key of a newly added tag is the same as that of an existing tag, the new tag value overwrites the value of the existing tag.</div>



1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the Region where the projects that you want to view are located.

3. In the left\-side navigation pane, choose **Resource management** \> **Project**.

   * Add tags to multiple projects at a time

      1. Select the projects to which you want to add tags, then click **Bind tag**.

      2. Configure **Tag Key** and **Tag Value**. Follow the tag setting rules to set a tag. For more information, refer to [Rules for setting tags](https://docs.byteplus.com/docs/tls/Add_tags#.5qCH562-6K6-572u6KeE5YiZ).

      3. Click **OK**.

   * Add tags to multiple topics at a time

      1. Click the name of the project to which the target topics belong.

      2. Select the topics to which you want to add tags, then click **Bind tag**.

      3. Configure **Tag Key** and **Tag Value**. Follow the tag setting rules to set a tag. For more information, refer to [Rules for setting tags](https://docs.byteplus.com/docs/tls/Add_tags#.5qCH562-6K6-572u6KeE5YiZ).

      4. Click **OK**.
