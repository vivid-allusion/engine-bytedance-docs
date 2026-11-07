---
title: "Pay-as-you-go pricing"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-pay-as-you-go-pricing"
---

This page introduces the pricing details of BytePlus VOD.

## Media storage

### Storage pricing

The amount you are charged for storing media files in the BytePlus VOD service is determined by the size of your media, the duration of storage, and the storage class you choose. Billing is based on the peak daily media storage usage, and invoices are issued daily.

|**Storage class** |**Price (Unit: USD/GiB/Month)**  |
|---|---|
|Standard storage |0.017 |

* **Formula:**  Daily media asset storage fee = Peak media storage usage x Storage unit price / 30.

* **Base:**  Media storage is measured using binary prefixes (powers of 1024). A unit of 1,024^3 bytes is a gibibyte (GiB). For consistency with industry standards, this document uses GiB for storage calculations.

* **Pricing example:**  If User A stored 300 GiB of media assets in December 2024, the charges for that month would be 300 GiB x 0.017 USD/GiB/Month = 5.1 USD.

### Storage outbound traffic pricing

You are charged for video files downloaded or played, and images previewed, from the BytePlus VOD storage address via public access (without acceleration from the BytePlus VOD CDN). Billing is based on the outbound traffic.

> **Note**

> This fee applies if you have not [configured an acceleration domain](https://docs.byteplus.com/docs/byteplus-vod/docs-domain-name-management) in the VOD. After configuring an acceleration domain, you will be charged for [Distribution acceleration](https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing#ef8c310c).

|**Billing item** |**Price (Unit: USD/GB)**  |
|---|---|
|Storage outbound traffic |0.08 |

* **Formula:**  Storage outbound traffic fee = Storage outbound traffic x Unit price.

* **Base:**  Traffic is measured using decimal prefixes (powers of 1000), where 1 GB equals 1,000 MB.

* **Pricing example:**  If User A downloaded 300 GB of video files in December 2025, the charges for that month would be 300 GB x 0.08 USD/GB = 24 USD.

## **Media processing**

### Transcoding pricing

You are charged for transcoding media files per minute for each output video. The per\-minute rate varies depending on the specific transcoding features that you use, as well as the codec and resolution of the output files.

> **Note**

> BytePlus VOD does not charge for failed transcodes.

|**Transcoding tier** ||**Price (Unit: USD/Minute)**  |
|---|---|---|
|Audio\-only transcoding |N/A |0.0019 |
|Remuxing |N/A |0.002 |
|Video transcoding (H.264) |4K (≤ 3840 x 2160 px) |0.0495 |
||2K (≤ 2560 x 1440 px) |0.023 |
||FHD (≤ 1920 x 1080 px) |0.0115 |
||HD (≤ 1280 x 720 px) |0.0058 |
||SD (≤ 640 x 480 px) |0.0029 |
|Video transcoding (H.265) |4K (≤ 3840 x 2160 px) |0.2395 |
||2K (≤ 2560 x 1440 px) |0.1197 |
||FHD (≤ 1920 x 1080 px) |0.0599 |
||HD (≤ 1280 x 720 px) |0.0299 |
||SD (≤ 640 x 480 px) |0.015 |
|Low\-bitrate HD transcoding (H.264) |4K (≤ 3840 x 2160 px) |0.1635 |
||2K (≤ 2560 x 1440 px) |0.076 |
||FHD (≤ 1920 x 1080 px) |0.038 |
||HD (≤ 1280 x 720 px) |0.019 |
||SD (≤ 640 x 480 px) |0.0095 |
|Low\-bitrate HD transcoding (H.265) |4K (≤ 3840 x 2160 px) |0.7903 |
||2K (≤ 2560 x 1440 px) |0.3952 |
||FHD (≤ 1920 x 1080 px) |0.1976 |
||HD (≤ 1280 x 720 px) |0.0988 |
||SD (≤ 640 x 480 px) |0.0494 |

**Pricing example**: Let's consider a scenario where a user performed video transcoding using the H.264 codec. The output files included resolutions of 2560 × 1440 and 1920 × 1080, each with a duration of 100 minutes. The total cost for media processing would be calculated as follows: 0.023 USD/minute x 100 minutes + 0.0115 USD/minute x 100 minutes = 3.45 USD.

### Video enhancement pricing

Billing for video enhancement is based on the output duration of the processed video, the selected enhancement tier, the output resolution, and the output frame rate. The unit for all prices is **USD per minute** of processed video output.

> **Note**

> Output resolutions lower than 720P are billed at the 720P rate.

|Enhancement tier |Resolution |Price (≤ 30fps) |Price (\> 30fps and ≤ 60fps) |Price (\> 60fps and ≤ 120fps) |
|---|---|---|---|---|
|Fast |720P |0.1033 |0.2066 |0.4132 |
||1080P |0.2066 |0.4132 |0.8264 |
||2K |0.4132 |0.8264 |1.6528 |
||4K |0.8264 |1.6528 |3.3056 |
||6K |1.6528 |3.3056 |6.6112 |
||8K |3.3056 |6.6112 |13.2224 |
|Standard |720P |0.2066 |0.4132 |0.8264 |
||1080P |0.4132 |0.8264 |1.6528 |
||2K |0.8264 |1.6528 |3.3056 |
||4K |1.6528 |3.3056 |6.6112 |
||6K |3.3056 |6.6112 |13.2224 |
||8K |6.6112 |13.2224 |26.4448 |
|Pro |720P |2.0661 |4.1322 |8.2644 |
||1080P |4.1322 |8.2644 |16.5288 |
||2K |8.2644 |16.5288 |33.0576 |
||4K |16.5288 |33.0576 |66.1152 |
||6K |33.0576 |66.1152 |132.2304 |
||8K |66.1152 |132.2304 |264.4608 |

**Pricing example**: Suppose you process two videos with an output resolution of 1080P and an output frame rate of 60fps: a 10\-minute video using the Fast tier and a 20\-minute video using the Pro tier. Since 60fps falls into the \> 30fps and ≤ 60fps billing range, the corresponding prices are 0.4132 USD/minute for Fast and 8.2644 USD/minute for Pro. The total cost would be calculated as follows: 0.4132 USD/minute × 10 minutes + 8.2644 USD/minute × 20 minutes = 169.42 USD.

### Image processing pricing

Image processing fees are calculated based on the following two processing tiers.

|**Processing tier** |**Price (Unit: USD/GiB)**  |
|---|---|
|Standard processing |0.0034 |
|Advanced compression |0.045 |

* **Formula:**  Total processing fee = Standard processing fee + Advanced compression fee

   > **Note**

   > Advanced compression applies exclusively to AVIF conversions and is billed based on the data saved. Conversions to other standard formats are not subject to advanced compression fees.

* **Base:**  The processing volume is calculated in GiB, using the standard binary prefix system (where 1 TiB = 1,024 GiB, 1 GiB = 1,024 MB).

* **Standard processing:**  Billed at a fixed price per GiB of original image size processed, calculated cumulatively. This includes all image processing features except for converting images to the AVIF format.

   * **Formula:**  Standard processing fee = Total original image size × Unit price

   * **Pricing example:**  If User A generated 2 TiB of image processing usage (total original image size) during the billing cycle from 2026\-01\-01 00:00:00 to 2026\-01\-01 23:59:59, the image processing cost would be: 2 x 1,024 x 0.0034 USD = 6.9632 USD.

   > **Note**

   * > Charges are incurred only for the original image size processed, regardless of the output image size.

   * > Each transformation applied to an image incurs a separate processing charge.

* **Advanced compression:**  Billed based on the amount of data saved during compression. This refers specifically to the process of converting images to the AVIF format.

   * **Formula:**  Advanced compression fee = (Original image size \- Output image size) × Unit price

   * **Pricing example:**  If User A converted 30 GiB images from JPG to AVIF format, and the output image size was 12 GiB, the image processing cost would be: (30 GiB \- 12 GiB) x 0.045 USD/GiB = 0.81 USD.

   > **Note**

   > When converting an image to the AVIF format, any associated standard processing operations (such as cropping or resizing) applied to that image are **not charged separately**.

### Image enhancement pricing

[Image enhancement](https://docs.byteplus.com/docs/byteplus-vod/docs-image-enhancement) is billed by the number of successful enhancement requests, at **USD 9.6 per 1,000 requests**.

* **Formula:**  Image enhancement fee = Successful requests ÷ 1,000 × USD 9.6.

* **Example:**  2,500 successful requests cost 2,500 ÷ 1,000 × USD 9.6 = USD 24.

Image previews that use an external storage address are billed as [storage outbound traffic](https://docs.byteplus.com/en/docs/25/7848#storage-outbound-traffic-pricing).

### Smart subtitling pricing

Smart subtitling is billed at a fixed rate per usage unit, calculated cumulatively throughout the billing cycle.

|**Feature** |**Price** |**Usage Unit** |
|---|---|---|
|Speech\-to\-text |0.057 USD / Minute |Minute |
|Machine translation |6.72 USD / Million characters |Million characters |

**Pricing example**: If User A processed 10,000 minutes of speech\-to\-text and 5 million characters of machine translation during the billing cycle from 2025\-01\-01 00:00:00 to 2025\-01\-30 23:59:59, the total bill would be: (10,000 minutes x 0.057 USD/minute) + (5 million characters x 6.72 USD/million characters) = 603.6 USD.

### Precision erasure pricing

Fees for precision erasure are calculated based on the actual duration of the output video.

|**Billing item** |**Price(Unit: USD/Minute)**  |
|---|---|
|Precision erasure |2 |

* **Formula:**  Precision erasure fee = Output video duration x Unit price.

* **Pricing example:**  If User A processes 30 minutes of video files on a given day, the precision erasure charge for that day would be 30 minutes x 2 USD/minute = 60 USD.

### Face mosaic pricing

Fees for face mosaic are calculated based on the duration of the video.

|**Billing item** |**Price(Unit: USD/Minute)**  |
|---|---|
|Face mosaic |0.15 |

* Formula: Face mosaic fee = Video duration × Unit price.

* Pricing example: If User A processes 30 minutes of video files on a given day, the face mosaic charge for that day would be 30 minutes × 0.15 USD/minute = 4.5 USD.

### Frame extraction pricing

Frame extraction is billed by the number of frames extracted. The unit price is USD 0.014 per thousand frames.

|**Billing item** |**Price (Unit: USD / Thousand frames)**  |
|---|---|
|Frame extraction |0.014 |

* **Formula:**  Frame extraction fee = (Total number of extracted frames / 1000) × Unit price

* **Pricing example:**  If User A extracted a total of 500,000 frames from various videos during a billing cycle, the frame extraction cost would be calculated as follows: (500,000 / 1,000) × 0.014 USD = 7 USD.

### Scene segmentation pricing

Fees for scene segmentation are calculated based on the duration of the input source file.

|**Billing item** |**Price(Unit: USD/Minute)**  |
|---|---|
|Scene segmentation |0.03 |

* **Formula:**  Scene segmentation fee = Input source file duration x Unit price.

* **Pricing example:**  If User A processes 30 minutes of video files on a given day, the scene segmentation charge for that day would be 30 minutes x 0.03 USD/minute = 0.9 USD.

### Voice and background audio separation pricing

Fees for voice and background audio separation are calculated based on the duration of the input source file.

|**Billing item** |**Price(Unit: USD/Minute)**  |
|---|---|
|Voice and background audio separation |0.01 |

* **Formula:**  Voice and background audio separation fee = Input source file duration x Unit price.

* **Pricing example:**  If User A processes 30 minutes of audio or video files on a given day, the voice and background audio separation charge for that day would be 30 minutes x 0.01 USD/minute = 0.3 USD.

## Video editing

The amount you are charged for video editing is calculated based on resolution and duration.

|**Resolution** |**Price (Unit: USD/Minute)**  |
|---|---|
|4K (≤ 3840 x 2160) |0.0336 |
|2K (≤2560 x 1440) |0.0168 |
|1080P (≤1920 x 1080) |0.0084 |
|720P (≤1280 x 720) |0.0042 |
|480P (≤640 x 480) |0.0021 |

* **Formula:**  Video editing fee = Duration of output files x Resolution unit price

* **Pricing example:**  If User A processed 300 minutes of 1080P videos and 200 minutes of 2K videos in January 2025, the charges for that month would be (300 minutes x 0.0084 USD/Minute) + (200 minutes x 0.0168 USD/Minute) = 5.88 USD.

## Distribution acceleration

> **Note**

> Currently, we use a tiered pricing structure for distribution acceleration, with costs based on traffic volume. If you wish to switch to a different billing method for the distribution acceleration service, such as billing based on peak bandwidth, please reach out to your [sales representative](https://www.byteplus.com/en/contact).

BytePlus VOD charges for data transferred over the BytePlus network. Adding a domain name incurs distribution acceleration fees. The distribution acceleration fee is calculated hourly for each billing region. To calculate your hourly cost, we determine your price tier based on your total cumulative traffic for the current calendar month. This tier's rate is then applied to the traffic you consumed in that hour. Higher usage results in a lower unit price.

The following table outlines the traffic tiers and corresponding prices in USD / GB for each billing region:

|**Traffic tier** |**Chinese Mainland** |**Asia Pacific 1** |**Asia Pacific 2** |**Asia Pacific 3** |**North America** |**Europe** |**Middle East and Africa** |**South America** |
|---|---|---|---|---|---|---|---|---|
|0 \- 10 TB (including 10 TB) |0.035 |0.06 |0.078 |0.088 |0.044 |0.044 |0.1 |0.1 |
|10 \- 50 TB (including 50 TB) |0.033 |0.052 |0.065 |0.075 |0.036 |0.036 |0.095 |0.095 |
|50 \- 100 TB (including 100 TB) |0.028 |0.046 |0.06 |0.065 |0.028 |0.028 |0.085 |0.085 |
|100 TB \- 1 PB (including 1 PB) |0.025 |0.042 |0.05 |0.058 |0.022 |0.022 |0.08 |0.08 |
|More than 1 PB |0.024 |0.04 |0.045 |0.054 |0.019 |0.019 |0.075 |0.075 |

* **Base:**  Traffic is calculated in units of 1,000, where 1 PB = 1,000 TB = 1,000 × 1,000 GB.

* **Settlement explanation:**  Billing follows a T+1 cycle, where charges for the previous day are finalized and deducted at approximately 18:00:00 on the current day.

* **Traffic statistics:**  Traffic is measured as the downstream data transferred from an edge node in response to a user request. Traffic is billed according to the region of the edge node that serves the request. For specific billing dates and details, refer to your monthly invoice.

* **Pricing example:**  If User A consumes 9,960 GB of traffic in the Asia Pacific 1 region on a given day, and the cumulative traffic for the month is also 9,960 GB, this usage falls within the 0\-10 TB tier. The resulting cost would be: 9,960 GB x 0.06 USD/GB = 597.6 USD.
