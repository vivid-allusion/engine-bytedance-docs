---
title: "OpenAPI 总览"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-openapi-overview-zh-CN"
---

本主题列出了 BytePlus MediaLive 提供的所有 OpenAPI 接口。

<span id="e401bf50"></span>
## 域名


|API |接口行为 |
|---|---|
|[CreateDomainV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-dj3h3u96xn) |调用 `CreateDomainV2` API，添加一个或多个用于推流或拉流的域名。 |
|[UpdateDomainVhost](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatedomainvhost) |调用 `UpdateDomainVhost` API，变更与域名关联的域名空间。 |
|[DeleteDomain](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletedomain-2023) |调用 `DeleteDomain` 接口，删除域名。 |
|[DisableDomain](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-disabledomain-2023) |调用 `DisableDomain` API，禁用域名。域名被禁用后，MediaLive 服务中的域名状态将从 `0-已开启` 变为 `2-未开启`。 |
|[EnableDomain](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-enabledomain-2023) |调用 `EnableDomain` API，启用已禁用的域名。域名被启用后，MediaLive 服务中的域名状态将从 `2-未开启` 变为 `0-已开启`。 |
|[DescribeDomain](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describedomain-2023) |调用 `DescribeDomain` API，查询指定域名的信息，包括域名空间、CNAME 地址、域名状态等。 |
|[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) |调用 `ListDomainDetail` API，查询账号下域名的信息。你可以根据域名状态、域名类型及其他维度筛选查询结果。 |


<span id="f462cd21"></span>
## 访问控制


|API |接口行为 |
|---|---|
|[UpdateClusterRateLimit](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateclusterratelimit) |调用 `UpdateClusterRateLimit` API，新增或修改拉流请求的频率限制。 |
|[DeleteClusterRateLimit](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleteclusterratelimit) |调用 `DeleteClusterRateLimit` API，删除拉流请求的频率限制。 |
|[DescribeClusterRateLimit](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeclusterratelimit) |调用 `DescribeClusterRateLimit` API，查询拉流请求的频率限制。 |
|[UpdateUserAgentAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateuseragentaccessrule) |调用 `UpdateUserAgentAccessRule` API，新增或更新 User\-Agent 限制。 |
|[DescribeUserAgentAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeuseragentaccessrule) |调用 `DescribeUserAgentAccessRule` API，查询 User\-Agent 限制。 |
|[DeleteUserAgentAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleteuseragentaccessrule_1) |调用 `DeleteUserAgentAccessRule` API，删除 User\-Agent 限制。 |
|[UpdateIPAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateipaccessrule) |调用 `UpdateIPAccessRule` API，为指定域名配置 IP 黑名单或白名单。 |
|[DescribeIPAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeipaccessrule) |调用 `DescribeIPAccessRule` API，查询已创建的 IP 访问规则配置。 |
|[DeleteIPAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleteipaccessrule) |调用 `DeleteIPAccessRule` API，删除指定域名的 IP 黑名单或白名单。 |
|[UpdateRegionAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateregionaccessrule) |调用 `UpdateRegionAccessRule` API，为指定域名创建地域限制。 |
|[DescribeRegionAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeregionaccessrule) |调用 `DescribeRegionAccessRule` API，查询指定域名的地域限制。 |
|[DeleteRegionAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleteregionaccessrule) |调用 `DeleteRegionAccessRule` API，删除指定域名的地域限制。 |
|[UpdateFormatAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateformataccessrule) |调用 `UpdateFormatAccessRule` API，创建协议限制。 |
|[DescribeFormatAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeformataccessrule) |调用 `DescribeFormatAccessRule` API，查询协议限制。 |
|[DeleteFormatAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleteformataccessrule) |调用 `DeleteFormatAccessRule` API，删除协议限制。 |
|[UpdateAuthKey](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateauthkey-2023) |调用 `UpdateAuthKey` API，新增或更新推流和拉流地址的 URL 鉴权配置。使用该 API 更新配置时，所有鉴权参数将被更新。 |
|[DescribeAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeauth-2023) |调用 `DescribeAuth` API，查询符合条件的 URL 鉴权配置。 |
|[UpdateReferer](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatereferer-2023) |调用 `UpdateReferer` API，创建域级（Vhost + 域名）或应用级（Vhost + 应用）的 Referer blocklist or allowlist configuration。 |
|[DeleteReferer](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletereferer-2023) |调用 `DeleteReferer` API，删除 Referer blocklist or allowlist configuration。 |
|[DescribeReferer](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describereferer-2023) |调用 `UpdateReferer` API，获取 Referer blocklist or allowlist configuration。 |
|[UpdateRelaySourceRewrite](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterelaysourcerewrite) |配置回源地址重写规则。回源地址重写功能允许根据预设的匹配规则，从新的地址获取流。详情请参见[回源地址重写](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-origin-address-rewrite)。 |
|[DescribeRelaySourceRewrite](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-dakt2mfojk) |查询回源地址重写规则。回源地址重写功能允许根据预设的匹配规则，从新的地址获取流。详情请参见[回源地址重写](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-origin-address-rewrite)。 |
|[DeleteRelaySourceRewrite](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-3nf0nln2b2) |删除回源地址重写规则。回源地址重写功能允许根据预设的匹配规则，从新的地址获取流。详情请参见[回源地址重写](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-origin-address-rewrite)。 |
|[UpdateRemoteAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateremoteauth-2023) |调用`UpdateRemoteAuth`接口，为拉流域名创建远程鉴权配置。创建成功后，用户的拉流请求将被发送至指定的鉴权服务器，由其对用户的拉流请求进行验证。 |
|[DescribeRemoteAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeremoteauth-2023) |调用`DescribeRemoteAuth`接口，查询拉流域名的远程鉴权配置。 |
|[DeleteRemoteAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleteremoteauth-2023) |调用`DeleteRemoteAuth`接口，删除已添加的远程鉴权配置。 |
|[ListVhostRemoteAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostremoteauth-2023) |调用`ListVhostRemoteAuth`接口，查询Vhost下所有拉流域名的远程鉴权配置。 |


