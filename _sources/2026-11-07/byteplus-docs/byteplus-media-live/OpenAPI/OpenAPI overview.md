---
title: "OpenAPI overview"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-openapi-overview"
---

This topic lists all OpenAPI endpoints offered by BytePlus MediaLive.

<span id="533dfe50"></span>
## Domain


|API |Description |
|---|---|
|[CreateDomainV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-dj3h3u96xn) |Call the `CreateDomainV2` API to add one or more domain names for push streaming or pull streaming. |
|[UpdateDomainVhost](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatedomainvhost) |Call the `UpdateDomainVhost` API to Change the domain name space associated with the domain name. |
|[DeleteDomain](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletedomain-2023) |Call the `DeleteDomain` interface to delete a domain name. |
|[DisableDomain](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-disabledomain-2023) |Call the `DisableDomain` API to disable a domain name. After the domain name is disabled, the domain status in the MediaLive service changes from `0-Enabled` to `2-Disabled`. |
|[EnableDomain](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-enabledomain-2023) |Call the `EnableDomain` API to enable a disabled domain name. After the domain name is enabled, the domain status in the MediaLive service changes from `2-Disabled` to `0-Enabled`. |
|[DescribeDomain](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describedomain-2023) |Call the `DescribeDomain` API to query the information of specified domain names, including the domain name space, CNAME address, and domain status, etc. |
|[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) |Call the `ListDomainDetail` API to query the information about the domain names under your account. You can filter your query results by domain status, domain type, and other dimensions. |


<span id="access-control"></span>
## Access control


|API |Description |
|---|---|
|[UpdateClusterRateLimit](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateclusterratelimit) |Call the `UpdateClusterRateLimit` API to add or modify the frequency limit for pull\-stream requests. |
|[DeleteClusterRateLimit](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleteclusterratelimit) |Call the `DeleteClusterRateLimit` API to delete the frequency limit for pull\-stream requests. |
|[DescribeClusterRateLimit](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeclusterratelimit) |Call the `DescribeClusterRateLimit` API to query the frequency limit for pull\-stream requests. |
|[UpdateUserAgentAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateuseragentaccessrule) |Call the `UpdateUserAgentAccessRule` API to add or update User\-Agent restrictions. |
|[DescribeUserAgentAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeuseragentaccessrule) |Call the `DescribeUserAgentAccessRule` API to query User\-Agent restrictions. |
|[DeleteUserAgentAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleteuseragentaccessrule_1) |Call the `DeleteUserAgentAccessRule` API to delete the User\-Agent restrictions. |
|[UpdateIPAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateipaccessrule) |Call the `UpdateIPAccessRule` API to configure an IP blocklist or allowlist for a specified domain name. |
|[DescribeIPAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeipaccessrule) |Call the `DescribeIPAccessRule` API to query the created IP access rules configuration. |
|[DeleteIPAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleteipaccessrule) |Call the `DeleteIPAccessRule` API to delete IP blocklists or allowlists for a specified domain name. |
|[UpdateRegionAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateregionaccessrule) |Call the `UpdateRegionAccessRule` API to create geographic restrictions for a specified domain name. |
|[DescribeRegionAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeregionaccessrule) |Call the `DescribeRegionAccessRule` API to query geographic restrictions for a specified domain name. |
|[DeleteRegionAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleteregionaccessrule) |Call the `DeleteRegionAccessRule` API to delete geographic restrictions for a specified domain name. |
|[UpdateFormatAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateformataccessrule) |Call the `UpdateFormatAccessRule` API to create protocol restrictions. |
|[DescribeFormatAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeformataccessrule) |Call the `DescribeFormatAccessRule` API to query the protocol restrictions. |
|[DeleteFormatAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleteformataccessrule) |Call the `DeleteFormatAccessRule` API to delete the protocol restrictions. |
|[UpdateAuthKey](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateauthkey-2023) |Call the `UpdateAuthKey` API to add or update the URL authentication configuration for push and pull streaming addresses. When using this API to update the configuration, all authentication parameters will be updated. |
|[DescribeAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeauth-2023) |Call the `DescribeAuth` API to query the URL authentication configuration that meets the query conditions. |
|[UpdateReferer](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatereferer-2023) |Calls the `UpdateReferer` API to create a domain\-level (Vhost + Domain) or app\-level (Vhost + App) Referer blacklist or whitelist configuration. |
|[DeleteReferer](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletereferer-2023) |Calls the `DeleteReferer` API to delete the referer blocklist or allowlist configuration. |
|[DescribeReferer](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describereferer-2023) |Calls the `UpdateReferer` API to get the referer blocklist or allowlist configuration. |
|[UpdateRelaySourceRewrite](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterelaysourcerewrite) |Configures origin address rewrite rules. The origin address rewrite feature enables fetching the stream from a new address based on predefined matching rules. For details, see [Origin address rewrite](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-origin-address-rewrite). |
|[DescribeRelaySourceRewrite](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-dakt2mfojk) |Queries origin address rewrite rules. The origin address rewrite feature enables fetching the stream from a new address based on predefined matching rules. For details, see [Origin address rewrite](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-origin-address-rewrite). |
|[DeleteRelaySourceRewrite](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-3nf0nln2b2) |Deletes origin address rewrite rules. The origin address rewrite feature enables fetching the stream from a new address based on predefined matching rules. For details, see [Origin address rewrite](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-origin-address-rewrite). |
|[UpdateRemoteAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateremoteauth-2023) |Call the `UpdateRemoteAuth` API to create a remote authentication configuration for the pull\-stream domain name. After the creation is successful, the user's pull\-stream request will be sent to the specified authentication server, which will verify the user's pull\-stream request. |
|[DescribeRemoteAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeremoteauth-2023) |Call the `DescribeRemoteAuth` API to query the remote authentication configuration of the pull domain. |
|[DeleteRemoteAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleteremoteauth-2023) |Call the `DeleteRemoteAuth` API to delete the added remote authentication configuration. |
|[ListVhostRemoteAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostremoteauth-2023) |Call the `ListVhostRemoteAuth` API to query the remote authentication configuration of all pull domains under the Vhost. |


