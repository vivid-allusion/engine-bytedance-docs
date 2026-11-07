---
title: "Analyzing data with segments"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-analyzing-data-with-segments"
---

If you want to see the behavioral data of a subset of viewers, for example, viewers that come from a specific app or promoter, you can provide a viewing address with a suffix to that subset of viewers. BytePlus supports two types of suffix: standard and custom.

<span id="Use cases"></span>
## Use cases

<span id="Segmenting statistics by platforms"></span>
### Segmenting statistics by platforms

If you publish a live stream on several platforms, for example, YouTube, Facebook, and your own app, you can assign different viewing addresses to each platform so that BytePlus Live can collect the viewer counts, questionnaires, votes, and ad conversion from the different platforms to generate separate reports.

<span id="Segmenting statistics by promoter"></span>
### Segmenting statistics by promoter

You can assign different viewing addresses and posters to each live stream promoter so that BytePlus Live can collect the questionnaires, phone numbers and other conversion data from different promoters to generate separate reports.

<span id="Segmenting statistics by viewer"></span>
### Segmenting statistics by viewer

If viewers enter the live stream from your own app or official website, you can identify the viewer and then assign different viewing addresses to each viewer.

<span id="Standard suffix"></span>
## Standard suffix

By default, BytePlus Live provides five viewing addresses: the default address and four others with suffixes ranging from `?source=1` to `?source=4`, as shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0dcadc48e2b49f6bfc4dcdb3ec55d4b~tplv-goo7wpa0wc-image.image) </span>

Use standard suffix if you need to divide your traffic into five segments or less. Provide different viewing addresses to each channel. BytePlus Live will then automatically generate reports on the viewing data, questionnaires, and other statistics for each viewing address.

We recommend that you record the mapping between each viewing address and channel.

<span id="Custom suffix"></span>
## Custom suffix

If you need to segment the data into more than five groups, you can define your own suffixes. The suffix must begin with `?extra=`. You can then append a user or channel identifier. For example:


* User identity: `https://live.byteoc.com/XXXX/XXXXXXX?extra=user1`

* Channel identify: `https://live.byteoc.com/XXXX/XXXXXXX?extra=channel_A`


You can then assign the viewing addresses to the corresponding viewers or channels manually or programmatically.

If you use custom suffixes, BytePlus Live does not generate reports for each viewing address automatically. You need to export the data sheets and perform the calculations yourself.
