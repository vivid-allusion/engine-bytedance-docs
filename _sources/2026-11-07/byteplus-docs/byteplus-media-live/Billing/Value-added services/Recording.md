---
title: "Recording"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-transcoding_2"
---

You will be charged both recording and storage fees when using the recording service. This page introduces how recording fees are charged.

<span id="Pricing (unit: USD/minute)"></span>
## Pricing

The unit price is 0.1676 USD/Stream/Day.

<span id="31e726f0"></span>
## Billing cycle

Recording supports both daily and monthly pay\-as\-you\-go.

<span id="8db5a702"></span>
## Billing details

The recording fees are calculated by multiplying the daily peak number of concurrent recording streams by the unit price.

The number of concurrent recording streams is counted every five minutes. The daily peak is determined by the highest count within a day.

Each recording format is considered a separate recording stream. For instance, if you record the same stream in both MP4 and HLS formats, each format will be counted as an individual recording stream.

<span id="Billing cycle"></span>
## Billing example

Suppose the streams under domain name A are recorded in one file format, and those under domain name B are recorded in two file formats.


* Under domain name A: on November 2nd, 20 live streams were pushed. On November 3rd, 10 live streams were pushed.

* Under domain name B: on November 3rd, 20 live streams were pushed.


The daily peak number of concurrent recording streams is calculated as follows:


* For November 2nd: 20 streams under domain name A × 1 format + 0 streams under domain name B × 2 formats = 20 streams.

* For November 3rd: 10 streams under domain name A × 1 format + 20 streams under domain name B × 2 formats = 50 streams.


Based on the above calculations, the recording fees can be determined as follows:


* For November 2nd: 0.1676 × 20 streams = 3.352 USD.

* For November 3rd: 0.1676 × 50 streams = 8.38 USD.


Fees will be charged once billing is generated the following day.
