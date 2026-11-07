---
title: "Redis 4.0 instances enter EOM phase"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/redis_4_0_enter_eom_phase"
---

To provide you with more stable, secure, and high\-performance services, Cache for Redis plans to adjust the lifecycle of Redis 4.0 instances. Redis 4.0 instances will enter the End of Marketing (EOM) phase starting February 15, 2026, and will reach End of Full Support (EOFS) on February 15, 2027. To ensure business continuity and data security, we recommend you promptly upgrade or migrate your Redis 4.0 instances to a higher version.

<span id="jXbl7M1O"></span>
## Termination plan and impact


|Termination phases |Date (Beijing Time) |Impact |
|---|---|---|
|Stop new purchases |February 15, 2026 |Stop creating new Redis 4.0 instances and subsequent product feature iterations (including new features and security patches). |
|Stop renewal and change configuration |August 15, 2026 |Stop renewals, upgrades, and downgrades for Redis 4.0 instances. Activated services will continue to run until the EOFS termination date. |
|Service termination |February 15, 2027 |No longer provide data storage, access capabilities, documentation, or technical support services for Redis 4.0 instances. Strongly recommend completing the upgrade or migration before this date. |


<span id="UHFlaxYt"></span>
## Upgrade recommendations


* You can select any of the following methods to upgrade or migrate Redis 4.0 instances to a higher version:

   * Use the [blue-green deployment](https://docs.byteplus.com/en/docs/redis/upgrade_major_version_using_blue_green_deployment) feature to smoothly upgrade Redis 4.0 instances to a higher version.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2"><a href="https://console.byteplus.com/workorder/create/">Submit a ticket</a> to contact technical support and apply for the major version upgrade feature.      </div>
      

   * Migrate Redis 4.0 instances to a higher version using the Database Transmission Service (DTS). For specific procedures, refer to [Migrate data to a BytePlus Cache for Redis instance](https://vsop-online.bytedance.net/doc/manage/detail/6293/6390/172035).

* We recommend upgrading or migrating Redis 4.0 instances to Redis 7.0. Redis 7.0, building on native Redis data structures, additionally supports extension modules such as ExBloomFilter, ExString, ExTimeSeries, and Valkey\-Search, to better meet diverse business scenario needs. For more details, refer to [Extension modules](https://docs.byteplus.com/en/docs/redis/extended-data-structure).


<span id="6leqNcKR"></span>
## FAQs


* **Q: How to confirm compatibility between different versions before upgrading?** 

   For more details on version compatibility, refer to [Redis major version compatibility](https://docs.byteplus.com/en/docs/redis/redis_major_version_compatibility).

* **Q: Will existing Redis 4.0 instances automatically upgrade to a higher version?** 

   No. We recommend you promptly [upgrading major versions using blue-green deployment](https://docs.byteplus.com/en/docs/redis/upgrade_major_version_using_blue_green_deployment) or [migrateing data using DTS](https://vsop-online.bytedance.net/doc/manage/detail/6293/6390/172035).

* **Q: What are the command support differences between different Redis versions?** 

   For more details on command support for each database version, refer to [Supported commands](https://docs.byteplus.com/en/docs/redis/supported-commands).

* **Q: How to troubleshoot issues encountered during upgrading?** 

   If you have any questions during the upgrade process, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support for assistance.