<span id="f84aacac"></span>
## 延迟控制


|API |接口行为 |
|---|---|
|[UpdateLatencyConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/updatelatencyconfig) |调用`UpdateLatencyConfig`接口，通过为指定拉流域名下的流配置服务器GOP缓存，降低直播流延迟。 |
|[DescribeLatencyConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/describelatencyconfig) |调用`DescribeLatencyConfig`接口，查询GOP的服务器缓存配置。 |
|[DeleteLatencyConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/deletelatencyconfig) |调用`DeleteLatencyConfig`接口，删除已创建的服务器GOP缓存配置。 |


<span id="83729421"></span>
## 封装


|API |接口行为 |
|---|---|
|[UpdateHLSConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/updatehlsconfig) |调用`UpdateHLSConfig`接口，为指定域名空间添加或更新HLS配置，包括分片大小和分片数量，以有效降低延迟并提升直播流兼容性。在HLS和低延迟HLS（LL\-HLS）中，直播流会被切分为TS（Transport Stream）。每个TS都有对应的URL，使用HLS协议进行拉流时，地址会不断变化。 |
|[DescribeHLSConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/describehlsconfig) |调用`DescribeHLSConfig`接口，查询指定域名空间的HLS配置，包括分片大小、分片数量等。 |
|[DeleteHLSConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/deletehlsconfig) |调用`DeleteHLSConfig`接口，将指定域名空间的HLS配置恢复为默认设置，包括分片大小、分片数量等。 |
|[UpdateCMAFConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/updatecmafconfig) |在DASH和低延迟DASH（LL\-DASH）中，直播流会被切分为CMAF（Common Media Application Format）分片。调用`UpdateCMAFConfig`接口，可调整时长和分片数量设置，在指定域名空间（Vhost）下有效降低延迟并提升直播流兼容性。 |
|[DescribeCMAFConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/describecmafconfig) |调用`DescribeCMAFConfig`接口，查询指定域名空间下流的时长和分片数量设置。 |
|[DeleteCMAFConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/deletecmafconfig) |调用`DeleteCMAFConfig`接口，删除指定域名空间（Vhost）下流的DASH设置，包括分片时长和分片数量。 |


<span id="2f90b23a"></span>
## Header