<span id="latency-control"></span>
## Latency control


|API |Description |
|---|---|
|[UpdateLatencyConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/updatelatencyconfig) |Call the `UpdateLatencyConfig` API to reduce the live streaming latency by configuring server GOP cache for streams under the specified domain name used in stream pulling. |
|[DescribeLatencyConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/describelatencyconfig) |Call the `DescribeLatencyConfig` API to query the server cache config of the GOP. |
|[DeleteLatencyConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/deletelatencyconfig) |Call the `DeleteLatencyConfig` API to delete the created server GOP cache configuration. |


<span id="encapsulation"></span>
## Encapsulation


|API |Description |
|---|---|
|[UpdateHLSConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/updatehlsconfig) |Call the `UpdateHLSConfig` API to add or update the HLS configuration for a specific domain space, including segment size, and segment number to effectively reduce latency and improve compatibility in live streaming. In HTTP Live Streaming (HLS) and Low\-Latency HLS (LL\-HLS), a live stream is sliced into Transport Stream (TS). Each TS has a corresponding URL, and the address changes constantly when using the HLS protocol for live pull streaming. |
|[DescribeHLSConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/describehlsconfig) |Call the `DescribeHLSConfig` API to query the HLS configuration for a specific domain name space, including segment size, segment number, and more. |
|[DeleteHLSConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/deletehlsconfig) |Call the `DeleteHLSConfig` API to restores the HLS configuration for specific domain space to default settings, including segment size, segment number, and more. |
|[UpdateCMAFConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/updatecmafconfig) |In Dynamic Adaptive Streaming over HTTP (DASH) and Low\-Latency DASH (LL\-DASH), a live stream is sliced into Common Media Application Format (CMAF) segments. Call the `UpdateCMAFConfig` API, you can adjust the duration and segment number settings to effectively reduce the latency and improve compatibility in live streaming under the specified domain name space (Vhost). |
|[DescribeCMAFConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/describecmafconfig) |Call the `DescribeCMAFConfig` API to query the duration and segment number settings for the streaming under the specified domain name space. |
|[DeleteCMAFConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/deletecmafconfig) |Call the `DeleteCMAFConfig` API to delete DASH settings for the streaming under the specified domain name space (Vhost) which includes the segment duration and segment number |


<span id="header"></span>
## Header


