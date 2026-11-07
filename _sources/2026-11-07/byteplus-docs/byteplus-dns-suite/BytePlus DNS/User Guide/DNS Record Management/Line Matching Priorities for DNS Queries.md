---
title: "Line Matching Priorities for DNS Queries"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-priority-in-dns-records"
---

In BytePlus DNS, you can configure different lines for different record sets. For DNS queries from different lines, BytePlus DNS will include record values from different record sets in the DNS response.

When receiving a DNS query, BytePlus DNS matches the lines in the following order from top to bottom. If a match is successful, BytePlus DNS will stop further matching; if a match fails, BytePlus DNS will continue to match downwards. The default line is used as a fallback and can match DNS queries from any source.

<span id="line-matching-sequence-for-dns-queries-from-global-excluding-chinese-mainland"></span>
## Line matching sequence for DNS queries from global (excluding Chinese mainland)

For DNS queries from global (excluding Chinese mainland), the line matching sequence is as follows:


1. IP\-based lines

2. ISP lines/Cloud vendor lines \- ISP/Cloud vendor \- Global (excluding Chinese mainland) Continent \- Country or Region \- (United States) State, (Vietnam) Province

3. ISP lines/Cloud vendor lines \- ISP/Cloud vendor \- Global (excluding Chinese mainland) Continent \- Country or Region

4. ISP lines/Cloud vendor lines \- ISP/Cloud vendor

5. Geolocation lines \- Global (excluding Chinese mainland) \- Continent \- Country or Region \- (US) Region \- (US) State, (Vietnam) Province

6. Geolocation lines \- Global (excluding Chinese mainland) \- Continent \- Country or Region \- (US) Region, (Vietnam) Province

7. Geolocation lines \- Global (excluding Chinese mainland) \- Continent \- Country or Region

8. Geolocation lines \- Global (excluding Chinese mainland) \- Continent

9. Geolocation lines \- Global (excluding Chinese mainland)

10. Default line


<span id="line-matching-sequence-for-dns-queries-from-chinese-mainland"></span>
## Line matching sequence for DNS queries from Chinese mainland

For DNS queries from Chinese mainland, the line matching sequence is as follows:


1. IP\-based lines

2. ISP lines/Cloud vendor lines \- ISP/Cloud vendor \- Chinese mainland \- Region \- Province

3. Geolocation lines \- Chinese mainland \- Region \- Province

4. ISP lines/Cloud vendor lines \- ISP/Cloud vendor \- Chinese mainland \- Region

5. Geolocation lines \- Chinese mainland \- Region

6. ISP lines/Cloud vendor lines \- ISP/Cloud vendor

7. Geolocation lines \- Chinese mainland

8. Default line


<span id="example"></span>
## Example

For example, `www.example.com` corresponds to the following multiple DNS records:


|**Record type** |**Record value** |**Line** |
|---|---|---|
|A |`203.0.113.1` |Geolocation line: Global (Excluding Chinese Mainland) \- Asia \- Singapore |
|A |`203.0.113.2` |Default line |


<span id="singapore-user"></span>
### Singapore user

If a Singapore user accesses `www.example.com`, the following multiple lines match:


* Geolocation line: Global (Excluding Chinese Mainland) \- Asia \- Singapore

* Default line


Because the matching sequence of the line **Geolocation line: Global (Excluding Chinese Mainland) \- Asia \- Singapore** is higher than the other line, BytePlus DNS will return the record value `203.0.113.1`.
