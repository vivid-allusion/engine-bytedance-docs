---
title: "屏蔽 URL"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-blocking-urls-zh-CN"
---

你可以启用 URL 屏蔽功能，使直播间安全且免受恶意链接或不需要的广告干扰，从而提升主播和观众的体验。

<span id="prerequisite"></span>
## 前提条件

你必须拥有 BytePlus 账号或具备 Producer \> Edit 权限的 IAM 用户。如需了解如何添加 IAM 用户，请参见[管理用户、组织和角色](https://docs.byteplus.com/en/byteplus-livesaas/docs/managing-iam-users-and-roles)。

<span id="procedure"></span>
## 操作流程


1. 登录[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)。

2. 在直播流列表中，点击打开一个直播间。

3. 在左侧导航栏，点击**Producer** \> **URL 过滤**。

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36cca073de054257a2e07d483176b1c4~tplv-goo7wpa0wc-image.image" width="1406px" />   </div>
   

4. 在**URL 过滤**页面，打开**URL 屏蔽**开关。然后：

   * 包含 URL 的评论仅对发送该评论的观众可见。

      该功能适用于聊天互动菜单和问答菜单。

   * 观众和嘉宾无法输入包含 URL 的昵称。

      默认情况下，打开开关后，包含`https://`、`http://`、`ftp://`和`www.string.`的评论和昵称将被屏蔽。此处，`string`可以包含字母、数字、点（.）和连字符（\-）。

5. （可选）如需允许评论和昵称包含特定 URL，可以将 URL 添加到白名单。此时，匹配白名单条目的 URL 不会被屏蔽。

   添加 URL 到白名单的方法如下：

   1. 点击**添加 URL 到白名单**。

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2adad3dfd4aa45c2adb2e965ede5dc01~tplv-goo7wpa0wc-image.image" width="1092px" />      </div>
      

   2. 在**添加 URL 到白名单**对话框中，通过以下方式添加一个或多个 URL，然后点击**确定**。

      * 直接在对话框中输入 URL。添加多个 URL 时，可用逗号（,）或按回车键分隔。

      * 点击**下载模版**，按照模版指引添加 URL，然后点击**从 Excel 批量导入**上传更新后的模版。

         你也可以在**操作**列点击**删除**，将 URL 从白名单中移除。
