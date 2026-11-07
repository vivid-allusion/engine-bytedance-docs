---
title: "BytePlus VOD API list"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-api-list"
---

This page lists all API operations available for use in BytePlus VOD.

## Spaces

|**API** |**Description** |
|---|---|
|[CreateSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-createspace) |Creates a space. |
|[ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) |Lists the information of all spaces under the current account. |
|[GetSpaceDetail](https://docs.byteplus.com/docs/byteplus-vod/reference-getspacedetail) |Gets the information of a specific space. |
|[UpdateSpaceUploadConfig](https://docs.byteplus.com/docs/byteplus-vod/reference-updatespaceuploadconfig) |Updates the upload configurations of a specific space. |

## Media upload

|**API** |**Description** |
|---|---|
|[ApplyUploadInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-applyuploadinfo) |Requests the upload address and credentials for an audio or video file. |
|[CommitUploadInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-commituploadinfo) |Confirms an upload and retrieves information about the uploaded files. |
|[UploadMediaByUrl](https://docs.byteplus.com/docs/byteplus-vod/reference-uploadmediabyurl) |Batch uploads media files using URLs. |
|[QueryUploadTaskInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-queryuploadtaskinfo) |Gets the status of the batch upload task. |

## Media assets

|**API** |**Description** |
|---|---|
|[GetMediaInfos](https://docs.byteplus.com/docs/byteplus-vod/reference-getmediainfos) |Gets the information of an audio or video file by specifying its unique video ID. |
|[UpdateMediaInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-updatemediainfo) |Updates the information of an audio or video file. |
|[UpdateMediaPublishStatus](https://docs.byteplus.com/docs/byteplus-vod/reference-updatemediapublishstatus) |Publishes or unpublishes an audio or video file. |
|[DeleteMedia](https://docs.byteplus.com/docs/byteplus-vod/reference-deletemedia) |Deletes an audio or video file from BytePlus VOD service by specifying its unique video ID. |
|[DeleteTranscodes](https://docs.byteplus.com/docs/byteplus-vod/reference-deletetranscodes) |Deletes all transcoded files of an audio or video file from BytePlus VOD by specifying its video ID. |
|[GetMediaList](https://docs.byteplus.com/docs/byteplus-vod/reference-getmedialist) |Gets the information of audio and video files in a specific space. |
|[GetSubtitleInfoList](https://docs.byteplus.com/docs/byteplus-vod/reference-getsubtitleinfolist) |Gets the subtitles by specifying the video ID, file ID, language, label, or status. |
|[UpdateSubtitleStatus](https://docs.byteplus.com/docs/byteplus-vod/reference-updatesubtitlestatus) |Publishes or unpublishes the subtitle files of a specific video. |
|[UpdateSubtitleInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-updatesubtitleinfo) |Updates the information of the subtitle files. |
|[ListSnapshots](https://docs.byteplus.com/docs/byteplus-vod/reference-listsnapshots) |Gets the screenshots of a specific video file. |
|[CreateVideoClassification](https://docs.byteplus.com/docs/byteplus-vod/reference-createvideoclassification) |Creates a category for managing the uploaded audio and video files. |
|[ListVideoClassifications](https://docs.byteplus.com/docs/byteplus-vod/reference-listvideoclassifications) |Gets the categories in a specific space. |
|[UpdateVideoClassification](https://docs.byteplus.com/docs/byteplus-vod/reference-updatevideoclassification) |Updates the name of a specific category. |
|[DeleteVideoClassification](https://docs.byteplus.com/docs/byteplus-vod/reference-deletevideoclassification) |Deletes a category. |
|[CreatePlaylist](https://docs.byteplus.com/docs/byteplus-vod/reference-createplaylist) |Creates a playlist. |
|[GetPlaylists](https://docs.byteplus.com/docs/byteplus-vod/reference-getplaylists) |Gets playlists. |
|[UpdatePlaylist](https://docs.byteplus.com/docs/byteplus-vod/reference-updateplaylist) |Updates a playlist. |
|[DeletePlaylist](https://docs.byteplus.com/docs/byteplus-vod/reference-deleteplaylist) |Deletes a playlist. |

## Image assets and processing

|**API** |**Description** |
|---|---|
|[GetImageList](https://docs.byteplus.com/docs/byteplus-vod/reference-getimagelist) |Lists image assets in a space. |
|[GetImageInfos](https://docs.byteplus.com/docs/byteplus-vod/reference-getimageinfos) |Gets original and processed image details. |
|[UpdateImageInfos](https://docs.byteplus.com/docs/byteplus-vod/reference-updateimageinfos) |Updates image titles, descriptions, tags, and categories. |
|[DeleteImages](https://docs.byteplus.com/docs/byteplus-vod/reference-deleteimages) |Deletes image assets and their processed files. |
|[DeleteImageProcessResults](https://docs.byteplus.com/docs/byteplus-vod/reference-deleteimageprocessresults) |Deletes specified processed image files. |
|[ImageAIProcess](https://docs.byteplus.com/docs/byteplus-vod/reference-imageaiprocess) |Submits an AI image enhancement task. |
|[ImageProcess](https://docs.byteplus.com/docs/byteplus-vod/reference-imageprocess) |Submits a basic image processing task. |
|[GetImageProcessTasks](https://docs.byteplus.com/docs/byteplus-vod/reference-getimageprocesstasks) |Lists image processing tasks and their status. |
|[ListFileMetaInfosByFileNames](https://docs.byteplus.com/docs/byteplus-vod/listfilemetainfosbyfilenames) |Looks up image metadata and Pid by file path. |

## Video editing

|**API** |**Description** |
|---|---|
|[SubmitDirectEditTaskAsync](https://docs.byteplus.com/docs/byteplus-vod/reference-submitdirectedittaskasync) |Submits a direct video editing task. |
|[SubmitDirectEditTaskSync](https://docs.byteplus.com/docs/byteplus-vod/reference-submitdirectedittasksync) |Synchronously submits a direct video editing task. |
|[CancelDirectEditTask](https://docs.byteplus.com/docs/byteplus-vod/reference-canceldirectedittask) |Cancels a direct video editing task. |
|[GetDirectEditResult](https://docs.byteplus.com/docs/byteplus-vod/reference-getdirecteditresult) |Gets the result of a direct video editing task. |
|[GetDirectEditProgress](https://docs.byteplus.com/docs/byteplus-vod/reference-getdirecteditprogress) |Gets the progress of a direct video editing task. |
|[SubmitEditTaskAsync](https://docs.byteplus.com/docs/byteplus-vod/reference-submitedittaskasync) |Submits a video editing task for an existing cloud editing project. |
|[GetTaskList](https://docs.byteplus.com/docs/byteplus-vod/reference-gettasklist) |Gets video editing task records. |
|[DeleteTask](https://docs.byteplus.com/docs/byteplus-vod/reference-deletetask) |Deletes a video editing task record. |
|[CreateProject](https://docs.byteplus.com/docs/byteplus-vod/reference-createproject) |Creates a cloud video editing project. |
|[SearchGlobalProject](https://docs.byteplus.com/docs/byteplus-vod/reference-searchglobalproject) |Searches editing projects in a VOD space. |
|[DeleteProject](https://docs.byteplus.com/docs/byteplus-vod/reference-deleteproject) |Deletes one or more editing projects. |
|[UpdateProject](https://docs.byteplus.com/docs/byteplus-vod/reference-updateproject) |Updates a cloud video editing project and its latest editing configuration. |
|[DescribeProject](https://docs.byteplus.com/docs/byteplus-vod/reference-describeproject) |Gets the details of one or more cloud video editing projects. |
|[CreateEditMaterial](https://docs.byteplus.com/docs/byteplus-vod/reference-createeditmaterial) |Adds a media asset to a cloud video editing project. |
|[DeleteEditMaterial](https://docs.byteplus.com/docs/byteplus-vod/reference-deleteeditmaterial) |Removes a material from a cloud video editing project. |
|[SearchEditMaterial](https://docs.byteplus.com/docs/byteplus-vod/reference-searcheditmaterial) |Gets materials associated with a cloud video editing project. |
|[GetURLsByStoreURIs](https://docs.byteplus.com/docs/byteplus-vod/reference-geturlsbystoreuris) |Gets accessible URLs for image storage URIs. |
|[GetEffectList](https://docs.byteplus.com/docs/byteplus-vod/reference-geteffectlist) |Gets effect resources used by the video editor. |
|[SearchVideo](https://docs.byteplus.com/docs/byteplus-vod/reference-searchvideo) |Searches audio and video assets for use in the video editor. |
|[GetVideoPlayInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-getvideoplayinfo) |Gets playback and media information used to preview a video. |
|[MGetMaterial](https://docs.byteplus.com/docs/byteplus-vod/reference-mgetmaterial) |Lists or searches materials for use in the video editor. |

## Media processing

|**API** |**Description** |
|---|---|
|[StartWorkflow](https://docs.byteplus.com/docs/byteplus-vod/reference-startworkflow) |Triggers a workflow for a specific audio or video file. |
|[RetrieveTranscodeResult](https://docs.byteplus.com/docs/byteplus-vod/reference-retrievetranscoderesults) |Retrieves the transcoding results of a specific audio or video file. |
|[GetWorkflowExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-getworkflowexecution) |Gets the execution status of a workflow. |

## Media playback

|**API** |**Description** |
|---|---|
|[GetPlayInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-getplayinfo) |Gets the playback addresses for a specified video ID. |

## Content distribution

|**API** |**Description** |
|---|---|
|[CreateDomain](https://docs.byteplus.com/docs/byteplus-vod/reference-createdomain) |Creates a domain name. |
|[ListDomain](https://docs.byteplus.com/docs/byteplus-vod/reference-listdomain) |Gets the list of domain names of a specific space. |
|[UpdateVodDomainConfig](https://docs.byteplus.com/docs/byteplus-vod/reference-updatevoddomainconfig) |Updates the configuration of a VOD domain name. |
|[CreateCdnRefreshTask](https://docs.byteplus.com/docs/byteplus-vod/reference-createcdnrefreshtask) |Creates a CDN refresh task. |
|[CreateCdnPreloadTask](https://docs.byteplus.com/docs/byteplus-vod/reference-createcdnpreloadtask) |Creates a CDN warm\-up task. |
|[ListCdnTasks](https://docs.byteplus.com/docs/byteplus-vod/reference-listcdntasks) |Gets a list of refresh and warm\-up tasks. |
|[SetMirrorSrcRule](https://docs.byteplus.com/docs/byteplus-vod/reference-setmirrorsrcrule) |Creates or updates the image mirror source rule (mirroring\-based back\-to\-origin rule) for a BytePlus VOD space. |
|[ListMirrorSrcRule](https://docs.byteplus.com/docs/byteplus-vod/reference-listmirrorsrcrule) |Queries the list of image mirror source rules (mirroring\-based back\-to\-origin rules) in a specified VOD space. |
|[DeleteMirrorSrcRule](https://docs.byteplus.com/docs/byteplus-vod/reference-deletemirrorsrcrule) |Deletes the specified image mirror source rule (mirroring\-based back\-to\-origin rule) in a VOD space. |

## Statistics

|**API** |**Description** |
|---|---|
|[DescribeVodDomainBandwidthData](https://docs.byteplus.com/docs/byteplus-vod/reference-describevoddomainbandwidthdata) |Gets the bandwidth usage of a specific domain name within a certain time range. |
|[DescribeVodDomainTrafficData](https://docs.byteplus.com/docs/byteplus-vod/reference-describevoddomaintrafficdata) |Gets the traffic of a specific domain name within a certain time range. |
|[DescribeVodSpaceStorageData](https://docs.byteplus.com/docs/byteplus-vod/reference-describevodspacestoragedata) |Gets the storage usage of a specific space within a certain time range. |
|[DescribeVodSpaceTranscodeData](https://docs.byteplus.com/docs/byteplus-vod/reference-describevodspacetranscodedata) |Gets the transcoding usage of a specific space within a certain time range. |
|[DescribeVodSpaceSubtitleStatisData](https://docs.byteplus.com/docs/byteplus-vod/reference-describevodspacesubtitlestatisdata) |Gets the usage of the smart subtitling feature within a certain time range. |
|[DescribeVodSnapshotData](https://docs.byteplus.com/docs/byteplus-vod/reference-describevodsnapshotdata) |Gets the usage of the snapshot feature of a specific space within a certain time range. |
|[DescribeVodEnhanceImageData](https://docs.byteplus.com/docs/byteplus-vod/reference-describevodenhanceimagedata) |Gets the usage of the video enhancement feature of a specific space within a certain time range. |
|[DescribeVodImageEnhancementData](https://docs.byteplus.com/docs/byteplus-vod/reference-describevodimageenhancementdata) |Queries image enhancement request counts for batch processing. |
|[DescribeVodImageCompressionData](https://docs.byteplus.com/docs/byteplus-vod/reference-describevodimagecompressiondata) |Queries image compression usage for batch or real\-time processing. |
|[DescribeVodRealtimeMediaData](https://docs.byteplus.com/docs/byteplus-vod/DescribeVodRealtimeMediaData) |Gets the access count for real\-time snapshots and audio\-video information retrieval. |
|[ListCdnUsageData](https://docs.byteplus.com/docs/byteplus-vod/reference-listcdnusagedata) |Gets the bandwidth and traffic data based on filters such as domain names. |
|[ListCdnPvData](https://docs.byteplus.com/docs/byteplus-vod/reference-listcdnpvdata) |Gets the number of requests based on filters such as domain names. |
|[ListCdnStatusData](https://docs.byteplus.com/docs/byteplus-vod/reference-listcdnstatusdata) |Gets the count of responses by status code (2xx, 3xx, 4xx, 5xx) from edge and origin servers. |
|[ListCdnTopAccess](https://docs.byteplus.com/docs/byteplus-vod/reference-listcdntopaccess) |Gets hot data and request count for specified domain names within a given time period. |
|[DescribeVodPlayedStatisData](https://docs.byteplus.com/docs/byteplus-vod/reference-describevodplayedstatisdata) |Gets the playback information of videos. |
|[DescribeVodMostPlayedStatisData](https://docs.byteplus.com/docs/byteplus-vod/reference-describevodmostplayedstatisdata) |Gets the information of the most viewed videos and videos with the highest playback traffic. |
|[GetVodMediaPlayData](https://docs.byteplus.com/docs/byteplus-vod/reference-getvodmediaplaydata) |Retrieves video playback QoS and QoE metrics within a specified time range using the application ID. |

## Settings

|**API** |**Description** |
|---|---|
|[SetCallbackEvent](https://docs.byteplus.com/docs/byteplus-vod/reference-setcallbackevent) |Configures callback settings. |
|[AddCallbackSubscription](https://docs.byteplus.com/docs/byteplus-vod/reference-addcallbacksubscription) |Adds a callback subscription. |

## Tools

|**API** |**Description** |
|---|---|
|[ListCdnAccessLog](https://docs.byteplus.com/docs/byteplus-vod/reference-listcdnaccesslog) |Queries and downloads CDN access logs for specified domains. |
|[DescribeIpInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-describeipinfo) |Checks whether one or more specified IP addresses belong to a BytePlus CDN node. |