|API |Description |
|---|---|
|[EnableHTTPHeaderConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-enablehttpheaderconfig) |Call the `EnableHTTPHeaderConfig` API to enable or disable the HTTP header configuration. |
|[DeleteHTTPHeaderConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletehttpheaderconfig) |Call the `DeleteHTTPHeaderConfig` API to delete HTTP header configurations for a specified domain name which have been added through UpdateHTTPHeaderConfig. |
|[DescribeHTTPHeaderConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describehttpheaderconfig) |Call the `DescribeHTTPHeaderConfig` API to query the HTTP header configurations for a specified domain name. |
|[UpdateHTTPHeaderConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatehttpheaderconfig) |Call the `UpdateHTTPHeaderConfig` API to add additional HTTP headers in the response sent from an edge server to a client, or add additional HTTP headers in the request sent to a third\-party origin server during an origin\-pull task. |


<span id="certificate"></span>
## Certificate


|API |Description |
|---|---|
|[CreateCert](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createcert-2023) |Call the `CreateCert` API to add or update your certificate to MediaLive so that it can later be bound to a domain name and start HTTPS. |
|[DeleteCert](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletecert-2023) |Call the `DeleteCert` API to delete the certificates that have been uploaded to MediaLive. |
|[BindCert](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-bindcert-2023) |Call the `BindCert` API to bind the uploaded HTTPS certificate to the domain name and enable HTTPS secure transmission for this domain name. |
|[UnbindCert](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-unbindcert-2023) |Call the `UnbindCert` API to unbind the certificate from the domain name. |
|[ListCertV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcertv2) |Call the `ListCertV2` API to view the list of certificates under the current account. |
|[DescribeCertDetailSecretV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdetailsecretv2-2023) |Call the `DescribeCertDetailSecretV2` API to view the detailed information of the certificate through the certificate ID or certificate chain ID. |


<span id="encryption"></span>
## Encryption


|API |Description |
|---|---|
|[DescribeLicenseDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelicensedrm) |Retrieves the DRM license. The player uses the license to decrypt a DRM\-encrypted live stream. |
|[DescribeCertDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdrm) |Retrieves the FairPlay certificate. The player uses the certificate together with the DRM license to decrypt a DRM\-encrypted live stream on Apple devices. |
|[UpdateEncryptDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateencryptdrm) |Uploads a DRM API key and/or FairPlay certificate, or updates an existing one. |
|[DescribeEncryptDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdrm_2) |Call the `DescribeEncryptDRM` API to view the configured DRM certificate management platform access keys and FairPlay certificate information. |
|[BindEncryptDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdrm_1) |Call the `BindEncryptDRM` API to add or update the DRM encryption configuration for live streams. |
|[UnBindEncryptDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdrm_3) |Call the `UnBindEncryptDRM` API to delete the created encryption configuration. |
|[ListBindEncryptDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdrm_4) |Invoke the `ListBindEncryptDRM` interface to query the encryption configuration for a specified domain namespace and application name, or to view all encryption configurations under a specified domain namespace. |
|[UpdateEncryptHLS](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateencrypthls) |Call the `UpdateEncryptHLS` interface to add or update the self\-built key management service address used for HLS standard encryption and the key update period for live video streaming. |
|[GetHLSEncryptDataKey](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-gethlsencryptdatakey) |Call the `GetHLSEncryptDataKey` API to query the key generated by the live video service server for use in HLS standard encryption. |
|[DescribeEncryptHLS](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeencrypthls) |Call the `DescribeEncryptHLS` API to query the address of the self\-managed key management service used for HLS standard encryption and the cycle for updating the keys. |


<span id="stream-address"></span>
## Stream address


|API |Description |
|---|---|
|[GeneratePushURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generatepushurl-2023) |Call the `GeneratePushURL` API to generate the push stream addresses for a specified stream. |
|[GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) |Call the `GeneratePlayURL` API to generate the pull stream addresses for a specified stream. |


<span id="stream"></span>
## Stream


|API |Description |
|---|---|
|[DescribeLiveStreamInfoByPage](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreaminfobypagev2023) |Call the `DescribeLiveStreamGroupByPage` API to retrieve information of ongoing live streams by page. |
|[DescribeClosedStreamInfoByPage](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeclosedstreaminfobypage-2023) |Call the `DescribeClosedStreamInfoByPage` API to retrieve information of ended live streams by page. |
|[DescribeForbiddenStreamInfoByPage](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeforbiddenstreaminfobypage-2023) |Call the `DescribeForbiddenStreamGroupByPage` API to retrieve information of disabled streams by page. |
|[ForbidStream](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-forbidstream-2023) |Call the `ForbidStream` API to disable a live stream. |
|[KillStream](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-killstream-2023) |Call the `KillStream` API to stop pushing a live stream. |
|[DescribeLiveStreamState](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivestreamstate-2023) |Call the `DescribeLiveStreamState` API to query the status of a live stream. |
|[ResumeStream](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-resumestream-2023) |Call the `ResumeStream` to resume the pushing of a disabled stream. |


