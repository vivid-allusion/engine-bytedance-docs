---
title: "Hotspot API"
product: "Market Insights"
product_code: "mkinsights"
source: "https://docs.byteplus.com/en/docs/mkinsights/HotspotAPIReference"
---

<span id="ahmlc3sm"></span>
## 1. Integration Guide

This document explains how to call the Social Media Hotspot Report OpenAPI through the BytePlus TOP gateway. The endpoints below are customer\-facing OpenAPI endpoints. The `/api/report/...` routes used inside the Platform service and the [console.byteplus.com/api/top/...](https://console.byteplus.com/api/top/...) endpoints used by the authenticated console must not be used as AK/SK client request endpoints.

<span id="xy2w1z8u"></span>
### 1.1 Provisioning and Authentication

Callers must prepare valid BytePlus AK/SK credentials and complete account and API permission provisioning themselves. This API reference does not handle credential applications or permission configuration on behalf of callers.

Callers must sign requests according to the BytePlus OpenAPI specification. The request description for each API provides fixed settings such as Host, Service, Region, Action, and Version. Region is a signing parameter, not an HTTP header. Do not put headers in the request body, and do not fabricate the gateway\-injected `X-Top-Account-Id` or `X-Top-Request-Id` headers.

Use the generation API below to obtain a `ReportID`, then query the report details using the same tenant identity. The creation API may incur charges. A successful creation response only means that the generation task has been accepted; it does not mean the report artifact is ready to read.

For signing rules, see [BytePlus OpenAPI Overview](https://docs.byteplus.com/en/docs/byteplus-platform/reference-overview-1) and [How To Calculate A Signature](https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature).

<span id="083xxuqb"></span>
### 1.2 Common Request Conventions


|**Item** |**Value** |
|---|---|
|Request endpoint |[https://mkt-insight.byteplusapi.com/](https://mkt-insight.byteplusapi.com/) |
|API Version |`2026-03-24` |
|Signing Service / Region |`mkt_insight` / `ap-southeast-1` |
|Action and Version |Include them in the URL query. See each API below for the location of business parameters. |
|Response |On success, read `Result`. On error, inspect the HTTP status and `ResponseMetadata.Error` (`Code` and `Message`). Retain `ResponseMetadata.RequestId` for troubleshooting. |


The request examples in this document show only business parameters. Actual requests must also include signing headers that comply with the BytePlus OpenAPI specification.

<span id="8ugr9mke"></span>
## 2. APIs

<span id="3824zowf"></span>
### 2.1 Generate a Report


|**Item** |**Description** |
|---|---|
|HTTP method |`POST` |
|Request body format |`application/json` |
|TOP Action |`GenerateReport` |
|Version |`2026-03-24` |
|Service (signing) |`mkt_insight` |
|Region (signing) |`ap-southeast-1` |
|Request endpoint |[https://mkt-insight.byteplusapi.com/](https://mkt-insight.byteplusapi.com/) |
|Full request URL |[https://mkt-insight.byteplusapi.com/?Action=GenerateReport&Version=2026-03-24](https://mkt-insight.byteplusapi.com/?Action=GenerateReport&Version=2026-03-24) |
|Authentication |The caller signs the request with its self\-managed BytePlus AK/SK according to the OpenAPI specification. An SDK may generate standard signing headers such as `Authorization`. Region is a signing parameter, not a standalone HTTP header. |
|Business parameters |Place them directly in the JSON body without an additional `Req` or `Header` wrapper. |



|Body **Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`ReportType` |`Int32` |Yes |Fixed value: `6`, indicating a social media hotspot trend report. |
|`ContentHotspot` |`Object` |Yes |Report generation parameters. See the fields below. |


<span id="e4ysvc8c"></span>
#### `ContentHotspot` Fields


|ConFields |**Type** |**Required** |**Description** |
|---|---|---|---|
|`CustomerName` |`String` |Yes |Customer name. It must not be empty after leading and trailing whitespace is removed. |
|`OrganizationType` |`String` |Yes |Organization type. Recommended values: `media`, `brand`, `research`, `gov`, `mcn`, `e-commerce_brand`, `creator_studio`, and `unknown`. |
|`ResearchDomain` |`String` |Yes |Research domain. It must not be empty after leading and trailing whitespace is removed. It is used to generate the report title, which must not exceed 256 characters. |
|`Platform` |`Int32` |Yes |Fixed value: `0`, indicating TikTok. Pass this value explicitly. |
|`UseCase` |`String` |Yes |One of `media_topic_selection`, `hotspot_product_follow_up`, or `marketing_creative`. |
|`Regions` |`Array<String>` |Yes |Currently, pass exactly one country code: `US`, `DE`, `IT`, or `GB`. |
|`TimeRange` |`Int32` |Yes |`0` means the last 7 days; `1` means the last 30 days. Pass this value explicitly. |


Text and parameters must pass server\-side capacity validation. Requests that exceed capacity are rejected before report creation and billing.

<span id="vto7bbyt"></span>
#### Request Body Example

```JSON
{
  "ReportType": 6,
  "ContentHotspot": {
    "CustomerName": "Example Media",
    "OrganizationType": "media",
    "ResearchDomain": "Artificial Intelligence",
    "Platform": 0,
    "UseCase": "media_topic_selection",
    "Regions": ["US"],
    "TimeRange": 0
  }
}
```



|Response Parameters |**Type** |**Description** |
|---|---|---|
|`Result.ReportID` |`Int64` |ID of the report created by this request. Use it with `GetReportDetail`. A returned ID does not mean that report content has already been generated. |
|`ResponseMetadata.RequestId` |`String` |Request identifier used for troubleshooting. It is not an idempotency key. |


<span id="1j63dmgd"></span>
#### Successful Response Example

```JSON
{
  "Result": {"ReportID": 123456},
  "ResponseMetadata": {"RequestId": "example-request-id"}
}
```


**Warning:**  Every valid creation request may create a new report and incur a charge. There is currently no idempotency guarantee across requests. If a request times out or its result is uncertain, do not immediately resend the creation request. First verify the report and billing results. The externally published product billing documentation governs actual pricing.


|**Business error code** |**Common scenario** |
|---|---|
|`InvalidParameter` |A field is missing, an enum value or region is unsupported, or text exceeds capacity. |
|`Unauthorized` |The account lacks the required access permission. |
|`QuotaExceeded` |The report quota is insufficient. |
|`InternalError` |An error occurred in storage, billing, or generation task processing. If the result is uncertain, manual verification may be required. |


<span id="7hxf8s0l"></span>
### 2.2 Get a Report


|**Item** |**Description** |
|---|---|
|HTTP method |`GET` |
|Request body format |No body |
|TOP Action |`GetReportDetail` |
|Version |`2026-03-24` |
|Service (signing) |`mkt_insight` |
|Region (signing) |`ap-southeast-1` |
|Request endpoint |[https://mkt-insight.byteplusapi.com/](https://mkt-insight.byteplusapi.com/) |
|Full request URL |[https://mkt-insight.byteplusapi.com/?Action=GetReportDetail&Version=2026-03-24&ReportID=123456](https://mkt-insight.byteplusapi.com/?Action=GetReportDetail&Version=2026-03-24&ReportID=123456) |
|Authentication |The caller signs the request with its self\-managed BytePlus AK/SK according to the OpenAPI specification. An SDK may generate standard signing headers such as `Authorization`. Region is a signing parameter, not a standalone HTTP header. |
|Business parameters |Put `ReportID` in the URL query. Use the same tenant identity that created the report. |



|**Query Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`ReportID` |`Int64` |Yes |Report ID returned by `GenerateReport`. |
|`ReportDisplay` |`Int32` |No |Hotspot reports use the default value `0`; omitting this parameter is recommended. Other display modes follow the existing `GetReportDetail` protocol. |



|Response Parameters |**Type** |**Description** |
|---|---|---|
|`Result.ReportInfo` |`Object`, optional |Basic report information, including `ReportID`, `Title`, `CreateTime`, `DialogID`, `UserInput`, `ImageUrl`, and optional `type`. `ImageUrl` is empty when the report has no cover image. |
|`Result.HtmlUrl` |`String`, optional |Console page URL available when the report can be viewed. Format: [https://console.byteplus.com/market-insights/report/{ReportID}](https://console.byteplus.com/market-insights/report/{ReportID}). |
|`Result.Content` |`String`, optional |Temporary download URL for the generated HTML artifact of a hotspot report. Use the URL from the current response. |
|`Result.json` |`String`, optional |Structured JSON report content. The field name is lowercase `json`. |


<span id="z8x8esqh"></span>
#### Example Response for a Generated Report (The fields in this example have been redacted.)

```JSON
{
  "header": {
    "report_id": "658",
    "content_field": "Smart Wearables",
    "platform": "TikTok",
    "region": ["US"],
    "data_window": "Last 7 days"
  },
  "summary": {
    "overseas_signal_samples": {"value": "37", "status": "Complete", "description": "Representative video evidence"},
    "trend_clusters": {"value": "8", "status": "Valid", "description": "Hot motifs"},
    "media_candidates": {"value": "3", "status": "In pool", "description": "Editorial topic suggestions"}
  },
  "trend_radar": {
    "categories": [{"name": "Consumer Electronics", "score": 74}],
    "themes": [{
      "time_window": "Last 7 days",
      "title": "Apple Watch Series 12 Unboxing and Design Discussion",
      "trend_indicator": "Accelerating"
    }]
  },
  "country_summary": [{
    "country": "US",
    "theme_count": 8,
    "accelerating_theme_count": 5,
    "top_themes": [{"title": "Apple Watch Series 12 Unboxing and Design Discussion", "growth_rate": "+747.02%"}]
  }],
  "hashtag_top10": [{
    "name": "#applewatch",
    "growth_7d": "+747.02%",
    "content_volume": "2.76K",
    "views": "12.51M",
    "main_regions": "US",
    "related_content_count": 10,
    "rep_videos": [{
      "title": "Apple Watch Series 12 has bigger bezels… kinda???  #applewatch #iphone #fyp #techtok #iphoneduo",
      "video_url": "https://www.tiktok.com/@thatchriscarley/video/7685921274408783117"
    }]
  }],
  "editorial_topics": [{
    "title": "What Is Driving Apple Watch Series 12 Unboxing Attention on TikTok?",
    "media_fit_score": 80
  }],
  "observe_pool": [{"title": "Showcase of AI glasses usage in creative and lifestyle scenarios"}],
  "discard_pool": [{"title": "Aesthetics and daily resonance of regular eyewear"}]
}
```



|**JSON field** |**Corresponding report content and meaning** |
|---|---|
|`header` |Overview information beneath the report title, including the research topic, platform, region, time window, and report summary. `report_id` identifies the report. |
|`summary` |The three overview metrics at the top of the page: representative video evidence, core hotspot themes, and editorial topic suggestions. For each metric, `value`, `status`, and `description` represent the value, status, and short description. The example uses strings for `value`. |
|`trend_radar` |“Overseas Trend Radar”: `categories` contains trend categories and scores, while `themes` contains hotspot themes. A `trend_indicator` such as `Accelerating` corresponds to the trend marker on the page. |
|`country_summary` |“Country / Region Hotspot Summary”: shows hotspot counts, accelerating hotspot counts, and key themes by country. Growth rates appear in `top_themes[].growth_rate`. |
|`hashtag_top10` |“Trending Hashtags and Linked Videos”: hashtags, growth rates, content volume, views, primary regions, and related videos. `rep_videos` contains the video entries shown when expanded. The actual list length depends on the response; do not assume there are always 10 entries solely from the field name. |
|`editorial_topics` |“Trending Topic Suggestions”: candidate topics and suggested angles, reasons, formats, and other details. `media_fit_score` corresponds to the page's Media Fit Score. |
|`observe_pool` / `discard_pool` |“Watchlist and Drop List”: topics to keep monitoring and topics not currently recommended for tracking, respectively. Entries may also include reasons. |


**Note:**  While a report is still being generated or has no available artifact, the detail response may contain only `ReportInfo`, without `HtmlUrl`, `Content`, or `json`. This release does not return a separate `GenerationStatus`. Do not interpret missing artifacts as a failed call. You may query the details at intervals acceptable to your business. If the wait limit is exceeded, contact support with the `RequestId` and `ReportID` for investigation. `GetReportDetail` does not create another report or incur another charge.

<span id="87regr3d"></span>
### 2.3 Get Detailed Video Interactions

Batch\-query TikTok video information and interaction metrics by video ID or URL. The following defines the external request and response contract for `GetVideoInteractions`. The official availability date is subject to the release announcement.


|**Item** |**Description** |
|---|---|
|HTTP method |`POST` |
|Request body format |`application/json` |
|TOP Action |`GetVideoInteractions` |
|Version |`2026-03-24` |
|Service (signing) |`mkt_insight` |
|Region (signing) |`ap-southeast-1` |
|Request endpoint |[https://mkt-insight.byteplusapi.com/](https://mkt-insight.byteplusapi.com/) |
|Full request URL |[https://mkt-insight.byteplusapi.com/?Action=GetVideoInteractions&Version=2026-03-24](https://mkt-insight.byteplusapi.com/?Action=GetVideoInteractions&Version=2026-03-24) |
|Authentication |The caller signs the request with its self\-managed BytePlus AK/SK according to the OpenAPI specification. An SDK may generate standard signing headers such as `Authorization`. Region is a signing parameter, not a standalone HTTP header. |
|Business parameters |Place business parameters directly in the JSON body without an additional `Req` wrapper. |



|**Body Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`Platform` |`String` |Yes |Currently, only `tiktok` is accepted. The value is case\-insensitive. |
|`Videos` |`Array<Object>` |Yes |List of 1–20 videos. Per\-item results are returned in the same order as the input. See the object fields below. |



|**Video Field** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`VideoID` |`String` |Conditionally required |Platform video ID. At least one of `VideoID` and `VideoURL` must be provided. Maximum 128 bytes after leading and trailing whitespace is removed. |
|`VideoURL` |`String` |Conditionally required |Video URL. At least one of `VideoID` and `VideoURL` must be provided. Maximum 2,048 bytes after leading and trailing whitespace is removed. It must be an HTTP(S) URL with a host. |
|`Region` |`String` |Yes |Country code of the video. Supported values: `US`, `DE`, `IT`, and `GB`. The value is case\-insensitive. |


`VideoID` and `VideoURL` may both be provided.

<span id="4r77mox8"></span>
#### Request Body Example 

(The video identifiers are illustrative only.)

```JSON
{
  "Platform": "tiktok",
  "Videos": [
    {"VideoID": "1234567890123456789", "Region": "US"},
    {"VideoURL": "https://www.tiktok.com/@example/video/9876543210987654321", "Region": "DE"}
  ]
}
```


A successful response wraps data in `Result` and `ResponseMetadata`. `Result.Results` follows the input order. A per\-item failure does not mean the entire HTTP request failed. `ResponseMetadata.RequestId` can be used for troubleshooting.


|Response Parameters |**Type** |**Description** |
|---|---|---|
|`Result.Results` |`Array<Object>` |Per\-item query results in the same order as `Videos`. A per\-item failure does not mean the entire request failed. |
|`Result.InputCount` |`Int32` |Number of videos submitted in this request. |
|`Result.FailedCount` |`Int32` |Number of videos whose per\-item queries failed. |
|`Result.Results[].VideoID` |`String`, optional |Platform video ID. Omitted if not returned. |
|`Result.Results[].VideoURL` |`String`, optional |Video URL. Omitted if not returned. |
|`Result.Results[].Region` |`String` |Country code of the video. |
|`Result.Results[].ItemStatus` |`Int32` |Per\-item status: `1` = success, `2` = invalid parameter, `3` = not found, `4` = query temporarily unavailable. |
|`Result.Results[].CoverURL` |`String`, optional |Video cover URL. Omitted if not returned. |
|`Result.Results[].Caption` |`String`, optional |Video title or caption. Omitted if not returned. |
|`Result.Results[].AuthorID` |`String`, optional |Creator ID. Omitted if not returned. |
|`Result.Results[].AuthorAccount` |`String`, optional |Creator account. Omitted if not returned. |
|`Result.Results[].PublishTime` |`String`, optional |Video publication time. The exact time format is to be confirmed. |
|`Result.Results[].ViewCount` |`Int64`, optional |View count. Omission does not mean `0`. |
|`Result.Results[].LikeCount` |`Int64`, optional |Like count. Omission does not mean `0`. |
|`Result.Results[].CommentCount` |`Int64`, optional |Comment count. Omission does not mean `0`. |
|`Result.Results[].FavoriteCount` |`Int64`, optional |Favorite count. Omission does not mean `0`. |
|`ResponseMetadata.RequestId` |`String` |Request identifier used for troubleshooting. |


<span id="exo4gev7"></span>
#### Response Structure Example

(The identifiers, metrics, and `RequestId` are fictitious.)

```JSON
{
  "Result": {
    "Results": [
      {
        "VideoID": "1234567890123456789",
        "VideoURL": "https://www.tiktok.com/@example/video/1234567890123456789",
        "Region": "US",
        "ItemStatus": 1,
        "CoverURL": "https://example.com/cover.jpg",
        "Caption": "Example video",
        "AuthorID": "author-123",
        "AuthorAccount": "example",
        "ViewCount": 100000,
        "LikeCount": 5000,
        "CommentCount": 120,
        "FavoriteCount": 800
      }
    ],
    "InputCount": 1,
    "FailedCount": 0
  },
  "ResponseMetadata": {"RequestId": "example-request-id"}
}
```


Billing is based on the number of requests, regardless of the number of videos in `Videos`. Under the current contract, each request consumes `0.2` report quota.

<span id="2f4ghc0q"></span>
#### Error Codes


|**Code** |**Service HTTP status** |**Description** |
|---|---|---|
|`InvalidParameter` |`400` |The platform, batch size, region, video identity, or URL is invalid. |
|`Unauthorized` |`403` |The account does not have SaaS access permission. |
|`QuotaExceeded` |`429` |The available quota is insufficient. |
|`InternalError` |`500` |Service processing failed or the result is temporarily unavailable. |


Callers must inspect the HTTP status and `ResponseMetadata.Error`, and retain `RequestId` for troubleshooting.

**Warning:**  This API has not yet completed formal availability validation. Follow the release announcement for official availability.

For gateway errors, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).
