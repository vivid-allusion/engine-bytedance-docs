---
title: "UA 限制"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-ua-blocklist-and-allowlist-zh-TW"
---

User\-Agent（UA）是 HTTP 請求標頭，包含發起請求的用戶端作業系統、瀏覽器版本等資訊。你可以通過拉流請求中的 UA 標頭值，允許或阻止特定用戶存取你的網域名稱。

<span id="630434dd"></span>
## 操作流程


1. 登入 [BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 在左側導覽窗格中，點擊 **網域**。

3. 找到你要設定的網域名稱，並在 **操作** 欄點擊 **設定**。

4. 點擊 **存取控制** 分頁。

5. 在 **UA 限制** 開關右側，點擊 **編輯**。

6. 在出現的 **編輯 UA blocklist 和 allowlist** 對話方塊中，設定以下參數。

   
   |**設定** |**說明** |
   |---|---|
   |清單類型 |此設定的選項如下：<br><br><br>* **Blocklist**：若請求的 UA 標頭在 blocklist 中，該請求會被以 403 狀態碼拒絕。<br><br>* **Allowlist**：僅當請求的 UA 標頭在 allowlist 中時，請求才能存取你的資源。其他所有請求都會被以 403 狀態碼拒絕。 |
   |規則 |輸入一個或多個 UA 標頭。所有條目的總長度不得超過 30,000 個字元。最多可輸入 1,000 個 UA 標頭。<br><br><br>* UA 標頭區分大小寫。<br><br>* 你可以使用萬用字元（\*）來表示任意數量的字元。`*` 只能出現在 UA 標頭的開頭或結尾。你可以在 UA 標頭的開頭和結尾都加上 `*`，例如 `*curl*`。<br><br>* UA 標頭不能為 `*`。<br><br>* UA 標頭不能包含 `**`。<br><br>* UA 標頭僅能包含可列印的 ASCII 字元，不包括 Delete（ASCII 代碼 127）。<br><br>* 每行輸入一個 UA。<br><br>* UA 標頭不能僅由空格組成。 |
   |包含空的 UA 標頭 |指定是否將規則套用於 UA 標頭為空或缺失的請求。例如，若 **清單類型** 設為 **Blocklist**，且 **包含空的 UA 標頭** 設為 **包含**，則 UA 標頭為空或缺失的請求會被拒絕。 |
   

7. 點擊 **確認**。
