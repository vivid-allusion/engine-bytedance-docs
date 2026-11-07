---
title: "DNS-based Routing With Lines"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-intelligent-dns-based-routing"
---

When you create or update DNS records in BytePlus DNS, you can set the geolocation line, ISP line, cloud vendor line, IP\-based line, and line group for a record set. You set lines for record sets to enable DNS\-based routing with lines.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The available line types for your domain depend on the edition of your domain. Please refer to <a href="https://docs.byteplus.com/docs/byteplus-dns-suite/docs-editions">Editions</a>.</div>


* <div data-tips="true" data-tips-type="tip">See <a href="https://docs.byteplus.com/docs/byteplus-dns-suite/docs-priority-in-dns-records">Line matching sequence for DNS queries</a> to learn the sequence BytePlus DNS follows when matching lines for DNS queries.</div>



<span id="what-is-a-line"></span>
## What is a line?

Lines indicate the source of user requests. A line can be defined by ISPs, geolocations, IP ranges, or combinations of ISPs, geolocations, and IP ranges.

If your domain can be resolved to different service IP addresses, and user requests are expected to be routed to an IP address that meet the following requirements to reduce user access latency:


* The ISP of the user's IP address is the same as the ISP of the service IP address.

* The geolocation of the user's IP address is as close to the geolocation of the service IP address.


You can assign a line to a record set that contains one or multiple service IP addresses. Each line represents the ISP, geolocation, or IP range of the service IP addresses in the record set.

When BytePlus DNS receives a DNS query, it gets the client's ISP, geolocation, IP address range, and other information based on the partial client IP address information included in the DNS query. If the client's ISP, geolocation or IP address range matches the line, only IP addresses within the corresponding record set will be included in the DNS response.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">BytePlus DNS prioritizes using the client IP address range included in the ECS protocol information in the query request to match the line. If the user's local DNS server does not support the ECS protocol, BytePlus DNS uses the client IP address in the UDP packet. Most of these client IP addresses are the egress IP addresses of the local DNS server. Refer to <a href="https://docs.byteplus.com/docs/byteplus-dns-suite/docs-how-it-works">How It Works</a> for more information.</div>


<span id="routing-with-geolocation-lines-and-isp-lines"></span>
## Routing with geolocation lines and ISP lines

You can configure different IP addresses for different geolocation lines and ISP lines. This allows users from different ISP lines and geolocation lines to access your services through the lines you have configured.

The network quality worldwide (excluding Chinese mainland) has the following characteristics:


* The network quality when users access IP addresses within the same ISP is superior to the network quality when accessing IP addresses across different ISPs.

* The network quality when users access IP addresses within the same country/region ISP is superior to the network quality when accessing IP addresses across different country/region ISPs.


The network quality in Chinese mainland has the following characteristics:


* The network quality for users accessing IP addresses within the same ISP line is better than accessing IP addresses across different ISP lines.

* The network quality for users accessing IP addresses within the same province and ISP line is better than accessing IP addresses across different provinces and ISP lines.

* The network quality for users accessing IP addresses across different provinces within the same ISP line is better than accessing IP addresses across different ISP lines within the same province.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The default line generally serves as a fallback, matching user requests from all sources. You need to ensure that the default line has corresponding service IP addresses to avoid resolution failures. For example, if some of your service IP addresses use BGP lines, it is recommended that you set the line for the corresponding record set to the default line.</div>


<span id="example"></span>
### Example

Your service has corresponding IP addresses in Singapore and South Korea for a specific ISP. You can create the following DNS records for your domain:


|**Record type** |**Line** |**Record value** |**Description** |
|---|---|---|---|
|A Record |Geolocation line \- Singapore |`203.0.113.1` |For users in Singapore. |
||Geolocation line \- South Korea |`203.0.113.4` |For users in South Korea. |
||Default line |`203.0.113.1`<br><br>`203.0.113.4` |For other users. |


<span id="routing-with-cloud-vendor-lines"></span>
## Routing with cloud vendor lines

Cloud vendor lines are used to identify DNS queries originating from resources of a cloud vendor, such as ECS, or RDS from Volcano Engine. For domains with enterprise, ultimate, and exclusive editions, cloud vendor lines support Alibaba Cloud, Tencent Cloud, Baidu Cloud, Huawei Cloud, and Volcano Engine. If your service IP address is on Volcano Engine, you can configure cloud vendor lines for that service IP address. This way, when receiving DNS queries from Volcano Engine, BytePlus DNS will return the service IP address from Volcano Engine, thereby reducing client access latency.

Cloud vendor resources are distributed across different regions. For domains with ultimate and exclusive editions, cloud vendor lines support Alibaba Cloud, Tencent Cloud, Baidu Cloud, Huawei Cloud, and Volcano Engine, with extra precision to regions/provinces. Therefore, for DNS queries from cloud vendor resources in a specific region, BytePlus DNS can return the service IP address from the same region of the same cloud vendor's resources. This further reduces client access latency.

<span id="example"></span>
### Example

You can refer to the following example. This example assumes your domain's edition is ultimate edition.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The types of cloud vendor lines depend on your domain's edition.</div>


