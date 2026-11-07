---
title: "High-Availability Virtual IP Address FAQ"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/HAVIP-FAQ"
---

<span id="bOD0DzD8"></span>
## Is there a charge for the High\-Availability Virtual IP Address (HAVIP) service?

Currently, no charges apply for using HAVIPs.

<span id=".5Y2V5Liq56eB5pyJ572R57uc5YaF5pyA5aSa5Y-v5Yib5bu65aSa5bCR5LiqSEFWSVDvvJ8="></span>
## How many HAVIPs can be created within a single VPC?

5.

<span id=".5L2_55SoS2VlcGFsaXZlZOaQreW7uumrmOWPr-eUqOmbhue-pOaXtuWvuUtlZXBhbGl2ZWTniYjmnKzmnInku4DkuYjopoHmsYLvvJ8="></span>
## What are the Keepalived version requirements when building a high\-availability cluster?

We recommend using Keepalived V1.2.24 or later.

<span id=".SEFWSVDnmoTpgJrkv6HmlrnlvI_mmK_ku4DkuYjvvJ8="></span>
## What is the communication method for HAVIP?

HAVIP supports only unicast communication and does not support broadcast or multicast. Therefore, if you use HAVIP with third\-party software (e.g., Keepalived) for high availability, manually adjust the communication method to unicast in the configuration file.

<span id=".5LqR5pyN5Yqh5Zmo6YWN572u5LqGS2VlcGFsaXZlZOS9huacque7keWumkhBVklQ77yM5piv5ZCm5Lya5oqi5Y2gSEFWSVDvvJ8="></span>
## Will ECSs running Keepalived without HAVIP binding preempt the HAVIP?

Yes. HAVIP guarantees only that the MASTER instance state can be detected, not the correctness of Keepalived negotiations. If an ECS not bound to HAVIP is misconfigured with Keepalived, it may illegally occupy the HAVIP.​​

Solution:

Before deploying a high\-availability cluster with HAVIP and Keepalived, verify that the HAVIP configuration aligns with Keepalived settings. Ensure ECSs without HAVIP assignments do not run Keepalived configurations.

<span id=".6YCa6L-H5ZG95Luk6YWN572uSVDmnaXljaDnlKhIQVZJUO-8jOWOu-aOiUlQ5ZCO5piv5ZCm5Lya6L-b6KGM5Li744CB5aSH5YiH5o2i77yf"></span>
## Will manually configuring an IP to occupy the HAVIP trigger an active/standby switchover after removing the IP?

No. HAVIP detects the primary instance (state=MASTER) via ARP packets. If a manually configured IP address occupies the HAVIP, removing this IP will prevent ARP sensing and detection, so the primary instance remains active and master\-slave (active/standby) failover will not be triggered until the next ARP packet exchange.