<span id="transcoding"></span>
## Transcoding


|API |Description |
|---|---|
|[CreateTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/createtranscodepresetv2023) |Call the `CreateTranscodePreset` API to create a transcoding configuration, and the system will perform real\-time transcoding on live streams that meet the conditions according to your transcoding configuration. |
|[UpdateTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatetranscodepreset_1) |Call the `UpdateTranscodePreset` API to update the added transcoding configuration. If the non\-required parameters are not filled in, the corresponding parameter configuration will not change. |
|[DeleteTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletetranscodepreset-2023) |Call the `DeleteTranscodePreset` API to delete the created transcoding configuration. |
|[ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1) |Call the `ListVhostTransCodePreset` API to query the transcoding configuration list. |
|[ListCommonTransPresetDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcommontranspresetdetail-2023) |Call the `ListCommonTransPresetDetail` API to query the detailed of the default transcoding configuration. |
|[CreateTranscodePresetBatch](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateTranscodePresetBatch-2023) |Call the `CreateTranscodePresetBatch` API to batch create ABR sub\-stream transcoding configurations. |
|[DeleteTranscodePresetBatch](https://docs.byteplus.com/en/docs/byteplus-media-live/DeleteTranscodePresetBatch-2023) |Call the `DeleteTranscodePresetBatch` API to batch delete the transcoding configurations of ABR sub\-streams. |


<span id="recording"></span>
## Recording


|API |Description |
|---|---|
|[CreateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023) |Call the `CreateRecordPresetV2` API to create a recording configuration. The system performs recording on live streams that meet the conditions according to your recording configuration. |
|[UpdateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterecordpresetv2-2023) |Call the `UpdateRecordPresetV2` API to update the created recording configuration. |
|[ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) |Call the `ListVhostRecordPresetV2` API to query all recording configurations under a Vhost, including all configurations at the three levels of Vhost, Vhost + App, Vhost + App + Stream. |
|[DescribeRecordTaskFileHistory](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerecordtaskfilehistory-2023) |Queries information about previous recordings of a specified domain name space, such as their duration, file format, start time, and end time. Ongoing recordings will not be retrieved. |
|[DeleteRecordPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleterecordpreset-2023) |Call the `DeleteRecordPreset` API to delete the created recording configuration. |
|[CreatePullRecordTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreatePullRecordTask) |Call the `CreatePullRecordTask` API to create a live pull stream recording task that starts and ends at a specified time. After successful creation, a single live stream of any duration can be recorded during the live broadcast and saved as a video file. |
|[StopPullRecordTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-stoppullrecordtask) |Call the `StopPullRecordTask` API to stop the recording task that has not started or is in effect. Stopping the recording task in effect will generate a recording file. |
|[ListPullRecordTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpullrecordtask) |This API is used to query the live broadcast recording task list created under the current account, and supports combined queries by conditions such as pagination, domain name, application name, and stream name. Through this API, you can obtain specific information about the task, such as the recording period, task status, etc., which helps you track the recording progress, monitor the task status, and support subsequent resource management work. |
|[GetPullRecordTask](https://docs.byteplus.com/en/docs/byteplus-media-live/GetPullRecordTask) |Call the `GetPullRecordTask` API to query the information of a single live recording task. |


<span id="screenshot-capturing"></span>
## Screenshot capturing


|API |Description |
|---|---|
|[CreateSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/createsnapshotpresetv2) |Adds the screenshot configuration to capture and save screenshots of the live stream when it falls within the effective range of the screenshot configuration. |
|[UpdateSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/updatesnapshotpresetv2) |Updates the added screenshot configuration. |
|[DeleteSnapshotPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletesnapshotpreset-2023) |Call the `DeleteRecordPreset` API to delete the created screenshot configuration. |
|[ListVhostSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/listvhostsnapshotpresetv2) |Gets all screenshot configuration information under a specific domain namespace. |
|[DescribeCDNSnapshotHistory](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecdnsnapshothistory-2023) |Call the `DescribeCDNSnapshotHistory` API to query the screenshot file information of the live stream. |


<span id="origin-pull"></span>
## Origin pull


|API |Description |
|---|---|
|[UpdateRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterelaysourcev3-2023) |Call the `UpdateRelaySourceV3` API to add or update the play\-triggered origin\-pull configuration. Play\-triggered origin\-pull means that the origin\-pull is only triggered when there are viewers watching, which can save the bandwidth resources of the source server and improve the overall efficiency of the system. |
|[DeleteRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleterelaysourcev3-2023) |Call the `DeleteRelaySourceV3` API to delete the play\-triggered origin\-pulling configuration. |
|[DescribeRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerelaysourcev3-2023) |Call the `DescribeRelaySourceV3` API to query the play\-triggered origin\-pulling configuration. |


<span id="time-shifting"></span>
## Time shifting


|API |Description |
|---|---|
|[CreateTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createtimeshiftpresetv2-2023) |Call the `CreateTimeShiftPresetV2` API to create live time\-shift configuration. After configuring the live stream for time\-shift, users will be able to watch previously broadcasted content during the live process. |
|[UpdateTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatetimeshiftpresetv2-2023) |Call the `UpdateTimeShiftPresetV2` API to update an already created time\-shift configuration. |
|[DeleteTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletetimeshiftpresetv2-2023) |Call the `DeleteTimeShiftPresetV2` API to delete an already created time\-shift configuration. |
|[ListTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listtimeshiftpresetv2-2023) |Call the `ListTimeShiftPresetV2` API to query the time\-shifting configurations of all appNames under a specified domain name space. |


<span id="watermarking"></span>
## Watermarking


|API |Description |
|---|---|
|[CreateWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createwatermarkpreset-2023) |Call the `CreateWatermarkPreset` API to create watermark configuration for Transcoding streams. |
|[DeleteWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletewatermarkpreset-2023) |Call the `DeleteWatermarkPreset` API to delete the existing watermark configuration. |
|[UpdateWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatewatermarkpreset-2023) |Call the `UpdateWatermarkPreset` API to update the existing watermark configuration. |
|[ListWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listwatermarkpreset-2023) |Call the `ListWatermarkPreset` API to query the watermark configuration of a specified AppNanme or StreamName. |
|[ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) |Call the `ListVhostWatermarkPreset` API to query all watermark configurations under a specified domain name space. |


<span id="ai-dubbing-and-subtitles"></span>
## AI Dubbing and subtitles


|API |Description |
|---|---|
|[CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask) |Call the `CreateSpeechTask` API to create an AI Dubbing task. After the task is created, when you start pushing a stream during the relay time period from `StartTime` to `EndTime`, the task automatically pulls the live stream for AI Dubbing processing and pushes the processed live stream to the specific push stream address. For example, you can start a live stream with OBS, process the live stream through an AI Dubbing task, and then stream the processed content on TikTok. For more information, see [AI Dubbing](https://docs.byteplus.com/en/docs/byteplus-media-live/ai-liveinterpret-simultaneous-audio-and-video-interpretation). |
|[SearchSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/SearchSpeechTask) |Call the `SearchSpeechTask` API to search for AI Dubbing tasks that match specific conditions. |
|[GetSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechTask) |Call the `GetSpeechTask` API to query information about a specific AI Dubbing task. |
|[UpdateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/UpdateSpeechTask) |Call the `UpdateSpeechTask` API to update the feature switch status of an AI Dubbing task. This API is commonly used to turn translation on or off as needed during a live stream. |
|[DeleteSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/DeleteSpeechTask) |Call the `DeleteSpeechTask` API to delete an AI Dubbing task that is no longer needed. If the task is running, MediaLive stops the task before deleting the task. |
|[RestartSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/RestartSpeechTask) |Call the `RestartSpeechTask` API to restart an AI Dubbing task that is running or starting. |
|[GetSpeechConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechConfig) |Call the `GetSpeechConfig` API to get the AI Dubbing configuration available to the current account, including supported fonts and languages. |
|[CreateSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023) |Call the `CreateSubtitleTranscodePreset` API to add a subtitle configuration. After the configuration is added, viewers can watch the subtitle effect by pulling a transcoded stream associated with the subtitle configuration, or by pulling the source stream with the subtitle suffix appended. For more information, see [Subtitle configuration](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-manage-subtitle-configuration). |
|[DeleteSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletesubtitletranscodepreset-2023) |Call the `DeleteSubtitleTranscodePreset` API to delete the added subtitle configuration. |
|[UpdateSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatesubtitletranscodepreset-2023) |Call the `UpdateSubtitleTranscodePreset` API to update the added subtitle configuration. |
|[ListVhostSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostsubtitletranscodepreset-2023) |Call the `ListVhostSubtitleTranscodePreset` API to query all subtitle configurations under a specific domain name space. |
|[GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig) |Call the `GetSubtitleTranscodePresetConfig` API to get the fonts and languages that are available to the current account for AI Dubbing mode in subtitle configurations. |
|[DescribeSubtitleTranscodePresetDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/DescribeSubtitleTranscodePresetDetail) |Call the `DescribeSubtitleTranscodePresetDetail` API to query the details of specific subtitle configurations. |


<span id="carousel-task"></span>
## Carousel Task


|API |Description |
|---|---|
|[UpdateCarouselTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatecarouseltask) |Call the `UpdateCarouselTask` API to modify the specified carousel task configuration, adjust the playback content, playback rules, or time range, and the system will execute the carousel task according to the new configuration after the update. |
|[ListCarouselTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcarouseltask) |Call the `ListCarouselTask` API to obtain the list of all current carousel tasks, including task IDs, statuses, and creation times, which can be used for task management and batch queries. |
|[DeleteCarouselTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletecarouseltask) |Call the `DeleteCarouselTask` API to delete the specified carousel task. After the task is deleted, the system will stop playing all the carousel content of the task and release the relevant resources. |
|[CreateCarouselTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createcarouseltask) |Call the `CreateCarouselTask` API to create a carousel task. During the live broadcast, the video live broadcast server will play the specified video content in a loop in the set order according to the task configuration. |
|[GetCarouselDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-getcarouseldetail) |Call the `GetCarouselDetail` API to query the detailed information of the specified carousel task, including the playback status, video list, and current playback progress, to facilitate the management and monitoring of the task execution status. |


<span id="relay"></span>
## Relay


|API |Description |
|---|---|
|[CreatePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createpulltopushtask-2023) |Call the `CreatePullToPushTask` API to create a relay task to pull content from a live\-stream source or on\-demand videos. |
|[ListPullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushtask-2023) |Call the `ListPullToPushTask` API to query the relay task list in pagination, supporting fuzzy search by Task name. |
|[StopPullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-stoppulltopushtask-2023) |Calling the `StopPullToPushTask` API to stop the relay task with a non\-terminated status |
|[DeletePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletepulltopushtask-2023) |Call the `DeletePullToPushTask` API to delete the created relay task. |
|[UpdatePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatepulltopushtask-2023) |Call the `UpdatePullToPushTask` API to update the information of a Relay task. |
|[CreatePullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createpulltopushgroup-2023) |Call the `CreatePullToPushGroup` API to create a relay task group and bind it to a project, which allows you to manage sub\-account permissions based on the project by configuring the group. |
|[DeletePullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletepulltopushgroup-2023) |Call the `DeletePullToPushGroup` API to delete a group name. |
|[ListPullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushgroup-2023) |Call the `ListPullToPushGroup` API to query a list of group name. |
|[ListPullToPushTaskV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushtaskv2-2023) |Call the `ListPullToPushTaskV2` API to query the relay task list in pagination, supporting fuzzy search by Task name. |
|[ContinuePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/continuepulltopushtask) |Call the `ContinuePullToPushTask` API to restart the relay task that is in a disabled state. |
|[RelaunchPullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-relaunchpulltopushtask) |Call the `RelaunchPullToPushTask` API to restart the relay task that is in a disabled state. |


<span id="vqscore"></span>
## VQScore


|API |Description |
|---|---|
|[CreateLiveVideoQualityAnalysisTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createlivevideoqualityanalysistask-2023) |Call the `CreateLiveVideoQualityAnalysisTask` API to create a video quality analysis task with a specified duration. The task will obtain the real\-time bitrate for each analysis point based on the interval you set, and score the picture quality of the analysis points. |
|[ListLiveVideoQualityAnalysisTasks](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listlivevideoqualityanalysistasks-2023) |Call the `ListLiveVideoQualityAnalysisTasks` API to query the list of video quality analysis task information. |
|[GetLiveVideoQualityAnalysisTaskDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-getlivevideoqualityanalysistaskdetail-2023) |Call the `GetLiveVideoQualityAnalysisTaskDetail` API to query the details of a single video quality analysis task, including the video bitrate and quality analysis scores obtained at the specified analysis point. |
|[DeleteLiveVideoQualityAnalysisTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletelivevideoqualityanalysistask-2023) |Call the `DeleteLiveVideoQualityAnalysisTask` API to delete video quality analysis tasks. You can delete both completed and ongoing tasks. |


<span id="usage-query"></span>
## Usage query


|API |Description |
|---|---|
|[DescribeLiveTrafficData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivetrafficdata) |Call the `DescribeLiveTrafficData` API to query the traffic usage of specified live streaming domains within the specified time range. Moreover, it includes upstream traffic data for push domains and downstream traffic data for pull domains. |
|[DescribeLiveBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/eescribelivebandwidthdata) |Call the `DescribeLiveBandwidthData` API to query the bandwidth usage of specified live streaming domains within the specified time range, including the upstream peak bandwidth of push domains and the downstream peak bandwidth of pull domains. |
|[DescribeLiveSnapshotData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesnapshotdata) |Call the `DescribeLiveSnapshotData` API to retrieve the number of snapshots generated by the screenshot feature for a specific live domain within a specified time range. |
|[DescribeLiveRecordData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliverecorddata) |Call the `DescribeLiveRecordData` API to query the recording usage, including the maximum number of concurrent recordings, of specified live streaming domains within the specified time range. |
|[DescribeLivePullToPushData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepulltopushdata) |Call the `DescribeLivePullToPushData` API to query the duration usage of all relay tasks generated by the group within a specified time range. |
|[DescribeLivePullToPushBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepulltopushbandwidthdata) |Call the `DescribeLivePullToPushBandwidthData` API to query the bandwidth usage of relay tasks generated within a specified time range. |
|[DescribeLiveTranscodeData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivetranscodedata) |Call the `DescribeLiveTranscodeData` API to query the transcoding duration usage of a specific live domain within a specified time range. |
|[DescribeLiveStorageSpaceData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestoragespacedata) |Call the `DescribeLiveStorageSpaceData` API to query the storage space usage of the live time\-shift function on a daily basis within a specified time range. |
|[DescribeLiveP95PeakBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivep95peakbandwidthdata) |Call the `DescribeLiveP95PeakBandwidthData` API to query the 95th percentile peak bandwidth usage of a specific live domain within a specified time range, including the upstream 95th percentile peak bandwidth of the push stream domain and the downstream 95th percentile peak bandwidth of the pull stream domain. |
|[DescribeLiveASRDurationData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveasrdurationdata) |Call the `DescribeLiveASRDurationData` API to query the duration of AI speech\-to\-subtitle conversion within a specified time range. |


<span id="log"></span>
## Log


|API |Description |
|---|---|
|[DescribeLiveLogData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivelogdata) |Call the `DescribeLiveLogData` API to query the information of log files generated by the domain. |


<span id="statistics-and-analysis"></span>
## Statistics and analysis


|API |Description |
|---|---|
|[DescribeLivePushStreamInfoData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepushstreaminfodata) |Call the `DescribeLivePushStreamInfoData` API to query the information about the push streaming and the cause of stream disconnection |
|[DescribeLiveISPData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata) |Call the `DescribeLiveISPData` API to retrieve the identifiers of Internet Service Providers (ISPs) that provide network access services for BytePlus MediaLive. Once you obtain the ISP identifiers, you can use them to query dimensional data for specific ISPs in APIs that support ISP\-based querying. |
|[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) |Call the `DescribeLiveRegionData` API to get the identifiers of the regions covered by MediaLive. Once you have the region identifiers, you can use them in APIs that support querying data by region to retrieve data for specific areas. |
|[DescribeLiveSourceTrafficData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesourcetrafficdata) |Call the `DescribeLiveSourceTrafficData` API to query the monitoring data of origin traffic and bandwidth generated by specified pull streaming domains or origin streams within the specified time range. |
|[DescribeLiveStreamCountData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreamcountdata) |Gets the peak count of specific pushed streams, origin\-pull streams, or transcoded streams within a specific time range. |
|[DescribeLivePushStreamMetrics](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepushstreammetrics) |Call the `DescribeLivePushStreamMetrics` API to query the monitoring data, such as audio\-video frame rate and bitrate, of a single pushed stream within the specified time range, to assess the health of the live stream. |
|[DescribeLivePlayStatusCodeData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveplaystatuscodedata) |Call the `DescribeLivePlayStatusCodeData` API to query the proportion of status codes for requests made to the domain within the specified time range, including push streaming requests, pull streaming requests, and source streaming requests. |
|[DescribeLiveStreamSessionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreamsessiondata) |Call the `DescribeLiveStreamSessionData` API to query the request count and maximum online audience number of all live streams or specified live streams under the specified domain within the specified time range. |
|[DescribeLiveSourceStreamMetrics](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesourcestreammetrics) |Call the `DescribeLiveSourceStreamMetrics` API to query the monitoring data, such as audio\-video frame rate and bitrate, of a single origin stream within the specified time range, to assess the health of the origin stream. |
|[DescribeCDNTrafficData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecdntrafficdata) |Call the `DescribeCDNTrafficData` API to query CDN traffic used when accessing live\-stream recordings and snapshots from within a specified time range. |
|[DescribeLiveBatchPushStreamMetrics](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivebatchpushstreammetrics-2023) |Call the `DescribeLiveBatchPushStreamMetrics` API to query push\-stream statistics for one or more streams under a domain name for push streaming, including frame rates, bitrates, presentation timestamps (PTS), and more. You can use the statistics to monitor the health of a stream\-pushing session. You can query the data for deleted domain names. |
|[DescribeLiveTranscodeInfoData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivetranscodeinfodata-2023) |Call the `DescribeLiveTranscodeInfoData` API to query detailed data, such as the transcode task ID, stream name, transcode suffix, and the start and end times of transcode for a specific live domain or live stream within a specified time range. |
|[DescribeLiveTopPlayData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivetopplaydata-2023) |Call the `DescribeLiveTopPlayData` API to query traffic and bandwidth details for the top live streams or top domains within a specified time range. |
|[DescribeLiveBatchStreamTrafficData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivebatchstreamtrafficdata-2023) |Call the `DescribeLiveBatchStreamTrafficData` API to query the upstream and downstream traffic data and its detailed data within the specified time range. |
|[DescribeLiveBatchStreamTranscodeData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivebatchstreamtranscodedata-2023) |Call the `DescribeLiveBatchStreamTranscodeData` API to query the transcoding data of all streams under a specified domain within a given time range. The data includes metrics such as transcoding duration, resolution level, and encoding method. |
|[DescribeLiveEdgeStatData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeliveedgestatdata-2023) |Call the `DescribeLiveEdgeStatData` interface to query data such as upstream and downstream traffic, upstream and downstream peak bandwidth, and the number of requests generated by live streams under the specified protocol, ISP, region, and time range. |
|[DescribeLiveBatchSourceStreamMetrics](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivebatchsourcestreammetrics) |Gets the monitoring data, such as frame rate and bitrate of audios and videos, for all or specific origin\-pull streams under specific domain name for stream pulling within specific time range. You can use the monitoring data to assess the health of origin\-pull streams.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can get historical origin\-pull stream data generated by deleted domains.</div><br> |


<span id="callback"></span>
## Callback


|API |Description |
|---|---|
|[UpdateCallback](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatecallback-2023) |Call the `UpdateCallback` API to add or update callback configurations for stream pushing, recording, and screenshot capturing events. |
|[DescribeCallback](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecallback-2023) |Call the `DescribeCallback` API to retrieve callback configurations for your applications. |
|[DeleteCallback](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletecallback-2023) |Call the `DeleteCallback` API to delete callback configurations. |
|[DescribeLiveCallbackData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivecallbackdata) |This API allows you to query callback records related to live streaming, including event types, statuses, request and response data. It helps you troubleshoot callback exceptions and verify whether callbacks were successfully delivered. |


<span id="storage-space"></span>
## Storage space


|API |Description |
|---|---|
|[ListStorageSpace](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-liststoragespace) |Call the `ListStorageSpace` API to query a list of all available storage spaces under an account. You can refer to the list when configuring recording and screenshot settings. |
|[ListStorageSpaceDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-liststoragespacedetail) |Call the `ListStorageSpaceDetail` API to query the details of the specified storage spaces under an account. |


&nbsp;
