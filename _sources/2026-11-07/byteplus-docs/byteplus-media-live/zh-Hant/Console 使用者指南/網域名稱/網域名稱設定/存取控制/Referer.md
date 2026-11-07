---
title: "Referer"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-referer-zh-TW"
---

你可以設定 Referer 封鎖清單或允許清單，以控制對內容的存取，並防止未經授權的存取。

HTTP 請求標頭中的 Referer 欄位表示請求的來源。例如，若你在頁面 `https://www.example.com/test.html` 上點擊連結至 `https://www.byteplus.com`，則 HTTP 請求標頭將包含：

```Plain
Referer: https://www.example.com/test.html
```


空的 Referer 表示該請求沒有可識別的來源。

<span id="0978b46f"></span>
## 適用於

拉流網域名稱

<span id="8e696869"></span>
## 先決條件

已新增網域名稱

<span id="882853d7"></span>
## 操作流程


1. 登入 [BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 在左側導覽窗格中，點擊 **網域名稱**。

3. 找到你要檢視的網域名稱，並在 **操作** 欄中點擊 **設定**。

4. 點擊 **存取控制** 分頁。

5. 點擊 **Referer** 開關右側的 **編輯**。

6. 在出現的 **編輯 Referer** 對話方塊中，**Referer** 會自動開啟。請設定以下參數。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1cf760bb74934ad396eb212ce2708631~tplv-goo7wpa0wc-image.image) </span>

   
   |**參數** |**說明** |
   |---|---|
   |Referer 類型 |選擇 **封鎖清單** 或 **允許清單**。<br><br><br>* **封鎖清單**：封鎖來自指定網域的請求。<br><br>* **允許清單**：僅允許來自指定網域的請求。 |
   |Referer \*\*\*\* 規則 |你可以新增完整網域名稱或萬用字元網域名稱作為規則。目前最多可設定 100 條規則。設定範例如下。<br><br><br>* **若你將規則設定為** `www.example.com`：<br><br>   * 此規則僅會精確比對網域 `www.example.com`。<br><br>   * 它將**不會**比對 `http(s):// www.example.com`、`www.example.com/` 或 `http(s):// www.example.com/path`。<br><br>* **若你將規則設定為** `*. example.com`：<br><br>   * 它將比對 `http(s):// www.example.com`。<br><br>   * 它將**不會**比對 `http(s):// www.example.com/`。<br><br>* **若你將規則設定為** `*.example.*`：<br><br>   它將比對以下所有項目：`www.example.com`、`http(s):// www.example.com`、`www.example.com/`，以及 `http(s):// www.example.com/path`。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若你需要設定超過 100 條規則，請<a href="https://console.byteplus.com/workorder/create">聯絡支援</a>。</div><br> |
   |空 Referer |勾選此選項以允許帶有空 Referer 的請求。 |
   

7. 點擊 **確認**。
