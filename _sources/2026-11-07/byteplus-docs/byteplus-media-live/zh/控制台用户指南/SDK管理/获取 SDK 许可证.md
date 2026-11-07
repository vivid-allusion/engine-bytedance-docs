---
title: "获取 SDK 许可证"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management-zh-CN"
---

如需在应用中使用 BytePlus MediaLive SDK，必须先获取有效许可证。该许可证会为你的特定应用激活 SDK 功能。本主题介绍完整流程，从在控制台创建 SDK 应用，到获取 SDK 集成所需的许可证。

> **注意**

> 仅在使用以下 BytePlus MediaLive SDK 时，才需要创建 SDK 应用并获取许可证：

* > Player SDK for iOS

* > Player SDK for Android

* > Player SDK for React Native

* > Player SDK for Flutter

* > Player SDK for Web（2.11.0 或更高版本）

## 前提条件

* 对于 Android 或 iOS 应用，请准备以下信息：

   * **Android**：应用的包名。你可以在项目 `app` 目录下的 `build.gradle` 文件中，通过 `applicationId` 值找到该信息。

   * **iOS**：应用的 bundle ID。你可以在 Xcode 中应用 target 的设置里，通过 `Bundle Identifier` 值找到该信息。

* 对于 Web 应用，请准备以下信息：

   * **Web**（用于浏览器页面）：通配符域名，例如 `*.example.com`，需覆盖你计划嵌入播放器的所有页面。

   * **WebOTT**（Web Over\-The\-Top，用于在 Tizen 和 webOS 智能电视系统上运行的 Web 应用，仅 Player SDK for Web 2.12.0 及更高版本支持）

      * **Tizen**：应用标识符。你可以在项目的 `config.xml` 文件中，通过 `applicationId` 值找到该信息。

      * **webOS**：应用标识符。你可以在项目的 `appinfo.json` 文件中，通过 `id` 值找到该信息。

## 步骤 1：创建或绑定 SDK 应用

1. 登录 [BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 在左侧导航窗格中，点击 **SDK 管理**。

3. 点击 **创建 SDK 应用** 创建 SDK 应用；如果你已在 BytePlus VOD 控制台创建应用，则点击 **绑定已有应用**。

4. 配置基本信息。

   **Android 或 iOS 应用**

对于 Android 或 iOS 应用，请完成以下步骤。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a82a7363c8a1444eaef0ea238d643f5c~tplv-goo7wpa0wc-topic.webp)

      * **SDK 类型**：选择 **App** 作为 SDK 类型。此类应用用于集成客户端 SDK。

      * **应用名称**：

         * 如果你要创建新应用，请输入唯一名称。名称长度必须为 1–128 个字符，可包含字母（A\-Z、a\-z）、数字（0\-9）、中文字符和部分特殊字符。

         * 如果你要绑定已有应用，请选择应用 ID。你可以在 BytePlus VOD 控制台的应用列表页面找到该 ID。

      * **项目**：选择 SDK 应用所属项目。这可确保只有有权访问该项目的子账号才能管理该应用。

      * **PackageName** 和 **Bundle ID**：输入 Android 应用的包名和 iOS 应用的 bundle ID。这会将 SDK 许可证绑定到你的应用，以防止未经授权的使用。如果应用同时支持两个平台，请同时提供两项；如果仅支持单个平台，则只需提供一项。

         > **注意**

         > 确保输入的 **PackageName** 和 **Bundle ID** 全局唯一。

   **Web 应用**

对于 Web 应用，请完成以下步骤。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87f6bb90aa7f40db931ce4da906f3864~tplv-goo7wpa0wc-topic.webp)

      * **SDK 类型**：选择 **Web** 作为 SDK 类型。此类应用用于集成 Player SDK for Web。

      * **应用名称**：

         * 如果你要创建新应用，请输入唯一名称。名称长度必须为 1–128 个字符，可包含字母（A\-Z、a\-z）、数字（0\-9）、中文字符和部分特殊字符。

         * 如果你要绑定已有应用，请选择应用 ID。你可以在 BytePlus VOD 控制台的应用列表页面找到该 ID。

      * **项目**：选择 SDK 应用所属项目。这可确保只有有权访问该项目的子账号才能管理该应用。

      * **通配符域名**：根据你的场景输入以下信息。

         * **Web**（用于浏览器页面）：如需授权播放，请输入通配符域名。该域名需覆盖你计划嵌入播放器的所有页面。这允许播放器在任何匹配的一级子域名上运行。

            **示例**：如果你输入 `*.example.com`：

            * **匹配**：`a.example.com`、`b.example.com`

            * **不匹配**：`a.b.example.com`（多级子域名）、`example.com`（根域名）

               **规则**：

            * 取值必须以星号（`*`）开头，且不能超过 128 个字符。

            * 通配符字符（`*`）必须用于你拥有的域名，不能用于公共后缀或顶级域名。

               * 正确：`*.example.com`（因为 `example.com` 是你拥有的特定域名）。

               * 错误：`*.com` 或 `*.com.cn`（因为 `.com` 是顶级域名，`.com.cn` 是公共后缀，二者都不由单个实体拥有）。

         * **WebOTT**（用于在 Tizen 和 webOS 智能电视系统上运行的 Web 应用，仅 Player SDK for Web 2.12.0 及更高版本支持）：输入你的应用标识符。

         > **注意**

         > 确保输入的通配符域名或应用标识符全局唯一。

