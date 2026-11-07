---
title: "Video playback issues"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/Video_playback_issues"
---

Refer to this document to resolve problems encountered while playing videos.

<span id="f5f11a2d"></span>
## How do I resolve the issues of failing to retrieve video file URLs?

Possible causes and corresponding solutions are as follows:


* **Domain not bound**: You have not bound a domain name. Please bind a domain immediately. For detailed steps, see [Adding domain name](https://docs.byteplus.com/docs/byteplus-vod/docs-domain-name-management).

* **Domain disabled**: If a domain is bound but its status is disabled, please enable the accelerated domain. For detailed steps, see [Configuring domain name](https://docs.byteplus.com/en/docs/byteplus-vod/docs-configuring-domain-name).

* **Signature key disabled**: If a domain is bound but the signature key is turned off, you must manually concatenate the URL parameters to access the file. For details, see [URL signing overview](https://docs.byteplus.com/docs/byteplus-vod/docs-url-authentication-overview).


<span id="ae554e0c"></span>
## How do I resolve playback stuttering issues in edited videos?

If you experience stuttering during playback after video editing, you can troubleshoot using the following methods:


* **Check the player**: Verify if the issue lies with the player itself. Try playing the edited video with a different player or update your current player to the latest version.

* **Check the source video**: Verify whether the source video is corrupted.


If the issue persists, please [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001112) for technical support.

<span id="c5edc2d7"></span>
## How do I resolve artifacts, black screens, stuttering or playback failures after transcoding?

These issues are typically caused by corrupted source videos or transcoding failures. You can troubleshoot as follows:


* **Check the source video**: Verify if the source video is corrupted or uses an unsupported format.

* **Check transcoding settings**: Ensure that the transcoding parameters, such as video codec, resolution, frame rate, are configured correctly. Try adjusting these settings and retranscoding the video.

* **Check the player**: Verify if the player is malfunctioning. Try an alternative player or update the current one to the latest version.


If the issue persists, please [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001112) for technical support.
