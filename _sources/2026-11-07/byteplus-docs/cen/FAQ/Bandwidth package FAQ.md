---
title: "Bandwidth package FAQ"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/CEN-bandwidth-packages-faq"
---

## Can the bandwidth size of a CEN bandwidth package be modified? How?

Yes, supported. Non\-cross\-border CEN bandwidth packages support modifying the bandwidth size as needed. Cross\-border bandwidth packages only support increasing the bandwidth, not decreasing it. For detailed actions, see [Modifying Bandwidth](https://docs.byteplus.com/en/docs/cen/CEN-bandwidth-packages-03).

## Is a bandwidth package required for CEN connectivity tests?

No. CEN provides a default 10 Kbps bandwidth for free connectivity testing.

* A bandwidth package is not required for communication between network instances within the same region.

* A bandwidth package and allocation of inter\-region bandwidth are required for communication between network instances across different regions.

## Can only one bandwidth package be bound per CEN instance?

Each CEN instance can only have one bandwidth package bound per interconnection region. However, it can simultaneously bind multiple bandwidth packages if they are for different interconnection regions.

## Does cross\-account interconnection require purchasing a bandwidth package under each account?

No. Cross\-account interconnection requires cross\-account authorization of the network instances. After authorization, the authorized network instances can be loaded into the CEN instance under the authorized account. Therefore, only the authorized account needs to purchase one bandwidth package.

## What is the difference between using CEN vs. VPN Connection for cross\-region VPC interconnection?

* CEN: Establishes direct private network access between the two VPCs. This method offers faster access speeds, higher stability, and lower latency.

* VPN Connection: Establishes communication between the two VPCs over the internet. The VPN connection encrypts transmitted data based on IKE and IPsec protocols to ensure secure data transmission. As it relies on the internet, it can be affected by network jitter, and latency/packet loss rates cannot be guaranteed.
