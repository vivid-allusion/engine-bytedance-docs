---
title: "Video preview"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-video-preview"
---

Video preview is a playback access control feature in BytePlus VOD that limits how much of a video viewers can watch. You can offer a preview to viewers who have not purchased, subscribed to, or been authorized to access the full content. This helps protect your content while supporting subscription sign\-ups, course purchases, and marketing conversions.

When a viewer requests playback using a preview URL, BytePlus VOD returns preview content according to the configured duration and the media format's playback boundaries. Your application can display a message when preview playback ends and direct viewers to a purchase or subscription page.

## Use cases

* Let viewers preview paid short dramas or subscription content before purchasing access.

* Offer an introduction to an online course before enrollment or purchase.

* Provide limited access to licensed content for viewers who are not yet authorized to watch the full video.

* Use a content preview to introduce a registration or subscription offer.

## How it works

![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261026094855-1415170446536.png)

1. Configure video preview and Type A URL signing for a playback domain.

2. The player requests a preview from your application server. Your application determines whether the viewer should receive preview or full\-video access.

3. For preview access, your server calls [GetPlayInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-getplayinfo) with `NeedPreview=true` and the configured preview domain, then passes the returned signed URL to the player.

4. The player requests content using that URL. The CDN validates the signed request and returns the preview content if validation succeeds, or rejects the request if validation fails.

The preview duration is configured on the domain. `NeedPreview` selects whether to request a preview URL; it does not specify a separate duration for an individual viewer.

## Before you begin

* Upload your video to BytePlus VOD and configure a playback domain for distribution.

* Enable Type A URL signing and check the format and duration requirements below.

