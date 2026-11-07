---
title: "部署 Web 伺服器"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-deploying-the-server-web-zh-TW"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">應用伺服器部署為可選項。如您不希望自行部署應用伺服器，可選擇使用 BytePlus 提供的應用伺服器作為替代方案。</div>


本文提供了部署 VideoOne 示例專案後端的分步指南。按照這些說明操作，您將能夠成功部署該專案，併為您的 VideoOne 應用獲取專屬伺服器。

<span id="356439a4"></span>
## 前提條件

安裝所需元件：


* Go 1.18 或更高版本

* MySQL 5.7 或更高版本

* Redis 6.2 或更高版本


<span id="41eb8ee1"></span>
## 操作流程

<span id="2b64bc99"></span>
### 專案初始化


1. 請聯絡技術支援團隊獲取 Demo 專案。

2. 在專案資料夾內，進入 `/Server/sql/` 目錄，並執行 `videoone.sql`，以建立 MySQL 資料庫。

3. 進入 `/Server/conf` 目錄，開啟 `config.yaml` 檔案，並進行相關配置。


```YAML
mysql_dsn: "{user_name}:{password}@tcp([{mysql_address}]:{port})/videoone?parseTime=true&loc=Local"
redis_init: false
port: "{port_number}"
vod_space: "{vod_space}"
vod_play_list_id: "{vod_play_list_id}"
```



|**引數** |**資料型別** |**說明** |**示例** |
|---|---|---|---|
|mysql_dsn |字串 |您的 MySQL 伺服器 DSN，其中：<br><br><br>* `user_name` 為您的 MySQL 賬戶使用者名稱。<br><br>* `password` 為您的 MySQL 賬戶密碼。<br><br>* `mysql_address` 為您的 MySQL 伺服器 IP 地址。<br><br>* `port` 為 MySQL 使用的埠號。 |user1:0EFF9BF\*\*\*\*\*\*\*2240CA35@tcp(192.0.2.1:3306)/videoone?parseTime=true&loc=Local |
|redis_init |布林值 |是否連線 Redis。 |此引數必須設定為 `false`。 |
|port |字串 |本應用服務使用的埠號。大多數情況下，您可將其設定為 `8080`。 |8080 |
|vod_space |字串 |您上傳媒體檔案的 BytePlus VOD 空間名稱。 |videoone |
|vod_play_list_id |字串 |影片播放列表的 ID。<br><br>僅在需要影片播放列表功能時需填寫此引數。您應先呼叫 [CreatePlaylist](https://docs.byteplus.com/en/byteplus-vod/reference/createplaylist?version=v1.0) 建立影片播放列表。ID 會在響應的 `result` 引數中返回。 |pb2d0\*\*\*\*\*\* |


<span id="08fa63c1"></span>
### 準備媒體檔案


1. 請按照以下步驟準備部分媒體檔案。您可參考 [BytePlus VOD 入門指南](https://docs.byteplus.com/en/byteplus-vod/docs/getting-started?version=v1.0)獲取更詳細的操作說明。

   1. 建立 VOD 空間。

   2. 將部分影片檔案上傳至 VOD 空間。選擇 **通用線上影片多位元速率模板**作為工作流模板。

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



|**引數** |**資料型別** |**說明** |**示例** |
|---|---|---|---|
|vid |字串 |影片 ID。 |v110exxdg |
|video_type |整數 |影片型別。您可根據影片長度選擇型別。<br><br><br>* `0` ：短影片。此類影片將在應用內 **首頁**標籤頁展示並播放。<br><br>* `1` ：中影片。此類影片將在應用內 **Feed**標籤頁展示並播放。<br><br>* `2` ：長影片。此類影片將在應用內 **頻道**標籤頁展示並播放。 |0 |
|anti_screenshot_and_record |整數 |是否啟用螢幕錄製保護。<br><br><br>* `0`：禁用<br><br>* `1`：啟用 |0 |
|support_smart_subtitle |整數 |是否啟用智慧字幕功能。<br><br><br>* `0`：禁用<br><br>* `1`：啟用 |0 |


<span id="432a754c"></span>
### 專案部署

在根目錄下，執行以下命令以編譯並部署專案：

```Shell
sh startserver.sh
```


<span id="fcd49e38"></span>
## 結果

使用以下命令呼叫 `ping` 介面：

```Shell
curl --location 'http://{your_server_address}:{port_number}/videoone_opensource/ping'
```


如下響應表示服務已正常執行：

```Plain
{"message":"pong"} 
```


<span id="9e6c064f"></span>
## 日誌檢查

如需訪問服務日誌，請進入 `/Server/output/log/app` 目錄，在 `app.log` 檔案中查詢日誌。以下為日誌條目示例：

```Plain
time="2021-12-31T15:35:14+08:00" level=info msg="get login userID: 123" Location="user.go:49" LogID=75119c42-3a98-4533-a3f7-d2b8468c03f6
```


您可以透過 `LogID` 標識客戶端請求。
