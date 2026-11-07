---
title: "添加 IAM 用户、组织或角色"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-managing-iam-users-and-roles-zh-CN"
---

本文档介绍如何添加 IAM 用户、组织或角色，包括为用户分配组织和角色，从而使 IAM 用户权限管理更加细粒度且灵活。

<span id="25abd8c1"></span>
## 前提条件

需拥有 BytePlus 账号或具备 **账号概览** \> **编辑**权限的 IAM 用户。更多信息，请参见 [注册 BytePlus 账号](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account)。

<span id="241e6b39"></span>
## 添加用户


1. 登录 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)。

2. 在 BytePlus Live 的菜单栏中，点击 **授权**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1055d6b0ea5d4435a6b7c2e8aa636081~tplv-goo7wpa0wc-image.image) </span>

3. 在 **用户**页面，点击 **添加用户**。

4. 在弹出的 **添加用户**对话框中，点击 **添加用户**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e52312be7bc475780d3566fb9d77214~tplv-goo7wpa0wc-image.image) </span>

5. 完成以下配置后，点击 **确定**。随后，用户会同时添加至 BytePlus Live 的 **授权** \> **用户**页面，以及 BytePlus 的 [IAM > 身份管理 > 用户](https://console.byteplus.com/iam/identitymanage/user)页面。

   
   |**配置项** |**接口行为** |**注意事项** |
   |---|---|---|
   |用户类型 |选择**邮箱**。目前仅支持通过邮箱添加用户。 |用户添加后，邮箱地址不可更改。请确保输入正确。 |
   |用户账号 |输入用户的邮箱地址，该邮箱将作为**子账号用户名**，用于在[IAM 用户登录](https://console.byteplus.com/auth/login/user/?redirectURI=%2Flivesaas%2FaccountManagement%2FroleManage)页面登录 BytePlus Live 控制台。 |无 |
   |用户昵称 |输入用户昵称。 |昵称不能超过16个字符，仅可包含英文字母、数字和中文字符。 |
   |所属组织 |选择用户所属的组织。关于如何添加组织，详见[Adding an organization](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles-zh-CN#442b626b)。 |无 |
   |角色 |选择一个或多个角色分配给该用户。关于如何创建角色，详见[添加角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles-zh-CN#08751041)。 |如未选择角色，系统将为用户分配默认角色，用户仅可查看和编辑其本人创建的直播间。 |
   

   用户添加后，将收到一封邮件，并可通过该邮件中的登录链接、邮箱地址和密码登录 BytePlus Live 控制台。

6. 您还可以执行以下操作：

   * 按昵称或邮箱地址搜索用户。支持模糊搜索。

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">英文字母不区分大小写。      </div>
      

   * 在 **操作**列点击 **编辑**，并在弹出的 **编辑用户**对话框中根据需要修改用户的昵称、组织和角色。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/706bfdd557344c66900d996200aee63c~tplv-goo7wpa0wc-image.image) </span>

   * 在 **操作**列点击 **重置密码**，可重置用户用于登录控制台的密码。系统将向用户发送包含随机新密码的邮件。目前，仅主 BytePlus 账号可自定义 IAM 用户的密码。更多信息，请参见 [如何自定义 IAM 用户的密码？](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles-zh-CN#fd3d4ba8)。

   * 在 **操作**列点击 **删除**，可删除用户。

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">在此处删除后，用户仍可登录 BytePlus 控制台使用其他服务。你也可以在本页面使用相同邮箱地址再次添加该用户。      </div>
      

<span id="08751041"></span>
## 添加角色


1. 登录 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)。

2. 在 BytePlus Live 的菜单栏中，点击 **授权**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1055d6b0ea5d4435a6b7c2e8aa636081~tplv-goo7wpa0wc-image.image) </span>

3. 在左侧导航栏，点击 **子账号** \> **角色**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f47f09a1251e4b0a87b2e7be022e013d~tplv-goo7wpa0wc-image.image) </span>

4. 在 **角色**页面，点击 **创建角色**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81d081d61dab4f389b1380316980afdf~tplv-goo7wpa0wc-image.image) </span>

