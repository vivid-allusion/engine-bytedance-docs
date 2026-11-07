---
title: "F 類型"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/typef_zh-tw"
---

本文檔介紹 BytePlus CDN 中 URL 鑑權模組的 F 類型配置。

<span id="概述"></span>
## 概述

在 F 類型的配置中，您可以：


* 配置請求的匹配條件。只有滿足条件的請求才需要被鑑權。

* 配置複雜的從用戶端請求中獲取權杖和權杖時間戳的方式。

* 配置複雜的權杖計算邏輯，包括指定用於權杖計算的各類參數、參數值的拼接方式、權杖演算法的組合等。

* 改寫影片 Manifest，將權杖和權杖時間戳新增到影片分片的 URL 中。

* 配置來源伺服器請求是否包含權杖。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">F 類型可以實現 A 類型、B 類型、C 類型、D 類型、E 類型中的配置。</div>


<span id="操作步驟"></span>
## 操作步驟


1. 開啟 **URL 鑑權** 配置頁面。操作步驟參見 [網域名稱設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-tw)。

2. 設定 **狀態** 為 **開啟**。

3. 設定 **認證類型** 為 **F 類型**。

4. 點擊 **新增規則**。您最多可以新增 5 條規則。

5. 參照 [配置說明](https://docs.byteplus.com/en/docs/18/46966#%E9%85%8D%E7%BD%AE%E8%AA%AA%E6%98%8E) 進行配置。

6. 配置完成後，點擊 **儲存**。


當 CDN 收到一個使用者請求時，CDN 會按規則的出現順序依次將規則與使用者請求匹配。第一條匹配該請求的規則生效，其餘規則都不生效。

<span id="配置說明"></span>
## 配置說明


|**配置大類** |**配置** |**說明** |
|---|---|---|
|認證規則 |生效條件 |表示一組匹配條件。CDN 對符合條件的使用者請求進行鑑權。您至少需要新增一個條件，最多可以新增 10 個。您可以指定多個條件之間的關係，預設是 **或**。<br><br><br>* **或** 表示匹配任何一個條件的請求就會被鑑權。<br><br>* **且** 表示只有匹配所有條件的請求才會被鑑權。每個條件包含匹配類型、匹配方式和匹配值。<br><br><br>匹配值的總長度不能超過 1,024 個字元，不能包含以下字元：<br><br><br>* 連續斜線（//）、空格、美元符號（$）、問號（?）、Delete（ASCII code 127）。<br><br><br>同時，<br><br><br>* 如果匹配類型是 **檔案副檔名**，匹配值必須是一個或者多個以分號（;）分隔的檔案副檔名。檔案副檔名無需以句點（.）開頭。例如：`png;txt`。<br><br>* 如果匹配類型是 **檔案目錄**，匹配值必須是一個或者多個以分號（;）分隔的路徑目錄。路徑目錄必須以斜線（/）開頭和結尾。例如：`/chs/foods/;/us/birds/`。<br><br>* 如果匹配類型是 **URL 全路徑**，匹配值必須是一個或者多個以分號（;）分隔的檔案路徑。檔案路徑必須以斜線（/）開頭，可以包含星號（\*）用來表示一個或者多個字元。例如：`/chs/foods/local*sets;/us/birds/chickadee`。<br><br>* 如果匹配類型是 **正規表示式**，匹配值必須是一個或者多個以分號（;）分隔的正規表示式，用於匹配請求路徑。例如：`/a{1,2}(.*)g`。 |
|認證參數獲取 |主金鑰 |表示主金鑰。 |
||輔助金鑰 |表示輔助金鑰。如果鑑權失敗，CDN 會使用輔助金鑰再計算一次權杖，與使用者請求中的權杖比對。 |
|認證權杖管理 |權杖獲取方式 |表示權杖的獲取方式，包含：<br><br><br>* 指定查詢參數：表示權杖來自請求 URL 中的一個查詢參數。您需要在下方輸入該查詢參數的名稱。<br><br>* 指定 URI 層級：表示權杖來自請求路徑中的一個目錄層級。您需要在下方指定該層級。層級是一個非 0 的整數。對於您指定的層級，其絕對值不能大於層級總數。<br><br>   * 如果層級是正整數，表示從路徑中最左邊的目錄開始向右計數，以定位相應目錄。<br><br>   * 如果層級是負整數，表示從路徑中最右邊的目錄開始向左計數。<br><br>      例子：<br><br>   * 請求路徑是 `/a/b/c/d`，權杖來自 `b` 。在這個情況下，您可以指定層級為 `2` 或者 `-3`。<br><br>* 自定義請求頭：表示權杖來自請求中的一個標頭。您需要在下方指定該請求標頭。<br><br>* Cookie：表示權杖來自請求中的一個 cookie。您需要在下方指定该 cookie 的 key，CDN 會獲取该 cookie 的 value。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Cookie 的格式必須符合 <a href="https://datatracker.ietf.org/doc/html/rfc6265">RFC 6265</a>。否則，CDN 可能無法獲取 cookie 的 value。   </div><br>   <br><br>當 **權杖獲取方式** 是 **指定查詢參數** 或者 **指定 URI 層級** 時，對於獲取到的內容，您可以指定以下選項：<br><br><br>* 不拆分參數內容：表示內容本身就是權杖。該選項是預設選項。<br><br>* 拆分參數內容：表示內容本身不是權杖，而是可被特定分隔符拆分的一個字串。權杖需要從內容中提取。提取方式包含以下選項：<br><br>   * 指定分隔符：表示用於分隔內容而使用的分隔符。<br><br>   * 選擇層級：表示在將內容以分隔符拆分為多個層級的片段後，權杖所在的層級。參見本配置中 **指定 URI 層級** 的說明。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">關於該配置的輸入要求，參見 <a href="https://docs.byteplus.com/en/docs/18/46966#%E9%85%8D%E7%BD%AE%E8%BC%B8%E5%85%A5%E8%A6%81%E6%B1%82">配置輸入要求</a>。</div><br> |
|過期時間管理 |獲取方式 |表示權杖時間戳的獲取方式。該配置的說明與 **權杖獲取方式** 配置的描述類似。 |
||有效時間 |表示權杖的有效時長，單位是秒，取值範圍是 0\-315,360,000，預設值是 `0`。<br><br><br>* 權杖過期時間 = 權杖時間戳所表示的時間 + 有效時間<br><br><br>當收到一個使用者請求時，如果 CDN 計算的權杖過期時間早於目前時間，CDN 判定權杖已過期，返回 403 回應狀態碼。 |
||時間戳格式 |表示權杖時間戳的格式。該參數有以下選項：<br><br><br>* 八進位 Unix 時間戳：表示過期時間是一個八進位的 Unix 時間戳，例如 `14751410031`。<br><br>* 十進位 Unix 時間戳：表示過期時間是一個十進位的 Unix 時間戳，例如 `1738936345`。<br><br>* 十六進位 Unix 時間戳：表示過期時間是一個十六進位的 Unix 時間戳，例如 `67a61019`。 |
|認證參數獲取 |認證參數選擇 |表示 CDN 在計算權杖時使用的簽算物件列表。點擊 **認證參數獲取** 新增一個物件。物件類型有：<br><br><br>* 認證金鑰：表示主金鑰或者輔助金鑰。<br><br>* 補充字串：表示一個字串。您需要在下方輸入該字串。<br><br>* 自訂 URI：表示請求路徑中的連續片段。路徑不包含查詢字串。對於該類型，您需要指定的選項有：<br><br>   * 分隔符：表示分隔 URL 路徑而使用的分隔符。<br><br>   * 拼接符：表示拼接這些片段所使用的拼接符。<br><br>   * 起始層級：表示起始片段所在的層級。<br><br>   * 結束層級：表示結束片段所在的層級。<br><br>   * 改寫時參數來源：在需要改寫影片 Manifest 的場景中，對於需要在影片分片 URL 中新增的權杖，該選項表示 CDN 在計算該權杖時使用的路徑來源。來源有：<br><br>      * 父（存取）連結：表示使用者請求 URL 中的路徑。<br><br>      * 子（被改寫）連結：表示影片分片的 URL 中的路徑。<br><br>      起始層級必須是正整數，結束層級可以是正整數，也可以是負整數。起始層級和結束層級的絕對值不能大於層級總數。另外，起始層級的路徑片段不能在結束層級的路徑片段右側。<br><br>   * 如果結束層級是負整數，表示從最右邊的層級開始向左計數。<br><br>      例子：<br><br>   * 請求路徑是 `/a/b/c/d/e`，分隔符 `/`，拼接符是 `-`。<br><br>      * 如果起始層級是 `1`，結束層級是 `-4`，則結果是 `a-b`。<br><br>      * 如果起始層級是 `2`，結束層級是 `-4`，则结果是 `b`。<br><br>      * 如果起始層級是 `3`，結束層級是 `-4`，錯誤。原因是起始層級的路徑片段在結束層級的路徑片段右側。<br><br>* 自定義URL參數：表示請求 URL 中的某類物件。對於該類型，您可以指定以下選項：<br><br>   * 指定查詢參數：表示某个查詢參數。您需要在下方輸入該查詢參數的名稱。<br><br>   * 指定 URI 層級：表示路徑中某个層級的目錄。您需要在下方輸入目錄層級。層級是非 0 的整數，絕對值不能大於層級總數。如果層級是負整數，表示從最右邊的層級開始向左計數。<br><br>   * 拆分選項。對於獲取到的物件，您可以額外指定以下選項：<br><br>      * 不拆分參數內容：表示獲取到的物件就是所要的物件。該選項是預設的。<br><br>      * 拆分參數內容：表示需要對獲取到的物件做進一步拆分，以提取所要的物件。您需要指定以下選項：<br><br>         * 指定分隔符：表示用於拆分物件而使用的分隔符。<br><br>         * 選擇層級：表示將獲取的物件拆分為多個層級的片段後，實際所要的物件所在的層級。層級是非 0 的整數，絕對值不能大於層級總數。如果層級是負整數，表示從最右邊的層級開始向左計數。<br><br>   * 改寫時參數來源：參見 **自定义URI** 中該配置的描述。<br><br>* 客戶端網域名稱：表示請求網域名稱。<br><br>* Referer Header：表示使用者請求中 Referer 標頭。<br><br>* Origin Header：表示使用者請求中 Origin 標頭。<br><br>* 客戶端IP：表示傳送使用者請求的用戶端 IP 位址。<br><br>* User\-Agent：表示使用者請求中 User\-Agent 標頭。<br><br>* 自定義請求頭：表示您指定的標頭。您需要在下方輸入該標頭。該標頭不能是 Referer、Origin 和 User\-Agent。需要留意的是：<br><br>   * 如果您指定的標頭不存在，則物件值為空（""）。<br><br>   * 關於該配置的輸入要求，參見 [配置輸入要求](https://docs.byteplus.com/en/docs/18/46966#%E9%85%8D%E7%BD%AE%E8%BC%B8%E5%85%A5%E8%A6%81%E6%B1%82)。<br><br>* Cookie：表示請求中的一個 cookie。您需要在下方指定该 cookie 的 key，CDN 會獲取该 cookie 的 value。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">cookie 的格式必須符合 <a href="https://datatracker.ietf.org/doc/html/rfc6265">RFC 6265</a>。否則，CDN 可能無法獲取到 cookie 的 value。   </div><br>   <br><br>* 完整URI：表示請求的完整路徑，不包含查詢字串。<br><br>   * 改寫時參數來源：參見上方 **自訂 URI** 中該配置的描述。 |
|參數組合 |驗證參數組合方式 |表示拼接籤算物件而使用的拼接符。按籤算物件列表中物件的順序，CDN 使用您指定的拼接符拼接這些物件，得到一個字串。然後，CDN 對該字串應用鑑權演算法計算權杖。<br><br>&nbsp;<br><br>如果您不指定該配置，表示拼接符為空（""）。<br><br><br>* 關於拼接符的輸入要求，參見 [配置輸入要求](https://docs.byteplus.com/en/docs/18/46966#%E9%85%8D%E7%BD%AE%E8%BC%B8%E5%85%A5%E8%A6%81%E6%B1%82)。 |
|鉴权算法 |鑑權參數計算規則 |表示計算權杖所使用的演算法。對於拼接籤算物件後得到的字串，CDN 對該字串應用您指定的演算法，以獲得權杖。您可以指定最多 5 個演算法，CDN 按演算法的出現順序產生權杖的計算公式。<br><br>&nbsp;<br><br>您可以指定的演算法有：Base64、Base64URL、MD5、MD5_Bin、SHA\-1、SHA\-224、SHA\-256、SHA\-384、SHA\-512、SHA3\-224、SHA3\-256、SHA3\-384、SHA3\-512、UpperCase()、LowerCase()。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">UpperCase() 將輸入字串轉換成大寫，LowerCase() 將輸入字串轉換成小寫。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">MD5_Bin 表示對輸入字串應用 MD5 演算法，演算法使用二進位模式讀取輸入字串。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">如果您指定了 MD5_Bin，您必須指定下一個演算法為 Base64URL。正確配置和錯誤配置的例子如下：</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">正確配置：SHA\-1、MD5_Bin、Base64URL</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">正確配置：SHA\-1、MD5_Bin、Base64URL、Base64URL、MD5_Bin、Base64URL</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">錯誤配置：SHA\-1、MD5_Bin、Base64URL、Base64URL、MD5_Bin</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">錯誤配置：SHA\-1、MD5_Bin</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">錯誤配置：SHA\-1、MD5_Bin、SHA3\-256、Base64URL</div><br> |
|M3U8 改寫 |M3U8 改寫 |如果請求 URL 指向一個 HLS Manifest，您可以配置是否對該 Manifest 中的 URL 新增權杖。<br><br><br>* 啟用：表示 CDN 會在返回 HLS Manifest 前，會先對檔案中 `EXTINF` 標籤下的影片分片 URL 新增權杖，然後返回改寫後的 HLS Manifest。<br><br>* 禁用：表示 CDN 不改寫 HLS Manifest。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">HLS Manifest 必須符合 <a href="https://datatracker.ietf.org/doc/html/rfc8216">RFC 8216</a>，否則 CDN 不會對檔案進行改寫。</div><br><br><br>關於 CDN 預設的改寫邏輯以及範例，參見 [影片 Manifest 的預設改寫邏輯](https://docs.byteplus.com/en/docs/18/46966#%E5%BD%B1%E7%89%87-manifest-%E6%AA%94%E6%A1%88%E7%9A%84%E9%A0%90%E8%A8%AD%E6%94%B9%E5%AF%AB%E9%82%8F%E8%BC%AF)。<br><br>&nbsp;<br><br>**注意事項**<br><br><br>* 如果 **權杖獲取方式** 是 **自定義請求頭** 或者 **Cookie**，您無法啟用 **M3U8 改寫**，該配置會置灰。<br><br>* 如果某个分片 URL 中包含相對路徑，CDN 會先將相對路徑替換為絕對路徑，然後再新增權杖。<br><br>* 如果分片 URL 中不存在相應的查詢參數或者相應的目錄層級，CDN 不改寫該 URL。<br><br>* 如果 HLS Manifest 和 DASH Manifest 是壓縮的，CDN 無法對檔案進行改寫。請求檔案被壓縮，主要有以下場景：<br><br>   * 來源伺服器向 CDN 返回檔案時，對檔案進行了壓縮。在這個情況下，請在來源伺服器做相應配置，不壓縮 HLS Manifest 。<br><br>   * 在 CDN 中，您启用了 "智能压缩"。在这个情况下，请配置 "智能压缩"，过滤掉后缀是 .m3u8 的文件。 |
||M3U8 標籤改寫開關 |在 HLS Manifest 中，如果其他標籤下有需要 CDN 新增權杖的 URL，您可以在該配置中指定這些標籤。您需要啟用該配置，然後點擊 **新增條件**。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">輸入的標籤無需以井字型大小（#）開頭。</div><br><br><br>在您新增標籤後，CDN 除了會對 `EXTINF` 和 `EXT-X-STREAM-INF` 標籤下的 URL 新增權杖外，還會對您指定的這些標籤裡的 URL 新增權杖。參見 [範例](https://docs.byteplus.com/en/docs/18/46966#m3u8-%E9%A1%8D%E5%A4%96%E6%A8%99%E7%B1%A4%E7%9A%84%E6%94%B9%E5%AF%AB%E7%AF%84%E4%BE%8B)。 |
|DashMPD |DashMPD |如果請求 URL 指向一個 DASH Manifest，您可以配置是否對該 Manifest 中的 URL 新增權杖。<br><br><br>* 啟用：表示 CDN 在傳回 DASH Manifest 前，會先對 `SegmentTemplate` 標籤內的 `initialization` 和 `media` 屬性中的視訊切片 URI 新增權杖，然後傳回改寫後的 DASH Manifest。<br><br>* 禁用：表示 CDN 不改寫 DASH Manifest。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">DASH Manifest 必須符合 <a href="https://www.iso.org/standard/83314.html">ISO/IEC 23009\-1:2022</a>，否則 CDN 不會對檔案進行改寫。</div><br><br><br>關於 CDN 預設的改寫邏輯，參見 [影片 Manifest 的預設改寫邏輯](https://docs.byteplus.com/en/docs/18/46966#%E5%BD%B1%E7%89%87-manifest-%E6%AA%94%E6%A1%88%E7%9A%84%E9%A0%90%E8%A8%AD%E6%94%B9%E5%AF%AB%E9%82%8F%E8%BC%AF)。關於 DASH Manifest 的改寫範例，參見 [改寫範例](https://docs.byteplus.com/en/docs/18/46966#%E5%BD%B1%E7%89%87-manifest-%E7%9A%84%E6%94%B9%E5%AF%AB%E7%AF%84%E4%BE%8B)。<br><br>&nbsp;<br><br>**注意事項**<br><br><br>* 如果 **權杖獲取方式** 是 **自定義請求頭** 或者 **Cookie**，您無法啟用 **DashMPD**，該配置會置灰。<br><br>* 如果某个分片 URL 中包含相對路徑，CDN 會先將相對路徑替換為絕對路徑，然後再新增權杖。<br><br>* 如果分片 URL 中不存在相應的查詢參數或者相應的目錄層級，CDN 不改寫該 URL。<br><br>* 如果 DASH Manifest 是壓縮的，CDN 無法對檔案進行改寫。請求檔案被壓縮，主要有以下場景：<br><br>   * 來源伺服器向 CDN 返回檔案時，對檔案進行了壓縮。在這個情況下，請在來源伺服器做相應配置，不壓縮 DASH Manifest。<br><br>   * 在 CDN 中，您啟用了「智慧壓縮」。在這個情況下，請配置「智慧壓縮」，過濾掉副檔名是 .mpd 的檔案。 |
||Dash MPD 變數擴展 |在上方 **驗證參數選擇** 配置中，如果您指定的籤算物件來自被改寫 URL，並且影片分片的 URL 中包含 `$RepresentationID$` 變數，您可以啟用 **Dash MPD 變數擴展**。<br><br><br>* 如果該配置啟用，CDN 會先改寫影片分片 URL，將 `$RepresentationID$` 變數替換為實際值。然後，CDN 基於改寫後的 URL 產生權杖。<br><br>* 如果該配置未啟用，`$RepresentationID$` 本身會作為固定字串用於產生權杖。<br><br><br>參見下方的 [額外說明](https://docs.byteplus.com/en/docs/18/46966#dash-mpd-%E8%AE%8A%E6%95%B8%E6%93%B4%E5%B1%95-%E9%85%8D%E7%BD%AE%E7%9A%84%E9%A1%8D%E5%A4%96%E8%AA%AA%E6%98%8E%E5%92%8C%E7%AF%84%E4%BE%8B)。 |
|特殊改寫方式 | |表示檔案改寫的擴展配置。只有當 **M3U8 改寫** 或 **DashMPD** 啟用、或者兩者均啟用時，您才能啟用該配置。<br><br>&nbsp;<br><br>在該配置中，您可以設定以下內容：<br><br><br>* 改寫方式：表示 CDN 如何在影片分片 URL 中新增權杖。<br><br>* 權杖獲取方式：當啟用特殊重寫時，您需要單獨指定一系列物件。CDN 會將這些物件串接成權杖並加入至影片片段 URL 中。<br><br><br>啟用此設定後，CDN 將不再依據預設重寫邏輯，而是依據特殊重寫邏輯來重寫影片 Manifest。<br><br><br>* 關於預設重寫邏輯，請參閱 [影片 Manifest 的預設重寫邏輯](https://docs.byteplus.com/en/docs/18/46966#%E5%BD%B1%E7%89%87-manifest-%E6%AA%94%E6%A1%88%E7%9A%84%E9%A0%90%E8%A8%AD%E6%94%B9%E5%AF%AB%E9%82%8F%E8%BC%AF)。<br><br>* 關於特殊重寫邏輯，請參閱 [影片 Manifest 的特殊重寫邏輯](https://docs.byteplus.com/en/docs/18/46966#%E5%BD%B1%E7%89%87-manifest-%E6%AA%94%E6%A1%88%E7%9A%84%E9%A0%90%E8%A8%AD%E6%94%B9%E5%AF%AB%E9%82%8F%E8%BC%AF)。 |
| |改寫方式 |表示 CDN 如何在影片分片 URL 中新增產生的權杖。該配置有以下選項：<br><br><br>* 指定查詢參數：表示將 URL 中指定的查詢參數設定為權杖。<br><br>   * 如果 URL 中不存在該查詢參數，CDN 會在 URL 中新增該查詢參數。<br><br>   * 如果 URL 中已存在該查詢參數，該查詢參數的值會被設定為權杖。<br><br>* 指定 URI 層級：表示將權杖新增到 URL 路徑中作為指定目錄層級的目錄。<br><br>   * 您需要在下方指定該目錄層級。層級是一個非 0 的整數。<br><br>      * 如果層級是一個正整數，表示從路徑中最左邊的目錄開始向右計數，以定位相應目錄。<br><br>      * 如果層級是一個負整數，表示從路徑中最右邊的目錄開始向左計數。<br><br>         例子：<br><br>      * 一個影片分片的 URL 是 `/dir1/dir2/videoclip1.ts`，您需要將權杖新增到該路徑中作為第一層級的目錄。在這個情況下，您可以指定 URL 層級為 `1` 或者 `-3`。<br><br>   * 如果 URL 中不存在該層級，則 CDN 不改寫該 URL。 |
| |驗證參數組合方式 |表示拼接籤算物件而使用的拼接符。按籤算物件列表中物件的順序，CDN 使用您指定的拼接符拼接這些物件，以產生新增到影片分片 URL 中的權杖。<br><br>&nbsp;<br><br>如果您不指定該配置，表示拼接符為空（""）。 |
| |驗證參數選擇 |表示一個物件列表。CDN 將這些物件拼接而產生新增到影片分片 URL 中的權杖。點擊 **驗證參數** 新增一個物件。物件類型有：<br><br><br>* 自定義（父連結）URL 參數：參見上方的 **驗證參數選擇** 中 **自定義URL參數** 的描述。<br><br>* 自定義字元：參見上方的 **驗證參數選擇** 中 **補充字串** 的描述。<br><br>* 自定義（父連結）URI：參見上方的 **驗證參數選擇** 中 **自定义URI** 的描述。<br><br>* 父連結過期時間：表示權杖的時間戳。參見上方 **過期時間管理** 中的描述。<br><br>* 籤算結果：表示 CDN 基於 **驗證參數選擇** 計算的權杖。<br><br>* 完整父連結URI：表示使用者請求的完整路徑，不包含查詢字串。 |
|其他設定 |鑑權參數設定 |表示是否在來源伺服器請求中包含使用者請求中的權杖。<br><br>&nbsp;<br><br>該配置有以下選項：<br><br><br>* 去鑑權參數來源伺服器請求：表示在來源伺服器請求中不包含權杖和權杖時間戳。<br><br>* 保留鑑權參數來源伺服器請求：表示在來源伺服器請求中包含權杖和權杖時間戳。來源伺服器請求中權杖出現的位置與 **權杖獲取方式** 相同。在這個情況下，請在來源伺服器上禁用 URL 鑑權。 |


<span id="配置輸入要求"></span>
## 配置輸入要求


|**配置** |**輸入要求** |
|---|---|
|權杖獲取方式 |**查詢參數**，**自定義請求頭**、**Cookie** 的輸入要求如下：<br><br><br>* 長度為 1 ~ 100 個字元。<br><br>* 只能包含字母、數字、底線（_）、連字元（\-）、句點（.）、逗號（,）、驚嘆號（!）。<br><br>* 不能只包含符號，也不能只包含數字。 |
|過期時間管理 |相關配置的輸入要求與 **權杖獲取方式** 的輸入要求相同。 |
|認證參數獲取 |**補充字串**、**分隔符**、**拼接符** 的輸入要求如下：<br><br><br>* 補充字串的長度為 1 ~ 20 個字元。分隔符和拼接符的長度為 1 個字元。<br><br>* 只能包含字母、數字、底線（_）、連字元（\-）、反斜線（/）、驚嘆號（!）。<br><br><br>**查詢參數**與 **自定義請求頭** 的輸入要求與 **權杖獲取方式** 的輸入要求相同。 |
|驗證參數組合方式 |該配置的輸入要求與 **認證參數獲取** 中 **拼接符** 的輸入要求相同。 |
|規則名稱 |長度不能超過 120 個字元，可以包含漢字、字母、數字、連字元（\-）、底線（_）和空格。一個漢字佔 3 個字元。 |


<span id="影片-manifest-檔案的預設改寫邏輯"></span>
## 影片 Manifest 檔案的預設改寫邏輯

CDN 預設基於 **權杖獲取方式** 和 **時間戳獲取方式** 的設定來改寫影片分片的 URL。


* 如果 **獲取方式** 是 **指定查詢參數**，CDN 將分片 URL 中相應的查詢參數設定為權杖或權杖時間戳。如果該查詢參數不存在，CDN 會在 URL 新增該查詢參數。

* 如果 **獲取方式** 是 **指定 URI 層級**，CDN 在分片 URL 的相應目錄層級插入一個目錄，並將該目錄設定為權杖或權杖時間戳。


範例：

待改寫的影片分片 URL 是 `/a/b/1.ts`。時間戳的獲取方式是請求路徑中第一層級的目錄。權杖是 `r5Bp7zX9k2Lc`，時間戳是 `1725786731`。


* 如果權杖的獲取方式是請求路徑中第二層級的目錄，改寫後的分片 URL 是 `/1725786731/r5Bp7zX9k2Lc/a/b/1.ts`。

* 如果權杖的獲取方式是請求路徑中第三層級的目錄，改寫後的分片 URL 是 `/1725786731/a/b/r5Bp7zX9k2Lc/1.ts`。

* 如果權杖的獲取方式是請求路徑中第四層級的目錄，則 CDN 不改寫该分片 URL。原因是分片 URL 中不存在該層級的目錄。


<span id="影片-manifest-的改寫範例"></span>
## 影片 Manifest 的改寫範例

**HLS Manifest 的改寫範例**

假設權杖的來源是使用者請求路徑中第一層級的目錄，Timestamp 的來源是使用者請求路徑中第二層級的目錄。權杖是 `r5Bp7zX9k2Lc`，timestamp 是 `1725786731`。來源伺服器上的 HLS Manifest 包含以下內容。

```xml
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:10
#EXT-X-MEDIA-SEQUENCE:0

#EXTINF:10,
/videos/segment0.ts
#EXT-X-ENDLIST
```


改寫後的 Manifest 內容如下。

```xml
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:10
#EXT-X-MEDIA-SEQUENCE:0

#EXTINF:10,
/r5Bp7zX9k2Lc/1725786731/videos/segment0.ts
#EXT-X-ENDLIST
```


**DASH Manifest 的改寫範例**

假設權杖的來源是使用者請求路徑中第一層級的目錄，Timestamp 的來源是使用者請求路徑中第二層級的目錄。權杖是 `r5Bp7zX9k2Lc`，timestamp 是 `1725786731`。來源伺服器上的 DASH Manifest 包含以下內容。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<MPD xmlns="urn:mpeg:dash:schema:mpd:2011"
     type="static"
     mediaPresentationDuration="PT0H10M0S"
     minBufferTime="PT2S">
  <Period duration="PT0H10M0S">
    <AdaptationSet mimeType="video/mp4" codecs="avc1.640028" frameRate="25/1">
      <Representation id="1" bandwidth="2000000" width="1280" height="720">
        <SegmentTemplate initialization="/videos/init.mp4"
                         media="/segments/seg-$Number$.m4s"
                         startNumber="1"
                         timescale="1000"
                         duration="4000"/>
      </Representation>
    </AdaptationSet>
  </Period>
</MPD>
```


改寫後的 Manifest 如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<MPD xmlns="urn:mpeg:dash:schema:mpd:2011"
     type="static"
     mediaPresentationDuration="PT0H10M0S"
     minBufferTime="PT2S">
  <Period duration="PT0H10M0S">
    <AdaptationSet mimeType="video/mp4" codecs="avc1.640028" frameRate="25/1">
      <Representation id="1" bandwidth="2000000" width="1280" height="720">
        <SegmentTemplate initialization="/r5Bp7zX9k2Lc/1725786731/videos/init.mp4"
                         media="/r5Bp7zX9k2Lc/1725786731/segments/seg-$Number$.m4s"
                         startNumber="1"
                         timescale="1000"
                         duration="4000"/>
      </Representation>
    </AdaptationSet>
  </Period>
</MPD>
```


<span id="m3u8-額外標籤的改寫範例"></span>
## M3U8 額外標籤的改寫範例

假設來源伺服器上的 HLS Manifest 的內容如下。

```m3u8
#EXTM3U
#EXT-X-VERSION:6
#EXT-X-STREAM-INF:BANDWIDTH=5000000,RESOLUTION=1920x1080,CODECS="avc1.64002A,mp4a.40.2",AUDIO="audio"
/video/high/stream.m3u8
#EXT-X-MEDIA:TYPE=AUDIO,GROUP-ID="audio",NAME="English",LANGUAGE="en",DEFAULT=YES,AUTOSELECT=YES,URI="/audio/en/audio.m3u8"
```


在該 Manifest 中，`EXT-X-STREAM-INF` 標籤指定了影片流的資訊，`EXT-X-MEDIA` 標籤指定了音訊流的資訊。您需要 CDN 改寫 Manifest 中所有標籤下的 URL。

在這個場景下，如果您僅僅啟用 M3U8 改寫，則 CDN 僅會改寫 `EXT-X-STREAM-INF` 標籤下的 URL。因此，您需要開啟 M3U8 標籤改寫開關，新增 `EXT-X-MEDIA` 標籤，然後儲存配置。

假設權杖的來源是使用者請求路徑中第一層級的目錄，Timestamp 的來源是使用者請求路徑中第二層級的目錄。權杖是 `r5Bp7zX9k2Lc`，timestamp 是 `1725786731`。則改寫後的 Manifest 內容如下：

```m3u8
#EXTM3U
#EXT-X-VERSION:6
#EXT-X-STREAM-INF:BANDWIDTH=5000000,RESOLUTION=1920x1080,CODECS="avc1.64002A,mp4a.40.2",AUDIO="audio"
/r5Bp7zX9k2Lc/1725786731/video/high/stream.m3u8
#EXT-X-MEDIA:TYPE=AUDIO,GROUP-ID="audio",NAME="English",LANGUAGE="en",DEFAULT=YES,AUTOSELECT=YES,URI="/r5Bp7zX9k2Lc/1725786731/audio/en/audio.m3u8"
```


<span id="影片-manifest-的特殊重寫邏輯"></span>
## 影片 Manifest 的特殊重寫邏輯

在 **特殊重寫** 設定中，您需要指定一系列物件。通常，這些物件包含權杖和權杖時間戳。CDN 會將您指定的物件進行串接以產生權杖，並將該權杖加入至影片片段 URL 中您指定的位置。

**範例**

在 **特殊重寫** 設定中，您指定的物件有使用者請求中的權杖、權杖時間戳和一個固定字串。權杖是 `r5Bp7zX9k2Lc`，時間戳是 `1725786731`、固定字串是 `abc123`、拼接符是 `-`。此外，您指定權杖加入至片段 URL 中第二個層級的目錄。假設重寫前的片段 URL 是 `/a/b/1.ts`，則重寫後的 URL 是 `/a/r5Bp7zX9k2Lc-1725786731-abc123/b/1.ts`。

<span id="dash-mpd-變數擴展-配置的額外說明和範例"></span>
## "Dash MPD 變數擴展" 配置的額外說明和範例

<span id="僅-representation-變數會被替換為實際值，其他變數不會被替換"></span>
### 僅 `$Representation$` 變數會被替換為實際值，其他變數不會被替換

在下方的變數替換範例一中，`$Number$`變數未被替換。因此，`BBB_720_1M_video_$Number$.mp4` 與 `BBB_720_2M_video_$Number$.mp4` 會作為一個字串參與權杖計算。

<span id="原始-segmenttemplate-內容會被保留"></span>
### **原始 ** **`SegmentTemplate`** ** 內容會被保留**

變數替換後的 Manifest 保留了原始 `SegmentTemplate` 的內容。例如，在範例一中，變數替換後的 Manifest保留了以下內容。

```xml
<SegmentTemplate timescale="12288" presentationTimeOffset="1024" duration="24576" media="BBB_720_$RepresentationID$M_video_$Number$.mp4" startNumber="1" initialization="BBB_720_$Representation$M_video_init.mp4"/>
```


<span id="配置生效的前提條件"></span>
### **配置生效的前提條件**

前提條件是`SegmentTemplate` 與 `Representation` 之間不能出現其他內容。否則，CDN 不會將 `$Representation$` 變數替換為實際值。在以下範例中，由於 `SegmentTemplate` 和 `Representation` 中出現了其他元素，CDN 不會替換 `$Representation$` 變數。

```xml
<SegmentTemplate timescale="12288" presentationTimeOffset="1024" duration="24576"media="BBB_720_$RepresentationID$M_video_$Number$.mp4" startNumber="1"initialization="BBB_720_$Representation$M_video_init.mp4"/>
<ContentComponent id="1" contentType="video" lang="en"/>
<Representation id="1" mimeType="video/mp4" codecs="avc1.4d401f" width="1280" height="720"frameRate="24" sar="1:1" startWithSAP="1" bandwidth="980104"/>
```


<span id="變數替換範例"></span>
### 變數替換範例

假設權杖的來源是使用者請求路徑中第一層級的目錄，Timestamp 的來源是使用者請求路徑中第二層級的目錄。權杖是 `r5Bp7zX9k2Lc`，timestamp 是 `1725786731`。

**範例一：SegmentTemplate 與 Representation 下均無子元素**

變數替換前的 Manifest 內容如下。

```xml
<AdaptationSet segmentAlignment="true" maxWidth="1280" maxHeight="720" maxFrameRate="24" par="16:9">
  <SegmentTemplate timescale="12288" presentationTimeOffset="1024" duration="24576" media="BBB_720_$RepresentationID$M_video_$Number$.mp4" startNumber="1" initialization="BBB_720_$Representation$M_video_init.mp4"/>
  <Representation id="1" mimeType="video/mp4" codecs="avc1.4d401f" width="1280" height="720" frameRate="24" sar="1:1" startWithSAP="1" bandwidth="980104"/>
</AdaptationSet>
```


變數替換後的 Manifest 內容如下。

```xml
<AdaptationSet segmentAlignment="true" maxWidth="1280" maxHeight="720" maxFrameRate="24" par="16:9">
  <SegmentTemplate timescale="12288" presentationTimeOffset="1024" duration="24576" media="BBB_720_$RepresentationID$M_video_$Number$.mp4" startNumber="1" initialization="BBB_720_$Representation$M_video_init.mp4"/>
  <Representation id="1" mimeType="video/mp4" codecs="avc1.4d401f" width="1280" height="720" frameRate="24" sar="1:1" startWithSAP="1" bandwidth="980104">
    <SegmentTemplate timescale="12288" presentationTimeOffset="1024" duration="24576" media="/ITrRYdyGL1LG9V7qrohmiQ/1725786731/BBB_720_1M_video_$Number$.mp4" startNumber="1" initialization="/ITrRYdyGL1LG9V7qrohmiQ/1725786731/BBB_720_1M_video_init.mp4"/>
  </Representation>
</AdaptationSet>
```


**範例二：SegmentTemplate 下無子元素，Representation 下有子元素**

變數替換前的 Manifest 內容如下。

```xml
<AdaptationSet lang="en" mimeType="audio/mp4" segmentAlignment="true" startWithSAP="1">
  <SegmentTemplate duration="4000" initialization="/video1/2023/08/31/07/3b679516/$RepresentationID$/init.mp4" media="/video1/2023/08/31/07/3b679516/$RepresentationID$/seg-$Number$.m4s" startNumber="1" timescale="1000"/>
  <Representation audioSamplingRate="44100" bandwidth="71514" codecs="mp4a.40.2" id="audio/en/mp4a/1">
    <AudioChannelConfiguration schemeIdUri="urn:mpeg:dash:23003:3:audio_channel_configuration:2011" value="2"/>
  </Representation>
</AdaptationSet>
```


變數替換後的 Manifest 內容如下。

```xml
<AdaptationSet lang="en" mimeType="audio/mp4" segmentAlignment="true" startWithSAP="1">
  <SegmentTemplate duration="4000" initialization="/video1/2023/08/31/07/3b679516/$RepresentationID$/init.mp4" media="/video1/2023/08/31/07/3b679516/$RepresentationID$/seg-$Number$.m4s" startNumber="1" timescale="1000"/>
  <Representation audioSamplingRate="44100" bandwidth="71514" codecs="mp4a.40.2" id="audio/en/mp4a/1">
    <SegmentTemplate duration="4000" initialization="/ITrRYdyGL1LG9V7qrohmiQ/1725786731/video1/2023/08/31/07/3b679516/audio/en/mp4a/1/init.mp4" media="/ITrRYdyGL1LG9V7qrohmiQ/1725786731/video1/2023/08/31/07/3b679516/audio/en/mp4a/1/seg-$Number$.m4s" startNumber="1" timescale="1000"/>
    <AudioChannelConfiguration schemeIdUri="urn:mpeg:dash:23003:3:audio_channel_configuration:2011" value="2"/>
  </Representation>
</AdaptationSet>
```


**範例三：SegmentTemplate 下有子元素，Representation 下無子元素**

變數替換前的 Manifest 內容如下。

```xml
<AdaptationSet id="1" contentType="video" segmentAlignment="true" startWithSAP="1" bitstreamSwitching="true">
    <SegmentTemplate timescale="90000" initialization="/media-static/261dd1e627/2367541c-3e96-4ba4-aa2e-ca77fc48d82b/2023110602/$RepresentationID$/$RepresentationID$-20231026193517-init.m4s" media="/media-static/261dd1e627/2367541c-3e96-4ba4-aa2e-ca77fc48d82b/2023110602/$RepresentationID$/20231026193517-$RepresentationID$-$Number%01d$.m4s" startNumber="148166">
         <SegmentTimeline>
            <S d="540000" r="19" t="80010231598"></S>
        </SegmentTimeline>
    </SegmentTemplate>
    <Representation id="360p" mimeType="video/mp4" codecs="avc1.4d001e" bandwidth="502000" width="640" height="360" frameRate="25/1"></Representation>
</AdaptationSet>
```


變數替換後的 Manifest 內容如下。

```xml
<AdaptationSet id="1" contentType="video" segmentAlignment="true" startWithSAP="1" bitstreamSwitching="true">
    <SegmentTemplate timescale="90000" initialization="/media-static/261dd1e627/2367541c-3e96-4ba4-aa2e-ca77fc48d82b/2023110602/$RepresentationID$/$RepresentationID$-20231026193517-init.m4s" media="/media-static/261dd1e627/2367541c-3e96-4ba4-aa2e-ca77fc48d82b/2023110602/$RepresentationID$/20231026193517-$RepresentationID$-$Number%01d$.m4s" startNumber="148166">
        <SegmentTimeline>
            <S d="540000" r="19" t="80010231598"></S>
        </SegmentTimeline>
    </SegmentTemplate>
    <Representation id="360p" mimeType="video/mp4" codecs="avc1.4d001e" bandwidth="501000" width="640" height="360" frameRate="25/1">
        <SegmentTemplate timescale="90000" initialization="/GDTD6aHs2waOPSaqrDz3-Q/1725786731/media-static/261dd1e627/2367541c-3e96-4ba4-aa2e-ca77fc48d82b/2023110602/360p/360p-20231026193517-init.m4s" media="/GDTD6aHs2waOPSaqrDz3-Q/1725786731/media-static/261dd1e627/2367541c-3e96-4ba4-aa2e-ca77fc48d82b/2023110602/360p/20231026193517-360p-$Number%01d$.m4s" startNumber="148161">
            <SegmentTimeline>
                <S d="540000" r="19" t="80007531598"></S>
            </SegmentTimeline>
        </SegmentTemplate>
    </Representation>
</AdaptationSet>
```


<span id="快取清除"></span>
## 快取清除

在您啟用了 URL 鑑權後，如果您需要對請求檔案發起快取清除操作，參考以下指引：


|**權杖或者權杖時間戳的來源** |**清除操作指引** |**額外說明** |
|---|---|---|
|查詢參數 |在您發起清除操作時，指定的 URL 中需要包含表示權杖或權杖時間戳的查詢參數。 |您可以在規則引擎或者常規配置中配置 "快取索引鍵" 特性，排除表示權杖或權杖時間戳的查詢參數。這樣，在您發起清除操作時，就無需在 URL 中包含這些查詢參數了。 |
|URI 層級 |在您發起清除操作時，指定的 URL 中不能包含權杖和權杖時間戳。 | |
|請求頭 |無法通過指定檔案 URL 來進行清除操作。 |您可以在規則引擎中配置 "快取索引鍵" 特性，排除表示權杖或權杖時間戳的請求頭或者 Cookie。這樣，您就可以通過指定檔案 URL 來進行清除操作了。 |
|Cookie |||


<span id="範例"></span>
### 範例

**範例一**

假設權杖的來源是查詢參數 `token-param`，權杖時間戳的來源是請求路徑中第 2 個目錄。請求 URL 是 `https://www.example.com/files/1747993083/chinese/myfile?token-param=sadfasdfasf`。


* 如果您未配置 "快取索引鍵" 特性排除 `token-param`，當您發起清除操作時，您指定的 URL 是 `https://www.example.com/files/chinese/myfile?token-param=sadfasdfasf`。

* 如果您配置了 "快取索引鍵" 特性排除 `token-param`，當您發起清除操作時，您指定的 URL 是 `https://www.example.com/files/chinese/myfile`。


**範例二**

假設權杖的來源是請求路徑中第 1 個目錄，權杖時間戳的來源是請求路徑中第 2 個目錄。請求 URL 是 `https://www.example.com/files/sadfasdfasf/1747993083/chinese/myfile`。在這個情況下，當您發起清除操作時，您指定的 URL 是 `https://www.example.com/files/chinese/myfile`。

<span id="權杖計算範例程式碼"></span>
## 權杖計算範例程式碼

用戶端請求中包含的權杖可以由專用的簽名伺服器提供，也可以在用戶端生成。您可以參考以下範例程式碼，使用您熟悉的程式語言在用戶端或者簽名伺服器上實現簽名的計算邏輯。

範例程式碼包含以下部分：


* Type\-F 配置模組。您可以通過以下任意方式定義 Type\-F 配置：

   * JSON 配置。

   * 結構體，僅在 Go 和 Java 範例程式碼中可用。

* 權杖計算模組：根據您定義的 Type\-F 配置生成權杖，並將其添加到請求中。


您可以在範例程式碼中指定請求 URL 進行測試。範例程式碼會生成包含權杖的請求，並列印請求正文和請求 URL。

**Go 範例程式碼**

使用 JSON 定義 Type\-F 配置

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_dad81b2171083a5024a24f29bd1a6caf.txt" name="TypeF for Go_JSON.txt">TypeF for Go_JSON.txt</Attachment>


使用結構體 `AuthRulesF` 定義 Type\-F 配置

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9d6ccf4f3a460da2e13ae0d99490dbb0.txt" name="TypeF for Go_Struct.txt">TypeF for Go_Struct.txt</Attachment>


**Python 範例程式碼**

使用 JSON 定義 Type\-F 配置

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f621b1613dda2f805840baaa34b1ad41.txt" name="TypeF for Python_JSON.txt">TypeF for Python_JSON.txt</Attachment>


**PHP 範例程式碼**

使用 JSON 定義 Type\-F 配置

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_76b52faf00b163847270cef67ec2595c.txt" name="TypeF for PHP_JSON.txt">TypeF for PHP_JSON.txt</Attachment>


**Java 範例程式碼**

使用 JSON 定義 Type\-F 配置

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e7a18b115d911780249d47acdfcce3bf.txt" name="TypeF for Java_JSON.txt">TypeF for Java_JSON.txt</Attachment>


使用結構體 `JsonArray` 定義 Type\-F 配置

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_98bda910c299b729027745814011b4c1.txt" name="TypeF for Java_Struct.txt">TypeF for Java_Struct.txt</Attachment>