5. 如果你要创建新应用，请点击 **创建应用**。如果你要绑定已有应用，请点击 **下一步**。

6. 配置许可证并将其绑定到 SDK 应用。

   > **说明**

   * > 每个许可证只能绑定到一个 SDK 应用。

   * > SDK 许可证的有效期仅在许可证绑定到 SDK 应用后开始。

   * > 许可证用于管理 SDK 及其增值服务的使用权限和时长。有关每种许可证类型支持的功能，请参见[客户端 SDK：SDK 概览](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction)和 [Player SDK for Web：SDK 概览](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-sdk-overview)。有关每种许可证类型的价格，请参见 [SDK 许可证](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-licenses)。

   * > 如果你需要集成早于 2.11.0 版本的 Player SDK for Web，则无需绑定许可证。你可以直接获取应用 ID 用于 SDK 集成。不过，建议将 Player SDK for Web 升级到 2.11.0 或更高版本，以获得更好的功能和服务。

   **试用许可证**

试用许可证**仅用于测试目的**，有效期为**一个月**。例如，在 2026 年 5 月 10 日 10:00 绑定到应用的许可证，将于 2026 年 6 月 10 日 10:00 过期。

   按以下步骤获取试用许可证：

      1. 选择 **Trial** 作为许可证类型，然后点击 **获取许可证**。系统会将你引导至 **License purchase** 页面。

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/16b9df9aacb04ab6a2c6a76077845250~tplv-goo7wpa0wc-topic.webp)

      2. 在购买页面，点击 **立即获取** 继续免费获取许可证。

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b997614ab172403f8aca0a33415b9cb6~tplv-goo7wpa0wc-topic.webp)

      3. 完成免费许可证的结算流程后，返回配置页面。选择刚获取的试用许可证，然后点击 **确认**。

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f206935371934e1ab2bd4917df8d9935~tplv-goo7wpa0wc-topic.webp)

         > **说明**

         > 如果新的试用许可证未立即显示在列表中，请点击刷新图标更新页面。

         > ![](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3afbc908af9f4304bae35f8dc76b10d9~tplv-goo7wpa0wc-topic.webp)

   在试用许可证过期前，或当你准备将应用发布到生产环境时，必须将许可证升级为基础版或高级版。更多信息，请参见[将试用许可证升级为基础版或高级版许可证](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#777c7de7)。

   **基础版许可证**

基础版许可证适用于**生产环境**，**有效期为一年**。例如，在 2026 年 5 月 10 日 10:00 绑定的许可证，有效期至 2027 年 5 月 10 日 10:00。你可以随时续订基础版许可证。更多信息，请参见[续订许可证](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#b2dde14f)。

   如需获取基础版许可证，请选择 **Basic** 作为许可证类型，然后选择以下方法之一：

      * 直接购买

         1. 点击 **立即购买**。

            ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5bedee922aa84a8184d924132120ef07~tplv-goo7wpa0wc-topic.webp)

         2. 完成购买后，返回配置页面。从列表中选择基础版许可证，然后点击 **确认**。

            ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a4ab8a8ff8b4d708dd4876ccf6006f9~tplv-goo7wpa0wc-topic.webp)

            > **说明**

            > 如果新购买的许可证未立即显示在列表中，请点击刷新图标更新页面。

            > ![](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3afbc908af9f4304bae35f8dc76b10d9~tplv-goo7wpa0wc-topic.webp)

      * 绑定流量包：通过将 100 TB 或更大的直播流量包绑定到你的应用，可获取一个免费的、一年期的基础版许可证。有关直播流量包的更多信息，请参见[资源包](https://docs.byteplus.com/docs/byteplus-media-live/docs-resource-packs)。

         > **说明**

         > 此方法**仅**适用于 App 类型的应用。

         * **如果你已有符合条件的流量包**：从列表中选择流量包，然后点击 **确认**。

         * **如果你没有符合条件的流量包**：

            1. 点击 **立即购买** 购买流量包。

               ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa45000672b94d6eae8a6509bae35357~tplv-goo7wpa0wc-topic.webp)

            2. 完成购买后，返回配置页面。从列表中选择流量包，然后点击 **确认**。

               > **说明**

               > 如果新购买的流量包未立即显示在列表中，请点击刷新图标更新页面。

               > ![](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3afbc908af9f4304bae35f8dc76b10d9~tplv-goo7wpa0wc-topic.webp)

   **高级版许可证**