5. 在弹出的 **新建角色**对话框中，完成以下配置后点击 **确定**。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">如需剪辑视频、开播和导出数据，用户必须拥有对应页面的编辑权限。   </div>
   

   
   |**配置项** |**接口行为** |
   |---|---|
   |角色名称 |输入角色名称。角色名称不能超过16个字符，仅可包含英文字母、数字和中文字符。 |
   |权限分配 |为分配该角色的用户配置权限及可见范围。<br><br><br>* **直播间权限：** 配置直播间权限及可见范围。<br><br>   被分配此角色的用户，对可见范围内的直播间拥有特定权限。例如，将组织A设为可见范围，并将**直播控制** \> **编辑**、**制作端** \> **仅查看**以及**洞察** \> **无权限**设置为直播间权限。则被分配此角色的用户，对组织A下用户创建的所有直播间中的**直播控制**页面拥有编辑权限，对**制作端**模块的所有页面拥有仅查看权限，对**洞察**模块的所有页面无权限。<br><br>   * 选择直播间权限。<br><br>   * 选择可见范围。<br><br>      * **本人**：被分配此角色的用户仅可访问或编辑其本人创建的所有直播间。该选项为默认选中，且不可取消。<br><br>      * **全部用户**：勾选此复选框后，拥有该角色的用户可访问或编辑其他用户（包括主BytePlus账号及其IAM用户）创建的所有直播间。<br><br>      * **指定用户**：勾选此复选框，并从对应下拉列表中选择用户。被分配此角色的用户仅可访问或编辑所选用户创建的直播间。<br><br>         可通过昵称或邮箱地址搜索用户。支持模糊搜索，且英文字母不区分大小写。<br><br>      * **指定组织**：勾选此复选框，并从对应下拉列表中选择组织。被分配此角色的用户仅可访问或编辑所选组织内用户创建的直播间。<br><br>         可通过名称搜索组织。支持模糊搜索，且英文字母不区分大小写。<br><br>      * **指定直播间**：勾选此复选框，并从对应下拉列表中选择直播间。被分配此角色的用户仅可访问或编辑所选直播间。<br><br>         可通过名称搜索直播间。支持模糊搜索，且英文字母不区分大小写。<br><br>* 账号权限：选择账号权限。<br><br>   被分配此角色的用户，对BytePlus Live控制台的特定页面拥有特定权限。例如，将**媒体库** \> **视频库** \> **编辑**、**数据中心** \> **用户画像** \> **仅查看**以及**账号中心** \> **账号总览** \> **无权限**设置为账号权限。则被分配此角色的用户，对**视频库**页面拥有编辑权限，对**用户画像**页面拥有仅查看权限，对**账号总览**页面无权限。<br><br>   选择**媒体库** \> **视频库** \> **仅查看**或**编辑**时，可选择用户范围和分类范围。若同时选择了用户范围和分类范围，最终可见范围为两者的交集。<br><br>   选择**媒体库** \> **直播临时** \> **仅查看**或**编辑**、**媒体库** \> **云剪辑** \> **仅查看**或**编辑**、以及**媒体库** \> **奖品库** \> **仅查看**或**编辑**后，选择用户范围。<br><br>   * 用户范围：定义被分配此角色的用户可访问或编辑的视频、云剪辑项目或奖品的范围。<br><br>      * **本人**：被分配此角色的用户仅可访问或编辑其本人上传或创建的视频和云剪辑项目。用户上传或创建的视频和云剪辑项目同样受所选账户权限的限制。该选项默认被选中，且无法取消选择。<br><br>      * **所有用户**：选中此复选框后，被分配此角色的用户可以访问或编辑其他用户（包括 BytePlus 账户及其 IAM 用户，但不包括自身）上传或创建的视频和云剪辑项目。<br><br>      * **指定用户**：选中此复选框，并从对应下拉列表中选择用户。被分配此角色的用户仅可访问或编辑所选用户上传或创建的视频和云剪辑项目。<br><br>         你可以通过昵称或邮箱地址搜索用户。支持模糊搜索，且英文字母不区分大小写。<br><br>      * **指定组织**：选中此复选框，并从对应下拉列表中选择组织。被分配此角色的用户仅可访问或编辑所选组织内用户上传或创建的视频和云剪辑项目。<br><br>         你可以通过名称搜索组织。支持模糊搜索，且英文字母不区分大小写。<br><br>   * **分类范围**：被分配此角色的用户仅可访问或编辑所选分类及其子分类下的视频。你可以通过名称搜索分类。支持模糊搜索，且英文字母不区分大小写。如未配置分类范围，拥有此角色的用户默认可访问或编辑所有分类下的视频。所有用户均可访问或编辑默认分类下的视频。 |
   

