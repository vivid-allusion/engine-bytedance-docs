---
title: "Security"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/security"
---

This topic summarizes frequently asked questions about RDS for PostgreSQL security.

<span id=".UG9zdGdyZVNRTCDlrp7kvovlv4Xpobvorr7nva4gSVAg55m95ZCN5Y2V5YiG57uE5ZCX77yf"></span>
#### Is an IP address allowlist required for PostgreSQL instances?

Yes, because the default IP address allowlist only contains `127.0.0.1`, meaning that no IP addresses are allowed to access this PostgreSQL instance. For more details, refer to [Creating an allowlist](https://docs.byteplus.com/en/docs/RDS_for_PG/adding_an_ip_address_allowlist). 

<span id=".5Y2V5Liq5a6e5L6L5pyA5aSa5pSv5oyB5aSa5bCR5LiqIElQIOeZveWQjeWNleWIhue7hO-8jOavj-S4quWIhue7hOacgOWkmuaUr-aMgeWkmuWwkSBJUCDmiJbogIUgSVAg5q6177yf"></span>
#### How many IP address allowlists does an instance support at the maximum? How many IP addresses or segments does an allowlist support at the maximum?

An instance supports up to 50 IP address allowlists, and each allowlist supports up to 20 IP addresses or segments. For more details, refer to [Creating an allowlist](https://docs.byteplus.com/en/docs/RDS_for_PG/adding_an_ip_address_allowlist).
