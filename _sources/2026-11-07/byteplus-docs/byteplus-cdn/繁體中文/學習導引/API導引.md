---
title: "API導引"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/learning_path_api_zh-tw"
---

<span id="首次使用-cdn（必讀）"></span>
## 首次使用 CDN（必讀）


1. 建立分發策略：[CreateServiceTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-CreateServiceTemplate_zh-tw)

2. 發佈分發策略：[LockTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-LockTemplate_zh-tw)

3. 新增網域名稱並綁定分發策略：[AddTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-AddTemplateDomain_zh-tw)

4. 測試對 CNAME 的存取。（無 API，參見 [操作指引](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-test-domain-name-with-hosts-zh-tw)）

5. 設定 CNAME 記錄。（無 API，參見 [操作指引](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-set-up-cname_zh-tw)）


<span id="啟用-https-加密服務（推薦）"></span>
## 啟用 HTTPS 加密服務（推薦）


1. 授權 CDN 存取憑證中心。（無 API，參見 [操作指引](https://docs.byteplus.com/en/docs/byteplus-cdn/allow-cdn-access-to-byteplus-service_zh-tw)）

2. 上傳憑證：[AddCertificate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-AddCertificate_zh-tw)

3. 為網域名稱啟用 HTTPS 加密服務：[UpdateTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-UpdateTemplateDomain_zh-tw)

4. 關聯憑證與網域名稱：[UpdateTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-UpdateTemplateDomain_zh-tw)


<span id="修改您網域名稱的-cdn-功能設定"></span>
## 修改您網域名稱的 CDN 功能設定


1. 複製網域名稱綁定的策略：[DuplicateTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DuplicateTemplate_zh-tw)

2. 確定需要修改的 CDN 功能：（無 API，參見 [功能列表](https://docs.byteplus.com/en/docs/byteplus-cdn/learning_path_console_zh-tw#%E5%AE%8C%E6%95%B4-cdn-%E5%8A%9F%E8%83%BD%E5%88%97%E8%A1%A8)）。

3. 在新策略中設定 CDN 功能。

   * 修改分發策略：[UpdateServiceTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-UpdateServiceTemplate_zh-tw)

   * 修改加密策略：[UpdateCipherTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-UpdateCipherTemplate_zh-tw)

4. 發佈策略：[LockTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-LockTemplate_zh-tw)

5. 綁定新策略與網域名稱：[UpdateTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-UpdateTemplateDomain_zh-tw)


<span id="工具中心"></span>
## 工具中心


* 清除快取與預取快取

   * 清除快取：[SubmitRefreshTask](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-SubmitRefreshTask_zh-tw)

   * 預取快取：[SubmitPreloadTask](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-SubmitPreloadTask_zh-tw)

* 診斷工具：

   * IP 檢測：[DescribeCdnIP](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnIP_zh-tw)

   * 網域名稱對比。（無 API，參見 [操作指引](https://docs.byteplus.com/en/docs/byteplus-cdn/diagnostic-tools_zh-tw#%E7%B6%B2%E5%9F%9F%E5%90%8D%E7%A8%B1%E5%B0%8D%E6%AF%94)）

   * 策略對比。（無 API，參見 [操作指引](https://docs.byteplus.com/en/docs/byteplus-cdn/diagnostic-tools_zh-tw#%E7%AD%96%E7%95%A5%E5%B0%8D%E6%AF%94)）


<span id="完整-cdn-api-列表"></span>
## 完整 CDN API 列表

<span id="策略管理-api"></span>
### 策略管理 API

**分發策略**


* 建立分發策略：[CreateServiceTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-CreateServiceTemplate_zh-tw)

* 修改分發策略：[UpdateServiceTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-UpdateServiceTemplate_zh-tw)

* 取得分發策略詳情：[DescribeServiceTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeServiceTemplate_zh-tw)


**加密策略**


* 建立加密策略：[CreateCipherTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-CreateCipherTemplate_zh-tw)

* 修改加密策略：[UpdateCipherTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-UpdateCipherTemplate_zh-tw)

* 取得加密策略詳情：[DescribeCipherTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeCipherTemplate_zh-tw)


**其它策略操作**


* 取得策略列表：[DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeTemplates_zh-tw)

* 複製策略：[DuplicateTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DuplicateTemplate_zh-tw)

* 發佈策略：[LockTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-LockTemplate_zh-tw)

* 刪除策略：[DeleteTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DeleteTemplate_zh-tw)


<span id="網域名稱管理-api"></span>
### 網域名稱管理 API


* 新增網域名稱：[AddTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-AddTemplateDomain_zh-tw)

* 修改網域名稱的基礎設定：[UpdateTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-UpdateTemplateDomain_zh-tw)

* 取得網域名稱列表：[DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeTemplateDomains_zh-tw)

* 啟用網域名稱：[StartCdnDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-StartCdnDomain_zh-tw)

* 停用網域名稱：[StopCdnDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-StopCdnDomain_zh-tw)

* 刪除網域名稱：[DeleteCdnDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DeleteCdnDomain_zh-tw)


<span id="憑證管理-api"></span>
### 憑證管理 API


* 上傳憑證：[AddCertificate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-AddCertificate_zh-tw)

* 取得憑證列表：[ListCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListCertInfo_zh-tw)

* 取得已與網域名稱關聯的憑證列表：[ListCdnCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListCdnCertInfo_zh-tw)

* 取得指定憑證的網域名稱關聯情況：[DescribeCertConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeCertConfig_zh-tw)


<span id="資料統計-api"></span>
### 資料統計 API

**使用者請求統計**


* 取得存取統計的細分資料：[DescribeDistrictData](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeDistrictData_zh-tw)

* 取得存取統計的彙總資料：[DescribeDistrictSummary](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeDistrictSummary_zh-tw)

* 取得存取資料的統計排名：[DescribeDistrictRanking](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeDistrictRanking_zh-tw)


**計費區域統計**


* 取得計費區域的細分資料：[DescribeEdgeData](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeEdgeData_zh-tw)

* 取得計費區域的彙總資料：[DescribeEdgeSummary](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeEdgeSummary_zh-tw)

* 取得計費區域的統計排名：[DescribeEdgeRanking](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeEdgeRanking_zh-tw)


**CDN 回應統計**


* 取得存取狀態碼的統計排名：[DescribeEdgeStatusCodeRanking](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeEdgeStatusCodeRanking_zh-tw)


**來源伺服器請求統計**


* 取得來源伺服器請求統計的細分資料：[DescribeOriginData](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeOriginData_zh-tw)

* 取得來源伺服器請求統計的彙總資料：[DescribeOriginSummary](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeOriginSummary_zh-tw)

* 取得來源伺服器請求資料的統計排名：[DescribeOriginRanking](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeOriginRanking_zh-tw)

* 取得來源伺服器請求狀態碼的統計排名：[DescribeOriginStatusCodeRanking](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeOriginStatusCodeRanking_zh-tw)


**業務分析**


* 取得熱門物件的統計排名：[DescribeStatisticalRanking](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeStatisticalRanking_zh-tw)

* 取得獨立訪客的細分資料：[DescribeUserData](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeUserData_zh-tw)


**其他**


* 取得支援的區域和 ISP 列表：[DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeCdnRegionAndIsp_zh-tw)


<span id="工具中心-api"></span>
### 工具中心 API


* 清除快取與預取快取

   * 提交預取任務：[SubmitPreloadTask](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-SubmitPreloadTask_zh-tw)

   * 提交清除任務：[SubmitRefreshTask](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-SubmitRefreshTask_zh-tw)

   * 取得清除與預取任務列表：[DescribeContentTasks](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeContentTasks_zh-tw)

   * 取得清除和預取的配額：[DescribeContentQuota](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeContentQuota_zh-tw)

* 其他工具

   * 查詢多個 IP 是否歸屬 CDN：[DescribeCdnIP](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnIP_zh-tw)
