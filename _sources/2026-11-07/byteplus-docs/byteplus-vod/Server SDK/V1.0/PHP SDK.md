---
title: "PHP SDK"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-php-sdk"
---

To integrate BytePlus Video on Demand (VOD) into your PHP application, this guide provides installation instructions and ready\-to\-use code examples. You will learn how to set up the SDK, configure authentication, and implement core functionalities such as media uploads and token generation to accelerate your development.

<span id="7ed1dd07"></span>
## Prerequisites


* A BytePlus account or an IAM user. For more information, see [Signing up for a BytePlus account](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account) or [Managing IAM users and roles](https://docs.byteplus.com/byteplus-livesaas/docs/managing-iam-users-and-roles).

* Obtain the AccessKey ID (AK) and Secret Access Key (SK) for authentication.

   * To obtain the AK and SK of a BytePlus account, go to [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) \> User Profile \> **IAM** \> **Key management**.

   * To obtain the AK and SK of an IAM user, complete the following steps:

      1. Go to [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) \> User Profile \> **IAM** \> **Identity management** \> **User**.

      2. Find the user and then click **View details**.

      3. On the **Access key** tab, click **Create new access key**.

* Environmental requirements: PHP 7.1 or higher is required. You can check the PHP version through the `php -v` command. If PHP is not installed, visit [php.net](https://www.php.net/downloads.php) to download and install the appropriate version.


<span id="e63ee629"></span>
## Installing the SDK

Follow these steps to install the PHP SDK:


1. Install [Composer](https://getcomposer.org/). Composer is a PHP tool for managing and installing project dependencies.

2. In terminal, run the following command to install the latest version of the PHP SDK through Composer:

   ```Bash
   composer require byteplus_sdk/byteplus-sdk-php
   ```
   


<span id="01584103"></span>
## Setting the AK and SK

To set the AK and SK, you can use either of the following methods:


* Call `VodService.setAccessKey` and `VodService.setSecretKey`.

* Set the environment variables `BYTEPLUS_ACCESSKEY` as `"YOUR_AK"` and `BYTEPLUS_SECRETKEY` as `"YOUR_SK"`.

* Set the AK and SK in the JSON file in `/.byteplus/config`:

   ```JSON
   {
       "ak":"YOUR_AK",
       "sk":"YOUR_SK"
    }
   ```
   


<span id="d8e0909a"></span>
## Setting the service region

To connect to the Asia Pacific Southeast (Johor) region, pass in the region during instance initialization. See the following code example:

```PHP
// For the Asia Pacific Southeast (Johor) region, use SDK version v1.0.18 or later
$client = Byteplus\Service\Vod\Vod::getInstance("ap-southeast-1");
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The region parameter is optional and defaults to <code>ap-singapore-1</code> (Singapore) if not provided.</div>


<span id="6e5071d1"></span>
## Code examples

<span id="5b24172a"></span>
### Overview

BytePlus offers [code examples](https://github.com/byteplus-sdk/byteplus-sdk-php/tree/master/examples/Vod) for the PHP SDK on GitHub, which can assist you in accelerating your development process. The table below lists the BytePlus VOD Open APIs and their corresponding PHP SDK code examples.


|**Feature** |**API** |**PHP SDK code example** |
|---|---|---|
|Spaces |[CreateSpace](https://docs.byteplus.com/en/byteplus-vod/reference/createspace) |[DemoCreateSpace.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoCreateSpace.php) |
||[ListSpace](https://docs.byteplus.com/en/byteplus-vod/reference/listspace) |[DemoListSpace.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoListSpace.php) |
||[GetSpaceDetail](https://docs.byteplus.com/en/byteplus-vod/reference/getspacedetail) |[DemoGetSpaceDetail.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoGetSpaceDetail.php) |
||[UpdateSpaceUploadConfig](https://docs.byteplus.com/en/byteplus-vod/reference/updatespaceuploadconfig) |[DemoUpdateSpaceUploadConfig.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoUpdateSpaceUploadConfig.php) |
|Media upload |[ApplyUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/applyuploadinfo) |[DemoApplyUploadInfo.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoApplyUploadInfo.php) |
||[CommitUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/commituploadinfo) |[DemoCommitUploadInfo.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoCommitUploadInfo.php) |
||[UploadMediaByUrl](https://docs.byteplus.com/en/byteplus-vod/reference/uploadmediabyurl) |[DemoUploadMediaByUrl.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoUploadMediaByUrl.php) |
||[QueryUploadTaskInfo](https://docs.byteplus.com/en/byteplus-vod/reference/queryuploadtaskinfo) |[DemoQueryUploadTaskInfo.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoQueryUploadTaskInfo.php) |
|Media assets |[GetMediaInfos](https://docs.byteplus.com/en/byteplus-vod/reference/getmediainfos) |[DemoGetMediaInfos.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoGetMediaInfos.php) |
||[UpdateMediaInfo](https://docs.byteplus.com/en/byteplus-vod/reference/updatemediainfo) |[DemoUpdateMediaInfo.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoUpdateMediaInfo.php) |
||[UpdateMediaPublishStatus](https://docs.byteplus.com/en/byteplus-vod/reference/updatemediapublishstatus) |[DemoUpdateMediaPublishStatus.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoUpdateMediaPublishStatus.php) |
||[DeleteMedia](https://docs.byteplus.com/en/byteplus-vod/reference/deletemedia) |[DemoDeleteMedia.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoDeleteMedia.php) |
||[DeleteTranscodes](https://docs.byteplus.com/en/byteplus-vod/reference/deletetranscodes) |[DemoDeleteTranscodes.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoDeleteTranscodes.php) |
||[GetMediaList](https://docs.byteplus.com/en/byteplus-vod/reference/getmedialist) |[DemoGetMediaList.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoGetMediaList.php) |
||[GetSubtitleInfoList](https://docs.byteplus.com/en/byteplus-vod/reference/getsubtitleinfolist) |[DemoGetSubtitleInfoList.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoGetSubtitleInfoList.php) |
||[UpdateSubtitleStatus](https://docs.byteplus.com/en/byteplus-vod/reference/updatesubtitlestatus) |[DemoUpdateSubtitleStatus.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoUpdateSubtitleStatus.php) |
||[UpdateSubtitleInfo](https://docs.byteplus.com/en/byteplus-vod/reference/updatesubtitleinfo) |[DemoUpdateSubtitleInfo.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoUpdateSubtitleInfo.php) |
||[ListSnapshots](https://docs.byteplus.com/en/byteplus-vod/reference/listsnapshots) |None |
||[CreateVideoClassification](https://docs.byteplus.com/en/byteplus-vod/reference/createvideoclassification) |None |
||[ListVideoClassifications](https://docs.byteplus.com/en/byteplus-vod/reference/listvideoclassifications) |None |
||[UpdateVideoClassification](https://docs.byteplus.com/en/byteplus-vod/reference/updatevideoclassification) |None |
||[DeleteVideoClassification](https://docs.byteplus.com/en/byteplus-vod/reference/deletevideoclassification) |None |
||[CreatePlaylist](https://docs.byteplus.com/docs/byteplus-vod/reference-createplaylist) |None |
||[GetPlaylists](https://docs.byteplus.com/docs/byteplus-vod/reference-getplaylists) |None |
||[UpdatePlaylist](https://docs.byteplus.com/docs/byteplus-vod/reference-updateplaylist) |None |
||[DeletePlaylist](https://docs.byteplus.com/docs/byteplus-vod/reference-deleteplaylist) |None |
|Media processing |[StartWorkflow](https://docs.byteplus.com/en/byteplus-vod/reference/startworkflow) |[DemoStartWorkflow.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoStartWorkflow.php) |
||[RetrieveTranscodeResult](https://docs.byteplus.com/en/byteplus-vod/reference/retrievetranscoderesults) |[DemoRetrieveTranscodeResult.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoRetrieveTranscodeResult.php) |
||[GetWorkflowExecution](https://docs.byteplus.com/en/byteplus-vod/reference/getworkflowexecution) |[DemoGetWorkflowExecution.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoGetWorkflowExecution.php) |
|Video playback |[GetPlayInfo](https://docs.byteplus.com/en/byteplus-vod/reference/getplayinfo) |[DemoGetPlayInfo.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoGetPlayInfo.php) |
|Content distribution |[CreateDomain](https://docs.byteplus.com/en/byteplus-vod/reference/createdomain) |None |
||[ListDomain](https://docs.byteplus.com/en/byteplus-vod/reference/listdomain) |[DemoListDomain.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoListDomain.php) |
||[CreateCdnRefreshTask](https://docs.byteplus.com/en/byteplus-vod/reference/createcdnrefreshtask) |[DemoCreateCdnRefreshTask.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoCreateCdnRefreshTask.php) |
||[CreateCdnPreloadTask](https://docs.byteplus.com/en/byteplus-vod/reference/createcdnpreloadtask) |[DemoCreateCdnPreloadTask.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoCreateCdnPreloadTask.php) |
||[ListCdnTasks](https://docs.byteplus.com/en/byteplus-vod/reference/listcdntasks) |[DemoListCdnTasks.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoListCdnTasks.php) |
|Statistics |[DescribeVodDomainBandwidthData](https://docs.byteplus.com/en/byteplus-vod/reference/describevoddomainbandwidthdata) |[DemoDescribeVodDomainBandwidthData.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoDescribeVodDomainBandwidthData.php) |
||[DescribeVodDomainTrafficData](https://docs.byteplus.com/en/byteplus-vod/reference/describevoddomaintrafficdata) |[DemoDescribeVodDomainTrafficData.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoDescribeVodDomainTrafficData.php) |
||[DescribeVodSpaceStorageData](https://docs.byteplus.com/en/byteplus-vod/reference/describevodspacestoragedata) |[DemoDescribeVodSpaceStorageData.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoDescribeVodSpaceStorageData.php) |
||[DescribeVodSpaceTranscodeData](https://docs.byteplus.com/en/byteplus-vod/reference/describevodspacetranscodedata) |[DemoDescribeVodSpaceTranscodeData.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoDescribeVodSpaceTranscodeData.php) |
||[DescribeVodSpaceSubtitleStatisData](https://docs.byteplus.com/en/docs/byteplus-vod/reference-describevodspacesubtitlestatisdata) |[DemoDescribeVodSpaceSubtitleStatisData.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoDescribeVodSpaceSubtitleStatisData.php) |
||[DescribeVodSnapshotData](https://docs.byteplus.com/en/docs/byteplus-vod/reference-describevodsnapshotdata) |[DemoDescribeVodSnapshotData.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoDescribeVodSnapshotData.php) |
||[DescribeVodEnhanceImageData](https://docs.byteplus.com/en/docs/byteplus-vod/reference-describevodenhanceimagedata) |[DemoDescribeVodEnhanceImageData.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoDescribeVodEnhanceImageData.php) |
||[DescribeVodRealtimeMediaData](https://docs.byteplus.com/en/docs/byteplus-vod/DescribeVodRealtimeMediaData) |[DemoDescribeVodRealtimeMediaData.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoDescribeVodRealtimeMediaData.php) |
||[ListCdnUsageData](https://docs.byteplus.com/en/byteplus-vod/reference/listcdnusagedata) |[DemoListCdnUsageData.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoListCdnUsageData.php) |
||[ListCdnPvData](https://docs.byteplus.com/en/byteplus-vod/reference/listcdnpvdata) |[DemoListCdnPvData.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoListCdnPvData.php) |
||[ListCdnStatusData](https://docs.byteplus.com/en/byteplus-vod/reference/listcdnstatusdata) |[DemoListCdnStatusData.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoListCdnStatusData.php) |
||[ListCdnHitrateData](https://docs.byteplus.com/docs/byteplus-vod/reference-listcdnhitratedata) |None |
||[ListCdnTopAccessUrl](https://docs.byteplus.com/en/byteplus-vod/reference/listcdntopaccessurl) |[DemoListCdnTopAccessUrl.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoListCdnTopAccessUrl.php) |
||[DescribeVodPlayedStatisData](https://docs.byteplus.com/en/byteplus-vod/reference/describevodplayedstatisdata) |[DemoDescribeVodPlayedStatisData.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoDescribeVodPlayedStatisData.php) |
||[DescribeVodMostPlayedStatisData](https://docs.byteplus.com/en/byteplus-vod/reference/describevodmostplayedstatisdata) |[DemoDescribeVodMostPlayedStatisData.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoDescribeVodMostPlayedStatisData.php) |
|Settings |[SetCallbackEvent](https://docs.byteplus.com/en/byteplus-vod/reference/setcallbackevent) |[DemoSetCallbackEvent.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoSetCallbackEvent.php) |
||[AddCallbackSubscription](https://docs.byteplus.com/en/byteplus-vod/reference/addcallbacksubscription) |[DemoAddCallbackSubscription.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoAddCallbackSubscription.php) |
|Tools |[ListCdnAccessLog](https://docs.byteplus.com/docs/byteplus-vod/reference-listcdnaccesslog) |[DemoListCdnAccessLog.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoListCdnAccessLog.php) |
||[DescribeIpInfo](https://docs.byteplus.com/en/docs/byteplus-vod/reference-describeipinfo) |[DemoDescribeIpInfo.php](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoDescribeIpInfo.php) |


<span id="e8a2a6a0"></span>
### Uploading audio and video files

Read [media asset upload overview](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload-overview) to learn about the types of media assets and supported formats. For detailed information on the request parameters and response parameters, please refer to [ApplyUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/applyuploadinfo) and [CommitUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/commituploadinfo).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The media asset upload is an asynchronous task, meaning that the successful submission of a task does not necessarily indicate the successful execution of the task.</div>


* <div data-tips="true" data-tips-type="tip">You must include the file extension. For example, if you want to upload an MP4 file, include <code>.mp4</code> or <code>.MP4</code>.</div>



```PHP
<?php
require('../../vendor/autoload.php');

use Byteplus\Service\Vod\Models\Request\VodUploadMediaRequest;
use Byteplus\Service\Vod\Models\Response\VodCommitUploadInfoResponse;
use Byteplus\Service\Vod\Upload\Functions;
use Byteplus\Service\Vod\Upload\VodUpload;

$client = VodUpload::getInstance();
$client->setAccessKey('');
$client->setSecretKey('');
$client->setSessionToken('');

$space = '';
$filePath = "";

$functions = new Functions();
$functions->addGetMetaFunc();
$functions->addSnapshotTimeFunc(2.1);
$functions = $functions->getFunctionsString();

$request = new VodUploadMediaRequest();
$request->setSpaceName($space);
$request->setFilePath($filePath);
$request->setFunctions($functions);
$request->setCallbackArgs("my callback");

$response = new VodCommitUploadInfoResponse();
try {
    $response = $client->uploadMedia($request);
} catch (Exception $e) {
    echo $e, "\n";
} catch (Throwable $e) {
    echo $e, "\n";
}
if ($response->getResponseMetadata() != null && $response->getResponseMetadata()->getError() != null) {
    echo $response->getResponseMetadata()->getError()->serializeToJsonString(), "\n";
}
echo $response->serializeToJsonString();
echo "\n";

if ($response->getResult() != null) {
    echo $response->getResult()->getData()->getVid(), "\n";
    echo $response->getResult()->getData()->getPosterUri(), "\n";
    echo $response->getResult()->getData()->getSourceInfo()->getWidth(), "\n";
    echo $response->getResult()->getData()->getSourceInfo()->getHeight(), "\n";
}
```


<span id="09910ffa"></span>
### Uploading materials

Read [media asset upload overview](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload-overview) to learn about the types of media assets and supported formats. For detailed information on the request parameters and response parameters, please refer to [ApplyUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/applyuploadinfo) and [CommitUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/commituploadinfo).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The media asset upload is an asynchronous task, meaning that the successful submission of a task does not necessarily indicate the successful execution of the task.</div>


* <div data-tips="true" data-tips-type="tip">You must include the file extension. For example, if you want to upload an MP4 file, include <code>.mp4</code> or <code>.MP4</code>.</div>



```PHP
<?php
require('../../vendor/autoload.php');

use Byteplus\Service\Vod\Models\Request\VodUploadMediaRequest;
use Byteplus\Service\Vod\Models\Response\VodCommitUploadInfoResponse;
use Byteplus\Service\Vod\Upload\Functions;
use Byteplus\Service\Vod\Upload\VodUpload;

$client = VodUpload::getInstance();
$client->setAccessKey('');
$client->setSecretKey('');
$client->setSessionToken('');

$space = '';
$filePath = "";

$functions = new Functions();
$functions->addGetMetaFunc();
$functions->addSnapshotTimeFunc(2.1);
$functions = $functions->getFunctionsString();

$request = new VodUploadMediaRequest();
$request->setSpaceName($space);
$request->setFilePath($filePath);
$request->setFunctions($functions);
$request->setCallbackArgs("my callback");

$response = new VodCommitUploadInfoResponse();
try {
    $response = $client->uploadMedia($request);
} catch (Exception $e) {
    echo $e, "\n";
} catch (Throwable $e) {
    echo $e, "\n";
}
if ($response->getResponseMetadata() != null && $response->getResponseMetadata()->getError() != null) {
    echo $response->getResponseMetadata()->getError()->serializeToJsonString(), "\n";
}
echo $response->serializeToJsonString();
echo "\n";

if ($response->getResult() != null) {
    echo $response->getResult()->getData()->getVid(), "\n";
    echo $response->getResult()->getData()->getPosterUri(), "\n";
    echo $response->getResult()->getData()->getSourceInfo()->getWidth(), "\n";
    echo $response->getResult()->getData()->getSourceInfo()->getHeight(), "\n";
}
```


<span id="9b1797b3"></span>
### Generating temporary upload token

You can generate a temporary upload token on your application server using an AK and SK. This process does not require an external network connection. If you need to generate multiple temporary upload tokens, call the generation method for each one. For how to use the temporary upload token, see [Client-side uploads](https://docs.byteplus.com/docs/byteplus-vod/docs-client-side-uploads).

```PHP
<?php
require('../../vendor/autoload.php');

use Byteplus\Service\Vod\Vod;

$client = Vod::getInstance();
// Call the method below if you have not set your AK and SK in ~/.byteplus/config
$client->setAccessKey('');
$client->setSecretKey('');

$expire = 6000000; // Default Sign Expire (minutes)

echo "\nSTS2 Auth and Sign\n";
$space = "";
$response = $client->getUploadVideoAuthWithExpiredTime($expire);
echo json_encode($response);

echo "\nSTS2 Auth and Sign, Default Expire after 1 Hour\n";
$response = $client->getUploadVideoAuth();
echo json_encode($response);
```


<span id="3030c24c"></span>
### Generating temporary playback token

You can generate a temporary playback token on your application server using an AK and SK. This process does not require an external network connection. If you need to generate multiple temporary playback tokens, call the generation method for each one.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To learn how to use the temporary playback token, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-playing-videos-with-temporary-playback-tokens">Playing videos with temporary playback tokens</a>.</div>


* <div data-tips="true" data-tips-type="tip">For detailed information on the parameters, please refer to <a href="https://docs.byteplus.com/en/docs/byteplus-vod/reference-getplayinfo">GetPlayInfo</a>.</div>



```PHP
<?php
require('../../vendor/autoload.php');

use Byteplus\Service\Vod\Models\Request\VodGetPlayInfoRequest;
use Byteplus\Service\Vod\Models\Response\VodGetPlayInfoResponse;
use Byteplus\Service\Vod\Vod;

$client = Vod::getInstance();
// $client->setAccessKey("");
// $client->setSecretKey("");

$vid = "your vid";
$expire = 6000000; // Sign Expire

echo "\nGenerate PlayAuthToken\n";
$req = new VodGetPlayInfoRequest();
$req->setVid($vid);
try {
    $response = $client->getPlayAuthToken($req, $expire);
    echo $response;
} catch (Exception $e) {
    echo $e, "\n";
} catch (Throwable $e) {
    echo $e, "\n";
}
```


<span id="9ecd7c53"></span>
### Generating private encryption token

For how to use the playback token for private encryption, see [Private encryption](https://docs.byteplus.com/docs/byteplus-vod/docs-private-encryption).

```PHP
<?php
require('../../vendor/autoload.php');

use Byteplus\Service\Vod\Vod;
use Byteplus\Service\Vod\Models\Request\VodGetPrivateDrmPlayAuthRequest;
use Byteplus\Service\Vod\Models\Response\VodGetPrivateDrmPlayAuthResponse;

$client = Byteplus\Service\Vod\Vod::getInstance();

$vid = "your vid";
$playAuthId = "your play auth id";
$expire = 6000000; // Signature expiration time
$req = new VodGetPrivateDrmPlayAuthRequest();
$req->setVid($vid);
$req->setDrmType("your drm type");
$req->setPlayAuthIds($playAuthId);
$req->setUnionInfo("your unionInfo");

echo "\nGet PrivateDrmAuthToken\n";
try {

    $response2 = $client->getPrivateDrmPlayAuthToken($req, $expire);
    echo $response2;
} catch (Exception|Throwable $e) {
    echo $e, "\n";
}
```


<span id="0489e76f"></span>
### Generating DRM auth token

```PHP
<?php
require('../../vendor/autoload.php');

use Byteplus\Service\Vod\Models\Request\VodGetDrmLicenseRequest;
use Byteplus\Service\Vod\Models\Response\VodGetDrmLicenseResponse;
use Byteplus\Service\Vod\Vod;


$client = Vod::getInstance();
$client->setAccessKey("your ak");
$client->setSecretKey("your sk");

$vid = "your vid";
$drmType = "your drmType"; // widevine or fairplay
$expire = 60; // Sign Expire

echo "\nGenerate ThirdPartyDrmToken\n";
$req = new VodGetDrmLicenseRequest();
$req->setVid($vid);
$req->setThirdPartyDrmType($drmType);
try {
    $response = $client->getThirdPartyDrmAuthToken($req, $expire);
    echo $response;
} catch (Exception $e) {
    echo $e, "\n";
} catch (Throwable $e) {
    echo $e, "\n";
}
```


<span id="43a6269c"></span>
### Getting the FairPlay certificate URL

```PHP
<?php
require('../../vendor/autoload.php');

use Byteplus\Service\Vod\Vod;


$client = Vod::getInstance();
// $client->setAccessKey("");
// $client->setSecretKey("");

$certId = "your cert id";
$expire = 6000000; // Sign Expire

echo "\nGenerate GetFairPlayCertUrl\n";
try {
    $response = $client->getFairPlayCertUrl($certId, $expire);
    echo $response;
} catch (Exception $e) {
    echo $e, "\n";
} catch (Throwable $e) {
    echo $e, "\n";
}
```