6. 您还可以执行以下操作：

   * 按角色名称搜索角色。支持模糊搜索，且英文大小写不敏感。

   * 在 **操作**列点击 **编辑**。在弹出的 **编辑角色**对话框中根据需要修改角色名称、权限及可见范围。

   * 在 **操作**列点击 **删除**，可删除角色。


<span id="08ecb0ea"></span>
### 内置角色

除了您创建的角色外，BytePlus Live 还提供以下内置角色：


* 超级管理员：该角色拥有编辑 BytePlus Live 控制台中直播间及所有页面的权限。该角色不可修改或删除。

* 默认角色：该角色通常用于查看和编辑直播间及媒体库。该角色不可删除。

* 运营：该角色通常用于查看 BytePlus Live 控制台中的直播间及页面。

* 数据：该角色通常用于查看和导出数据。

* 助手：该角色通常用于在直播流过程中发送互动工具，如问卷、投票和抽奖。


<span id="c86a1f31"></span>
## 添加组织


1. 登录[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)。

2. 在 BytePlus Live 的菜单栏中，点击**授权**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1055d6b0ea5d4435a6b7c2e8aa636081~tplv-goo7wpa0wc-image.image) </span>

3. 在左侧导航栏，点击**子账号**\> **组织**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9f0c9309bbd4940912b8d32c38b7299~tplv-goo7wpa0wc-image.image) </span>

4. 在**组织**页面，点击**新增组织**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94bb4d99d2b44b57aa3046722a35a284~tplv-goo7wpa0wc-image.image) </span>

5. 在弹出的**新增组织**对话框中，输入组织名称并点击**确定**。

   组织名称不能超过20个字符，仅可包含英文字母、数字和中文字符。

6. 你还可以执行以下操作：

   * 通过组织名称搜索组织。支持模糊搜索，英文字母不区分大小写。

   * 点击**编辑**，位于**操作**列。根据需要修改组织名称，并可在弹出的**编辑组织**对话框中查看已添加到该组织的用户。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5bde8ea9fcbe43b4ab7e95208a69b003~tplv-goo7wpa0wc-image.image) </span>

   * 点击**删除**，位于**操作**列，以删除组织。


<span id="5f820fa0"></span>
## 常见问题

<span id="fd3d4ba8"></span>
### 如何自定义 IAM 用户的密码？

目前，仅 BytePlus 账号可以自定义 IAM 用户的密码。


1. 以 BytePlus 账号身份登录[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)。

2. 点击控制台右上角的头像，选择**IAM**。

3. 在**身份管理** \> **用户**页面，点击 IAM 用户名，或在**操作**列点击**查看详情**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ff2952462984a2b9942285d42bbb43d~tplv-goo7wpa0wc-image.image) </span>

4. 在**用户详情**页面，点击**控制台登录**标签页，然后点击**重置密码**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6756ecc6c58f4d0eaf379eae4b0c9b7d~tplv-goo7wpa0wc-image.image) </span>

5. 在弹出的**重置密码**对话框中，输入新密码并点击**确定**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e6ec608b379427abe1bc655e598f7ff~tplv-goo7wpa0wc-image.image) </span>
