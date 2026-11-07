---
title: "OAuth 2.0"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-oauth-2-0-zh-TW"
---

若要限制直播間的存取權限並啟用單一登入體驗，你可以將 OAuth 2.0 設定為觀看限制。此方法要求觀眾在觀看影片或發送評論前，必須先登入你的用戶帳號系統。本指南提供設定 BytePlus Live 直播間 OAuth 2.0 整合的概念背景與逐步操作說明。

<span id="1746671a"></span>
## 先決條件


* 你必須擁有 BytePlus 帳號或具備 Producer \> Edit 權限的 IAM 使用者。如需新增 IAM 使用者的詳細資訊，請參閱 [管理使用者、組織與角色](https://docs.byteplus.com/docs/byteplus-livesaas/guan-li-shi-yong-zhe-zu-zhi-yu-jue-se-zh-TW)。

* 請聯絡你的業務代表以取得 redirect URI。若你沒有業務代表，請點擊 [此處](https://www.byteplus.com/en/contact)填寫表單，以便 BytePlus 業務團隊稍後與你聯繫。

* 在你的用戶帳號系統中完成 BytePlus Live 的註冊。註冊過程中需要提供 redirect URI。註冊完成後，系統會產生 client ID 和 client secret，用於識別 BytePlus Live。


<span id="aa6a6a14"></span>
## 背景說明

OAuth 2.0 是一種開放且標準化的授權協議，允許第三方應用程式透過令牌存取用戶資源，而無需使用帳號名稱與密碼。在本主題中，第三方應用程式指的是 BytePlus Live。

OAuth 2.0 定義了以下四種取得令牌的授權方式：授權碼模式（Authorization Code Grant）、隱式模式（Implicit Grant）、密碼模式（Password Grant）以及用戶端憑證模式（Client Credentials Grant）。BytePlus Live 採用授權碼模式，先請求授權碼，再將其兌換為存取令牌。此授權方式在所有授權模式中提供最高安全等級。如需此授權方式的詳細資訊，請參閱 [Process](https://docs.byteplus.com/docs/byteplus-livesaas/docs-oauth-2-0-zh-TW#Process)。

<span id="ae3f70e6"></span>
## 流程

透過授權碼模式，BytePlus Live 可從你的帳號系統取得用戶資料。詳細流程如下。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e67a4a4a707e43cfa8a71c364a22bca8~tplv-goo7wpa0wc-image.image) </span>


1. 用戶透過連結或 QR code 存取 BytePlus Live 的觀看頁面。

2. BytePlus Live 向你的授權伺服器請求授權碼，並提供 client ID 與 scope。用戶會被導向你的用戶帳號系統的登入頁面。

3. 用戶登入你的用戶帳號系統後，授權伺服器會將授權碼回傳給 BytePlus Live。用戶會被導向業務代表提供的 redirect URI。

4. BytePlus Live 透過 client ID 和 client secret 驗證自身身份，並使用授權碼向你的授權伺服器請求存取令牌。

5. 授權伺服器會驗證 BytePlus Live 的身份與授權碼。驗證成功後，授權伺服器會發放存取令牌給 BytePlus Live。

6. BytePlus Live 向你的資源伺服器請求受保護的用戶資料，並提供存取令牌以進行身份驗證。

7. 資源伺服器會驗證存取令牌。驗證成功後，資源伺服器會將用戶資料提供給 BytePlus Live。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">若採用非標準 OAuth 2.0 登入模式，授權伺服器在步驟 5 發放存取權杖時，會將受保護的用戶資料回傳給 BytePlus Live。</div>


* <div data-tips="true" data-tips-type="tip">若用戶的瀏覽器已儲存自有帳號系統的登入狀態，資源擁有者在 BytePlus Live 請求授權碼後，會直接將授權碼回傳給 BytePlus Live，無需用戶再次登入。</div>



<span id="aad845fb"></span>
## 操作步驟


1. 登入 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)。

2. 在直播間列表中，點擊以開啟直播間。

3. 於左側導覽窗格，點擊 **Producer** \> **觀看限制**。

4. 將**OAuth2.0**設為驗證類型，並完成以下設定。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02cf75b685284b28982255c0eb737495~tplv-goo7wpa0wc-image.image) </span>

   
   |參數名稱 |說明 |
   |---|---|
   |登入平台名稱 |自有帳號系統的平台名稱。建議您以英文輸入名稱。 |
   |重定向 URI |用於接收授權碼的回呼 URL。此 URL 必須與您帳號系統中為 BytePlus Live 應用程式設定的 URL 相符。 |
   |授權端點 |用於取得授權碼的 URL。 |
   |權杖端點 |用於取得存取權杖的 URL。 |
   |UserInfo 端點 |選擇**URL**或**識別欄位**。<br><br><br>* **URL**：輸入用於取得用戶資訊的 URL。<br><br>* **識別欄位**：輸入用於解析用戶資訊的識別欄位。若採用非標準 OAuth 2.0 登入模式，請選擇此選項。授權伺服器在發放存取權杖給 BytePlus Live 時，BytePlus Live 可取得受保護的用戶資料。 |
   |用戶名稱欄位 |對應您帳號系統中用戶名稱的欄位，用於提取用戶名稱。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">為防止個人資訊洩露，請勿在自有帳號系統中將手機號碼等資訊作為用戶名稱。</div><br> |
   |用戶 ID 欄位 |對應您帳號系統中用戶 ID 的欄位，用於提取用戶 ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">為防止個人資訊洩露，請勿在自有帳號系統中將手機號碼等資訊作為用戶 ID。</div><br> |
   |Client id |識別 BytePlus Live 的 client ID，於 BytePlus Live 在自有帳號系統註冊後產生。 |
   |Client secret |識別 BytePlus Live 的 client secret，於 BytePlus Live 在自有帳號系統註冊後產生。 |
   |Scope |授權範圍。BytePlus Live 僅能存取指定範圍內的資源。<br><br>若`Scope`在自有帳號系統中未設預設值，則此參數為必填。 |
   |試看 |啟用此選項並選擇時長。在試看期間，觀眾可於未登入直播間的情況下觀看直播或回放。 |