Your service has corresponding IP addresses in both Volcano Engine's East China 1 (Hangzhou) region and Alibaba Cloud's North China 2 (Beijing) region, which are `203.0.113.1` and `203.0.113.2` respectively. You want clients from Volcano Engine East China 1 (Hangzhou) to access `203.0.113.1`, and clients from Alibaba Cloud North China 2 (Beijing) to access `203.0.113.2`.

You can add the following DNS records for your domain:


|**Record type** |**Line** |**Record value** |**Description** |
|---|---|---|---|
|A Record |Cloud vendor line \- Volcano Engine \- East China \- Hangzhou |`203.0.113.1` |For clients from Volcano Engine East China 1 (Hangzhou). |
||Cloud vendor line \- Alibaba Cloud \- North China \- Beijing |`203.0.113.2` |For clients from Alibaba Cloud North China 2 (Beijing). |
| |Default line |`203.0.113.1` |For all other clients. |
|||`203.0.113.2` ||


<span id="routing-with-ip-based-lines"></span>
## Routing with IP\-based lines

With [IP-based lines](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-what-is-an-ip-based-line), you can configure different IP addresses for users from different IP ranges. This allows users from different IP ranges to access your services through the lines you have configured.

<span id="example"></span>
### Example

Your service has corresponding IP addresses in Company A, Company B, and Company C, which are `203.0.113.1`, `203.0.113.2`, and `203.0.113.3`, respectively. At the same time, the IP ranges for each company's users are as follows:


* The IP range for Company A's users is: `203.0.113.1/24`

* The IP range for Company B's users is: `203.0.113.2/22`

* The IP range for Company C's users is: `203.0.113.3/19`


You can add the following IP\-based lines:


|**IP\-based line name** |**Range** |**Description** |
|---|---|---|
|IP\-based Line A |`203.0.113.1/24` |For users from Company A. |
|IP\-based Line B |`203.0.113.2/22` |For users from Company B. |
|IP\-based Line C |`203.0.113.3/19` |For users from Company C. |


Then, you can add the following DNS records for your domain:


|**Record type** |**Line** |**Record value** |**Description** |
|---|---|---|---|
|A Record |IP\-based Line \- IP\-based Line A |`203.0.113.1` |For users from Company A. |
||IP\-based Line \- IP\-based Line B |`203.0.113.2` |For users from Company B. |
||IP\-based Line \- IP\-based Line C |`203.0.113.3` |For users from Company C. |
||Default Line |`203.0.113.1` |For other users. |
|||`203.0.113.2` ||
|||`203.0.113.3` ||


<span id="routing-with-line-groups"></span>
## Routing with line groups

You can combine multiple ISP lines, secondary ISP lines, cloud vendor lines, or geolocation lines and use them as a single line. This feature simplifies line management and configuration, suitable for scenarios where you need to configure multiple lines for a single DNS record.

<span id="example"></span>
### Example

Assume your domain's edition is exclusive edition.

Your service has corresponding IP addresses for Singapore, Japan, and South Korea, which are `203.0.113.1`, `203.0.113.2`, and `203.0.113.3` respectively.

Additionally, your service has the same IP address `203.0.113.4` for Indonesia, Vietnam, Thailand, and Malaysia.

You can add the following line group as an aggregate line:


|**Line group name** |**Lines** |**Description** |
|---|---|---|
|Line Group A |Asia_Indonesia, Asia_Vietnam, Asia_Thailand, Asia_Malaysia |Line group for Indonesia, Vietnam, Thailand, and Malaysia |


You can create the following DNS records for your domain:


|**Record type** |**Line** |**Record value** |**Description** |
|---|---|---|---|
|A Record |Geolocation line \- Asia_Singapore |`203.0.113.1` |For users from Singapore. |
||Geolocation line \- Asia_Japan |`203.0.113.2` |For users from Japan. |
||Geolocation line \- Asia_South Korea |`203.0.113.3` |For users from South Korea. |
||Line group \- Line Group A |`203.0.113.4` |For users from Indonesia, Vietnam, Thailand, and Malaysia. |
||Default Line |`203.0.113.1` |For all other users. |
|||`203.0.113.2` ||
|||`203.0.113.3` ||
|||`203.0.113.4` ||


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If a DNS record is configured with both ISP/geolocation/cloud vendor lines and aggregate lines, and one of the lines included in the aggregate line is the same as one of the ISP/geolocation/cloud vendor lines configured for that DNS record, when these two lines are hit, BytePlus DNS will deduplicate identical record values in the record sets corresponding to the lines. Depending on whether load balancing is enabled for the record sets corresponding to the lines, BytePlus DNS returns record values differently:</div>



* <div data-tips="true" data-tips-type="tip">If load balancing is enabled for the record set corresponding to either line, when these two lines are hit, BytePlus DNS will return a record value according to the weight ratio of record values in the two record sets. For record values without a set weight, the default weight is 1.</div>


* <div data-tips="true" data-tips-type="tip">If load balancing is not enabled for both record sets, when these two lines are hit, BytePlus DNS will return all record values from both record sets at once.</div>