|API |接口行为 |
|---|---|
|[EnableHTTPHeaderConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-enablehttpheaderconfig) |调用`EnableHTTPHeaderConfig`接口，启用或禁用HTTP头配置。 |
|[DeleteHTTPHeaderConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletehttpheaderconfig) |调用`DeleteHTTPHeaderConfig`接口，删除通过UpdateHTTPHeaderConfig添加的指定域名的HTTP头配置。 |
|[DescribeHTTPHeaderConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describehttpheaderconfig) |调用`DescribeHTTPHeaderConfig`接口以查询指定域名的HTTP头部配置。 |
|[UpdateHTTPHeaderConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatehttpheaderconfig) |调用`UpdateHTTPHeaderConfig`接口，在边缘服务器返回给客户端的响应中添加额外的HTTP头部，或在回源任务中向第三方源站的请求中添加额外的HTTP头部。 |


<span id="71b39aaa"></span>
## 证书


|API |接口行为 |
|---|---|
|[CreateCert](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createcert-2023) |调用`CreateCert`接口，将证书添加或更新到MediaLive，以便后续绑定到域名并开启HTTPS。 |
|[DeleteCert](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletecert-2023) |调用`DeleteCert`接口，删除已上传到MediaLive的证书。 |
|[BindCert](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-bindcert-2023) |调用`BindCert`接口，将已上传的HTTPS证书绑定到域名，并为该域名开启HTTPS安全传输。 |
|[UnbindCert](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-unbindcert-2023) |调用`UnbindCert`接口，将证书从域名解绑。 |
|[ListCertV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcertv2) |调用`ListCertV2`接口，查看当前账号下的证书列表。 |
|[DescribeCertDetailSecretV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdetailsecretv2-2023) |调用`DescribeCertDetailSecretV2`接口，通过证书ID或证书链ID查看证书的详细信息。 |


<span id="8afc3b8a"></span>
## 加密


|API |接口行为 |
|---|---|
|[DescribeLicenseDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelicensedrm) |获取DRM许可证。播放器使用该许可证解密DRM加密的直播流。 |
|[DescribeCertDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdrm) |获取FairPlay证书。播放器在Apple设备上结合DRM许可证和该证书解密DRM加密的直播流。 |
|[UpdateEncryptDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateencryptdrm) |上传DRM API密钥和/或FairPlay证书，或更新已有的密钥或证书。 |
|[DescribeEncryptDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdrm_2) |调用`DescribeEncryptDRM`接口，查看已配置的DRM证书管理平台访问密钥和FairPlay证书信息。 |
|[BindEncryptDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdrm_1) |调用`BindEncryptDRM`接口，为直播流添加或更新DRM加密配置。 |
|[UnBindEncryptDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdrm_3) |调用`UnBindEncryptDRM`接口，删除已创建的加密配置。 |
|[ListBindEncryptDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdrm_4) |调用`ListBindEncryptDRM`接口，查询指定域名空间和应用名称下的加密配置，或查看指定域名空间下的所有加密配置。 |
|[UpdateEncryptHLS](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateencrypthls) |调用`UpdateEncryptHLS`接口，添加或更新用于HLS标准加密的自建密钥管理服务地址及直播流的密钥更新周期。 |
|[GetHLSEncryptDataKey](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-gethlsencryptdatakey) |调用`GetHLSEncryptDataKey`接口，查询由直播流服务端生成并用于HLS标准加密的密钥。 |
|[DescribeEncryptHLS](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeencrypthls) |调用`DescribeEncryptHLS`接口，查询用于HLS标准加密的自建密钥管理服务地址及密钥更新周期。 |


<span id="45c4efae"></span>
## 流地址


|API |接口行为 |
|---|---|
|[GeneratePushURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generatepushurl-2023) |调用`GeneratePushURL`接口，生成指定流的推流地址。 |
|[GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) |调用`GeneratePlayURL`接口，生成指定流的拉流地址。 |


<span id="c695e1d3"></span>
## 流


|API |接口行为 |
|---|---|
|[DescribeLiveStreamInfoByPage](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreaminfobypagev2023) |调用`DescribeLiveStreamGroupByPage`接口，分页获取正在进行的在线流信息。 |
|[DescribeClosedStreamInfoByPage](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeclosedstreaminfobypage-2023) |调用`DescribeClosedStreamInfoByPage`接口，分页获取已结束的在线流信息。 |
|[DescribeForbiddenStreamInfoByPage](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeforbiddenstreaminfobypage-2023) |调用`DescribeForbiddenStreamGroupByPage`接口，分页获取禁用流的信息。 |
|[ForbidStream](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-forbidstream-2023) |调用`ForbidStream`接口，禁用直播流。 |
|[KillStream](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-killstream-2023) |调用`KillStream`接口，停止推送直播流。 |
|[DescribeLiveStreamState](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivestreamstate-2023) |调用`DescribeLiveStreamState`接口，查询直播流状态。 |
|[ResumeStream](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-resumestream-2023) |调用`ResumeStream`以恢复已禁用流的推送。 |


