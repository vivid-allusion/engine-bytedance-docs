---
title: "API 指引"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/learning_path_api_cn"
---

<span id="首次使用-cdn（必读）"></span>
## 首次使用 CDN（必读）


1. 创建分发策略：[CreateServiceTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-createservicetemplate-cn)

2. 发布分发策略：[LockTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-locktemplate-cn)

3. 添加域名并绑定分发策略：[AddTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-addtemplatedomain-cn)

4. 测试对 CNAME 的访问。（无 API，参见 [操作指引](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-test-domain-name-with-hosts-cn)）

5. 配置 CNAME 记录。（无 API，参见 [操作指引](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-set-up-cname-cn)）


<span id="启用-https-加密服务（推荐）"></span>
## 启用 HTTPS 加密服务（推荐）


1. 授权 CDN 访问证书中心。（无 API，参见 [操作指引](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-authorize-byteplus-cdn-to-access-byteplus-certificate-center-cn)）

2. 上传证书：[AddCertificate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-cn-addcertificate)

3. 为域名启用 HTTPS 加密服务：[UpdateTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-updatetemplatedomain-05d27-cn)

4. 关联证书与域名：[UpdateTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-updatetemplatedomain-05d27-cn)


<span id="修改您域名的-cdn-功能配置"></span>
## 修改您域名的 CDN 功能配置


1. 复制域名绑定的策略：[DuplicateTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-duplicatetemplate-cn)

