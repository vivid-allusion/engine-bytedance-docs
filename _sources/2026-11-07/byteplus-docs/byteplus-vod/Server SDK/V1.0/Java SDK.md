---
title: "Java SDK"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-java-sdk"
---

This article introduces how to install the Java SDK and provides code examples to help you accelerate your development process.

<span id="0069116f"></span>
## Prerequisites


* A BytePlus account or an IAM user. For more information, see [Signing up for a BytePlus account](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account) or [Managing IAM users and roles](https://docs.byteplus.com/byteplus-livesaas/docs/managing-iam-users-and-roles).

* Obtain the AccessKey ID (AK) and Secret Access Key (SK) for authentication.

   * To obtain the AK and SK of a BytePlus account, go to [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) \> User Profile \> **IAM** \> **Key management**.

   * To obtain the AK and SK of an IAM user, complete the following steps:

      1. Go to [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) \> User Profile \> **IAM** \> **Identity management** \> **User**.

      2. Find the user and then click **View details**.

      3. On the **Access key** tab, click **Create new access key**.

* Environmental requirements: JDK 1.8 or later


<span id="8572c1a1"></span>
## Installing the SDK

Add the following dependencies to your project:

```Groovy
<dependency>
    <groupId>com.byteplus</groupId>
    <artifactId>byteplus-sdk-java</artifactId>
    <version>latest</version>
</dependency>
```


<span id="89149adf"></span>
## Setting the AK and SK

To set the AK and SK, you can use either of the following methods:


* Call `vodService.setAccessKey` and `vodService.setSecretKey`.

* Set the environment variables `BYTEPLUS_ACCESSKEY` as `"YOUR_AK"` and `BYTEPLUS_SECRETKEY` as `"YOUR_SK"`.

* Set the AK and SK in the JSON file in `/.byteplus/config`:

   ```JSON
   {
       "ak":"YOUR_AK",
       "sk":"YOUR_SK"
    }
   ```
   


<span id="37eb4f42"></span>
## Setting the service region

To connect to the Asia Pacific Southeast (Johor) region, set the `Region` parameter during instance initialization. See the following code example:

```Java
// For the Asia Pacific Southeast(Johor) region, use SDK version v1.1.45 or later
IVodService vodService = VodServiceImpl.getInstance(com.byteplus.helper.Const.REGION_AP_SOUTHEAST_1);
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The region parameter is optional and defaults to <code>ap-singapore-1</code> (Singapore) if not provided.</div>


<span id="75f8c9a1"></span>
## Code examples

<span id="23e3096a"></span>
### Overview

BytePlus offers [code examples](https://github.com/byteplus-sdk/byteplus-sdk-java/tree/master/example/src/main/java/com/byteplus/example/vod) for the Java SDK on GitHub, which can assist you in accelerating your development process. The table below presents the BytePlus VOD Open APIs along with their respective Java SDK code examples.


|**Feature** |**API** |**Java SDK code example** |
|---|---|---|
|Spaces |[CreateSpace](https://docs.byteplus.com/en/byteplus-vod/reference/createspace) |[VodCreateSpaceDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/space/VodCreateSpaceDemo.java) |
||[ListSpace](https://docs.byteplus.com/en/byteplus-vod/reference/listspace) |[VodListSpaceDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/space/VodListSpaceDemo.java) |
||[GetSpaceDetail](https://docs.byteplus.com/en/byteplus-vod/reference/getspacedetail) |[VodGetSpaceDetailDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/space/VodGetSpaceDetailDemo.java) |
||[UpdateSpaceUploadConfig](https://docs.byteplus.com/en/byteplus-vod/reference/updatespaceuploadconfig) |[VodUpdateSpaceUploadConfigDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/space/VodUpdateSpaceUploadConfigDemo.java) |
|Media upload |[ApplyUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/applyuploadinfo) |[VodApplyUploadInfoDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/upload/VodApplyUploadInfoDemo.java) |
||[CommitUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/commituploadinfo) |[VodCommitUploadInfoDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/upload/VodCommitUploadInfoDemo.java) |
||[QueryUploadTaskInfo](https://docs.byteplus.com/en/byteplus-vod/reference/queryuploadtaskinfo) |[VodQueryUploadTaskInfoDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/upload/VodQueryUploadTaskInfoDemo.java) |
||[UploadMediaByUrl](https://docs.byteplus.com/en/byteplus-vod/reference/uploadmediabyurl) |[VodUploadMediaByUrlDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/upload/VodUploadMediaByUrlDemo.java) |
|Media assets |[GetMediaInfos](https://docs.byteplus.com/en/byteplus-vod/reference/getmediainfos) |[VodGetMediaInfosDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/media/VodGetMediaInfosDemo.java) |
||[UpdateMediaInfo](https://docs.byteplus.com/en/byteplus-vod/reference/updatemediainfo) |[VodUpdateMediaInfoDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/media/VodUpdateMediaInfoDemo.java) |
||[UpdateMediaPublishStatus](https://docs.byteplus.com/en/byteplus-vod/reference/updatemediapublishstatus) |[VodUpdateMediaPublishStatusDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/media/VodUpdateMediaPublishStatusDemo.java) |
||[DeleteMedia](https://docs.byteplus.com/en/byteplus-vod/reference/deletemedia) |[VodDeleteMediaDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/media/VodDeleteMediaDemo.java) |
||[DeleteTranscodes](https://docs.byteplus.com/en/byteplus-vod/reference/deletetranscodes) |[VodDeleteTranscodesDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/media/VodDeleteTranscodesDemo.java) |
||[GetMediaList](https://docs.byteplus.com/en/byteplus-vod/reference/getmedialist) |[VodGetMediaListDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/media/VodGetMediaListDemo.java) |
||[GetSubtitleInfoList](https://docs.byteplus.com/en/byteplus-vod/reference/getsubtitleinfolist) |[VodGetSubtitleInfoListDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/media/VodGetSubtitleInfoListDemo.java) |
||[UpdateSubtitleStatus](https://docs.byteplus.com/en/byteplus-vod/reference/updatesubtitlestatus) |[VodUpdateSubtitleStatusDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/media/VodUpdateSubtitleStatusDemo.java) |
||[UpdateSubtitleInfo](https://docs.byteplus.com/en/byteplus-vod/reference/updatesubtitleinfo) |[VodUpdateSubtitleInfoDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/media/VodUpdateSubtitleInfoDemo.java) |
||[ListSnapshots](https://docs.byteplus.com/en/byteplus-vod/reference/listsnapshots) |[VodListSnapshotsDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/media/VodListSnapshotsDemo.java) |
||[CreateVideoClassification](https://docs.byteplus.com/en/byteplus-vod/reference/createvideoclassification) |[VodCreateVideoClassificationDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/media/VodCreateVideoClassificationDemo.java) |
||[ListVideoClassifications](https://docs.byteplus.com/en/byteplus-vod/reference/listvideoclassifications) |[VodListVideoClassificationsDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/media/VodListVideoClassificationsDemo.java) |
||[UpdateVideoClassification](https://docs.byteplus.com/en/byteplus-vod/reference/updatevideoclassification) |[VodUpdateVideoClassificationDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/media/VodUpdateVideoClassificationDemo.java) |
||[DeleteVideoClassification](https://docs.byteplus.com/en/byteplus-vod/reference/deletevideoclassification) |[VodDeleteVideoClassificationDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/media/VodDeleteVideoClassificationDemo.java) |
||[CreatePlaylist](https://docs.byteplus.com/docs/byteplus-vod/reference-createplaylist) |[VodCreatePlaylistDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/media/VodCreatePlaylistDemo.java) |
||[GetPlaylists](https://docs.byteplus.com/docs/byteplus-vod/reference-getplaylists) |[VodGetPlaylistsDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/media/VodGetPlaylistsDemo.java) |
||[UpdatePlaylist](https://docs.byteplus.com/docs/byteplus-vod/reference-updateplaylist) |[VodUpdatePlaylistDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/media/VodUpdatePlaylistDemo.java) |
||[DeletePlaylist](https://docs.byteplus.com/docs/byteplus-vod/reference-deleteplaylist) |[VodDeletePlaylistDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/media/VodDeletePlaylistDemo.java) |
|Media processing |[StartWorkflow](https://docs.byteplus.com/en/byteplus-vod/reference/startworkflow) |[VodStartWorkflowDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/workflow/VodStartWorkflowDemo.java) |
||[RetrieveTranscodeResult](https://docs.byteplus.com/en/byteplus-vod/reference/retrievetranscoderesults) |[VodRetrieveTranscodeResultDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/workflow/VodRetrieveTranscodeResultDemo.java) |
||[GetWorkflowExecution](https://docs.byteplus.com/en/byteplus-vod/reference/getworkflowexecution) |[VodGetWorkflowExecutionDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/workflow/VodGetWorkflowExecutionDemo.java) |
|Video playback |[GetPlayInfo](https://docs.byteplus.com/en/byteplus-vod/reference/getplayinfo) |[VodGetPlayInfoDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/play/VodGetPlayInfoDemo.java) |
|Content distribution |[CreateDomain](https://docs.byteplus.com/en/byteplus-vod/reference/createdomain) |[VodCreateDomainDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/cdn/VodCreateDomainDemo.java) |
||[ListDomain](https://docs.byteplus.com/en/byteplus-vod/reference/listdomain) |[VodListDomainDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/cdn/VodListDomainDemo.java) |
||[CreateCdnRefreshTask](https://docs.byteplus.com/en/byteplus-vod/reference/createcdnrefreshtask) |[VodCreateDomainDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/cdn/VodCreateDomainDemo.java) |
||[CreateCdnPreloadTask](https://docs.byteplus.com/en/byteplus-vod/reference/createcdnpreloadtask) |[VodDescribeIpInfoDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/cdn/VodDescribeIpInfoDemo.java) |
||[ListCdnTasks](https://docs.byteplus.com/en/byteplus-vod/reference/listcdntasks) |[VodListCdnTasksDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/cdn/VodListCdnTasksDemo.java) |
|Statistics |[DescribeVodDomainBandwidthData](https://docs.byteplus.com/en/byteplus-vod/reference/describevoddomainbandwidthdata) |[VodDescribeVodDomainBandwidthDataDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/cdn/VodDescribeVodDomainBandwidthDataDemo.java) |
||[DescribeVodDomainTrafficData](https://docs.byteplus.com/en/byteplus-vod/reference/describevoddomaintrafficdata) |[VodDescribeVodDomainTrafficDataDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/cdn/VodDescribeVodDomainTrafficDataDemo.java) |
||[DescribeVodSpaceStorageData](https://docs.byteplus.com/en/byteplus-vod/reference/describevodspacestoragedata) |[VodDescribeVodSpaceStorageDataDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/space/VodDescribeVodSpaceStorageDataDemo.java) |
||[DescribeVodSpaceTranscodeData](https://docs.byteplus.com/en/byteplus-vod/reference/describevodspacetranscodedata) |[VodDescribeVodSpaceTranscodeDataDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/measure/VodDescribeVodSpaceTranscodeDataDemo.java) |
||[DescribeVodSpaceSubtitleStatisData](https://docs.byteplus.com/en/docs/byteplus-vod/reference-describevodspacesubtitlestatisdata) |[VodDescribeVodSpaceSubtitleStatisDataDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/measure/VodDescribeVodSpaceSubtitleStatisDataDemo.java) |
||[DescribeVodSnapshotData](https://docs.byteplus.com/en/docs/byteplus-vod/reference-describevodsnapshotdata) |[VodDescribeVodSnapshotDataDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/measure/VodDescribeVodSnapshotDataDemo.java) |
||[DescribeVodEnhanceImageData](https://docs.byteplus.com/en/docs/byteplus-vod/reference-describevodenhanceimagedata) |[VodDescribeVodEnhanceImageDataDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/measure/VodDescribeVodEnhanceImageDataDemo.java) |
||[DescribeVodRealtimeMediaData](https://docs.byteplus.com/en/docs/byteplus-vod/DescribeVodRealtimeMediaData) |[VodDescribeVodRealtimeMediaDataDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/measure/VodDescribeVodRealtimeMediaDataDemo.java) |
||[ListCdnUsageData](https://docs.byteplus.com/en/byteplus-vod/reference/listcdnusagedata) |[VodListCdnUsageDataDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/cdn/VodListCdnUsageDataDemo.java) |
||[ListCdnPvData](https://docs.byteplus.com/en/byteplus-vod/reference/listcdnpvdata) |[VodListCdnPvDataDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/cdn/VodListCdnPvDataDemo.java) |
||[ListCdnStatusData](https://docs.byteplus.com/en/byteplus-vod/reference/listcdnstatusdata) |[VodListCdnStatusDataDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/cdn/VodListCdnStatusDataDemo.java) |
||[ListCdnHitrateData](https://docs.byteplus.com/docs/byteplus-vod/reference-listcdnhitratedata) |None |
||[ListCdnTopAccessUrl](https://docs.byteplus.com/en/byteplus-vod/reference/listcdntopaccessurl) |[VodListCdnTopAccessUrlDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/cdn/VodListCdnTopAccessUrlDemo.java) |
||[DescribeVodPlayedStatisData](https://docs.byteplus.com/en/byteplus-vod/reference/describevodplayedstatisdata) |[VodDescribeVodPlayedStatisDataDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/measure/VodDescribeVodPlayedStatisDataDemo.java) |
||[DescribeVodMostPlayedStatisData](https://docs.byteplus.com/en/byteplus-vod/reference/describevodmostplayedstatisdata) |[VodDescribeVodMostPlayedStatisDataDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/measure/VodDescribeVodMostPlayedStatisDataDemo.java) |
|Settings |[SetCallbackEvent](https://docs.byteplus.com/en/byteplus-vod/reference/setcallbackevent) |[VodSetCallbackEventDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/callback/VodSetCallbackEventDemo.java) |
||[AddCallbackSubscription](https://docs.byteplus.com/en/byteplus-vod/reference/addcallbacksubscription) |[VodAddCallbackSubscriptionDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/callback/VodAddCallbackSubscriptionDemo.java) |
|Tools |[ListCdnAccessLog](https://docs.byteplus.com/docs/byteplus-vod/reference-listcdnaccesslog) |[VodListCdnAccessLogDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/cdn/VodListCdnAccessLogDemo.java) |
||[DescribeIpInfo](https://docs.byteplus.com/en/docs/byteplus-vod/reference-describeipinfo) |[VodDescribeIpInfoDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/cdn/VodDescribeIpInfoDemo.java) |


<span id="643963c5"></span>
### Uploading audio and video files

Read [media asset upload overview](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload-overview) to learn about the types of media assets and supported formats. For detailed information on the request parameters and response parameters, please refer to [ApplyUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/applyuploadinfo) and [CommitUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/commituploadinfo).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The media asset upload is an asynchronous task, meaning that the successful submission of a task does not necessarily indicate the successful execution of the task.</div>


* <div data-tips="true" data-tips-type="tip">You must include the file extension. For example, if you want to upload an MP4 file, include <code>.mp4</code> or <code>.MP4</code>.</div>



```Java
package com.byteplus.service.vod.impl;

import com.alibaba.fastjson.JSON;
import com.byteplus.helper.VodUploadMediaProcessListener;
import com.byteplus.helper.VodUploadProgressListener;
import com.byteplus.model.beans.Functions;
import com.byteplus.service.vod.IVodService;
import com.byteplus.service.vod.model.request.VodUploadMediaRequest;
import com.byteplus.service.vod.model.response.VodCommitUploadInfoResponse;

import java.util.ArrayList;
import java.util.List;

public class VodUploadMediaDemo {

    public static void main(String[] args) {
        IVodService vodService = VodServiceImpl.getInstance();

        // call below method if you dont set ak and sk in ~/.vcloud/config
        vodService.setAccessKey("your ak");
        vodService.setSecretKey("your sk");

        String space = "your space name";
        String filePath = "your file path";

        List<Functions> functionsList = new ArrayList<>();
        Functions getMetaFunc = Functions.GetMetaFunction();
        functionsList.add(getMetaFunc);

        Functions snapShotFunc = Functions.SnapShotFunction(2.3);
        functionsList.add(snapShotFunc);

        Functions addOptionInfo = Functions.AddOptionInfoFunction("hl", "test", "test1, test2", 0, true);
        functionsList.add(addOptionInfo);

        VodUploadMediaRequest vodUploadMediaRequest = VodUploadMediaRequest.newBuilder()
                .setSpaceName(space)
                .setFilePath(filePath)
                .setFileName("hello/vod/video.mp4")
                .setFunctions(JSON.toJSONString(functionsList))
                .setStorageClass(0)
                .build();
        // When progress bar functionality is needed, add the corresponding listener; if not required, pass a null value.
        VodUploadProgressListener listener = new VodUploadMediaProcessListener();

        try {
            VodCommitUploadInfoResponse vodCommitUploadInfoResponse = vodService.uploadMedia(vodUploadMediaRequest, listener);
            if (vodCommitUploadInfoResponse.getResponseMetadata().hasError()) {
                System.out.println(vodCommitUploadInfoResponse.getResponseMetadata().getError());
                System.exit(-1);
            }
            System.out.println(vodCommitUploadInfoResponse.toString());
            System.out.println(vodCommitUploadInfoResponse.getResult().getData().getVid());
            System.out.println(vodCommitUploadInfoResponse.getResponseMetadata().getRequestId());
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

}
```


<span id="a3bfabe8"></span>
### Uploading materials

Read [media asset upload overview](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload-overview) to learn about the types of media assets and supported formats. For detailed information on the request parameters and response parameters, please refer to [ApplyUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/applyuploadinfo) and [CommitUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/commituploadinfo).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The media asset upload is an asynchronous task, meaning that the successful submission of a task does not necessarily indicate the successful execution of the task.</div>


* <div data-tips="true" data-tips-type="tip">You must include the file extension. For example, if you want to upload an MP4 file, include <code>.mp4</code> or <code>.MP4</code>.</div>



```Java
package com.byteplus.service.vod.impl;

import com.alibaba.fastjson.JSON;
import com.byteplus.service.vod.Const;
import com.byteplus.model.beans.Functions;
import com.byteplus.service.vod.IVodService;
import com.byteplus.service.vod.impl.VodServiceImpl;
import com.byteplus.service.vod.model.request.VodUploadMaterialRequest;
import com.byteplus.service.vod.model.response.VodCommitUploadInfoResponse;

import java.util.ArrayList;
import java.util.List;

public class VodUploadMaterialDemo {

    public static void main(String[] args) {
        IVodService vodService = VodServiceImpl.getInstance();

        // call below method if you dont set ak and sk in ~/.vcloud/config
        vodService.setAccessKey("your ak");
        vodService.setSecretKey("your sk");

        String space = "your space name";
        String filePath = "your file path";

        List<Functions> functionsList = new ArrayList<>();
        Functions getMetaFunc = Functions.GetMetaFunction();
        functionsList.add(getMetaFunc);

        Functions snapShotFunc = Functions.SnapShotFunction(2.3);
        functionsList.add(snapShotFunc);

        Functions addOptionInfo = Functions.AddOptionInfoFunction("test-video", "test", "test1, test2", Const.CategoryVideo, "mp4");
        functionsList.add(addOptionInfo);

        VodUploadMaterialRequest vodUploadMaterialRequest = VodUploadMaterialRequest.newBuilder()
                .setSpaceName(space)
                .setFilePath(filePath)
                .setFileType(Const.FileTypeMedia)
                .setFunctions(JSON.toJSONString(functionsList))
                .build();

        try {
            VodCommitUploadInfoResponse vodCommitUploadInfoResponse = vodService.uploadMaterial(vodUploadMaterialRequest, null);
            if (vodCommitUploadInfoResponse.getResponseMetadata().hasError()) {
                System.out.println(vodCommitUploadInfoResponse.getResponseMetadata().getError());
                System.exit(-1);
            }
            System.out.println(vodCommitUploadInfoResponse.toString());
            System.out.println(vodCommitUploadInfoResponse.getResult().getData().getMid());
            System.out.println(vodCommitUploadInfoResponse.getResponseMetadata().getRequestId());
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

////  Upload image files
//    public static void main(String[] args) {
//        IVodService vodService = VodServiceImpl.getInstance();
//
//        // call below method if you dont set ak and sk in ~/.vcloud/config
//        vodService.setAccessKey("your ak");
//        vodService.setSecretKey("your sk");
//
//        String space = "your space name";
//        String filePath = "your file path";
//
//        List<Functions> functionsList = new ArrayList<>();
//        Functions getMetaFunc = Functions.GetMetaFunction();
//        functionsList.add(getMetaFunc);
//
//        Functions snapShotFunc = Functions.SnapShotFunction(2.3);
//        functionsList.add(snapShotFunc);
//
//        Functions addOptionInfo = Functions.AddOptionInfoFunction("test-image", "test", "test1, test2", Const.CategoryImage, "jpg");
//        functionsList.add(addOptionInfo);
//
//        VodUploadMaterialRequest vodUploadMaterialRequest = VodUploadMaterialRequest.newBuilder()
//                .setSpaceName(space)
//                .setFilePath(filePath)
//                .setFileType(Const.FileTypeImage)
//                .setFileName("hello/vod/image.jpg")
//                .setFunctions(JSON.toJSONString(functionsList))
//                .build();
//
//        try {
//            VodCommitUploadInfoResponse vodCommitUploadInfoResponse = vodService.uploadMaterial(vodUploadMaterialRequest,null);
//            if (vodCommitUploadInfoResponse.getResponseMetadata().hasError()) {
//                System.out.println(vodCommitUploadInfoResponse.getResponseMetadata().getError());
//                System.exit(-1);
//            }
//            System.out.println(vodCommitUploadInfoResponse.toString());
//            System.out.println(vodCommitUploadInfoResponse.getResult().getData().getMid());
//            System.out.println(vodCommitUploadInfoResponse.getResponseMetadata().getRequestId());
//        } catch (Exception e) {
//            e.printStackTrace();
//        }
//    }

////    Upload subtitle files
//    public static void main(String[] args) {
//        IVodService vodService = VodServiceImpl.getInstance();
//
//        // call below method if you dont set ak and sk in ~/.vcloud/config
//        vodService.setAccessKey("your ak");
//        vodService.setSecretKey("your sk");
//
//        String space = "your space name";
//        String filePath = "your file path";
//
//        List<Functions> functionsList = new ArrayList<>();
//        Functions getMetaFunc = Functions.GetMetaFunction();
//        functionsList.add(getMetaFunc);
//
//        Functions snapShotFunc = Functions.SnapShotFunction(2.3);
//        functionsList.add(snapShotFunc);
//
//        Functions addOptionInfo = Functions.AddOptionInfoFunction("test-subtitle", "test", "test1, test2", Const.CategorySubtitle, "vtt");
//        functionsList.add(addOptionInfo);
//
//        VodUploadMaterialRequest vodUploadMaterialRequest = VodUploadMaterialRequest.newBuilder()
//                .setSpaceName(space)
//                .setFilePath(filePath)
//                .setFileType(Const.FileTypeObject)
//                .setFileName("hello/vod/object.vtt")
//                .setFunctions(JSON.toJSONString(functionsList))
//                .build();
//
//        try {
//            VodCommitUploadInfoResponse vodCommitUploadInfoResponse = vodService.uploadMaterial(vodUploadMaterialRequest,null);
//            if (vodCommitUploadInfoResponse.getResponseMetadata().hasError()) {
//                System.out.println(vodCommitUploadInfoResponse.getResponseMetadata().getError());
//                System.exit(-1);
//            }
//            System.out.println(vodCommitUploadInfoResponse.toString());
//            System.out.println(vodCommitUploadInfoResponse.getResult().getData().getMid());
//            System.out.println(vodCommitUploadInfoResponse.getResponseMetadata().getRequestId());
//        } catch (Exception e) {
//            e.printStackTrace();
//        }
//    }

}
```


<span id="c257d0b8"></span>
### Generating temporary upload token

You can generate a temporary upload token on the application server using AK and SK without needing the external network. If you need to generate multiple temporary upload tokens at the same time, call the generation method repeatedly. For how to use the temporary upload token, see [Client-side uploads](https://docs.byteplus.com/docs/byteplus-vod/docs-client-side-uploads).

```Java
package com.byteplus.service.vod.impl;

import com.alibaba.fastjson.JSON;
import com.byteplus.model.sts2.SecurityToken2;
import com.byteplus.service.vod.IVodService;
import com.byteplus.service.vod.impl.VodServiceImpl;
import com.byteplus.util.Time;

public class GetUploadSts2Demo {

    public static void main(String[] args) throws Exception {
        IVodService vodService = VodServiceImpl.getInstance();

        // call below method if you don't set ak and sk in ~/.vcloud/config
        vodService.setAccessKey("your ak");
        vodService.setSecretKey("your sk");

        SecurityToken2 sts2WithExpire = vodService.getUploadSts2WithExpire(Time.Hour);
        System.out.println(JSON.toJSONString(sts2WithExpire));

        SecurityToken2 sts2 = vodService.getUploadSts2WithExpire(Time.Hour);
        System.out.println(JSON.toJSONString(sts2));

    }
}
```


<span id="f3108712"></span>
### Generating temporary playback token

You can generate a temporary playback token on the application server using AK and SK without needing the external network. If you need to generate multiple temporary playback tokens at the same time, call the generation method repeatedly.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To learn how to use the temporary playback token, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-playing-videos-with-temporary-playback-tokens">Playing videos with temporary playback tokens</a>.</div>


* <div data-tips="true" data-tips-type="tip">For detailed information on the parameters, please refer to <a href="https://docs.byteplus.com/en/docs/byteplus-vod/reference-getplayinfo">GetPlayInfo</a>.</div>



```Java
package com.byteplus.example.vod.play;

import com.byteplus.service.vod.IVodService;
import com.byteplus.service.vod.impl.VodServiceImpl;
import com.byteplus.service.vod.model.request.VodGetPlayInfoRequest;

public class VodGetPlayAuthTokenDemo {

    public static void main(String[] args) throws Exception {
        IVodService vodService = VodServiceImpl.getInstance();

        String vid = "your vid";

        // call below method if you dont set ak and sk in ~/.byteplus/config
        vodService.setAccessKey("your ak");
        vodService.setSecretKey("your sk");

        try {
            VodGetPlayInfoRequest.Builder reqBuilder = VodGetPlayInfoRequest.newBuilder();
            reqBuilder.setVid(vid);

            String resp = vodService.getPlayAuthToken(reqBuilder.build(), 3600000L);
            System.out.println(resp);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```


<span id="0114c224"></span>
### Generating private encryption token

For how to use the playback token for private encryption, see [Private encryption](https://docs.byteplus.com/docs/byteplus-vod/docs-private-encryption).

```Java
package com.byteplus.example.vod.play;

import com.byteplus.service.vod.IVodService;
import com.byteplus.service.vod.impl.VodServiceImpl;
import com.byteplus.service.vod.model.request.VodGetPrivateDrmPlayAuthRequest;

public class VodGetPrivateDrmAuthTokenDemo {
    public static void main(String[] args) throws Exception {
        IVodService vodService = VodServiceImpl.getInstance();
        // call below method if you dont set ak and sk in ～/.vcloud/config
        vodService.setAccessKey("your ak");
        vodService.setSecretKey("your sk");
        String vid = "your vid";
        String unionInfo = "your unionInfo";
        Long expireTime = 3600L; // token expireTime
        try {
            VodGetPrivateDrmPlayAuthRequest.Builder reqBuilder = VodGetPrivateDrmPlayAuthRequest.newBuilder();
            reqBuilder.setVid(vid);
            reqBuilder.setDrmType("your drm type");
            reqBuilder.setPlayAuthIds("your playAuthIds");
            reqBuilder.setUnionInfo(unionInfo);

            String resp = vodService.getPrivateDrmAuthToken(reqBuilder.build(), expireTime);
            System.out.println(resp);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```


<span id="02a7dc7d"></span>
### Generating DRM auth token

```Java
package com.byteplus.example.vod.drm;

import com.byteplus.service.vod.IVodService;
import com.byteplus.service.vod.impl.VodServiceImpl;
import com.byteplus.service.vod.model.request.VodGetDrmLicenseRequest;

public class VodGetThirdPartyDrmAuthTokenDemo {

    public static void main(String[] args) throws Exception {
        IVodService vodService = VodServiceImpl.getInstance();

        String vid = "your vid";
        String thirdPartyDrmType = "your drmType"; // widevine or fairplay

        // call below method if you dont set ak and sk in ~/.byteplus/config
        vodService.setAccessKey("your ak");
        vodService.setSecretKey("your sk");

        try {
            VodGetDrmLicenseRequest.Builder reqBuilder = VodGetDrmLicenseRequest.newBuilder();
            reqBuilder.setVid(vid);
            reqBuilder.setThirdPartyDrmType(thirdPartyDrmType);

            String resp = vodService.getThirdPartyDrmAuthToken(reqBuilder.build(), 3600000L);
            System.out.println(resp);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```


<span id="988ba707"></span>
### Generating HLS decryption token

```Java
package com.byteplus.example.vod.play;

import com.byteplus.service.vod.IVodService;
import com.byteplus.service.vod.impl.VodServiceImpl;

public class VodGetHlsDecryptionAuthTokenDemo {

    public static void main(String[] args) throws Exception {
        IVodService vodService = VodServiceImpl.getInstance();

        // call below method if you dont set ak and sk in ~/.vcloud/config
        vodService.setAccessKey("");
        vodService.setSecretKey("");

        try {
            String resp = vodService.createSha1HlsDrmAuthToken(3600L);
            System.out.println(resp);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```


<span id="1318556a"></span>
### Getting the FairPlay certificate URL

```Java
package com.byteplus.example.vod.drm;

import com.byteplus.service.vod.IVodService;
import com.byteplus.service.vod.impl.VodServiceImpl;

public class VodGetFairPlayCertUrlDemo {

    public static void main(String[] args) throws Exception {
        IVodService vodService = VodServiceImpl.getInstance();

        String certId = "your cert id";

        // call below method if you dont set ak and sk in ~/.byteplus/config
        vodService.setAccessKey("your ak");
        vodService.setSecretKey("your sk");

        try {
            String resp = vodService.getFairPlayCertUrl(certId, 3600000L);
            System.out.println(resp);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
