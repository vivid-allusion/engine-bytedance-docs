---
title: "設定 hosts 檔案測試網域名稱"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-test-domain-name-with-hosts-zh-tw"
---

在前面的步驟中，您已成功地在 BytePlus CDN 控制台中新增了網域名稱。同時，CDN 已經為您的網域名稱分配了一個 CNAME。在您配置 DNS 解析記錄將您網站的網域名稱指向該 CNAME 之前，建議您配置 hosts 檔案測試網域名稱的存取。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">需要留意的是，測試 CNAME 的過程會在 CDN 側產生極少量的流量，這些流量是會被計費的。</div>


* <div data-tips="true" data-tips-type="tip">該文件是基於 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs-overview_zh-tw">教學簡介</a> 中描述的場景。</div>



<span id="步驟一：取得-cname"></span>
# 步驟一：取得 CNAME


1. 登入 [BytePlus CDN 管理控制台](https://console.byteplus.com/cdn)。

2. 在左側導覽列，點擊 **網域名稱**。

3. 在 **網域名稱** 頁面，找到您新增的網域名稱 `www.example.com`。

4. 在 **CNAME** 列，點擊 **複製** 按鈕。

   您取得的 CNAME 應該是 `www.example.com.bplslb.com`。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_23cf273e4cad9adc812c451f9248af2a.png) </span>


<span id="步驟二：取得該-cname-的-ip-位址"></span>
# 步驟二：取得該 CNAME 的 IP 位址

根據您用戶端的作業系統，參考以下步驟取得 CNAME 的 IP 位址。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">以下截圖中的那個 IP 位址僅用於演示目的，並不是真實的。</div>


<span id="macos-和-linux：使用-dig-命令取得該-ip-位址"></span>
## macOS 和 Linux：使用 dig 命令取得該 IP 位址


1. 在一個 Terminal 視窗中，執行命令 `dig www.example.com.bplslb.com`。

2. 在 **ANSWER SECTION** 下方，找到該 CNAME 的 IP 位址。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_004df10162659ecc7b86c105e5061295.png) </span>


<span id="windows：使用-ping-命令取得該-ip-位址"></span>
## Windows：使用 ping 命令取得該 IP 位址


1. 在一個 **命令提示字元** 視窗中，執行命令 `ping www.example.com.bplslb.com`。

2. 在命令下方的資訊中，找到該 CNAME 的 IP 位址。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c1de146606226ae567cdd4f04d55fd64.png) </span>


<span id="第三步：驗證該-ip-位址是否歸屬於-cdn"></span>
# 第三步：驗證該 IP 位址是否歸屬於 CDN

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在本文中，假設您取得的 IP 位址是 <code>203.0.113.5</code>。</div>



1. 開啟 [診斷工具](https://console.byteplus.com/cdn/cdn-volc/diagnosis)。

2. 輸入取得的 IP 位址，點擊 **查詢**。

3. 在查詢結果中，查看 **是否歸屬於 CDN** 列顯示的值。

   * 如果值是 **是**，表示該 IP 位址是一個 CDN 邊緣伺服器的，符合預期。

   * 如果值是 **否**，表示該 IP 位址不歸屬於 CDN。請 [提交工單](https://console.byteplus.com/workorder/create)。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f6f7c3357f98bc6f88b0bcba18f1231e.png) </span>

<span id="第四步：配置作業系統的-hosts-檔案"></span>
# 第四步：配置作業系統的 hosts 檔案

在 hosts 檔案中，您需要新增一個條目，將您網站的網域名稱指向該 IP 位址。

根據您用戶端的作業系統，參考以下步驟配置 hosts 檔案。

<span id="macos：修改-hosts-檔案"></span>
## macOS：修改 hosts 檔案


1. 在一個 Terminal 視窗中，執行命令 `sudo nano /etc/hosts`。

2. 在 hosts 檔案檔案末尾，輸入 `203.0.113.5 www.example.com`。

3. 按 `CTRL` + `O` 儲存檔案，然後按 `CTRL` + `X` 退出編輯。

4. 為了使變更生效，執行命令 `sudo killall -HUP mDNSResponder`。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_580c68beca18fbf7b34c311d4fd06a1d.png) </span>


<span id="windows：修改-hosts-檔案"></span>
## Windows：修改 hosts 檔案


1. 使用 **以系統管理員身分執行** 選項開啟記事本。

2. 按 `CTRL` + `O`，在 **檔案名稱** 處輸入 `%Windir%\System32\drivers\etc\hosts`，然後點擊 **開啟**。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a14fc1f526ec32b2efa5f3f5e7ee79df.png) </span>

3. 在 hosts 檔案末尾，輸入 `203.0.113.5 www.example.com`。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_5025e1778d51d53d116d95b6dc082c22.png) </span>

4. 按 `CTRL` + `SHIFT` + `S` 儲存變更。

5. 為了使變更生效，開啟一個 **命令提示字元** 視窗，然後執行命令 `ipconfig /flushdns`。


<span id="步驟五：測試網域名稱"></span>
# 步驟五：測試網域名稱

測試前，請檢查控制台中您新增的網域名稱的狀態是否是 **在線**。如果不是，請稍等幾分鐘後，再重新整理頁面檢查。如果依然不是 **在線**，請 [提交工單](https://console.byteplus.com/workorder/create)。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_dd0d8497fe6da72f2ce94b2cdf0b67a6.png) </span>


1. 使用瀏覽器存取您網站上的某個檔案。假設該檔案的地址是 `www.example.com/sample.png`。

2. 按 `F12` 開啟 **Developer tools**。

3. 在 **Network** 標籤頁中的左側檔案列表中，找到 `sample.png`，然後點擊該檔案。

4. 在右側的 **Headers** 標籤頁中，查看 **Remote Address** 是否為 `203.0.113.5`。

   * 如果是，表示測試成功。

   * 如果不是，表示測試不成功。請檢查 hosts 檔案是否配置正確。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_abd3bbe1441a7551bf08cc605d246878.png) </span>

如果測試成功，請在 hosts 檔案中刪除您剛才新增的條目。然後在您網域名稱的 DNS 解析服務商處，建立一條 CNAME 記錄。在 CNAME 記錄中，將您的網站網域名稱指向 `www.example.com.bplslb.com`。