2. 确定需要修改的 CDN 功能：（无 API，参见 [功能列表](https://docs.byteplus.com/en/docs/byteplus-cdn/learning_path_console_cn#%E5%AE%8C%E6%95%B4-cdn-%E5%8A%9F%E8%83%BD%E5%88%97%E8%A1%A8)）。

3. 在新策略中配置 CDN 功能。

   * 修改分发策略：[UpdateServiceTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-updateservicetemplate-cn)

   * 修改加密策略：[UpdateCipherTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-updateciphertemplate-ac087-cn)

4. 发布策略：[LockTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-locktemplate-cn)

5. 绑定新策略与域名：[UpdateTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-updatetemplatedomain-05d27-cn)


<span id="使用边缘函数（可选）"></span>
## 使用边缘函数（可选）


1. 授权 CDN 访问 BytePlus 边缘函数。（无 API，参见 [操作指引](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-authorize-byteplus-cdn-to-access-byteplus-certificate-center-cn)）

2. 为域名启用边缘函数：[UpdateTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-updatetemplatedomain-05d27-cn)

3. 创建函数：[CreateFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateFunction-cn)

4. 发布函数

   * 全量发布：[FullPublish](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-FullPublish-cn)

   * 灰度发布：[CanaryPublish](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CanaryPublish-cn)

5. 关联域名：[FunctionBindDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-FunctionBindDomainList-cn)

6. 创建转发规则：[UpdateTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-updatetemplatedomain-05d27-cn)


<span id="边缘-kv"></span>
### 边缘 KV


1. 创建存储空间：[CreateKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateKvNamespace-cn)

2. 在存储空间中添加键值对：[CreateKeyValue](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateKeyValue-cn)


<span id="工具中心"></span>
## 工具中心


* 刷新预热

   * 缓存刷新：[SubmitRefreshTask](https://docs.byteplus.com/en/docs/byteplus-cdn/submitrefreshtask)

   * 文件预热：[SubmitPreloadTask](https://docs.byteplus.com/en/docs/byteplus-cdn/submitpreloadtask)

* 诊断工具：

   * IP 检测：[DescribeCdnIP](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnIP_Cn)

   * 域名对比。（无 API，参见 [操作指引](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-diagnostic-tools-cn#%E5%9F%9F%E5%90%8D%E5%AF%B9%E6%AF%94)）

   * 策略对比。（无 API，参见 [操作指引](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-diagnostic-tools-cn#%E7%AD%96%E7%95%A5%E5%AF%B9%E6%AF%94)）


<span id="完整-cdn-api-列表"></span>
## 完整 CDN API 列表

<span id="策略管理-api"></span>
### 策略管理 API

**分发策略**


* 创建分发策略：[CreateServiceTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-createservicetemplate-cn)

* 修改分发策略：[UpdateServiceTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-updateservicetemplate-cn)

* 获取分发策略详情：[DescribeServiceTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-describeservicetemplate-00652-cn)


**加密策略**


* 创建加密策略：[CreateCipherTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-createciphertemplate-cf232-cn)

* 修改加密策略：[UpdateCipherTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-updateciphertemplate-ac087-cn)

* 获取加密策略详情：[DescribeCipherTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-describeciphertemplate-f8c12-cn)


**其它策略操作**


* 获取策略列表：[DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-describetemplates-cn)

* 复制策略：[DuplicateTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-duplicatetemplate-cn)

* 发布策略：[LockTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-locktemplate)

* 删除策略：[DeleteTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-deletetemplate-cn)


<span id="域名管理-api"></span>
### 域名管理 API


* 添加域名：[AddTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-addtemplatedomain-cn)

* 修改域名的基础配置：[UpdateTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-updatetemplatedomain-05d27-cn)

* 获取域名列表：[DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-describetemplatedomains-7f84f-cn)

* 启用域名：[StartCdnDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/startcdndomain)

* 停用域名：[StopCdnDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/stopcdndomain)

* 删除域名：[DeleteCdnDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/deletecdndomain)


<span id="证书管理-api"></span>
### 证书管理 API


* 上传证书：[AddCertificate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-cn-addcertificate)

* 获取证书列表：[ListCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-listcertinfo-cn)

* 获取已与域名关联的证书列表：[ListCdnCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-listcdncertinfo-cn)

* 获取指定证书的域名关联情况：[DescribeCertConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-describecertconfig-9ea17-cn)


<span id="数据统计-api"></span>
### 数据统计 API

**用户请求统计**


* 获取访问统计的细分数据：[DescribeDistrictData](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeDistrictData)

* 获取访问统计的汇总数据：[DescribeDistrictSummary](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeDistrictSummary)

* 获取访问数据的统计排名：[DescribeDistrictRanking](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeDistrictRanking)


**计费区域统计**


* 获取计费区域的细分数据：[DescribeEdgeData](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeEdgeData)

* 获取计费区域的汇总数据：[DescribeEdgeSummary](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeEdgeSummary)

* 获取计费区域的统计排名：[DescribeEdgeRanking](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeEdgeRanking)


**CDN 响应统计**


* 获取访问状态码的统计排名：[DescribeEdgeStatusCodeRanking](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeEdgeStatusCodeRanking)


**回源请求统计**


* 获取回源统计的细分数据：[DescribeOriginData](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeOriginData)

* 获取回源统计的汇总数据：[DescribeOriginSummary](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeOriginSummary)

* 获取回源数据的统计排名：[DescribeOriginRanking](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeOriginRanking)

* 获取回源状态码的统计排名：[DescribeOriginStatusCodeRanking](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeOriginStatusCodeRanking)


**业务分析**


* 获取热门对象的统计排名：[DescribeStatisticalRanking](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeStatisticalRanking)

* 获取独立访客的细分数据：[DescribeUserData](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeUserData)


**其他**


* 获取支持的区域和 ISP 列表：[DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp)


<span id="工具中心-api"></span>
### 工具中心 API


* 刷新预热

   * 提交预热任务：[SubmitPreloadTask](https://docs.byteplus.com/en/docs/byteplus-cdn/submitpreloadtask)

   * 提交刷新任务：[SubmitRefreshTask](https://docs.byteplus.com/en/docs/byteplus-cdn/submitrefreshtask)

   * 获取刷新与预热任务列表：[DescribeContentTasks](https://docs.byteplus.com/en/docs/byteplus-cdn/describecontenttasks)

   * 获取刷新和预热的配额：[DescribeContentQuota](https://docs.byteplus.com/en/docs/byteplus-cdn/describecontentquota)

* 其他工具

   * 查询多个 IP 是否归属 CDN：[DescribeCdnIP](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnIP_Cn)


<span id="边缘函数-api"></span>
### 边缘函数 API


* 函数

   * 创建函数：[CreateFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateFunction-cn)

   * 更新函数：[UpdateFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-UpdateFunction-cn)

   * 获取函数信息：[GetFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetFunction-cn)

   * 获取函数列表：[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-cn)

   * 删除函数：[DeleteFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-DeleteFunction-cn)

* 域名

   * 获取可关联的域名：[ListFunctionDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCDNDomain-cn)

   * 为函数关联域名：[FunctionBindDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-FunctionBindDomainList-cn)

   * 为函数解除关联域名：[FunctionUnBindDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-FunctionUnBindDomains-cn)

* 发布

   * 回滚函数：[SnapshotPublish](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-SnapshotPublish-cn)

   * 灰度发布函数：[CanaryPublish](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CanaryPublish-cn)

   * 全量发布函数：[FullPublish](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-FullPublish-cn)

* 代码

   * 获取函数代码版本列表：[ListVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListVersions-cn)

   * 获取指定版本的函数代码：[GetSnapshot](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetsnapShot-cn)

   * 获取函数全部代码文件的代码：[GetScriptSourceCode](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetScriptSourceCode-cn)

   * 更新函数代码：[UpdateSourceCode](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-UpdateSourceCode-cn)

   * 获取函数 default 代码文件的代码：[GetSourceCode](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetSourceCode-cn)

* 发布历史

   * 获取函数的发布历史列表：[ListTicket](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListTicket-cn)

   * 获取函数的发布历史：[GetTicket](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetTicket-cn)

* 环境变量

   * 添加环境变量：[AddEnv](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-AddEnv-cn)

   * 更新环境变量：[EditEnv](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-EditEnv-cn)

   * 删除环境变量：[DeleteEnv](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-DeleteEnv-cn)

   * 获取环境变量：[GetEnv](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetEnv-cn)

* 灰度环境

   * 获取边缘节点列表：[ListContinentCluster](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListContinentCluster-cn)

   * 获取可用的边缘节点所在的大洲列表：[ListContinent](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListContinent-cn)

   * 获取可用的边缘节点所在的国家列表：[ListCountry](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCountry-cn)

   * 更新灰度环境或全量环境所包含的边缘节点：[UpdateCountryCluster](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-UpdateCountryCluster-cn)

* Cron 触发器

   * 创建 Cron 触发器：[CreateCronJob](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateCronJob-cn)

   * 获取 Cron 触发器列表：[ListCronJob](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCronJob-cn)

   * 删除 Cron 触发器：[DeleteCronJob](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-DeleteCronJob-cn)

   * 获取指定 Cron 触发器的任务执行列表：[ListCronJobTask](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCronJobTask-cn)

   * 获取 Cron 触发器的信息：[GetCronJob](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetCronJob-cn)

   * 停用 Cron 触发器：[StopCronJob](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-StopCronJob-cn)

   * 获取指定 Cron 触发器的任务执行日志列表：[ListCronJobTaskLog](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCronJobTaskLog-cn)

   * 启用 Cron 触发器：[StartCronJob](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-StartCronJob-cn)

   * 更新 Cron 触发器：[UpdateCronJob](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-UpdateCronJob-cn)

* 边缘 KV

   * 创建存储空间：[CreateKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateKvNamespace-cn)

   * 创建键值对：[CreateKeyValue](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateKeyValue-cn)

   * 删除存储空间：[DeleteKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-DeleteKvNamespace-cn)

   * 删除键值对：[DeleteKvKey](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-DeleteKvKey-cn)

   * 获取存储空间信息：[GetKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetKvNamespace-cn)

   * 获取键值对的值：[GetKeyValue](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetKeyValue-cn)

   * 获取存储空间列表：[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-cn)

   * 获取键值对列表：[ListKvKey](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvKey-cn)

   * 更新存储空间备注：[UpdateKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-UpdateKvNamespace-cn)

   * 更新键值对的值：[UpdateKeyValue](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-UpdateKeyValue-cn)
