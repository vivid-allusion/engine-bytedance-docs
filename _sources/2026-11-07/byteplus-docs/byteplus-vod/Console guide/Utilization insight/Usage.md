---
title: "Usage"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-usage"
---

The **Usage** page provides precise metrics on your usage of BytePlus VOD features, including bandwidth, traffic, transcoding, snapshots, video enhancement, smart subtitling, and real\-time processing. This data can help you understand how, when, and where you use the BytePlus VOD features and verify your billing details.

## Overview

The supported data includes:

* Bandwidth and traffic:

   * Peak bandwidth

   * 95th percentile bandwidth

   * Total traffic

   * Bandwidth and traffic trends

* Media storage usage: Total standard storage usage

* Transcoding usage:

   * Duration of basic transcoding

   * Duration of low\-bitrate HD transcoding

* Snapshot usage: Number of snapshots

* Video enhancement: Duration of output content

* Smart subtitling usage:

   * Duration of speech\-to\-text transcription

   * Character count of machine translation

* Real\-time processing: Number of visits

* Image processing: Enhancement request counts and image processing usage, grouped by space for batch processing and by domain for real\-time image processing.

## Procedure

1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Utilization insights** \> **Usage** on the left navigation bar.

3. Select the relevant tab: **Bandwidth and Traffic**, **Media assets**, **Transcoding**, **Screenshot and Frame extraction**, **Quality enhancement**, **Media AI**, **Smart subtitling**, **Video editing**, **Real\-time processing**, or **Image processing**. Adjust the filters to refine your search.

   > **Note**

   * > Only usage data for the past two years is available.

   * > Each query can cover a maximum of 93 days.

## Image processing usage

On the **Image processing** tab, select a processing mode:

|Mode |Data and filters |
|---|---|
|**Batch processing** |Includes **Image enhancement** and **Image processing**. Enhancement usage is measured in requests. Image processing provides total, standard processing, and advanced compression usage. Filter by region, space, time range, and aggregation interval. |
|**Real\-time processing** |Includes total, standard processing, and advanced compression usage for image URL requests. Filter by region, domain, time range, and aggregation interval. |

For API queries, use [DescribeVodImageEnhancementData](https://docs.byteplus.com/docs/byteplus-vod/reference-describevodimageenhancementdata) for image enhancement request counts. In [DescribeVodImageCompressionData](https://docs.byteplus.com/docs/byteplus-vod/reference-describevodimagecompressiondata), set `ProcessMode` to `Batch` and use `SpaceList` for batch processing, or use `Realtime` (the default) for domain\-based real\-time processing. `DomainList` and `DetailFieldList` apply only to `Realtime` queries.

For these image usage APIs, the start time must be within the past 366 days, and each query can cover a maximum of 93 days.

For processing instructions, see [Image enhancement and processing](https://docs.byteplus.com/docs/byteplus-vod/docs-image-enhancement).