高级版许可证适用于**生产环境**，**有效期为一年**。例如，在 2026 年 5 月 10 日 10:00 绑定的许可证，有效期至 2027 年 5 月 10 日 10:00。你可以随时续订高级版许可证。更多信息，请参见[续订许可证](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#b2dde14f)。

   按以下步骤获取高级版许可证：

      1. 选择 **Premium** 作为许可证类型。

      2. 点击 **立即购买**。

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a98e6675afe345348571f5ef165106c8~tplv-goo7wpa0wc-topic.webp)

      3. 完成购买后，返回配置页面。选择高级版许可证，然后点击 **确认**。

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31b655fa42144106a5f1b0836dca473b~tplv-goo7wpa0wc-topic.webp)

         > **说明**

         > 如果新购买的许可证未立即显示在列表中，请点击刷新图标更新页面。

         > ![](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3afbc908af9f4304bae35f8dc76b10d9~tplv-goo7wpa0wc-topic.webp)

7. 你的应用现在会显示在 **SDK 管理** 页面的应用列表中。在列表中找到你的应用，并查看 **App ID** 和 **应用名称**。集成和初始化 SDK 时需要使用这两项。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ac12129476144c8b5a06412796f84e3~tplv-goo7wpa0wc-topic.webp)

## 步骤 2：获取许可证

BytePlus MediaLive SDK 必须与 SDK 许可证配合使用。你获取的许可证仅对绑定的 SDK 应用有效。

在 [SDK 管理](https://console.byteplus.com/live/main/sdk)页面，找到目标应用。

* 对于 Android 或 iOS 应用，点击下载图标下载许可证文件。然后使用许可证文件集成 SDK。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44a07076e89243e38d48f42a5ad23276~tplv-goo7wpa0wc-topic.webp)

* 对于 Web 应用，点击下载图标下载许可证文件，或点击 **详情** 获取用于集成 Player SDK for Web 的许可证 URL。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/954db88e8e494a199525032b09044587~tplv-goo7wpa0wc-topic.webp)

> **说明**

> 确保应用状态为 **已激活**。

* > 如果状态为 **已过期**，你必须先续订许可证。更多信息，请参见[续订许可证](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#b2dde14f)。

* > 如果状态为 **未激活**，请点击 **操作** 列中的省略号图标（...），然后选择 **激活** 以配置并绑定许可证。有关如何配置并绑定许可证的更多信息，请参见[步骤 1：创建或绑定 SDK 应用](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management#91608dc8)。

## 相关操作

在 **SDK 管理** 页面，你可以在 **操作** 列中执行以下操作。

* **编辑**：点击 **编辑**，可更改应用名称、**PackageName**、**Bundle ID**、通配符域名或 WebOTT 应用标识符。

   * 如果许可证已激活，变更后系统会根据更新后的应用信息重新生成许可证。你需要替换 SDK 许可证文件或许可证 URL。原许可证会在一段时间内保持有效，新许可证的到期时间与原许可证相同。

   * 如果许可证已过期，续订许可证时系统会根据更新后的应用信息生成新许可证。续订完成后，你需要替换 SDK 许可证文件或许可证 URL。

* **删除**：点击省略号（...）图标并选择 **删除**，可永久删除应用。

   > **注意**

   > 如果你误删了应用，可以通过 **绑定已有应用** 恢复应用，并继续使用原 App ID。绑定应用时，你需要重新配置 **PackageName**、**Bundle ID**、通配符域名或 WebOTT 应用标识符。系统不会保留删除前的配置信息。如果 SDK 应用刚被删除，可能不会立即显示在 **绑定已有应用** 对话框中。在这种情况下，请稍后重试。

* **续订**：当许可证即将过期或已过期时，点击 **续订** 续订许可证。更多信息，请参见[续订许可证](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#b2dde14f)。

* **升级**：点击 **升级**，将试用许可证升级为基础版或高级版许可证。更多信息，请参见[将试用许可证升级为基础版或高级版许可证](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#777c7de7)。

* **激活**：如果许可证尚未绑定到应用，请点击省略号（...）图标并选择 **激活**，以配置并绑定许可证。有关如何配置并绑定许可证的更多信息，请参见[步骤 1：创建或绑定 SDK 应用](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management#91608dc8)。

## 后续操作

使用从控制台获取的许可证文件、许可证 URL、应用 ID 和应用名称来集成并初始化 SDK。更多信息，请参见：

* iOS：[集成 Player SDK for iOS](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios)和[初始化 Player SDK for iOS](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-ios)

* Android：[集成 Player SDK for Android](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-android)和[初始化 Player SDK for Android](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-android)

* Flutter：[集成 Player SDK for Flutter](https://docs.byteplus.com/docs/byteplus-media-live/integrating-the-player-sdk-for-flutter)和[初始化 Player SDK for Flutter](https://docs.byteplus.com/docs/byteplus-media-live/initializing-the-player-sdk-for-flutter)

* React Native：[集成 Player SDK for React Native](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-rn)和[初始化 Player SDK for React Native](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-rn)

* Player SDK for Web：[集成 Player SDK for Web](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1)
