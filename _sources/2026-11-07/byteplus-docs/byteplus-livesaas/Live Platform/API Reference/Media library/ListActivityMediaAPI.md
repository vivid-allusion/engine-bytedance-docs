---
title: "ListActivityMediaAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivitymediaapi"
---

Gets information of videos in the video library or temporary storage under the media library, including the video ID and name.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When calling this API with an IAM user, you can only get information of videos that the IAM user can access or edit. For more information on how to configure the user range and classification range of IAM users, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles">Managing users, organizations, and roles</a>.</div>


<span id="requirements"></span>
## Requirements


* Rate limit: 120 requests per minute per account

* Prerequisite: A BytePlus account or an IAM user with the following permissions. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

   * **Media library** \> **Videos** \> **Temporary storage** \> **Edit** or **View only** permission: Used to get information of videos in the temporary storage.

   * **Media library** \> **Videos** \> **Video library** \> **Edit** or **View only** permission: Used to get information of videos in the video library.


<span id="http-request"></span>
## HTTP request


* Method: GET

* Endpoint: https://livesaas.byteplusapi.com/?Action=ListActivityMediaAPI&Version=2020\-06\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListActivityMediaAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|PageNum |Integer |No |`1` |The number of the page to return. Default value: `1`. The value must be greater than or equal to 1. |
|PageSize |Integer |No |`10` |The number of results to return on each page. Default value: `10`. |
|SearchType |Integer |Yes |`2` |The storage location of the video. Valid values:<br><br><br>* `1`: Video library<br><br>* `2`: Temporary storage |
|Vid |String |No |`v02a49g10000ck****3c77u8uhf09ebg` |Vid of the video. |
|Name |String |No |`A` |Name of the video, which supports fuzzy search and is case\-insensitive. For example, if the parameter value is `A`, videos with names such as `Video A` and `video abc` will be returned. |
|SourceType |Integer |No |`2` |Source of the video. By default, videos from all sources are returned. Valid values:<br><br><br>* `1`: Upload, which means videos are uploaded locally.<br><br>* `2`: Recording, which means videos are automatically generated after the live stream ends.<br><br>* `3`: Cloud clips, which means videos are clipped using the cloud clips feature.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter only takes effect when the value of <code>SearchType</code> is <code>1</code>.</div><br> |
|OrderKey |String |No |`create_time` |Sort order of the videos. By default, videos are sorted in descending order by their update time. Valid values:<br><br><br>* `create_time`: Sorted in descending order by the video creation time.<br><br>* `Other values`: Sorted in descending order by the video update time. Update time refers to the time when the video information, such as cover image and name, is updated. |
|FolderId |Long |No |`0` |Category ID. Videos under the category with this ID will be returned. The default value is `0`, which means videos under all categories will be returned. You can get the category ID by calling [GetVideoLibraryFolderTree](https://docs.byteplus.com/en/docs/byteplus-livesaas/getvideolibraryfoldertree).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter only takes effect when the value of <code>SearchType</code> is <code>1</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When calling this API with an IAM user, if you need to pass this parameter, make sure the category with this ID is visible to the IAM user. For more information on how to configure the classification range of IAM users, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles">Managing users, organizations, and roles</a>.</div><br> |
|IncludeSubFolder |Boolean |No |`false` |Whether to include sub\-categories. Default value: `false`. Valid values:<br><br><br>* `true`: Include, which means all videos under the current category and its sub\-categories are returned.<br><br>* `false`: Not include, which means only videos under the current category are returned.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter only takes effect when the value of <code>SearchType</code> is <code>1</code>.</div><br> |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Data |Array of [Data](https://docs.byteplus.com/en/docs/11/47201#data) |`-` |List of returned videos. |
|Pagination |Object of [Pagination](https://docs.byteplus.com/en/docs/11/47201#pagination) |`-` |The pagination information. |


<span id="data"></span>
### Data


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Id |String |`43**98` |ID of the video. |
|MediaName |String |`video A` |Name of the video. |
|CoverImage |String |`https://www.example.com.image` |Cover image URL of the video. The URL of the default cover image has a protocol header, while the URL of the cover image uploaded through the console does not have a protocol header. |
|Vid |String |`v02a49g10000ck****3c77u8uhf09ebg` |Vid of the video. |
|MediaVideoDuration |Integer |`191` |Video duration. Unit: seconds. |
|MediaLibraryVideoType |Integer |`2` |The storage location of the video. Valid values:<br><br><br>* `1`: Video library<br><br>* `2`: Temporary storage |
|ReviewStatus |Integer |`2` |Review status of the video. Valid values:<br><br><br>* `1`: Not reviewed.<br><br>* `2`: Reviewed |
|CreateTime |Integer |`1696980251` |Creation time of the video in Unix timestamp format. Unit: seconds. If the video is transferred from temporary storage to the video library, it indicates the transfer time to the video library. |
|UpdateTime |Integer |`1696990559` |Most recent update time of the video in Unix timestamp format, which means the last time video information, such as the cover image and name, is updated. Unit: seconds. |
|Creator |String |`admin@bytedance.com` |Creator of the video. The value `admin@bytedance.com` indicates that the current video was created by the BytePlus account. |
|SourceType |Integer |`2` |Source of the video. Valid values:<br><br><br>* `1`: Upload, which means videos are uploaded locally.<br><br>* `2`: Recording, which means videos are automatically generated after the live stream ends.<br><br>* `3`: Cloud clips, which means videos are clipped using the cloud clips feature. |
|ActivityVideo |Array of [ActivityVideo](https://docs.byteplus.com/en/docs/11/47201#activityvideo) |`-` |Live rooms associated with the video, which means the live rooms that are using the video. |
|FailureTime |Integer |`1796980251` |Expiration time of the video. A value of `0` indicates the video is permanently saved and has no expiration time. |
|MediaSize |Integer |`24725029` |Size of the video. Unit: bytes. |
|VideoWidth |Long |`1080` |Horizontal pixel count of the video. `VideoWidth` and `VideoHeight` together determine the video resolution. |
|VideoHeight |Long |`1920` |Vertical pixel count of the video. `VideoWidth` and `VideoHeight` together determine the video resolution. |
|FolderName |String |`Category A` |Name of the category.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter only takes effect when the value of <code>MediaLibraryVideoType</code> is <code>1</code>.</div><br> |
|FolderId |Long |`0` |ID of the category.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter only takes effect when the value of <code>MediaLibraryVideoType</code> is <code>1</code>.</div><br> |


<span id="pagination"></span>
### Pagination


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|PageNum |Integer |`1` |The page number of the returned page. |
|PageSize |Integer |`10` |The number of results returned on each page. |
|TotalCount |Integer |`1` |The total number of returned videos. |


<span id="activityvideo"></span>
### ActivityVideo


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Id |Long |`177934****622756` |Activity ID of the live room. |
|Name |String |`Live room A` |Name of the live room. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
GET https://livesaas.byteplusapi.com/?Action=ListActivityMediaAPI&Version=2020-06-01&PageNum=1&PageSize=10&SearchType=2&Vid=v02a49g10000ck****3c77u8uhf09ebg&Name=A&SourceType=2&OrderKey=create_time&FolderId=0&IncludeSubFolder=false
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListActivityMediaAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "Data": [
            {
                "Id": "4****8",
                "MediaName": "video A",
                "CoverImage": "https://www.example.com.image",
                "Vid": "v02a49g10000ck****3c77u8uhf09ebg",
                "MediaVideoDuration": 191,
                "MediaLibraryVideoType": 2,
                "ReviewStatus": 2,
                "CreateTime": 1696980251,
                "UpdateTime": 1696990559,
                "Creator": "admin@bytedance.com",
                "SourceType": 2,
                "ActivityVideo": [
                    {
                        "Id": 177934****622756,
                        "Name": "Live room A"
                    }
                ],
                "FailureTime": 1796980251,
                "MediaSize": 24725029,
                "FolderId": 0,
                "FolderName": "Category A",
                "VideoHeight": 1920,
                "VideoWidth": 1080
            }
        ],
        "Pagination": {
            "PageNum": 1,
            "PageSize": 10,
            "TotalCount": 1
        }
    }
}
```


<span id="error-codes"></span>
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).

&nbsp;
