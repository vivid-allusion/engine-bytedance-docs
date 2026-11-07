---
title: "使用 RTMPS 協議推流"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/pushrtmps-zh-TW"
---

本文檔說明如何使用 RTMPS 協議進行推流。

<span id="ee524a0d"></span>
## 背景

即時消息協議（RTMP）是一種在 Flash 播放器與伺服器之間傳輸串流音訊和視訊的網路協議。RTMP 建立於 TCP 之上，預設使用 1935 埠。這是一種標準的、未加密的即時消息協議。

RTMPS 是 RTMP 的一種變體。它是在 TLS/SSL 之上運作的 RTMP。它使用 SSL 在傳輸層對網路連線進行加密。預設埠為 443。RTMPS 能很好地解決 RTMP 的安全性問題。

<span id="2f3f62dc"></span>
## 操作流程

<span id="3257ec21"></span>
### **配置 RTMPS 功能**

預設情況下，BytePlus MediaLive 為推流域名啟用 RTMPS 功能。但若要使 RTMPS 功能生效，必須先為推流域名配置憑證和 HTTPS。有關如何配置憑證，請參考[管理 SSL 憑證](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-managing-certificates)。有關如何配置 HTTPS，請參考[HTTPS 配置](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-https)。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71d9f2ce91014b28949f804b853d0d89~tplv-goo7wpa0wc-image.image) </span>

<span id="73bf2511"></span>
### 使用 RTMPS 協議推流

您可以修改 RTMP 位址以取得 RTMPS 位址並進行推流。


1. 使用**位址產生器**取得 RTMP 推流位址。

2. 將產生的 RTMP 推流位址的協議頭改為**RTMPS**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/963694262ccc4a95b165175e5a43d3fc~tplv-goo7wpa0wc-image.image) </span>

3. 將 RTMPS 推流位址輸入至 OBS 軟體，即可開始推流。播放器可按照正常的拉流播放流程進行。支援 RTMP、FLV、HLS 和 RTM 協議。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52462e79c96d4196a2ce6aa3a9d8906d~tplv-goo7wpa0wc-image.image) </span>