* Decide how your application will handle the end of a preview. Prepare any purchase, subscription, or sign\-in page that viewers should visit to obtain full access. For suggested player interactions, see [Integrate preview playback](https://docs.byteplus.com/en/docs/25/123540#integrate-preview-playback).

## Requirements and limits

* Video preview supports MP4 and HLS. The resource path must end in `.mp4` or `.m3u8`, respectively. Resources without these extensions are not supported, even if the origin returns a matching `Content-Type` header. Adding an extension to an existing URL does not rename the stored file and can cause a 404 error.

* Video preview limits playback duration. It does not limit the number of viewers or distinct public IP addresses that can use a preview URL.

* Enable Type A [URL signing](https://docs.byteplus.com/docs/byteplus-vod/docs-url-authentication-overview) on the playback domain. Type C signing is not supported for video preview.

* The preview duration must be a positive integer of at least 5 seconds. Choose a duration shorter than the video. If the configured duration exceeds the video's total duration, the preview URL can play the entire video.

* Disable scheduling for the domain before changing its preview status. For domain distribution settings, see [Configuring the distribution rule](https://docs.byteplus.com/docs/byteplus-vod/docs-domain-name-settings#configuring-the-distribution-rule).

* After saving a configuration change, wait for it to take effect before requesting a new preview URL.

> **HLS preview duration**

> HLS preview ends at a TS segment boundary at or before the configured preview duration. The returned M3U8 playlist contains only segments within the preview duration. It does not round up to include the next segment. Set the preview duration greater than the TS segment duration. If the first TS segment is longer than the configured preview duration, no playable segment is returned.

> For example, for a video with 10\-second TS segments, a 15\-second preview returns 10 seconds of content, while a 5\-second preview returns no playable content. The limit depends on the video's segment durations; 10 seconds is not a fixed minimum for all HLS videos.

## Procedure

### Configure video preview

> **Previously signed URLs become invalid**

> Enabling or disabling video preview on a domain invalidates playback URLs signed before the change once the new configuration takes effect. This applies in both directions: when enabling preview and when disabling it. Wait for the change to take effect, then generate new signed playback URLs for the new preview status and replace the URLs used by your application.

#### Using the console

1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter your space.

2. Go to **Distribution acceleration \> Domain names** and select the **Playback domain name** tab.

3. Find the domain and click **Configure**. Open **Access Control** and click **Modify**.

4. Under **URL signing**, enable Type A signing and turn on **Support preview**. Video preview is disabled by default. Set **Preview duration** in seconds. Enter a positive integer of at least 5 seconds and choose a duration shorter than the video to provide a partial preview. For HLS, also follow the TS segment duration requirements above.

   ![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261026095449-124670564550.png)

5. Click **Save** and wait for the configuration to take effect.

#### Using the API

For a playback domain with Type A signing enabled, call [UpdateVodDomainConfig](https://docs.byteplus.com/docs/byteplus-vod/reference-updatevoddomainconfig) with `PreviewControl.Status` set to `enable` and `PreviewControl.PreviewTime` set to the duration in seconds. The following request body configures a 60\-second preview:

```json
{
  "SpaceName": "your-space",
  "DomainType": "vod_play",
  "PreviewControl": {
    "Status": "enable",
    "PreviewTime": 60
  },
  "UpdateCdnConfigParam": {
    "Domain": "preview.example.com"
  }
}
```

To disable video preview, set `PreviewControl.Status` to `disable`. You do not need to specify `PreviewTime` when disabling it. Omitting the entire `PreviewControl` object leaves the existing preview configuration unchanged.

### Get a preview URL

Call [GetPlayInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-getplayinfo) with the following parameters:

|Parameter |Value |
|---|---|
|`Vid` |The video ID. |
|`Format` |`mp4` or `hls`, matching an available video stream with the required file extension. |
|`NeedPreview` |`true`. |
|`PlayConfig` |A JSON string containing the preview domain, such as `{"PlayDomain":"preview.example.com"}`. |

Use the returned `PlayInfoList[].MainPlayUrl` or `BackupPlayUrl` as the playback URL. For a domain configured with a 60\-second preview, the returned URL includes `preview_time=60`. Pass the returned signed URL to the player unchanged.

The response's `Result.PreviewTime` indicates the configured preview duration in seconds, returned as a string such as `"60"`. For HLS, the actual playable duration can be shorter because of TS segment boundaries. If the domain has no enabled preview configuration, `NeedPreview=true` alone does not enforce a preview limit.

### Integrate preview playback

Pass the signed URL returned by `GetPlayInfo` to your player as its playback source. Keep the URL unchanged, including its signing and preview parameters.

The following are recommendations for your application's user interface:

* Clearly identify the content as a preview. Show elapsed playback time and the playable preview duration. If you also display the full video's duration, label it separately so viewers can distinguish it from the preview duration.

* Near the end of the preview, explain how to access the full video. For HLS, account for the actual playable duration rather than relying only on the configured `PreviewTime`.

* When preview playback ends, display a message or overlay with a clear action, such as **Subscribe**, **Buy full access**, or **Sign in**. Customize the wording and destination to match your service.

* After your application confirms that the viewer has full access, obtain a new signed playback URL using a domain without preview enabled. Do not remove or change `preview_time` on the existing URL.

Implement these messages, buttons, navigation, and access checks in your application. They are UI integration recommendations, not automatic behavior provided by enabling video preview on a domain.

## Usage recommendations

### How should I choose a preview duration?

Choose a duration that introduces the content and gives viewers enough context to decide whether to continue, such as a course introduction or an opening scene. Keep it shorter than the full video to avoid exposing the entire content. For very short videos, consider whether a preview provides a useful distinction from full access.

For HLS, check the TS segment durations before choosing a preview duration. A value that is valid in the console can still produce no playable content if it is shorter than the first segment. Test the returned URL with your actual content and player before offering it to viewers.

### How can I encourage viewers to continue after a preview?

Explain what viewers will receive with full access, and provide a clear action on the end\-of\-preview screen, such as **Subscribe now**, **Buy now**, or **Contact us**. Keep the message, button text, and destination consistent with your service and the viewer's next step.

### Can I provide different preview durations for different viewers?

The preview duration is configured for the playback domain. The `NeedPreview` parameter in `GetPlayInfo` controls whether to request a preview URL; it does not set a duration for an individual viewer. Your application can use the viewer's purchase, subscription, or authorization status to decide whether to provide preview or full\-video access.

## Troubleshooting

### Previously signed URLs stop working after enabling or disabling preview

Changing a domain's preview status invalidates URLs signed before the change once the new configuration takes effect. Wait for the configuration to take effect, then obtain new signed playback URLs: request preview URLs with `NeedPreview=true` after enabling preview, or obtain full\-video playback URLs after disabling it. Replace the old URLs in your application rather than modifying their signing or preview parameters.

### The HLS preview is empty or shorter than expected

Check the TS segment durations in the M3U8 file. Preview content is limited to complete segments within the configured duration. Increase the preview duration above the segment duration if no playable segment is returned.

### The preview URL returns 403

Make sure you requested the URL with `NeedPreview=true` after the domain's preview configuration took effect. A URL obtained with `NeedPreview` omitted or set to `false` has no preview parameter and can fail authentication on a domain configured for preview. Obtain a new signed preview URL instead of appending or changing `preview_time` yourself.

For full\-video playback, use a domain without preview enabled. We recommend using separate domains for preview and full\-video playback so that changing the preview configuration does not interrupt existing playback URLs.

### The preview plays the entire video

Confirm that preview is enabled for the domain used in the returned URL and that the configured duration is shorter than the video. Wait for any configuration change to take effect, then request a new URL.

### The video has no supported file extension

Use a resource whose stored path ends in `.mp4` or `.m3u8`. Do not append an extension to an existing resource URL as a workaround: the modified path can point to a file that does not exist.
