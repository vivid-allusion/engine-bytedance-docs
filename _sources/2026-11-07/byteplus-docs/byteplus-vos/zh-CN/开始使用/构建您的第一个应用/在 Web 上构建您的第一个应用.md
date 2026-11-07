---
title: "在 Web 上构建您的第一个应用"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-running-the-demo-web-zh-CN"
---

为了快速探索如何构建具备短剧和互动视频等功能的应用，您可以使用本指南来搭建并运行 VideoOne Web Demo 项目。该示例项目展示了 VideoOne SDK 的核心能力，帮助您理解其集成方式并加速您的应用开发。

<span id="a61579f1"></span>
# 前置条件


* 具备图形用户界面的操作系统

* 终端或命令行界面

* 与 Web SDK 兼容的网页浏览器。我们建议使用最新版 Chrome 浏览器以获得最佳体验。

* 已安装 [pnpm](https://pnpm.io/installation) 包管理器。


<span id="84342d05"></span>
# 操作流程

<span id="3772c012"></span>
## 步骤 1：克隆项目并安装依赖


1. 运行 `git clone https://github.com/byteplus-sdk/videoone-example.git` 克隆 [videoone-example](https://github.com/byteplus-sdk/videoone-example) 仓库。

2. 在项目根目录下，运行 `pnpm install --registry=https://registry.npmmirror.com` 安装依赖。


<span id="d2338e5e"></span>
## 步骤 2：启动项目


1. 运行 `pnpm run dev` 启动项目。默认端口号为 8000。

2. 在浏览器中打开 [localhost:8000/videoone](localhost:8000/videoone)，以查看 Demo 项目。打开该 URL 后，首页会展示两种场景：“短剧”和“互动视频”。

   1. 点击“短剧”可体验连续、竖屏全屏剧集，支持滑动切换和内容解锁功能。

   2. 点击“互动视频”可查看动态视频实现，包含可滚动内容、评论及点赞功能。

   
   |首页 |短剧 |互动视频 |
   |---|---|---|
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce65fcea68b845089d4c8d253eb8f7c9~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a27e4f281e64def93a1aafa2bca4109~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cfe034e2fe8345298af91076f2320427~tplv-goo7wpa0wc-image.image) </span> |
   


<span id="4e723578"></span>
## 步骤 3：构建与部署

如需生成部署用的构建产物，请运行以下命令：`pnpm run build`。

部署时需重点关注 `base` 和 `build` 配置项，位于 `vite.config.ts` 文件中。请注意以下两点：


1. **构建输出目录：** 默认情况下，构建产物会生成到 `output` 目录。您可通过修改 `build` 配置下的 `outDir` 属性进行自定义。

2. **构建资源的公共路径前缀：** 此设置决定构建过程中所有资源的公共基础路径。

   * 若构建资源由服务器直接托管于根目录或固定子路径，`base` 通常可设置为 `/`（根路径）或空字符串。

   * 若静态资源上传至内容分发网络（CDN）托管，则需获取相应的 CDN 加速域名。该值应替换 `*`，用于 `base` 配置项。

      ```TypeScript
      export default defineConfig({
        base: isProd ? '*' : '/',
        server: {
          port: 8000,
        },
        build: {
          outDir: 'output',
        },
      });
      ```
      


<span id="eb0670bb"></span>
# 代码解析

Demo 项目的目录结构如下：

```Plain
.
├── build.sh
├── commitlint.config.cjs
├── index.html            // Template entrance
├── node_modules
├── package.json          // Project manifest and dependencies
├── pnpm-lock.yaml
├── public // Common files
├── README.md
├── src
│   ├── @types           // TypeScript type declarations
│   ├── App.tsx
│   ├── assets           // Static resources, such as images, SVGs, Lottie animations, etc.
│   ├── components       // Components
│   ├── hooks
│   ├── index.less
│   ├── interface        // Interface declarations
│   ├── main.tsx
│   ├── pages            // Page routing
│   ├── player.ts
│   ├── plugins
│   ├── redux
│   ├── service          // API service definitions
│   ├── utils
│   └── vite-env.d.ts
├── tsconfig.json
├── tsconfig.node.json
└── vite.config.ts        // Vite configuration
```
