---
title: "Python SDK"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-python-sdk"
---

To integrate BytePlus Video on Demand (VOD) into your application, this guide provides everything you need to get started with the Python SDK. It walks you through installation, authentication, and configuration, and offers a rich collection of code examples for core functionalities like media uploading, token generation, and data statistics. These resources are designed to help you accelerate your development process.

<span id="7ed1dd07"></span>
## Prerequisites


* A BytePlus account or an IAM user. For more information, see [Signing up for a BytePlus account](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account) or [Managing IAM users and roles](https://docs.byteplus.com/byteplus-livesaas/docs/managing-iam-users-and-roles).

* Obtain the AccessKey ID (AK) and Secret Access Key (SK) for authentication.

   * To obtain the AK and SK of a BytePlus account, go to [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) \> User Profile \> **IAM** \> **Key management**.

   * To obtain the AK and SK of an IAM user, complete the following steps:

      1. Go to [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) \> User Profile \> **IAM** \> **Identity management** \> **User**.

      2. Find the user and then click **View details**.

      3. On the **Access key** tab, click **Create new access key**.

* Environmental requirements:

   * Python 3.0 or a higher version required. If you don't have Python installed, visit python.org to download and install the appropriate version.

   * You also need pip, which is a package manager for Python. If you don't have pip installed, visit the [pip documentation](https://pip.pypa.io/en/stable/getting-started/) for instructions on how to install it.


<span id="e63ee629"></span>
## Installing the SDK

In a terminal, run the following command to install the latest version of the Python SDK:

```Bash
pip3 install --user byteplus-sdk
```


<span id="65b6738a"></span>
## Setting the AK and SK

To set the AK and SK, you can use either of the following methods:


* Set the AK and SK in the JSON file at `~/.byteplus/config`:

   ```JSON
   {
       "ak":"YOUR_AK",
       "sk":"YOUR_SK"
    }
   ```
   

* Set the environment variables `BYTEPLUS_ACCESSKEY` to `"YOUR_AK"` and `BYTEPLUS_SECRETKEY` to `"YOUR_SK"`.

* Call `vod_service.set_ak` and `vod_service.set_sk`.

   ```Python
   # coding:utf-8
   
   from byteplus_sdk.vod.VodService import VodService
   
   if __name__ == '__main__':
       vod_service = VodService(region='cn-north-1')
   
       # Call the following methods if you have not set the AK and SK in ~/.byteplus/config
       vod_service.set_ak('YOUR_AK')
       vod_service.set_sk('YOUR_SK')
       # Then call specific action
   ```
   


<span id="15075adf"></span>
## Setting the service region

To connect to the Asia Pacific Southeast (Johor) region, pass in the region during instance initialization. See the following code example:

```Python
# For the Asia Pacific Southeast (Johor) region, use SDK version v1.0.47 or later
vod_service = VodService('ap-southeast-1')  
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The region parameter is optional and defaults to <code>ap-singapore-1</code> (Singapore) if not provided.</div>


<span id="6e5071d1"></span>
## Code examples

<span id="076a06ea"></span>
### Overview

BytePlus offers [code examples](https://github.com/byteplus-sdk/byteplus-sdk-python/tree/master/byteplus_sdk/example/vod) for the Python SDK on GitHub, which can assist you in accelerating your development process. The table below presents the BytePlus VOD Open APIs along with their respective Python SDK code examples.


|**Feature** |**API** |**Python SDK code example** |
|---|---|---|
|Spaces |[CreateSpace](https://docs.byteplus.com/en/byteplus-vod/reference/createspace) |[CreateSpaceExample.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/space/CreateSpaceExample.py) |
||[ListSpace](https://docs.byteplus.com/en/byteplus-vod/reference/listspace) |[ListSpaceExample.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/space/ListSpaceExample.py) |
||[GetSpaceDetail](https://docs.byteplus.com/en/byteplus-vod/reference/getspacedetail) |[GetSpaceDetailExample.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/space/GetSpaceDetailExample.py) |
||[UpdateSpaceUploadConfig](https://docs.byteplus.com/en/byteplus-vod/reference/updatespaceuploadconfig) |[UpdateSpaceUploadConfigExample.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/space/UpdateSpaceUploadConfigExample.py) |
|Media upload |[ApplyUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/applyuploadinfo) |[ApplyUploadInfoExample.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/upload/ApplyUploadInfoExample.py) |
||[CommitUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/commituploadinfo) |[CommitUploadInfoExample.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/upload/CommitUploadInfoExample.py) |
||[UploadMediaByUrl](https://docs.byteplus.com/en/byteplus-vod/reference/uploadmediabyurl) |[UploadUrl.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/upload/UploadUrl.py) |
||[QueryUploadTaskInfo](https://docs.byteplus.com/en/byteplus-vod/reference/queryuploadtaskinfo) |[QueryUploadTaskInfo.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/upload/QueryUploadTaskInfo.py) |
|Media assets |[GetMediaInfos](https://docs.byteplus.com/en/byteplus-vod/reference/getmediainfos) |* [MediaExample.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/media/MediaExample.py)<br><br>* [SubtitleExample.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/subtitle/SubtitleExample.py) |
||[UpdateMediaInfo](https://docs.byteplus.com/en/byteplus-vod/reference/updatemediainfo) ||
||[UpdateMediaPublishStatus](https://docs.byteplus.com/en/byteplus-vod/reference/updatemediapublishstatus) ||
||[DeleteMedia](https://docs.byteplus.com/en/byteplus-vod/reference/deletemedia) ||
||[DeleteTranscodes](https://docs.byteplus.com/en/byteplus-vod/reference/deletetranscodes) ||
||[GetMediaList](https://docs.byteplus.com/en/byteplus-vod/reference/getmedialist) ||
||[GetSubtitleInfoList](https://docs.byteplus.com/en/byteplus-vod/reference/getsubtitleinfolist) ||
||[UpdateSubtitleStatus](https://docs.byteplus.com/en/byteplus-vod/reference/updatesubtitlestatus) ||
||[UpdateSubtitleInfo](https://docs.byteplus.com/en/byteplus-vod/reference/updatesubtitleinfo) ||
||[ListSnapshots](https://docs.byteplus.com/en/byteplus-vod/reference/listsnapshots) ||
||[CreateVideoClassification](https://docs.byteplus.com/en/byteplus-vod/reference/createvideoclassification) ||
||[ListVideoClassifications](https://docs.byteplus.com/en/byteplus-vod/reference/listvideoclassifications) ||
||[UpdateVideoClassification](https://docs.byteplus.com/en/byteplus-vod/reference/updatevideoclassification) ||
||[DeleteVideoClassification](https://docs.byteplus.com/en/byteplus-vod/reference/deletevideoclassification) ||
||[CreatePlaylist](https://docs.byteplus.com/docs/byteplus-vod/reference-createplaylist) ||
||[GetPlaylists](https://docs.byteplus.com/docs/byteplus-vod/reference-getplaylists) ||
||[UpdatePlaylist](https://docs.byteplus.com/docs/byteplus-vod/reference-updateplaylist) ||
||[DeletePlaylist](https://docs.byteplus.com/docs/byteplus-vod/reference-deleteplaylist) ||
|Media processing |[StartWorkflow](https://docs.byteplus.com/en/byteplus-vod/reference/startworkflow) |[WorkflowExample.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/workflow/WorkflowExample.py) |
||[RetrieveTranscodeResult](https://docs.byteplus.com/en/byteplus-vod/reference/retrievetranscoderesults) |[RetrieveTranscodeResultExample.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/workflow/RetrieveTranscodeResultExample.py) |
||[GetWorkflowExecution](https://docs.byteplus.com/en/byteplus-vod/reference/getworkflowexecution) |[GetWorkflowExecutionExample.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/workflow/GetWorkflowExecutionExample.py) |
|Video playback |[GetPlayInfo](https://docs.byteplus.com/en/byteplus-vod/reference/getplayinfo) |[GetPlayInfoExample.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/play/GetPlayInfoExample.py) |
|Content distribution |[CreateDomain](https://docs.byteplus.com/en/byteplus-vod/reference/createdomain) |None |
||[ListDomain](https://docs.byteplus.com/en/byteplus-vod/reference/listdomain) |[ListDomainExample.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/cdn/ListDomainExample.py) |
||[CreateCdnRefreshTask](https://docs.byteplus.com/en/byteplus-vod/reference/createcdnrefreshtask) |[CreateCdnPreloadTaskExample.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/cdn/CreateCdnPreloadTaskExample.py) |
||[CreateCdnPreloadTask](https://docs.byteplus.com/en/byteplus-vod/reference/createcdnpreloadtask) |[CreateCdnRefreshTaskExample.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/cdn/CreateCdnRefreshTaskExample.py) |
||[ListCdnTasks](https://docs.byteplus.com/en/byteplus-vod/reference/listcdntasks) |[ListCdnTasksExample.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/cdn/ListCdnTasksExample.py) |
|Statistics |[DescribeVodDomainBandwidthData](https://docs.byteplus.com/en/byteplus-vod/reference/describevoddomainbandwidthdata) |[DescribeVodDomainBandwidthDataExample.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/cdn/DescribeVodDomainBandwidthDataExample.py) |
||[DescribeVodDomainTrafficData](https://docs.byteplus.com/en/byteplus-vod/reference/describevoddomaintrafficdata) |[DescribeVodDomainTrafficDataExample.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/cdn/DescribeVodDomainTrafficDataExample.py) |
||[DescribeVodSpaceStorageData](https://docs.byteplus.com/en/byteplus-vod/reference/describevodspacestoragedata) |[DescribeVodSpaceStorageDataExample.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/space/DescribeVodSpaceStorageDataExample.py) |
||[DescribeVodSpaceTranscodeData](https://docs.byteplus.com/en/byteplus-vod/reference/describevodspacetranscodedata) |[DescribeVodSpaceTranscodeData.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/measure/DescribeVodSpaceTranscodeData.py) |
||[DescribeVodSpaceSubtitleStatisData](https://docs.byteplus.com/en/docs/byteplus-vod/reference-describevodspacesubtitlestatisdata) |None |
||[DescribeVodSnapshotData](https://docs.byteplus.com/en/docs/byteplus-vod/reference-describevodsnapshotdata) |[DescribeVodSpaceTranscodeData.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/measure/DescribeVodSpaceTranscodeData.py) |
||[ListCdnUsageData](https://docs.byteplus.com/en/byteplus-vod/reference/listcdnusagedata) |[ListCdnUsageDataExample.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/cdn/ListCdnUsageDataExample.py) |
||[ListCdnPvData](https://docs.byteplus.com/en/byteplus-vod/reference/listcdnpvdata) |[ListCdnPvDataExample.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/cdn/ListCdnPvDataExample.py) |
||[ListCdnStatusData](https://docs.byteplus.com/en/byteplus-vod/reference/listcdnstatusdata) |[ListCdnStatusDataExample.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/cdn/ListCdnStatusDataExample.py) |
||[ListCdnHitrateData](https://docs.byteplus.com/docs/byteplus-vod/reference-listcdnhitratedata) |None |
||[ListCdnTopAccessUrl](https://docs.byteplus.com/en/byteplus-vod/reference/listcdntopaccessurl) |[ListCdnTopAccessUrlExample.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/cdn/ListCdnTopAccessUrlExample.py) |
||[DescribeVodPlayedStatisData](https://docs.byteplus.com/en/byteplus-vod/reference/describevodplayedstatisdata) |None |
||[DescribeVodMostPlayedStatisData](https://docs.byteplus.com/en/byteplus-vod/reference/describevodmostplayedstatisdata) |None |
||[GetVodMediaPlayData](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getvodmediaplaydata) |[GetVodMediaPlayData.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/quality_platform/GetVodMediaPlayData.py) |
|Settings |[SetCallbackEvent](https://docs.byteplus.com/en/byteplus-vod/reference/setcallbackevent) |[SetCallbackEvent.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/callback/SetCallbackEvent.py) |
||[AddCallbackSubscription](https://docs.byteplus.com/en/byteplus-vod/reference/addcallbacksubscription) |[AddCallbackSubscriptionExample.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/callback/AddCallbackSubscriptionExample.py) |
|Tools |[ListCdnAccessLog](https://docs.byteplus.com/docs/byteplus-vod/reference-listcdnaccesslog) |[ListCdnAccessLogExample.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/cdn/ListCdnAccessLogExample.py) |
||[DescribeIpInfo](https://docs.byteplus.com/en/docs/byteplus-vod/reference-describeipinfo) |[DescribeCdnIpExample.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/cdn/DescribeCdnIpExample.py) |


<span id="754aa312"></span>
### Uploading audio and video files

Read [media asset upload overview](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload-overview) to learn about the types of media assets and supported formats. For detailed information on the request parameters and response parameters, please refer to [ApplyUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/applyuploadinfo) and [CommitUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/commituploadinfo).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The media asset upload is an asynchronous task, meaning that the successful submission of a task does not necessarily indicate the successful execution of the task.</div>


* <div data-tips="true" data-tips-type="tip">You must include the file extension. For example, if you want to upload an MP4 file, include <code>.mp4</code> or <code>.MP4</code>.</div>



```Python
# coding:utf-8
from __future__ import print_function

import json

from byteplus_sdk.util.Functions import Function
from byteplus_sdk.vod.VodService import VodService
from byteplus_sdk.vod.models.request.request_vod_pb2 import VodUploadMediaRequest

if __name__ == '__main__':
    vod_service = VodService()

    # Call the following methods if you have not set the AK and SK in ~/.byteplus/config
    vod_service.set_ak('your ak')
    vod_service.set_sk('your sk')

    space_name = 'your space name'
    file_path = 'your file path'

    get_meta_function = Function.get_meta_func()
    snapshot_function = Function.get_snapshot_func(2.3)
    apply_function = Function.get_add_option_info_func("title1", "tag1", "desc1")

    try:
        req = VodUploadMediaRequest()
        req.SpaceName = space_name
        req.FilePath = file_path
        req.Functions = json.dumps([get_meta_function, snapshot_function])
        req.CallbackArgs = ''
        req.FileName = 'hello/vod.mp4'
        req.FileExtension = '.mp4'
        req.StorageClass = 0
        resp = vod_service.upload_media(req)
    except Exception:
        raise
    else:
        print(resp)
        if resp.ResponseMetadata.Error.Code == '':
            print(resp.Result.Data)
            print(resp.Result.Data.Vid)
            print(resp.Result.Data.PosterUri)
            print(resp.Result.Data.SourceInfo.FileName)
            print(resp.Result.Data.SourceInfo.Height)
            print(resp.Result.Data.SourceInfo.Width)
        else:
            print(resp.ResponseMetadata.Error)
            print(resp.ResponseMetadata.RequestId)
```


<span id="e47f1717"></span>
### Uploading materials

Read [media asset upload overview](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload-overview) to learn about the types of media assets and supported formats. For detailed information on the request parameters and response parameters, please refer to [ApplyUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/applyuploadinfo) and [CommitUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/commituploadinfo).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The media asset upload is an asynchronous task, meaning that the successful submission of a task does not necessarily indicate the successful execution of the task.</div>


* <div data-tips="true" data-tips-type="tip">You must include the file extension. For example, if you want to upload an MP4 file, include <code>.mp4</code> or <code>.MP4</code>.</div>



```Python
# coding:utf-8
from __future__ import print_function

import json

from byteplus_sdk.util.Functions import Function
from byteplus_sdk.vod.VodService import VodService
from byteplus_sdk.const.Const import *
from byteplus_sdk.vod.models.request.request_vod_pb2 import VodUploadMaterialRequest

if __name__ == '__main__':
    vod_service = VodService()

    # Call the following methods if you have not set the AK and SK in ~/.byteplus/config
    vod_service.set_ak('your ak')
    vod_service.set_sk('your sk')

    space_name = 'your space name'
    file_path = 'your file path'

    get_meta_function = Function.get_meta_func()
    snapshot_function = Function.get_snapshot_func(2.3)
    add_option_function = Function.get_add_material_option_info_func(title='test video', tags='test',
                                                                     description='Video file',
                                                                     category=CATEGORY_VIDEO, record_type=2,
                                                                     format_input='MP4')

    try:
        req = VodUploadMaterialRequest()
        req.FileType = FILE_TYPE_MEDIA
        req.SpaceName = space_name
        req.FilePath = file_path
        req.Functions = json.dumps([get_meta_function, snapshot_function, add_option_function])
        req.CallbackArgs = ''
        req.FileExtension = '.mp4'

        resp = vod_service.upload_material(req)
    except Exception:
        raise
    else:
        print(resp)
        if resp.ResponseMetadata.Error.Code == '':
            print(resp.Result.Data)
            print(resp.Result.Data.Mid)
            print(resp.Result.Data.PosterUri)
            print(resp.Result.Data.SourceInfo.FileName)
            print(resp.Result.Data.SourceInfo.Height)
            print(resp.Result.Data.SourceInfo.Width)
        else:
            print(resp.ResponseMetadata.Error)
            print(resp.ResponseMetadata.RequestId)

if __name__ == '__main__':
    vod_service = VodService()

    # Call the following methods if you have not set the AK and SK in ~/.byteplus/config
    vod_service.set_ak('your ak')
    vod_service.set_sk('your sk')

    space_name = 'your space name'
    file_path = 'your file path'

    get_meta_function = Function.get_meta_func()
    snapshot_function = Function.get_snapshot_func(0)
    add_option_function = Function.get_add_material_option_info_func(title='test picture', tags='test',
                                                                     description='Picture file',
                                                                     category=CATEGORY_IMAGE, record_type=2,
                                                                     format_input='jpg')

    try:
        req = VodUploadMaterialRequest()
        req.FileType = FILE_TYPE_IMAGE
        req.SpaceName = space_name
        req.FilePath = file_path
        req.Functions = json.dumps([get_meta_function, snapshot_function, add_option_function])
        req.CallbackArgs = ''
        req.FileName = ''
        req.FileExtension = '.jpg'

        resp = vod_service.upload_material(req)
    except Exception:
        raise
    else:
        print(resp)
        if resp.ResponseMetadata.Error.Code == '':
            print(resp.Result.Data)
            print(resp.Result.Data.Mid)
            print(resp.Result.Data.PosterUri)
            print(resp.Result.Data.SourceInfo.FileName)
            print(resp.Result.Data.SourceInfo.Height)
            print(resp.Result.Data.SourceInfo.Width)
        else:
            print(resp.ResponseMetadata.Error)
            print(resp.ResponseMetadata.RequestId)

if __name__ == '__main__':
    vod_service = VodService()

    # Call the following methods if you have not set the AK and SK in ~/.byteplus/config
    vod_service.set_ak('your ak')
    vod_service.set_sk('your sk')

    space_name = 'your space name'
    file_path = 'your file path'

    get_meta_function = Function.get_meta_func()
    add_option_function = Function.get_add_material_option_info_func(title='test subtitle', tags='test',
                                                                     description='Subtitle file',
                                                                     category=CATEGORY_FONT, record_type=2,
                                                                     format_input='vtt')

    try:
        req = VodUploadMaterialRequest()
        req.FileType = FILE_TYPE_OBJECT
        req.SpaceName = space_name
        req.FilePath = file_path
        req.Functions = json.dumps([get_meta_function, add_option_function])
        req.CallbackArgs = ''
        req.FileName = ''
        req.FileExtension = '.vtt'

        resp = vod_service.upload_material(req)
    except Exception:
        raise
    else:
        print(resp)
        if resp.ResponseMetadata.Error.Code == '':
            print(resp.Result.Data)
            print(resp.Result.Data.Mid)
        else:
            print(resp.ResponseMetadata.Error)
            print(resp.ResponseMetadata.RequestId)
```


<span id="54c43523"></span>
### Generating temporary upload token

You can generate a temporary upload token on the application server using AK and SK without needing the external network. If you need to generate multiple temporary upload tokens at the same time, call the generation method repeatedly. To learn how to use the temporary upload token, see [Client-side uploads](https://docs.byteplus.com/docs/byteplus-vod/docs-client-side-uploads).

```Python
# coding:utf-8
from __future__ import print_function

from byteplus_sdk.vod.VodService import VodService

if __name__ == '__main__':
    vod_service = VodService()

    # Call the following methods if you have not set the AK and SK in ~/.byteplus/config
    vod_service.set_ak('your ak')
    vod_service.set_sk('your sk')
    sts2 = vod_service.get_upload_sts2_with_expired_time(60 * 60)
    print(sts2)

    sts2 = vod_service.get_upload_sts2()
    print(sts2)
```


<span id="8fc6b9ee"></span>
### Generating temporary playback token

You can generate a temporary playback token on the application server using AK and SK without needing the external network. If you need to generate multiple temporary playback tokens at the same time, call the generation method repeatedly.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To learn how to use the temporary playback token, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-playing-videos-with-temporary-playback-tokens">Playing videos with temporary playback tokens</a>.</div>


* <div data-tips="true" data-tips-type="tip">For detailed information on the parameters, please refer to <a href="https://docs.byteplus.com/en/docs/byteplus-vod/reference-getplayinfo">GetPlayInfo</a>.</div>



```Python
# coding:utf-8
from __future__ import print_function

from byteplus_sdk.vod.VodService import VodService
from byteplus_sdk.vod.models.request.request_vod_pb2 import VodGetPlayInfoRequest

if __name__ == '__main__':

    vod_service = VodService()
    # call below method if you dont set ak and sk in $HOME/.vcloud/config
    vod_service.set_ak('your ak')
    vod_service.set_sk('your sk')
    try:
        vid = 'your vid'
        req = VodGetPlayInfoRequest()
        req.Vid = vid
        expire = 60  # seconds
        resp = vod_service.get_play_auth_token(req, expire)
    except Exception:
        raise
    else:
        print(resp)
    print('*' * 100)
```


<span id="5b62355c"></span>
### Generating DRM auth token

```Python
# coding:utf-8
from __future__ import print_function

from byteplus_sdk.vod.VodService import VodService
from byteplus_sdk.vod.models.request.request_vod_pb2 import VodGetDrmLicenseRequest

if __name__ == '__main__':

    vod_service = VodService()
    # Call the following methods if you have not set the AK and SK in ~/.byteplus/config
    vod_service.set_ak('your ak')
    vod_service.set_sk('your sk')
    try:
        vid = 'your vid'
        drmType = "your drm type"
        req = VodGetDrmLicenseRequest()
        req.Vid = vid
        req.ThirdPartyDrmType = drmType # widevine or fairplay
        expire = 60  # seconds
        resp = vod_service.get_third_party_drm_auth_token(req, expire)
    except Exception:
        raise
    else:
        print(resp)
    print('*' * 100)
```


<span id="7c425bb2"></span>
### Getting the FairPlay certificate URL

```Python
# coding:utf-8
from __future__ import print_function

from byteplus_sdk.vod.VodService import VodService
from byteplus_sdk.vod.models.request.request_vod_pb2 import VodGetDrmLicenseRequest

if __name__ == '__main__':

    vod_service = VodService()
    # Call the following methods if you have not set the AK and SK in ~/.byteplus/config
    vod_service.set_ak('your ak')
    vod_service.set_sk('your sk')
    try:
        certId = "your cert id"
        expire = 600  # seconds
        resp = vod_service.get_fairplay_cert_url(certId, expire)
    except Exception:
        raise
    else:
        print(resp)
    print('*' * 100)
```


<span id="9b74c2e9"></span>
### Getting VOD playback data

For detailed information on request and response parameters, please refer to [GetVodMediaPlayData](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getvodmediaplaydata).

```Python
# coding:utf-8
from __future__ import print_function

from byteplus_sdk.vod.VodService import VodService
import byteplus_sdk.vod.models.request.request_vod_pb2 as rq
import byteplus_sdk.vod.models.response.response_vod_pb2 as rsp

if __name__ == '__main__':
    service = VodService()
    subFilter = rq.GetVodMediaPlayDataFilter(
        Op='in',
        Field='your field',
        Values=['your value'],
    )
    filter = rq.GetVodMediaPlayDataFilter(
        Logic='and',
        Filters=[subFilter]
    )
    req = rq.GetVodMediaPlayDataRequest(
        AppID='your app_id',
        StartTime='2025-07-16T00:00:00+00:00',
        EndTime='2025-07-16T08:00:00+00:00',
        Platform='xxx',
        Metrics=['aaa', 'bbb'],
        Dimensions=['ccc', 'ddd'],
        Filter=filter
    )
    resp =  rsp.GetVodMediaPlayDataResponse()
    resp = service.get_vod_media_play_data(req)
    print(resp)
    print(resp.Result.Data[0]['aaa'])
    print(resp.Result.Data[0]['ccc'])
```
