---
title: "PROXY Protocol"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/proxy-protocol_zh-tw"
---

<span id="背景"></span>
## 背景

PROXY 協定（PROXY protocol）是一種網路協定，旨在解決代理環境中伺服器無法獲取用戶端真實資訊的問題。這些資訊包括用戶端的 IP 位址和連接埠，以及用戶端需要存取的目標 IP 位址和連接埠。在與伺服器建立 TCP/UDP 連線時，代理伺服器會傳送 PROXY 協定標頭來傳輸用戶端的真實資訊。

<span id="特性介紹"></span>
## 特性介紹

BytePlus CDN 支援 PROXY 協定，涵蓋版本 1 和版本 2。當您在 CDN 中啟用了 PROXY 協定，CDN 就可以對收到的 PROXY 協定標頭進行解析，以獲取用戶端的真實 IP 位址。

<span id="使用場景"></span>
## 使用場景

在您的業務架構中，CDN 前部署了代理，譬如 BytePlus Global Accelerator（GA），並且該代理會傳送 PROXY 協定標頭。您還設定了 IP 黑白名單，希望根據用戶端的真實 IP 位址控制對 CDN 的存取。

<span id="操作步驟"></span>
## 操作步驟


1. 打開 **PROXY Protocol** 設定頁面。操作步驟參見 [網域名稱設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-tw)。

2. 設定 **狀態** 為啟用。

3. 設定完成後，點擊 **儲存**。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a7eca3bcb6a29a31fdf9006058613b26.png) </span>
