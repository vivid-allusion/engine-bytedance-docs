---
title: "Solution overview"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-interactive-live-streaming-solution-overview"
---

Interactive live streaming incorporates interactive features into the standard live streaming experience. This includes activities such as host PK battle and co\-hosting with audience members, providing a more engaging experience than standard live streaming that only allows interaction through text chat and virtual gifts. Interactive live streaming brings the host and audience closer together, resulting in a more immersive and enjoyable experience for both parties.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1be2eb3d58c449b58d67d8b12482f1cc~tplv-goo7wpa0wc-image.image) </span>

<span id="1162ea27"></span>
## Billing

This solution incurs fees for both live streaming and RTC services. For details, refer to [BytePlus MediaLive pricing overview](https://docs.byteplus.com/en/byteplus-media-live/docs/overview-1) and [RTC service fees](https://docs.byteplus.com/en/byteplus-rtc/docs/69871).

<span id="93a79cd0"></span>
## Highlights


* This solution is optimized for live streaming that involves occasional co\-hosting.

* This solution is more cost\-effective, as RTC service fees are charged only during co\-hosting.


<span id="12e15847"></span>
## Architecture

This section describes the technical architecture of the solution.

<span id="d090214a"></span>
### Solo hosting

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707113306-1587728378461.png) </span>

In solo hosting, the RTC engine handles audio and video capture, preview, and beauty AR. The RTC engine then mixes the stream on the server side and pushes the resulting stream to the CDN, and the audience can watch the stream on their apps.

<span id="790e081e"></span>
### Co\-hosting with audience members

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bafd25972b594264811de949414efd32~tplv-goo7wpa0wc-image.image) </span>

When the host begins co\-hosting with audience members, the co\-hosts' streams are added to the server\-side mixing. The RTC engine mixes the host's and co\-hosts' streams on the server side and pushes the resulting stream to the CDN.

During this process, the host receives the audio and video from the co\-hosts, and the audience can watch the mixed stream on their apps.

Once co\-hosting stops, solo\-hosting mode resumes.

<span id="dece16f2"></span>
### Host PK battle

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f463efdea4e4c20942c340165968c5a~tplv-goo7wpa0wc-image.image) </span>

When the host begins a host PK battle, host A and host B forward their streams to each other's rooms, and the RTC engine mixes the streams from host A and host B on the server side and pushes the resulting mixed stream to the CDN.

During this process, host A receives the audio and video from host B, and the audience can watch the mixed stream on their apps.

Once the host PK battle stops, solo\-hosting mode resumes.

<span id="1d052753"></span>
## Implementation

For implementation details, see the following topics:


* [Implementing interactive live for Android](https://docs.byteplus.com/docs/byteplus-vos/docs-implementing-interactive-live-for-android)

* [Implementing interactive live for iOS](https://docs.byteplus.com/docs/byteplus-vos/docs-implementing-interactive-live-for-ios)

* [Implementing interactive live for Server](https://docs.byteplus.com/docs/byteplus-vos/Implementing_interactive_live_for_Server)
