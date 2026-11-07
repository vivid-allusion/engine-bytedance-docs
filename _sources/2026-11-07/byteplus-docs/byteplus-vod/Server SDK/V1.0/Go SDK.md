---
title: "Go SDK"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-go-sdk"
---

To integrate BytePlus Video on Demand (VOD) features into your Go applications, you can use the official Go SDK. This guide provides comprehensive instructions on installing and initializing the SDK. It also includes a rich set of code examples for common operations such as uploading media, generating playback tokens, and managing content distribution, helping you to accelerate your development process.

<span id="7ed1dd07"></span>
## Prerequisites


* A BytePlus account or an IAM user. For more information, see [Signing up for a BytePlus account](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account) or [Managing IAM users and roles](https://docs.byteplus.com/byteplus-livesaas/docs/managing-iam-users-and-roles).

* Obtain the AccessKey ID (AK) and Secret Access Key (SK) for authentication.

   * To obtain the AK and SK of a BytePlus account, go to [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) \> **User Profile** \> **IAM** \> **Key management**.

   * To obtain the AK and SK of an IAM user, complete the following steps:

      1. Go to [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) \> User Profile \> **IAM** \> **Identity management** \> **User**.

      2. Find the user and then click **View details**.

      3. On the **Access key** tab, click **Create new access key**.

* Environmental requirements: Install the latest version of Go. For instructions to download and install the Go compilers, tools, and libraries, view the [install documentation](https://go.dev/doc/install).


<span id="e63ee629"></span>
## Installing the SDK

In a terminal, run the following command to install the latest version of the Go SDK:

```Bash
go get -u github.com/byteplus-sdk/byteplus-sdk-golang
```


<span id="01584103"></span>
## Setting the AK and SK

To set the AK and SK, you can use either of the following methods:


* Method one: Set the AK and SK in the JSON file in `/.byteplus/config`:

   ```JSON
   {
       "ak":"YOUR_AK",
       "sk":"YOUR_SK"
    }
   ```
   

* Method two: Set the environment variables `BYTEPLUS_ACCESSKEY` as `"YOUR_AK"` and `BYTEPLUS_SECRETKEY` as `"YOUR_SK"`.

* Method three: Call `SetCredential`.

   ```Go
   instance := vod.NewInstance()
   instance.SetCredential(base.Credentials{
                   AccessKeyID:     "YOUR_AK",
                   SecretAccessKey: "YOUR_SK",
   })
   ```
   


<span id="0e1c954a"></span>
## Setting the service region

To connect to the Asia Pacific (Johor) region, pass in the region during instance initialization. See the following code example:

```Go
// For the Asia Pacific (Johor) region, use SDK version v1.0.56 or later
instance := vod.NewInstanceWithRegion(base.RegionApSouthEast1)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The region parameter is optional and defaults to <code>ap-singapore-1</code> (Singapore) if not provided.</div>


<span id="6e5071d1"></span>
## Code examples

BytePlus offers [code examples](https://github.com/byteplus-sdk/byteplus-sdk-golang/tree/master/example/vod) for the Go SDK on GitHub, which can assist you in accelerating your development process. The table below presents the BytePlus VOD Open APIs along with their respective Go SDK code examples.

<span id="40d8c12b"></span>
### Overview


|**Feature** |**API** |**Go SDK code example** |
|---|---|---|
|Spaces |[CreateSpace](https://docs.byteplus.com/en/byteplus-vod/reference/createspace) |[demo_vod_space_service_test.go](https://github.com/byteplus-sdk/byteplus-sdk-golang/blob/master/example/vod/demo_vod_space_service_test.go) |
||[ListSpace](https://docs.byteplus.com/en/byteplus-vod/reference/listspace) ||
||[GetSpaceDetail](https://docs.byteplus.com/en/byteplus-vod/reference/getspacedetail) ||
||[UpdateSpaceUploadConfig](https://docs.byteplus.com/en/byteplus-vod/reference/updatespaceuploadconfig) ||
||[DescribeVodSpaceStorageData](https://docs.byteplus.com/en/byteplus-vod/reference/describevodspacestoragedata) ||
|Media upload |[ApplyUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/applyuploadinfo) |* [demo_vod_upload_service_test.go](https://github.com/byteplus-sdk/byteplus-sdk-golang/blob/master/example/vod/demo_vod_upload_service_test.go)<br><br>* [demo_upload_media_test.go](https://github.com/byteplus-sdk/byteplus-sdk-golang/blob/master/example/vod/upload/demo_upload_media_test.go)<br><br>* [demo_upload_material_test.go](https://github.com/byteplus-sdk/byteplus-sdk-golang/blob/master/example/vod/upload/demo_upload_material_test.go) |
||[CommitUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/commituploadinfo) ||
||[QueryUploadTaskInfo](https://docs.byteplus.com/en/byteplus-vod/reference/queryuploadtaskinfo) ||
||[UploadMediaByUrl](https://docs.byteplus.com/en/byteplus-vod/reference/uploadmediabyurl) ||
|Media assets |[UpdateMediaInfo](https://docs.byteplus.com/en/byteplus-vod/reference/updatemediainfo) |[demo_vod_media_service_test.go](https://github.com/byteplus-sdk/byteplus-sdk-golang/blob/master/example/vod/demo_vod_media_service_test.go) |
||[UpdateMediaPublishStatus](https://docs.byteplus.com/en/byteplus-vod/reference/updatemediapublishstatus) ||
||[GetMediaInfos](https://docs.byteplus.com/en/byteplus-vod/reference/getmediainfos) ||
||[DeleteMedia](https://docs.byteplus.com/en/byteplus-vod/reference/deletemedia) ||
||[DeleteTranscodes](https://docs.byteplus.com/en/byteplus-vod/reference/deletetranscodes) ||
||[GetMediaList](https://docs.byteplus.com/en/byteplus-vod/reference/getmedialist) ||
||[CreateVideoClassification](https://docs.byteplus.com/en/byteplus-vod/reference/createvideoclassification) ||
||[ListVideoClassifications](https://docs.byteplus.com/en/byteplus-vod/reference/listvideoclassifications) ||
||[UpdateVideoClassification](https://docs.byteplus.com/en/byteplus-vod/reference/updatevideoclassification) ||
||[DeleteVideoClassification](https://docs.byteplus.com/en/byteplus-vod/reference/deletevideoclassification) ||
||[ListSnapshots](https://docs.byteplus.com/en/byteplus-vod/reference/listsnapshots) ||
||[GetSubtitleInfoList](https://docs.byteplus.com/en/byteplus-vod/reference/getsubtitleinfolist) ||
||[UpdateSubtitleStatus](https://docs.byteplus.com/en/byteplus-vod/reference/updatesubtitlestatus) ||
||[UpdateSubtitleInfo](https://docs.byteplus.com/en/byteplus-vod/reference/updatesubtitleinfo) ||
|Media processing |[StartWorkflow](https://docs.byteplus.com/en/byteplus-vod/reference/startworkflow) |[demo_vod_workflow_service_test.go](https://github.com/byteplus-sdk/byteplus-sdk-golang/blob/master/example/vod/demo_vod_workflow_service_test.go) |
||[RetrieveTranscodeResults](https://docs.byteplus.com/en/byteplus-vod/reference/retrievetranscoderesults) ||
||[GetWorkflowExecution](https://docs.byteplus.com/en/byteplus-vod/reference/getworkflowexecution) ||
|Video playback |[GetPlayInfo](https://docs.byteplus.com/en/byteplus-vod/reference/getplayinfo) |[demo_vod_play_service_test.go](https://github.com/byteplus-sdk/byteplus-sdk-golang/blob/master/example/vod/demo_vod_play_service_test.go) |
|Statistics |[DescribeVodSpaceTranscodeData](https://docs.byteplus.com/en/byteplus-vod/reference/describevodspacetranscodedata) |[demo_vod_measure_service_test.go](https://github.com/byteplus-sdk/byteplus-sdk-golang/blob/master/example/vod/demo_vod_measure_service_test.go) |
||[DescribeVodSpaceSubtitleStatisData](https://docs.byteplus.com/en/docs/byteplus-vod/reference-describevodspacesubtitlestatisdata) ||
||[DescribeVodSnapshotData](https://docs.byteplus.com/en/docs/byteplus-vod/reference-describevodsnapshotdata) ||
||[DescribeVodEnhanceImageData](https://docs.byteplus.com/en/docs/byteplus-vod/reference-describevodenhanceimagedata) ||
||[DescribeVodRealtimeMediaData](https://docs.byteplus.com/en/docs/byteplus-vod/DescribeVodRealtimeMediaData) ||
||[DescribeVodPlayedStatisData](https://docs.byteplus.com/en/docs/byteplus-vod/reference-describevodplayedstatisdata) ||
||[DescribeVodMostPlayedStatisData](https://docs.byteplus.com/en/docs/byteplus-vod/reference-describevodmostplayedstatisdata) ||
|Settings |[SetCallbackEvent](https://docs.byteplus.com/en/byteplus-vod/reference/setcallbackevent) |[demo_vod_callback_service_test.go](https://github.com/byteplus-sdk/byteplus-sdk-golang/blob/master/example/vod/demo_vod_callback_service_test.go) |
||[AddCallbackSubscription](https://docs.byteplus.com/en/byteplus-vod/reference/addcallbacksubscription) ||
|Content distribution |[CreateDomain](https://docs.byteplus.com/en/byteplus-vod/reference/createdomain) |[demo_vod_cdn_service_test.go](https://github.com/byteplus-sdk/byteplus-sdk-golang/blob/master/example/vod/demo_vod_cdn_service_test.go) |
||[ListDomain](https://docs.byteplus.com/en/byteplus-vod/reference/listdomain) ||
||[CreateCdnPreloadTask](https://docs.byteplus.com/en/byteplus-vod/reference/createcdnpreloadtask) ||
||[CreateCdnRefreshTask](https://docs.byteplus.com/en/byteplus-vod/reference/createcdnrefreshtask) ||
||[ListCdnTasks](https://docs.byteplus.com/en/byteplus-vod/reference/listcdntasks) ||
||[ListCdnUsageData](https://docs.byteplus.com/en/byteplus-vod/reference/listcdnusagedata) ||
||[ListCdnPvData](https://docs.byteplus.com/en/byteplus-vod/reference/listcdnpvdata) ||
||[ListCdnStatusData](https://docs.byteplus.com/en/byteplus-vod/reference/listcdnstatusdata) ||
||[ListCdnTopAccessUrl](https://docs.byteplus.com/en/byteplus-vod/reference/listcdntopaccessurl) ||
||[DescribeVodDomainBandwidthData](https://docs.byteplus.com/en/byteplus-vod/reference/describevoddomainbandwidthdata) ||
||[DescribeVodDomainTrafficData](https://docs.byteplus.com/en/byteplus-vod/reference/describevoddomaintrafficdata) ||
||[ListCdnAccessLog](https://docs.byteplus.com/docs/byteplus-vod/reference-listcdnaccesslog) ||
||[DescribeIpInfo](https://docs.byteplus.com/en/docs/byteplus-vod/reference-describeipinfo) ||


<span id="70e00df8"></span>
### Uploading audio and video files

Read [media asset upload overview](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload-overview) to learn about the types of media assets and supported formats. For detailed information on the request parameters and response parameters, please refer to [ApplyUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/applyuploadinfo) and [CommitUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/commituploadinfo).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The media asset upload is an asynchronous task, meaning that the successful submission of a task does not necessarily indicate the successful execution of the task.</div>


* <div data-tips="true" data-tips-type="tip">You must include the file extension. For example, if you want to upload an MP4 file, include <code>.mp4</code> or <code>.MP4</code>.</div>



```Go
package upload

import (
        "encoding/json"
        "fmt"
        "github.com/byteplus-sdk/byteplus-sdk-golang/base"
        "github.com/byteplus-sdk/byteplus-sdk-golang/service/vod"
        "github.com/byteplus-sdk/byteplus-sdk-golang/service/vod/models/business"
        "github.com/byteplus-sdk/byteplus-sdk-golang/service/vod/models/request"
        "github.com/byteplus-sdk/byteplus-sdk-golang/service/vod/upload/functions"
        "testing"
)

func TestVod_UploadMediaWithCallback(t *testing.T) {
        // Call the method below if you haven't set the Access Key and Secret Key in ~/.vcloud/config
        instance := vod.NewInstance()
        instance.SetCredential(base.Credentials{
                AccessKeyID:     "your access key",
                SecretAccessKey: "your secret key",
        })

        // Or set the Access Key and Secret Key as follows
        // vod.NewInstance().SetAccessKey("")
        // vod.NewInstance().SetSecretKey("")

        spaceName := "your space"
        filePath := "media file path"

        getMetaFunc := functions.GetMetaFunc()
        snapShotFunc := functions.SnapshotFunc(business.VodUploadFunctionInput{SnapshotTime: 1.3}) 
        startWorkFlowFunc := functions.StartWorkflowFunc(business.VodUploadFunctionInput{TemplateId: "templateId"})
        optionFunc := functions.AddOptionInfoFunc(business.VodUploadFunctionInput{
                Title:            "title",
                Tags:             "Go,Programming",
                Description:      "Advanced Go Programming",
                Format:           "MP4", 
                ClassificationId: 0,
        })
        vodFunctions := []business.VodUploadFunction{snapShotFunc, getMetaFunc, startWorkFlowFunc, optionFunc}
        fbts, _ := json.Marshal(vodFunctions)

        vodUploadMediaRequest := &request.VodUploadMediaRequest{
                SpaceName:       spaceName, 
                FilePath:        filePath, 
                CallbackArgs:    "my callback", 
                Functions:       string(fbts),
                FileName:        "",
                FileExtension:   ".mp4",
                VodUploadSource: "upload",
        }

        resp, _, err := instance.UploadMediaWithCallback(vodUploadMediaRequest)
        if err != nil {
                fmt.Printf("error %v", err)
        } else {
                bts, _ := json.Marshal(resp)
                fmt.Printf("resp = %s", bts)
        }

        fmt.Println()
        fmt.Println(resp.GetResponseMetadata().GetRequestId())
        fmt.Println(resp.GetResult().GetData().GetVid())
        fmt.Println(resp.GetResult().GetData().GetSourceInfo().GetFileName())

}
```


<span id="fd962e72"></span>
### Uploading materials

Read [media asset upload overview](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload-overview) to learn about the types of media assets and supported formats. For detailed information on the request parameters and response parameters, please refer to [ApplyUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/applyuploadinfo) and [CommitUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/commituploadinfo).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The media asset upload is an asynchronous task, meaning that the successful submission of a task does not necessarily indicate the successful execution of the task.</div>


* <div data-tips="true" data-tips-type="tip">You must include the file extension. For example, if you want to upload an MP4 file, include <code>.mp4</code> or <code>.MP4</code>.</div>



```Go
package upload

import (
        "encoding/json"
        "fmt"
        "github.com/byteplus-sdk/byteplus-sdk-golang/base"
        "github.com/byteplus-sdk/byteplus-sdk-golang/service/vod"
        "github.com/byteplus-sdk/byteplus-sdk-golang/service/vod/models/business"
        "github.com/byteplus-sdk/byteplus-sdk-golang/service/vod/models/request"
        "github.com/byteplus-sdk/byteplus-sdk-golang/service/vod/upload/consts"
        "github.com/byteplus-sdk/byteplus-sdk-golang/service/vod/upload/functions"
        "testing"
)

func TestVod_UploadMediaMaterialWithCallback(t *testing.T) {
        // Call the method below if you don't set ak and sk in ~/.vcloud/config
        instance := vod.NewInstance()
        instance.SetCredential(base.Credentials{
                AccessKeyID:     "your ak",
                SecretAccessKey: "your sk",
        })

        // or set AK and SK as follows
        //vod.NewInstance().SetAccessKey("")
        //vod.NewInstance().SetSecretKey("")

        spaceName := "your space"
        filePath := "material file path"

        snapShotFunc := functions.SnapshotFunc(business.VodUploadFunctionInput{SnapshotTime: 1.3})
        getMetaFunc := functions.GetMetaFunc()
        addOptionFunc := functions.AddOptionInfoFunc(business.VodUploadFunctionInput{
                Title:       "test-video", 
                Tags:        "test", 
                Description: "test1，test2", 
                Category:    consts.CategoryVideo,
                RecordType:  2, 
                Format:      "mp4",
        })

        vodFunctions := []business.VodUploadFunction{addOptionFunc, getMetaFunc, snapShotFunc}
        fbts, _ := json.Marshal(vodFunctions)

        vodUploadMaterialRequest := &request.VodUploadMaterialRequest{
                SpaceName:     spaceName,
                FilePath:      filePath,
                CallbackArgs:  "my callback",
                Functions:     string(fbts),
                FileType:      consts.FileTypeMedia,
                FileName:      "",
                FileExtension: ".mp4",
        }

        resp, _, err := instance.UploadMaterialWithCallback(vodUploadMaterialRequest)
        if err != nil {
                fmt.Printf("error %v", err)
        } else {
                bts, _ := json.Marshal(resp)
                fmt.Printf("\nresp = %s", bts)
        }

        fmt.Println(resp.GetResponseMetadata().GetRequestId())
        fmt.Println(resp.GetResult().GetData().GetMid())
        fmt.Printf("%d\n", int(resp.GetResult().GetData().GetSourceInfo().GetSize()))

}

func TestVod_UploadImageMaterialWithCallback(t *testing.T) {
        // call the method below if you don't set ak and sk in ~/.vcloud/config
        instance := vod.NewInstance()
        instance.SetCredential(base.Credentials{
                AccessKeyID:     "your ak",
                SecretAccessKey: "your sk",
        })

        // or set AK and SK as follows
        //vod.NewInstance().SetAccessKey("")
        //vod.NewInstance().SetSecretKey("")

        spaceName := "your space"
        filePath := "material file path"

        getMetaFunc := functions.GetMetaFunc()
        addOptionFunc := functions.AddOptionInfoFunc(business.VodUploadFunctionInput{
                Title:       "test-image",
                Tags:        "test",
                Description: "test1，test2",
                Category:    consts.CategoryImage,
                RecordType:  2,
                Format:      "jpg",
        })

        vodFunctions := []business.VodUploadFunction{addOptionFunc, getMetaFunc}
        fbts, _ := json.Marshal(vodFunctions)

        vodUploadMaterialRequest := &request.VodUploadMaterialRequest{
                SpaceName:     spaceName,
                FilePath:      filePath,
                CallbackArgs:  "my callback",
                Functions:     string(fbts),
                FileType:      consts.FileTypeImage,
                FileName:      "",
                FileExtension: ".jpg",
        }

        resp, _, err := instance.UploadMaterialWithCallback(vodUploadMaterialRequest)
        if err != nil {
                fmt.Printf("error %v", err)
        } else {
                bts, _ := json.Marshal(resp)
                fmt.Printf("\nresp = %s", bts)
        }

        fmt.Println(resp.String())
        fmt.Println(resp.GetResponseMetadata().GetRequestId())
        fmt.Println(resp.GetResult().GetData().GetMid())

}

func TestVod_UploadObjectMaterialWithCallback(t *testing.T) {
        // call the method below if you don't set ak and sk in ~/.vcloud/config
        instance := vod.NewInstance()
        instance.SetCredential(base.Credentials{
                AccessKeyID:     "your ak",
                SecretAccessKey: "your sk",
        })

        // or set AK and SK as follows
        //vod.NewInstance().SetAccessKey("")
        //vod.NewInstance().SetSecretKey("")

        spaceName := "your space"
        filePath := "material file path"

        getMetaFunc := functions.GetMetaFunc()
        addOptionFunc := functions.AddOptionInfoFunc(business.VodUploadFunctionInput{
                Title:       "test-subtitle",
                Tags:        "test",
                Description: "test1，test2",
                Category:    consts.CategorySubtitle,
                RecordType:  2,
                Format:      "vtt",
        })

        vodFunctions := []business.VodUploadFunction{addOptionFunc, getMetaFunc}
        fbts, _ := json.Marshal(vodFunctions)

        vodUploadMaterialRequest := &request.VodUploadMaterialRequest{
                SpaceName:     spaceName,
                FilePath:      filePath,
                CallbackArgs:  "my callback",
                Functions:     string(fbts),
                FileType:      consts.FileTypeObject,
                FileName:      "",
                FileExtension: ".vtt",
        }

        resp, _, err := instance.UploadMaterialWithCallback(vodUploadMaterialRequest)
        if err != nil {
                fmt.Printf("error %v", err)
        } else {
                bts, _ := json.Marshal(resp)
                fmt.Printf("\nresp = %s", bts)
        }

        fmt.Println(resp.String())
        fmt.Println(resp.GetResponseMetadata().GetRequestId())
        fmt.Println(resp.GetResult().GetData().GetMid())

}
```


<span id="db98cf19"></span>
### Generating temporary upload token

You can generate a temporary upload token on the application server using AK and SK without needing the external network. If you need to generate multiple temporary upload tokens at the same time, call the generation method repeatedly. For how to use the temporary upload token, see [Client-side uploads](https://docs.byteplus.com/docs/byteplus-vod/docs-client-side-uploads).

```Go
package vod

import (
        "encoding/json"
        "fmt"
        "testing"
        "time"

        "github.com/byteplus-sdk/byteplus-sdk-golang/service/vod"
        "github.com/byteplus-sdk/byteplus-sdk-golang/service/vod/models/request"
)

func TestVod_GetUploadAuthWithExpiredTime(t *testing.T) {
        instance := vod.NewInstance()
        instance.SetAccessKey("")
        instance.SetSecretKey("")

        // Default expire time is 1 hour
        ret, _ := instance.GetUploadAuth()
        b, _ := json.Marshal(ret)
        fmt.Println(string(b))

        ret2, _ := instance.GetUploadAuthWithExpiredTime(3 * time.Hour)
        b2, _ := json.Marshal(ret2)
        fmt.Println(string(b2))
}
```


<span id="6df7020f"></span>
### Generating temporary playback token

You can generate a temporary playback token on the application server using AK and SK without needing the external network. If you need to generate multiple temporary playback tokens at the same time, call the generation method repeatedly.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To learn how to use the temporary playback token, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-playing-videos-with-temporary-playback-tokens">Playing videos with temporary playback tokens</a>.</div>


* <div data-tips="true" data-tips-type="tip">For detailed information on the parameters, please refer to <a href="https://docs.byteplus.com/en/docs/byteplus-vod/reference-getplayinfo">GetPlayInfo</a>.</div>



```Go
package vod

import (
        "encoding/json"
        "fmt"
        "testing"
        "time"

        "github.com/byteplus-sdk/byteplus-sdk-golang/service/vod"
        "github.com/byteplus-sdk/byteplus-sdk-golang/service/vod/models/request"
)

func TestVod_GetPlayAuthToken(t *testing.T) {
        vid := "your vid"
        tokenExpireTime := 600 // Token Expire Duration (s)
        instance := vod.NewInstance()

        //instance.SetCredential(base.Credentials{
        // AccessKeyID:     "your ak",
        // SecretAccessKey: "your sk",
        //})

        // or set AK and SK as follows
        //instance.SetAccessKey("")
        //instance.SetSecretKey("")

        query := &request.VodGetPlayInfoRequest{
                Vid:             vid,
                Format:          "mp4",
                Definition:      "360p",
                FileType:        "video",
                LogoType:        "",
                Ssl:             "1",
                NeedThumbs:      "0",
                NeedBarrageMask: "0",
                CdnType:         "0",
        }
        newToken, _ := instance.GetPlayAuthToken(query, tokenExpireTime)
        fmt.Println(newToken)
}
```


<span id="9922ce0b"></span>
### Generating private encryption token

For how to use the playback token for private encryption, see [Private encryption](https://docs.byteplus.com/docs/byteplus-vod/docs-private-encryption).

```Go
package vod

import (
        "encoding/json"
        "fmt"
        "testing"
        "time"

        "github.com/byteplus-sdk/byteplus-sdk-golang/service/vod"
        "github.com/byteplus-sdk/byteplus-sdk-golang/service/vod/models/request"
)

func TestVod_GetPrivateDrmAuthToken(t *testing.T) {
        instance := vod.NewInstance()

        //instance.SetCredential(base.Credentials{
        // AccessKeyID:     "your ak",
        // SecretAccessKey: "your sk",
        //})

        // or set AK and SK as follows
        instance.SetAccessKey("your ak")
        instance.SetSecretKey("your sk")

        query := &request.VodGetPrivateDrmPlayAuthRequest{
                Vid:         "your vid",
                DrmType:     "your drmType",
                PlayAuthIds: "your playAuthIds",
                UnionInfo:   "your unionInfo",
        }
        tokenExpireTime := 6000000 // Token Expire Duration (s)
        newToken, _ := instance.GetPrivateDrmAuthToken(query, tokenExpireTime)
        fmt.Println(newToken)
}
```


<span id="70223726"></span>
### Generating DRM auth token

```Go
// Code generated by protoc-gen-byteplus-sdk
// source: VodDrmService
// DO NOT EDIT!

package vod

import (
        "fmt"
        "testing"

        "github.com/byteplus-sdk/byteplus-sdk-golang/service/vod"
        "github.com/byteplus-sdk/byteplus-sdk-golang/service/vod/models/request"
)

func Test_GetThirdPartyDrmAuthToken(t *testing.T) {
        vid := "your vid"
        tokenExpireTime := 600 // Token Expire Duration (s)
        instance := vod.NewInstance()

        //instance.SetCredential(base.Credentials{
        // AccessKeyID:     "your ak",
        // SecretAccessKey: "your sk",
        //})

        // or set AK and SK as follows
        instance.SetAccessKey("your ak")
        instance.SetSecretKey("your sk")

        query := &request.VodGetDrmLicenseRequest{
                Vid:               vid,
                ThirdPartyDrmType: "your DrmType", // widevine or fairplay
        }
        newToken, err := instance.GetThirdPartyDrmAuthToken(query, tokenExpireTime)
        if err != nil {
                t.Fatal(err)
        }
        fmt.Println(newToken)
}

func Test_GetFairplayCertUrl(t *testing.T) {
        certId := "your Cert Id"
        expireTime := 600000 // Url Expire Duration (s)
        instance := vod.NewInstance()

        //instance.SetCredential(base.Credentials{
        // AccessKeyID:     "your ak",
        // SecretAccessKey: "your sk",
        //})

        // or set AK and SK as follows
        instance.SetAccessKey("your ak")
        instance.SetSecretKey("your sk")

        certUrl, err := instance.GetFairPlayCertSignUrl(certId, expireTime)
        if err != nil {
                t.Fatal(err)
        }
        fmt.Println(certUrl)
}
```


<span id="857c5e9e"></span>
### Generating HLS decryption token

```Go
package vod

import (
        "encoding/json"
        "fmt"
        "testing"
        "time"

        "github.com/byteplus-sdk/byteplus-sdk-golang/service/vod"
        "github.com/byteplus-sdk/byteplus-sdk-golang/service/vod/models/request"
)

func TestVod_GetSha1HlsDrmAuthToken(t *testing.T) {
        instance := vod.NewInstance()
        //instance.SetCredential(base.Credentials{
        // AccessKeyID:     "your ak",
        // SecretAccessKey: "your sk",
        //})
        // or set ak and ak as follows
        instance.SetAccessKey("")
        instance.SetSecretKey("")
        expireDuration := int64(6000000) // change to your expire duration (s), no default duration
        hlsToken, _ := instance.CreateSha1HlsDrmAuthToken(expireDuration)
        fmt.Println(hlsToken)
}
```


<span id="fd201196"></span>
### Getting the FairPlay certificate URL

```Go
package vod

import (
        "fmt"
        "testing"

        "github.com/byteplus-sdk/byteplus-sdk-golang/service/vod"
        "github.com/byteplus-sdk/byteplus-sdk-golang/service/vod/models/request"
)

func Test_GetThirdPartyDrmAuthToken(t *testing.T) {
        vid := "your vid"
        tokenExpireTime := 600 // Token Expire Duration (s)
        instance := vod.NewInstance()

        //instance.SetCredential(base.Credentials{
        // AccessKeyID:     "your ak",
        // SecretAccessKey: "your sk",
        //})
        
        // or set AK and SK as follows
        instance.SetAccessKey("your ak")
        instance.SetSecretKey("your sk")

        query := &request.VodGetDrmLicenseRequest{
                Vid:               vid,
                ThirdPartyDrmType: "your DrmType", // widevine or fairplay
        }
        newToken, err := instance.GetThirdPartyDrmAuthToken(query, tokenExpireTime)
        if err != nil {
                t.Fatal(err)
        }
        fmt.Println(newToken)
}

func Test_GetFairplayCertUrl(t *testing.T) {
        certId := "your Cert Id"
        expireTime := 600000 // Url Expire Duration (s)
        instance := vod.NewInstance()

        //instance.SetCredential(base.Credentials{
        // AccessKeyID:     "your ak",
        // SecretAccessKey: "your sk",
        //})

        // or set AK and SK as follows
        instance.SetAccessKey("your ak")
        instance.SetSecretKey("your sk")

        certUrl, err := instance.GetFairPlayCertSignUrl(certId, expireTime)
        if err != nil {
                t.Fatal(err)
        }
        fmt.Println(certUrl)
}
```


<span id="a1d6e593"></span>
### Generating subtitle auth token

```Go
package vod

import (
        "encoding/json"
        "fmt"
        "testing"
        "time"

        "github.com/byteplus-sdk/byteplus-sdk-golang/service/vod"
        "github.com/byteplus-sdk/byteplus-sdk-golang/service/vod/models/request"
)

func TestVod_GetSubtitleAuthToken(t *testing.T) {
        instance := vod.NewInstance()
        // call the method below if you don't set ak and sk in ~/.byteplus/config
        //vod.NewInstance().SetCredential(base.Credentials{
        //        AccessKeyID:     "your ak",
        //        SecretAccessKey: "your sk",
        //})
        // or set ak and ak as follow
        // instance.SetAccessKey("")
        // instance.SetSecretKey("")

        // Media Info
        query := &request.VodGetSubtitleInfoListRequest{
                Vid: "your search vid",
        }
        expireSeconds := 100 // expire time duration: (s)
        token, err := instance.GetSubtitleAuthToken(query, expireSeconds)
        fmt.Println("token ===> ", token)
        fmt.Println("err ===> ", err)
}
```
