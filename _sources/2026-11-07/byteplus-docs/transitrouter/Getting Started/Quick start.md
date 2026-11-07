---
title: "Quick start"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Quick-start-01"
---

<span id=".5qaC6L-w"></span>
## Overview

Transit Router (TR) supports cloud network connection across accounts and regions, allowing you to flexibly achieve interconnectivity and isolation for diverse complex networking scenarios. By integrating with Virtual Private Network (VPN) or Direct Connect (DC) services, you can also flexibly implement complex cloud and on\-premises networking scenarios.

This section describes how to use TR to quickly achieve interconnectivity and isolation for cloud resources.

<span id=".6Lev55Sx6KeE5YiS"></span>
## Route planning

Before proceeding with the configuration, see [Planning principles](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-02#.6KeE5YiS5Y6f5YiZ) to plan routes for specific networking scenarios.

<span id=".6YWN572u5rWB56iL"></span>
## Configuration procedures

TR can connect and isolate separate Virtual Private Clouds (VPCs) across accounts and regions. Select a solution that best suits your networking scenario to get started with TR.


* [Implementing private interconnectivity and isolation between different VPCs (same account, same region)](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-02)

   Implement the networking scenario where three VPCs are under the same account in the same region, connecting vpc01 and vpc02 to vpc03 and isolating vpc01 from vpc02.

* [Implementing private interconnectivity and isolation between different VPCs (same account, cross-region)](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-03)

   Implement the networking scenario where three VPCs are under the same account across regions, connecting vpc01 and vpc02 in Region A to vpc03 in Region B and isolating vpc01 from vpc02.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c55aff41083b9db576e8cfd123f6f565.png) </span>

* [Implementing private interconnectivity and isolation between different VPCs (cross-account, same region)](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-04)

   Implement the networking scenario where three VPCs are under separate accounts in the same region, connecting vpc01 and vpc02 under Account A to vpc03 under Account B and isolating vpc01 from vpc02.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1bbe09fecb08f557e1bf3aaa6723b30c.png) </span>

* [Implementing private interconnectivity and isolation between different VPCs (cross-account, cross-region)](https://docs.byteplus.com/en/docs/transitrouter/Connecting-and-isolating-different-VPCs-across-accounts-and-Regions)

   Implement the networking scenario where three VPCs are under separate accounts across regions, connecting vpc01 and vpc02 in Region A under Account A to vpc03 in Region B under Account B and isolating vpc01 from vpc02.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9b78309605bb24ab58930f23665bfb73.png) </span>