<span id="28f9a89c"></span>
## 转码


|API |接口行为 |
|---|---|
|[CreateTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/createtranscodepresetv2023) |调用`CreateTranscodePreset` API 创建转码配置，系统会根据你的转码配置对满足条件的直播流进行实时转码。 |
|[UpdateTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatetranscodepreset_1) |调用`UpdateTranscodePreset` API 更新已添加的转码配置。如未填写非必填参数，则对应的参数配置不会发生变化。 |
|[DeleteTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletetranscodepreset-2023) |调用`DeleteTranscodePreset` API 删除已创建的转码配置。 |
|[ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1) |调用`ListVhostTransCodePreset` API 查询转码配置列表。 |
|[ListCommonTransPresetDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcommontranspresetdetail-2023) |调用`ListCommonTransPresetDetail` API 查询通用转码配置的详细信息。 |
|[CreateTranscodePresetBatch](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateTranscodePresetBatch-2023) |调用`CreateTranscodePresetBatch` API 批量创建 ABR 子流转码配置。 |
|[DeleteTranscodePresetBatch](https://docs.byteplus.com/en/docs/byteplus-media-live/DeleteTranscodePresetBatch-2023) |调用`DeleteTranscodePresetBatch` API 批量删除 ABR 子流的转码配置。 |


<span id="7cfc1b40"></span>
## 录制


|API |接口行为 |
|---|---|
|[CreateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023) |调用`CreateRecordPresetV2` API 创建录制配置。系统会根据你的录制配置对满足条件的直播流进行录制。 |
|[UpdateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterecordpresetv2-2023) |调用`UpdateRecordPresetV2` API 更新已创建的录制配置。 |
|[ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) |调用`ListVhostRecordPresetV2` API 查询某 Vhost 下的所有录制配置，包括 Vhost、Vhost+应用、Vhost+应用+流三种层级的所有配置。 |
|[DescribeRecordTaskFileHistory](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerecordtaskfilehistory-2023) |查询指定域名空间下历史录制的相关信息，如时长、文件格式、开始时间和结束时间。正在进行中的录制不会被检索。 |
|[DeleteRecordPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleterecordpreset-2023) |调用`DeleteRecordPreset` API 删除已创建的录制配置。 |
|[CreatePullRecordTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreatePullRecordTask) |调用`CreatePullRecordTask` API 创建在指定时间段内开始和结束的直播拉流录制任务。创建成功后，可在直播期间录制任意时长的单路直播流，并保存为视频文件。 |
|[StopPullRecordTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-stoppullrecordtask) |调用`StopPullRecordTask` API 停止未开始或正在生效的录制任务。停止正在生效的录制任务会生成录制文件。 |
|[ListPullRecordTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpullrecordtask) |该 API 用于查询当前账号下创建的直播录制任务列表，支持按分页、域名、应用名、流名等条件组合查询。通过该 API 可获取任务的具体信息，如录制周期、任务状态等，帮助你跟踪录制进度、监控任务状态，并支持后续资源管理工作。 |
|[GetPullRecordTask](https://docs.byteplus.com/en/docs/byteplus-media-live/GetPullRecordTask) |调用`GetPullRecordTask` API 查询单个直播录制任务的信息。 |


<span id="6aa3aad5"></span>
## 截图采集


|API |接口行为 |
|---|---|
|[CreateSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/createsnapshotpresetv2) |添加截图配置后，当直播流处于截图配置的有效范围内时，将对直播流进行截图并保存。 |
|[UpdateSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/updatesnapshotpresetv2) |更新已添加的截图配置。 |
|[DeleteSnapshotPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletesnapshotpreset-2023) |调用`DeleteRecordPreset` API 删除已创建的截图配置。 |
|[ListVhostSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/listvhostsnapshotpresetv2) |获取指定域名空间下的所有截图配置信息。 |
|[DescribeCDNSnapshotHistory](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecdnsnapshothistory-2023) |调用`DescribeCDNSnapshotHistory` API 查询直播流的截图文件信息。 |


<span id="de791ec6"></span>
## 拉流回源


|API |接口行为 |
|---|---|
|[UpdateRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterelaysourcev3-2023) |调用`UpdateRelaySourceV3` API 添加或更新播放触发的拉流转推配置。按需拉源指仅在有观众观看时才会触发拉源操作，这样可以节省源站服务器的带宽资源，并提升系统整体效率。 |
|[DeleteRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleterelaysourcev3-2023) |调用`DeleteRelaySourceV3`接口删除按需拉源配置。 |
|[DescribeRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerelaysourcev3-2023) |调用`DescribeRelaySourceV3`接口查询按需拉源配置。 |


<span id="0a526019"></span>
## 直播时移


|API |接口行为 |
|---|---|
|[CreateTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createtimeshiftpresetv2-2023) |调用`CreateTimeShiftPresetV2`接口创建直播时移配置。配置直播流时移后，用户可在直播过程中观看之前已播出的内容。 |
|[UpdateTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatetimeshiftpresetv2-2023) |调用`UpdateTimeShiftPresetV2`接口更新已创建的时移配置。 |
|[DeleteTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletetimeshiftpresetv2-2023) |调用`DeleteTimeShiftPresetV2`接口删除已创建的时移配置。 |
|[ListTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listtimeshiftpresetv2-2023) |调用`ListTimeShiftPresetV2`接口查询指定域名空间下所有 appName 的时移配置。 |


<span id="1256ecf3"></span>
## 水印


|API |接口行为 |
|---|---|
|[CreateWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createwatermarkpreset-2023) |调用`CreateWatermarkPreset`接口为转码流创建水印配置。 |
|[DeleteWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletewatermarkpreset-2023) |调用`DeleteWatermarkPreset`接口删除现有水印配置。 |
|[UpdateWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatewatermarkpreset-2023) |调用`UpdateWatermarkPreset`接口更新现有水印配置。 |
|[ListWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listwatermarkpreset-2023) |调用`ListWatermarkPreset`接口查询指定 AppNanme 或 StreamName 的水印配置。 |
|[ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) |调用`ListVhostWatermarkPreset`接口查询指定域名空间下的所有水印配置。 |


<span id="4cf0323f"></span>
## AI 配音与字幕


|API |接口行为 |
|---|---|
|[CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask) |调用 `CreateSpeechTask` API 创建 AI 配音任务。任务创建后，在拉流转推时间段内从 `StartTime` 到 `EndTime` 开始推流时，任务会自动拉取直播流进行 AI 配音处理，并将处理后的直播流推送到指定推流地址。例如，你可以使用 OBS 开播，通过 AI 配音任务处理直播流，然后将处理后的内容推送到 TikTok 进行直播。更多信息，请参见 [AI Dubbing](https://docs.byteplus.com/en/docs/byteplus-media-live/ai-liveinterpret-simultaneous-audio-and-video-interpretation)。 |
|[SearchSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/SearchSpeechTask) |调用 `SearchSpeechTask` API，按指定条件搜索 AI 配音任务。 |
|[GetSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechTask) |调用 `GetSpeechTask` API 查询指定 AI 配音任务的信息。 |
|[UpdateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/UpdateSpeechTask) |调用 `UpdateSpeechTask` API 更新 AI 配音任务的功能开关状态。该 API 常用于在直播过程中根据需要开启或关闭翻译功能。 |
|[DeleteSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/DeleteSpeechTask) |调用 `DeleteSpeechTask` API 删除不再需要的 AI 配音任务。如果任务正在运行，MediaLive 会先停止任务再进行删除。 |
|[RestartSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/RestartSpeechTask) |调用 `RestartSpeechTask` API 重启正在运行或启动中的 AI 配音任务。 |
|[GetSpeechConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechConfig) |调用 `GetSpeechConfig` API 获取当前账号可用的 AI 配音配置，包括支持的字体和语言。 |
|[CreateSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023) |调用 `CreateSubtitleTranscodePreset` API 添加字幕配置。配置添加后，观众可以通过拉取与字幕配置关联的转码流，或拉取带字幕后缀的源流观看字幕效果。更多信息，请参见 [Subtitle configuration](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-manage-subtitle-configuration)。 |
|[DeleteSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletesubtitletranscodepreset-2023) |调用 `DeleteSubtitleTranscodePreset` API 删除已添加的字幕配置。 |
|[UpdateSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatesubtitletranscodepreset-2023) |调用 `UpdateSubtitleTranscodePreset` API 更新已添加的字幕配置。 |
|[ListVhostSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostsubtitletranscodepreset-2023) |调用 `ListVhostSubtitleTranscodePreset` API 查询指定域名空间下的所有字幕配置。 |
|[GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig) |调用 `GetSubtitleTranscodePresetConfig` API 获取当前账号在字幕配置中 AI 配音模式下可用的字体和语言。 |
|[DescribeSubtitleTranscodePresetDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/DescribeSubtitleTranscodePresetDetail) |调用 `DescribeSubtitleTranscodePresetDetail` API 查询指定字幕配置的详细信息。 |


<span id="4ed85b01"></span>
## 轮播任务


|API |接口行为 |
|---|---|
|[UpdateCarouselTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatecarouseltask) |调用`UpdateCarouselTask`接口修改指定轮播任务配置，调整回放内容、播放规则或时间范围，更新后系统将按照新配置执行轮播任务。 |
|[ListCarouselTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcarouseltask) |调用`ListCarouselTask`接口获取当前所有轮播任务列表，包括任务ID、状态和创建时间，可用于任务管理和批量查询。 |
|[DeleteCarouselTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletecarouseltask) |调用`DeleteCarouselTask`接口删除指定轮播任务。任务删除后，系统将停止播放该任务的所有轮播内容并释放相关资源。 |
|[CreateCarouselTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createcarouseltask) |调用`CreateCarouselTask`接口创建轮播任务。直播过程中，视频直播服务器将根据任务配置按设定顺序循环播放指定视频内容。 |
|[GetCarouselDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-getcarouseldetail) |调用`GetCarouselDetail`接口查询指定轮播任务的详细信息，包括回放状态、视频列表及当前播放进度，便于管理和监控任务执行状态。 |


<span id="28d32781"></span>
## 拉流转推


|API |接口行为 |
|---|---|
|[CreatePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createpulltopushtask-2023) |调用`CreatePullToPushTask`接口创建拉流转推任务，从直播流源或点播视频拉取内容。 |
|[ListPullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushtask-2023) |调用`ListPullToPushTask`接口分页查询拉流转推任务列表，支持按任务名称模糊搜索。 |
|[StopPullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-stoppulltopushtask-2023) |调用`StopPullToPushTask`接口停止未终止状态的拉流转推任务 |
|[DeletePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletepulltopushtask-2023) |调用`DeletePullToPushTask`接口删除已创建的拉流转推任务。 |
|[UpdatePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatepulltopushtask-2023) |调用 `UpdatePullToPushTask` API 更新拉流转推任务的信息。 |
|[CreatePullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createpulltopushgroup-2023) |调用 `CreatePullToPushGroup` API 创建拉流转推任务组并绑定到项目，通过配置该组可以基于项目管理子账号权限。 |
|[DeletePullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletepulltopushgroup-2023) |调用 `DeletePullToPushGroup` API 删除组名。 |
|[ListPullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushgroup-2023) |调用 `ListPullToPushGroup` API 查询组名列表。 |
|[ListPullToPushTaskV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushtaskv2-2023) |调用 `ListPullToPushTaskV2` API 分页查询拉流转推任务列表，支持按任务名称模糊搜索。 |
|[ContinuePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/continuepulltopushtask) |调用 `ContinuePullToPushTask` API 重启处于未开启状态的拉流转推任务。 |
|[RelaunchPullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-relaunchpulltopushtask) |调用 `RelaunchPullToPushTask` API 重启处于未开启状态的拉流转推任务。 |


<span id="f441942b"></span>
## VQScore


|API |接口行为 |
|---|---|
|[CreateLiveVideoQualityAnalysisTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createlivevideoqualityanalysistask-2023) |调用 `CreateLiveVideoQualityAnalysisTask` API 创建指定时长的视频质量分析任务。该任务会根据你设置的间隔获取每个分析点的实时码率，并对分析点的画面质量进行评分。 |
|[ListLiveVideoQualityAnalysisTasks](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listlivevideoqualityanalysistasks-2023) |调用 `ListLiveVideoQualityAnalysisTasks` API 查询视频质量分析任务信息列表。 |
|[GetLiveVideoQualityAnalysisTaskDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-getlivevideoqualityanalysistaskdetail-2023) |调用 `GetLiveVideoQualityAnalysisTaskDetail` API 查询单个视频质量分析任务的详情，包括指定分析点获取的视频码率和质量分析评分。 |
|[DeleteLiveVideoQualityAnalysisTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletelivevideoqualityanalysistask-2023) |调用 `DeleteLiveVideoQualityAnalysisTask` API 删除视频质量分析任务。你可以删除已完成和进行中的任务。 |


<span id="d308523e"></span>
## 用量查询


|API |接口行为 |
|---|---|
|[DescribeLiveTrafficData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivetrafficdata) |调用 `DescribeLiveTrafficData` API 查询指定流式域名在指定时间范围内的流量使用情况。此外，还包括推流域名的上行流量数据和拉流域名的下行流量数据。 |
|[DescribeLiveBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/eescribelivebandwidthdata) |调用 `DescribeLiveBandwidthData` API 查询指定流式域名在指定时间范围内的带宽使用情况，包括推流域名的上行带宽峰值和拉流域名的下行带宽峰值。 |
|[DescribeLiveSnapshotData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesnapshotdata) |调用 `DescribeLiveSnapshotData` API 获取指定直播域名在指定时间范围内由截图功能生成的截图数量。 |
|[DescribeLiveRecordData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliverecorddata) |调用 `DescribeLiveRecordData` API 查询指定流式域名在指定时间范围内的录制使用情况，包括最大并发录制数。 |
|[DescribeLivePullToPushData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepulltopushdata) |调用 `DescribeLivePullToPushData` API 查询指定时间范围内该组生成的所有拉流转推任务的时长使用情况。 |
|[DescribeLivePullToPushBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepulltopushbandwidthdata) |调用 `DescribeLivePullToPushBandwidthData` API 查询指定时间范围内生成的拉流转推任务的带宽使用情况。 |
|[DescribeLiveTranscodeData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivetranscodedata) |调用 `DescribeLiveTranscodeData` API 查询指定直播域名在指定时间范围内的转码时长使用情况。 |
|[DescribeLiveStorageSpaceData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestoragespacedata) |调用 `DescribeLiveStorageSpaceData` API 查询指定时间范围内直播时移功能每日的空间使用情况。 |
|[DescribeLiveP95PeakBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivep95peakbandwidthdata) |调用 `DescribeLiveP95PeakBandwidthData` API 查询指定直播域名在指定时间范围内的95分位带宽峰值使用情况，包括推流域名的上行95分位带宽峰值和拉流域名的下行95分位带宽峰值。 |
|[DescribeLiveASRDurationData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveasrdurationdata) |调用 `DescribeLiveASRDurationData` API，查询指定时间范围内 AI 语音转字幕的时长。 |


<span id="dc8cc5d1"></span>
## 日志


|API |接口行为 |
|---|---|
|[DescribeLiveLogData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivelogdata) |调用 `DescribeLiveLogData` API，查询域名生成的日志文件信息。 |


<span id="120fcc5b"></span>
## 统计与分析


|API |接口行为 |
|---|---|
|[DescribeLivePushStreamInfoData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepushstreaminfodata) |调用 `DescribeLivePushStreamInfoData` API，查询推流信息及流断开原因。 |
|[DescribeLiveISPData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata) |调用 `DescribeLiveISPData` API，获取为 BytePlus MediaLive 提供网络接入服务的互联网服务提供商（ISP）标识符。获取 ISP 标识符后，可在支持基于 ISP 查询的 API 中，用于查询特定 ISP 的维度数据。 |
|[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) |调用 `DescribeLiveRegionData` API，获取 MediaLive 覆盖区域的标识符。获取区域标识符后，可在支持按区域查询数据的 API 中，用于检索特定区域的数据。 |
|[DescribeLiveSourceTrafficData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesourcetrafficdata) |调用 `DescribeLiveSourceTrafficData` API，查询指定拉流流式域名或源流在指定时间范围内产生的源流量和带宽监控数据。 |
|[DescribeLiveStreamCountData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreamcountdata) |获取指定时间范围内特定推流、源拉流或转码流的峰值数量。 |
|[DescribeLivePushStreamMetrics](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepushstreammetrics) |调用 `DescribeLivePushStreamMetrics` API，查询指定时间范围内单路推流的监控数据，如音视频帧率和码率，以评估直播流的健康状况。 |
|[DescribeLivePlayStatusCodeData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveplaystatuscodedata) |调用 `DescribeLivePlayStatusCodeData` API，查询指定时间范围内对域名发起的请求状态码占比，包括推流请求、拉流请求和源流请求。 |
|[DescribeLiveStreamSessionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreamsessiondata) |调用 `DescribeLiveStreamSessionData` API，查询指定时间范围内指定域名下所有直播流或指定直播流的请求次数及最大在线观众数。 |
|[DescribeLiveSourceStreamMetrics](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesourcestreammetrics) |调用 `DescribeLiveSourceStreamMetrics` API，查询指定时间范围内单路源流的监控数据，如音视频帧率和码率，以评估源流的健康状况。 |
|[DescribeCDNTrafficData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecdntrafficdata) |调用 `DescribeCDNTrafficData` API，查询指定时间范围内访问直播录制和截图时所用的 CDN 流量。 |
|[DescribeLiveBatchPushStreamMetrics](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivebatchpushstreammetrics-2023) |调用 `DescribeLiveBatchPushStreamMetrics` API，查询某域名下一个或多个推流的推流统计数据，包括帧率、码率、显示时间戳（PTS）等。可通过统计数据监控推流会话的健康状况。可查询已删除域名的数据。 |
|[DescribeLiveTranscodeInfoData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivetranscodeinfodata-2023) |调用 `DescribeLiveTranscodeInfoData` API，查询指定时间范围内特定直播域名或直播流的详细数据，如转码任务 ID、流名称、转码后缀、转码开始和结束时间。 |
|[DescribeLiveTopPlayData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivetopplaydata-2023) |调用 `DescribeLiveTopPlayData` API，查询指定时间范围内流量和带宽排名前列的直播流或域名的详细信息。 |
|[DescribeLiveBatchStreamTrafficData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivebatchstreamtrafficdata-2023) |调用 `DescribeLiveBatchStreamTrafficData` API，查询指定时间范围内的上行和下行流量数据及其详细数据。 |
|[DescribeLiveBatchStreamTranscodeData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivebatchstreamtranscodedata-2023) |调用`DescribeLiveBatchStreamTranscodeData` API 查询指定域名下所有流在指定时间范围内的转码数据。数据包括转码时长、分辨率等级和编码方式等指标。 |
|[DescribeLiveEdgeStatData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeliveedgestatdata-2023) |调用`DescribeLiveEdgeStatData`接口，查询指定协议、运营商、区域和时间范围下，直播流产生的上行和下行流量、上行和下行带宽峰值，以及请求数等数据。 |
|[DescribeLiveBatchSourceStreamMetrics](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivebatchsourcestreammetrics) |获取指定拉流域名下，所有或指定源站拉流在指定时间范围内的音视频帧率、码率等监控数据。可通过监控数据评估源站拉流的健康状况。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">可获取已删除域名产生的历史源站拉流数据。</div><br> |


<span id="687d20b7"></span>
## 回调


|API |接口行为 |
|---|---|
|[UpdateCallback](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatecallback-2023) |调用`UpdateCallback` API，添加或更新推流、录制和截图等事件的回调配置。 |
|[DescribeCallback](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecallback-2023) |调用`DescribeCallback` API，查询应用的回调配置。 |
|[DeleteCallback](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletecallback-2023) |调用`DeleteCallback` API，删除回调配置。 |
|[DescribeLiveCallbackData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivecallbackdata) |该 API 支持查询与直播相关的回调记录，包括事件类型、状态、请求和返回调用结果数据。可用于排查回调异常，并验证回调是否成功送达。 |


<span id="58f2977b"></span>
## 存储空间


|API |接口行为 |
|---|---|
|[ListStorageSpace](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-liststoragespace) |调用`ListStorageSpace` API，查询账号下所有可用存储空间列表。配置录制和截图参数时可参考该列表。 |
|[ListStorageSpaceDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-liststoragespacedetail) |调用`ListStorageSpaceDetail` API，查询账号下指定存储空间的详细信息。 |
