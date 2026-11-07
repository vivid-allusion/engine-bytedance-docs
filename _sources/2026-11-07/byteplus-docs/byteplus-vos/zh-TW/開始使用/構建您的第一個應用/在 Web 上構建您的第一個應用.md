---
title: "在 Web 上構建您的第一個應用"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-running-the-demo-web-zh-TW"
---

為了快速探索如何構建具備短劇和互動影片等功能的應用，您可以使用本指南來搭建並執行 VideoOne Web Demo 專案。該示例專案展示了 VideoOne SDK 的核心能力，幫助您理解其整合方式並加速您的應用開發。

<span id="a61579f1"></span>
# 前置條件


* 具備圖形使用者介面的作業系統

* 終端或命令列介面

* 與 Web SDK 相容的網頁瀏覽器。我們建議使用最新版 Chrome 瀏覽器以獲得最佳體驗。

* 已安裝 [pnpm](https://pnpm.io/installation) 包管理器。


<span id="84342d05"></span>
# 操作流程

<span id="3772c012"></span>
## 步驟 1：克隆專案並安裝依賴


1. 執行 `git clone https://github.com/byteplus-sdk/videoone-example.git` 克隆 [videoone-example](https://github.com/byteplus-sdk/videoone-example) 倉庫。

2. 在專案根目錄下，執行 `pnpm install --registry=https://registry.npmmirror.com` 安裝依賴。


<span id="d2338e5e"></span>
## 步驟 2：啟動專案


1. 執行 `pnpm run dev` 啟動專案。預設埠號為 8000。

2. 在瀏覽器中開啟 [localhost:8000/videoone](localhost:8000/videoone)，以檢視 Demo 專案。開啟該 URL 後，首頁會展示兩種場景：“短劇”和“互動影片”。

   1. 點選“短劇”可體驗連續、豎屏全屏劇集，支援滑動切換和內容解鎖功能。

   2. 點選“互動影片”可檢視動態影片實現，包含可滾動內容、評論及點贊功能。

   
   |首頁 |短劇 |互動影片 |
   |---|---|---|
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce65fcea68b845089d4c8d253eb8f7c9~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a27e4f281e64def93a1aafa2bca4109~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cfe034e2fe8345298af91076f2320427~tplv-goo7wpa0wc-image.image) </span> |
   


<span id="4e723578"></span>
## 步驟 3：構建與部署

如需生成部署用的構建產物，請執行以下命令：`pnpm run build`。

部署時需重點關注 `base` 和 `build` 配置項，位於 `vite.config.ts` 檔案中。請注意以下兩點：


1. **構建輸出目錄：** 預設情況下，構建產物會生成到 `output` 目錄。您可透過修改 `build` 配置下的 `outDir` 屬性進行自定義。

2. **構建資源的公共路徑字首：** 此設定決定構建過程中所有資源的公共基礎路徑。

   * 若構建資源由伺服器直接託管於根目錄或固定子路徑，`base` 通常可設定為 `/`（根路徑）或空字串。

   * 若靜態資源上傳至內容分發網路（CDN）託管，則需獲取相應的 CDN 加速域名。該值應替換 `*`，用於 `base` 配置項。

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
# 程式碼解析

Demo 專案的目錄結構如下：

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
