---
title: "Live-streaming service fees"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-live-streaming-service-fees"
---

BytePlus MediaLive provides the following billing methods and billing cycles for its live\-streaming service.


|**Billing Method** |**Daily Pay\-As\-You\-Go (Default)**  |**Monthly Pay\-As\-You\-Go** |
|---|---|---|
|Bill by traffic |Supported |Supported |
|Bill by peak bandwidth |Supported |Supported |
|Bill by 95th percentile bandwidth |Not supported |Supported |
|Bill by average daily peak bandwidth |Not supported |Supported |



* After activating the BytePlus MediaLive service, you will be billed on a daily basis by default. You can [Contact your sales representative](https://www.byteplus.com/en/contact) if you want to use a different billing cycle. Additionally, you have the option to modify your billing method through the console. For detailed instructions on changing the billing method, please refer to [Changing the billing method](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-overview#changing-the-billing-method).

* The pricing for upstream traffic in [Real Time Media (RTM)](https://docs.byteplus.com/en/byteplus-media-live/docs/introduction-to-real-time-media) streaming is the same as that of standard streaming. The downstream traffic in RTM streaming is priced differently.

* By default, RTM streaming uses the same billing method and cycle as standard streaming. If you are billed monthly, you can [Contact your sales representative](https://www.byteplus.com/en/contact) to change the billing method for your RTM streaming service if necessary.

* BytePlus MediaLive also provides resource packs that allow you to deduct any consumed traffic, including standard and RTM streaming traffic. For more information on resource packs, refer to [Resource packs](https://docs.byteplus.com/byteplus-media-live/docs/resource-packs).


<span id="Bill by traffic"></span>
## Bill by traffic

If you choose this billing method, you are charged based on the total amount of upstream and downstream traffic used, and fees are calculated by multiplying the total traffic consumed in a day in a billing region by the unit price of the corresponding tier.

> The conversion factor for units of traffic is 1,000. For example, 1 GB = 1,000 MB.


<span id="Pricing (unit: USD/GB)"></span>
### Standard pricing

Unit: USD/GB


|**Traffic** |**The Chinese mainland** |**Asia Pacific 1** |**Asia Pacific 2** |**Asia Pacific 3** |**North America** |**Europe** |**Middle East** |**South America** |
|---|---|---|---|---|---|---|---|---|
|0–10 TB (including 10 TB) |0.034 |0.069 |0.0897 |0.1012 |0.0506 |0.0506 |0.115 |0.115 |
|10–50 TB (including 50 TB) |0.033 |0.0598 |0.0748 |0.0863 |0.0414 |0.0414 |0.1093 |0.1093 |
|50–100 TB (including 100 TB) |0.03 |0.0529 |0.069 |0.0748 |0.0322 |0.0322 |0.0978 |0.0978 |
|100 TB – 1 PB (including 1 PB) |0.026 |0.0483 |0.0575 |0.0667 |0.0253 |0.0253 |0.092 |0.092 |
|\> 1 PB |0.021 |0.046 |0.0518 |0.0621 |0.0219 |0.0219 |0.0863 |0.0863 |


<span id="c1116be3"></span>
#### Billing example

Throughout November, User A consumed 9 TB upstream traffic on November 10th and 10 TB downstream traffic on November 11th, both of which took place in North America.


* The first 10 TB falls under the 0–10 TB tier and is charged at a rate of 0.0506 USD/GB.

* The remaining 9 TB falls under the 10–50 TB tier and is charged at a rate of 0.0414 USD/GB.


The fees are calculated as follows:


* For November 10th, the 9 TB falls under the 0–10 TB tier, so the total is 9 × 1,000 × 0.0506 = 455.4 USD.

* For November 11th, the first 1 TB falls under the 0–10 TB tier and the remaining 9 TB falls under the 10–50 TB tier, so the total is (1 × 1000 × 0.0506) + (9 × 1000 × 0.0414) = 423.2 USD.


<span id="4fe5cb68"></span>
### Pricing for RTM stream pulling

Unit: USD/GB


|**Traffic** |**The Chinese mainland** |**Asia Pacific 1** |**Asia Pacific 2** |**Asia Pacific 3** |**North America** |**Europe** |**Middle East** |**South America** |
|---|---|---|---|---|---|---|---|---|
|0–10 TB (including 10 TB) |0.068 |0.138 |0.1794 |0.2024 |0.1012 |0.1012 |0.23 |0.23 |
|10–50 TB (including 50 TB) |0.066 |0.1196 |0.1496 |0.1726 |0.0828 |0.0828 |0.2186 |0.2186 |
|50–100 TB (including 100 TB) |0.06 |0.1058 |0.138 |0.1496 |0.0644 |0.0644 |0.1956 |0.1956 |
|100 TB – 1 PB (including 1 PB) |0.052 |0.0966 |0.115 |0.1334 |0.0506 |0.0506 |0.184 |0.184 |
|\> 1 PB |0.042 |0.092 |0.1036 |0.1242 |0.0438 |0.0438 |0.1726 |0.1726 |


<span id="e8ae85c3"></span>
#### Billing example

Throughout November, User A consumed 9 TB RTM downstream traffic on November 10th and 10 TB RTM downstream traffic on November 11th, both of which took place in North America.


* The first 10 TB falls under the 0–10 TB tier and is charged at a rate of 0.1012 USD/GB.

* The remaining 9 TB falls under the 10–50 TB tier and is charged at a rate of 0.0828 USD/GB.


The fees are calculated as follows:


* For November 10th, the 9 TB falls under the 0–10 TB tier, so the total is 9 × 1,000 × 0.1012 = 910.8 USD.

* For November 11th, the first 1 TB falls under the 0–10 TB tier and the remaining 9 TB falls under the 10–50 TB tier, so the total is (1 × 1000 × 0.1012) + (9 × 1000 × 0.0828) = 846.4 USD.


<span id="Bill by peak bandwidth"></span>
## Bill by peak bandwidth

If you choose this billing method, you are charged based on daily peak bandwidth (including both upstream and downstream), and fees are calculated by multiplying peak bandwidth consumed in a day in a billing region by the unit price of the corresponding tier.

> The conversion factor for units of bandwidth is 1,000. For example, 1 Gbps = 1,000 Mbps.


<span id="Pricing (unit: USD/Mbps/Day)"></span>
### Standard pricing

Unit: USD/Mbps/Day


|**Daily Peak Bandwidth** |**The Chinese mainland** |**Asia Pacific 1** |**Asia Pacific 2** |**Asia Pacific 3** |**North America** |**Europe** |**Middle East** |**South America** |
|---|---|---|---|---|---|---|---|---|
|0–500 Mbps (including 500 Mbps) |0.094 |0.3335 |0.3757 |0.4217 |0.1648 |0.1648 |0.6555 |0.575 |
|500 Mbps – 5 Gbps (including 5 Gbps) |0.086 |0.2913 |0.3258 |0.368 |0.1418 |0.1418 |0.5903 |0.4983 |
|5–20 Gbps (including 20 Gbps) |0.083 |0.2492 |0.276 |0.3143 |0.1227 |0.1227 |0.5252 |0.4255 |
|\> 20 Gbps |0.08 |0.2262 |0.253 |0.2875 |0.1112 |0.1112 |0.4907 |0.3795 |


<span id="2ac5181b"></span>
#### Billing example

The peak bandwidth of User A on November 10th and November 11th were both 3.5 Gbps, and the traffic took place in North America.

Since 3.5 Gbps falls under the 500 Mbps – 5Gbps (including 5 Gbps) tier, User A is charged the price of 0.1418 USD/Mbps/Day.

Thus, the fee User A should pay each day is 3.5 × 1,000 × 0.1418 × 1 = 496.3 USD.

<span id="52ca9621"></span>
### Pricing for RTM stream pulling

Unit: USD/Mbps/Day


|**Daily Peak Bandwidth** |**The Chinese mainland** |**Asia Pacific 1** |**Asia Pacific 2** |**Asia Pacific 3** |**North America** |**Europe** |**Middle East** |**South America** |
|---|---|---|---|---|---|---|---|---|
|0–500 Mbps (including 500 Mbps) |0.188 |0.667 |0.7514 |0.8434 |0.3296 |0.3296 |1.311 |1.15 |
|500 Mbps – 5 Gbps (including 5 Gbps) |0.172 |0.5826 |0.6516 |0.736 |0.2836 |0.2836 |1.1806 |0.9966 |
|5–20 Gbps (including 20 Gbps) |0.166 |0.4984 |0.552 |0.6286 |0.2454 |0.2454 |1.0504 |0.851 |
|\> 20 Gbps |0.16 |0.4524 |0.506 |0.575 |0.2224 |0.2224 |0.9814 |0.759 |


<span id="ad6675e4"></span>
#### Billing example

The peak downstream bandwidth of User A on November 10th and November 11th were both 3.5 Gbps, and the traffic took place in North America.

Since 3.5 Gbps falls under the 500 Mbps – 5Gbps (including 5 Gbps) tier, User A is charged the price of 0.2836 USD/Mbps/Day.

Thus, the fee User A should pay each day is 3.5 × 1,000 × 0.2836 × 1 = 992.6 USD.

<span id="Bill by 95th percentile bandwidth"></span>
## Bill by 95th percentile bandwidth

If you choose this billing method, you are charged based on the 95th percentile bandwidth (including both upstream and downstream), and fees are calculated in the following formula: 95th percentile bandwidth × Unit price of the corresponding tier × Effective factor.


* 95th percentile bandwidth: Collect the bandwidth value every 5 minutes throughout a calendar month, and exclude the highest 5%. The highest rate among the remainder is the 95th percentile bandwidth.

* Effective factor: Divide the number of days in a calendar month when the BytePlus MediaLive service is enabled by the total number of days of that month. The quotient is the effective factor.


<span id="Pricing (unit: USD/Mbps/Month)"></span>
### Standard pricing

Unit: USD/Mbps/Month


|**95th Percentile Bandwidth** |**The Chinese mainland** |**Asia Pacific 1** |**Asia Pacific 2** |**Asia Pacific 3** |**North America** |**Europe** |**Middle East** |**South America** |
|---|---|---|---|---|---|---|---|---|
|0–500 Mbps (including 500 Mbps) |2.829 |10.005 |11.27 |12.65 |4.945 |4.945 |19.665 |17.25 |
|500 Mbps – 5 Gbps (including 5 Gbps) |2.734 |8.74 |9.775 |11.04 |4.255 |4.255 |17.71 |14.95 |
|5–20 Gbps (including 20 Gbps) |2.64 |7.475 |8.28 |9.43 |3.68 |3.68 |15.755 |12.765 |
|\> 20 Gbps |2.546 |6.785 |7.59 |8.625 |3.335 |3.335 |14.72 |11.385 |


<span id="Billing example"></span>
#### Billing example

User A started to use the service on November 16th and was billed by 95th percentile bandwidth till the end of the month.


* User A used the service for 15 days in November, and the bandwidth value was collected every 5 minutes or 12 times per hour. The total number of bandwidth values collected in November was thus 15 × 24 × 12 = 4,320. After these values were placed in descending order and the top 216 (4,320 × 5%) were excluded, the 217th value was the 95th percentile bandwidth.

* Suppose the 95th percentile bandwidth was 3.5 Gbps. In that case, the bandwidth falls under the 500 Mbps – 5 Gbps tier, with a unit price of 4.255 USD/Mbps/Month.

* The effective factor is 15 / 30 = 0.5.


Thus, the fee that User A should pay in November was 3.5 × 1000 × 4.255 × 0.5 = 7446.25 USD.

<span id="21ff51be"></span>
### Pricing for RTM stream pulling

Unit: USD/Mbps/Month


|**95th Percentile Bandwidth** |**The Chinese mainland** |**Asia Pacific 1** |**Asia Pacific 2** |**Asia Pacific 3** |**North America** |**Europe** |**Middle East** |**South America** |
|---|---|---|---|---|---|---|---|---|
|0–500 Mbps (including 500 Mbps) |5.658 |20.01 |22.54 |25.3 |9.89 |9.89 |39.33 |34.5 |
|500 Mbps – 5 Gbps (including 5 Gbps) |5.468 |17.48 |19.55 |22.08 |8.51 |8.51 |35.42 |29.9 |
|5–20 Gbps (including 20 Gbps) |5.28 |14.95 |16.56 |18.86 |7.36 |7.36 |31.51 |25.53 |
|\> 20 Gbps |5.092 |13.57 |15.18 |17.25 |6.67 |6.67 |29.44 |22.77 |


<span id="6a34b237"></span>
#### Billing example

User A started to use the service on November 16th and was billed by 95th percentile bandwidth till the end of the month.


* User A used the service for 15 days in November, and the downstream bandwidth value was collected every 5 minutes or 12 times per hour. The total number of bandwidth values collected in November was thus 15 × 24 × 12 = 4,320. After these values were placed in descending order and the top 216 (4,320 × 5%) were excluded, the 217th value was the 95th percentile bandwidth.

* Suppose the 95th percentile bandwidth was 3.5 Gbps. In that case, the bandwidth falls under the 500 Mbps – 5 Gbps tier, with a unit price of 8.51 USD/Mbps/Month.

* The effective factor is 15 / 30 = 0.5.


Thus, the fee that User A should pay in November was 3.5 × 1000 × 8.51 × 0.5 = 14892.5 USD.

<span id="Bill by average daily peak bandwidth"></span>
## Bill by average daily peak bandwidth

If you choose this billing method, you are charged based on average daily peak bandwidth (including both upstream and downstream), and fees are calculated in the following formula: Average daily peak bandwidth × Unit price of the corresponding tier × Effective factor.


* Average daily peak bandwidth: Add up the peak bandwidth of each day in a calendar month, and divide the sum by the number of days to get the average daily peak bandwidth.

* Effective factor: Divide the number of days in a calendar month when the BytePlus MediaLive service is enabled by the total number of days of that month. The quotient is the effective factor.


<span id="Pricing (unit: USD/Mbps/Month)"></span>
### Standard pricing

Unit: USD/Mbps/Month


|**Daily Peak Bandwidth** |**The Chinese mainland** |**Asia Pacific 1** |**Asia Pacific 2** |**Asia Pacific 3** |**North America** |**Europe** |**Middle East** |**South America** |
|---|---|---|---|---|---|---|---|---|
|0–1 Gbps (including 500 Mbps) |2.6593 |9.4047 |10.5938 |11.891 |4.6483 |4.6483 |18.4851 |16.215 |
|1–10 Gbps (including 5 Gbps) |2.57 |8.2156 |9.1885 |10.3776 |3.9997 |3.9997 |16.6474 |14.053 |
|10–20 Gbps (including 20 Gbps) |2.4816 |7.0265 |7.7832 |8.8642 |3.4592 |3.4592 |14.8097 |11.9991 |
|\> 20 Gbps |2.3932 |6.3779 |7.1346 |8.1075 |3.1349 |3.1349 |13.8368 |10.7019 |


<span id="Billing example"></span>
#### Billing example

User A started to use the service on November 29th, and the peak bandwidth on November 29th and November 30th were 2.5 Gbps and 3.5 Gbps, respectively. The traffic took place in North America.


* The average daily peak bandwidth is (2.5 + 3.5) / 2 = 3 Gbps.

* Since 3 Gbps falls under the 1–10 Gbps (including 5 Gbps) tier, User A is charged the price of 3.9997 USD/Mbps/Month.

* The effective factor is 2 / 30 = 0.0667


Thus, the fee that User A should pay in November is 3 × 1,000 × 3.9997 × 0.0667 = 800.34 USD.

<span id="ccd97221"></span>
### Pricing for RTM stream pulling

Unit: USD/Mbps/Month


|**Daily Peak Bandwidth** |**The Chinese mainland** |**Asia Pacific 1** |**Asia Pacific 2** |**Asia Pacific 3** |**North America** |**Europe** |**Middle East** |**South America** |
|---|---|---|---|---|---|---|---|---|
|0–1 Gbps (including 500 Mbps) |5.3186 |18.8094 |21.1876 |23.782 |9.2966 |9.2966 |36.9702 |32.43 |
|1–10 Gbps (including 5 Gbps) |5.14 |16.4312 |18.377 |20.7552 |7.9994 |7.9994 |33.2948 |28.106 |
|10–20 Gbps (including 20 Gbps) |4.9632 |14.053 |15.5664 |17.7284 |6.9184 |6.9184 |29.6194 |23.9982 |
|\> 20 Gbps |4.7864 |12.7558 |14.2692 |16.215 |6.2698 |6.2698 |27.6736 |21.4038 |


<span id="a3e8a579"></span>
#### Billing example

User A started to use the service on November 29th, and the peak downstream bandwidth on November 29th and November 30th were 2.5 Gbps and 3.5 Gbps, respectively. The traffic took place in North America.


* The average daily peak bandwidth is (2.5 + 3.5) / 2 = 3 Gbps.

* Since 3 Gbps falls under the 1–10 Gbps (including 5 Gbps) tier, User A is charged the price of 7.9994 USD/Mbps/Month.

* The effective factor is 2 / 30 = 0.0667


Thus, the fee that User A should pay in November is 3 × 1,000 × 7.9994 × 0.0667 = 1600.68 USD.
