---
title: "為 Android 和 iOS 部署伺服器"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-backend-deployment-guide-zh-TW"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">為了方便您編譯 VideoOne Android & iOS 示例程式碼，BytePlus 為您提供了可用於測試階段的應用伺服器。</div>


<div data-tips="true" data-tips-type="tip">測試 App 伺服器域名：<code>https://videocloud.byteplusapi.com/videoone_opensource</code></div>


<div data-tips="true" data-tips-type="tip">請注意，該 App 伺服器僅供測試階段使用。您可根據當前業務需求，參考本文件在您的伺服器上修改並部署開原始碼。</div>


本文提供了有關部署 VideoOne 示例專案 App 伺服器的分步指南。按照這些說明操作，您將能夠成功部署該專案，併為您的 VideoOne 應用獲取專屬伺服器。

App 伺服器提供多項服務，包括：


* 管理直播間，例如建立和結束直播間會話。

* 管理媒體檔案。

* 實時信令，例如當觀眾申請連麥時向主播傳送通知。


<span id="39f66eba"></span>
## 前提條件

安裝所需元件：


* [Go](https://go.dev/doc/tutorial/getting-started) 1.18 或更高版本

* [MySQL](https://dev.mysql.com/doc/mysql-getting-started/en/) 5.7 或更高版本

* [Redis](https://redis.io/docs/latest/operate/oss_and_stack/install/install-redis/) 6.2 或更高版本


<span id="e1b4bd8c"></span>
## 操作流程

<span id="348d72cf"></span>
### 專案設定


1. 前往 GitHub 並克隆 [VideoOneSolutions](https://github.com/byteplus-sdk/VideoOneSolutions) 倉庫。

2. 在專案資料夾內，進入 `/Server/sql/` 目錄並執行 `videoone.sql` 以建立 MySQL 資料庫。

3. 進入 `/Server/conf` 目錄，開啟 `config.yaml` 檔案並進行相關配置。示例程式碼中的所有引數並非必填。請參閱程式碼下方的表格，瞭解每個引數的具體使用場景。

   ```YAML
   # mysql/redis config
   mysql_dsn: "{user_name}:{password}@tcp([{mysql_address}]:{port})/videoone?parseTime=true&loc=Local"
   redis_init: true
   redis_addr: "127.0.0.1:6379"
   redis_password: ""
   
   # common service config
   port: "8080"
   access_key: ""
   secret_access_key: ""
   
   # rtc service config
   rtc_app_id: ""
   rtc_app_key: ""
   
   # live service config
   live_app_name: ""
   live_pull_domain: ""
   live_push_domain: ""
   live_stream_key: ""
   
   # vod service config
   vod_space: ""
   vod_play_list_id: "{your_vod_play_list_id}"
   
   # Interactive Live scene config
   live_timer_enable: true
   live_experience_time: 20
   ```
   

   
   |**引數** |**資料型別** |**描述** |**引數依賴的場景/功能** |**示例** |
   |---|---|---|---|---|
   |mysql_dsn |字串 |您的 MySQL 伺服器的 DSN，其中：<br><br><br>* `user_name` 為您的 MySQL 賬戶使用者名稱。<br><br>* `password` 為您的 MySQL 賬戶密碼。<br><br>* `mysql_address` 為您的 MySQL 伺服器 IP 地址。<br><br>* `port` 為 MySQL 使用的埠號。 |全部 |user1:0EFF9BF\*\*\*\*\*\*\*2240CA35@tcp(xxx.xxx.xxx.xxx:3306)/videoone?parseTime=true&loc=Local |
   |redis_init |布林值 |指定是否連線 Redis。 |全部 |如果您的應用使用互動直播功能，請將其設定為 `true`。 |
   |redis_addr |字串 |您的 Redis 伺服器的 IP 地址和埠號。 |全部 | |
   |redis_password |字串 |您的 Redis 服務的密碼。 |全部 |0EFF9BF\*\*\*\*\*\*\*2240CA35 |
   |port |字串 |此應用服務使用的埠號。在大多數情況下，您可以將其設定為 `8080`。 |全部 |8080 |
   |access_key |字串 |[您的 BytePlus 賬戶的訪問金鑰 ID（AK）。](https://docs.byteplus.com/en/byteplus-platform/docs/creating-an-accesskey) |全部 |AKAPZ7\*\*\*\*\*\*\*\*FLBFK4k9 |
   |secret_access_key |字串 |[您的 BytePlus 賬戶的訪問金鑰（SK）。](https://docs.byteplus.com/en/byteplus-platform/docs/creating-an-accesskey) |全部 |8dk39vK\*\*\*\*\*\*\*\*k7D93K37WODKu3oQ |
   |rtc_app_id |字串 |您的 BytePlus RTC 應用的**AppId**。 |互動直播 | |
   |rtc_app_key |字串 |您的 BytePlus RTC 應用的**AppKey**。 |互動直播 | |
   |live_app_name |字串 |您在 MediaLive 中配置轉碼模板的**AppName**。 |互動直播 |videoone |
   |live_pull_domain |字串 |http://{domain_name}，其中“domain_name”表示**拉流域名**。 |互動直播 |`http://pull-demo.com` |
   |live_push_domain |字串 |rtmp://{domain_name}，其中“domain_name”表示**推流域名**。 |互動直播 |`rtmp://push-demo.com` |
   |live_stream_key |字串 |用於 URL 鑑權的**主金鑰**。 |互動直播 |DLH\*\*\*\*\*\*\*\*KDF |
   |live_timer_enable |布林值 |指定是否在對應 `live_experience_time` 引數設定的時長後自動結束會話。<br><br><br>* true：啟用自動結束<br><br>* false：禁用自動結束 |互動直播 |true |
   |live_experience_time |整數 |會話自動結束前的時長（單位：分鐘）。僅當對應 `live_timer_enable` 引數設定為 true 時，此引數生效。 |互動直播 |20 |
   |vod_space |字串 |您上傳媒體檔案的 BytePlus VOD 空間名稱。 |用於影片播放功能 |videoone |
   |vod_play_list_id |字串 |影片播放列表的 ID。<br><br>僅在需要影片播放列表功能時，才需此引數。您應先呼叫[CreatePlaylist](https://docs.byteplus.com/en/byteplus-vod/reference/createplaylist?version=v1.0)建立影片播放列表，然後可從響應的 result 引數中獲取 ID。 |影片播放列表 |pb2d0\*\*\*\*\*\* |
   


<span id="26a0db10"></span>
### 準備媒體檔案

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">僅在需要影片播放功能時，此任務才必需。</div>



1. 請按照以下步驟準備一些媒體檔案。您可以參考 [BytePlus VOD 入門指南](https://docs.byteplus.com/en/byteplus-vod/docs/getting-started?version=v1.0) 獲取更詳細的操作說明。

   1. 建立一個 VOD 空間。

   2. 將一些影片檔案上傳至 VOD 空間。選擇 **通用線上影片多位元速率模板** 作為工作流模板。

   3. 新增域名。

   4. 釋出影片檔案。

2. 填寫您已上傳至 BytePlus VOD 的媒體檔案資訊。

   ```SQL
   INSERT INTO
     video_info(vid, video_type, anti_screenshot_and_record, support_smart_subtitle)
   VALUES
     ('{vid-1}', 0, 0, 0),
     ('{vid-2}', 1, 0, 1);
   ```
   

   
   |**引數** |**資料型別** |**描述** |**示例** |
   |---|---|---|---|
   |vid |字串 |影片 ID。 |v110exxdg |
   |video_type |整數 |影片型別。根據影片長度選擇型別。<br><br><br>* `0`：短影片。此類別的影片將在應用的**首頁**標籤頁展示並播放。<br><br>* `1`：中影片。此類別的影片將在應用的**Feed**標籤頁展示並播放。<br><br>* `2`：長影片。此類別的影片將在應用的**頻道**標籤頁展示並播放。 |0 |
   |anti_screenshot_and_record |整數 |指定是否啟用錄屏保護。<br><br><br>* `0`：禁用<br><br>* `1`：啟用 |0 |
   |support_smart_subtitle |整數 |指定是否啟用智慧字幕功能。<br><br><br>* `0`：禁用<br><br>* `1`：啟用 |0 |
   


<span id="3e8efd6d"></span>
### 部署專案

在根目錄下，執行以下命令以編譯並部署專案：

```Shell
sh startserver.sh
```


<span id="ef5084a5"></span>
## 結果

使用以下命令呼叫 `ping` 介面：

```Shell
curl --location 'http://{your_server_address}:{port_number}/videoone_opensource/ping'
```


出現以下響應表示服務已啟動並執行：

```Plain
{"message":"pong"} 
```


<span id="dc361956"></span>
## 檢視日誌

要訪問服務日誌，請進入 `/Server/output/log/app` 目錄，在 `app.log` 檔案中查詢日誌。以下為日誌條目示例：

```Plain
time="2021-12-31T15:35:14+08:00" level=info msg="get login userID: 123" Location="user.go:49" LogID=75119c42-3a98-4533-a3f7-d2b8468c03f6
```


您可以透過 `LogID` 標識客戶端請求。
