---
title: "Billing Overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/VCI-billing-overview"
---

This topic describes the billable VCI resources and corresponding billing methods.

<span id=".6K6h6LS56K-05piO"></span>
## Billing description


* **Billing duration: **  Fees are incurred based on the instance running duration. The running duration refers to the time window starting when the container image download (Pending state) and ending when any of the conditions are met:

   * The instance is released.

   * It enters the **Succeeded** state.

   * It enters the **Failed** state.

* **Balance deduction granularity**: The fee details displayed on bills are accurate down to 6 decimal places, while the actual amount deducted from the account balance is accurate down to 2 decimal places.

* **Billing mode:** 

   * Billing is based on the vCPU, memory, and GPU specifications applied during instance creation.

   * If you specify unsupported vCPU, memory, or GPU specifications, the system will adjust them and bill you based on the adjusted specifications. For details, see [General-purpose specifications](https://docs.byteplus.com/en/docs/vke/Create_General_purpose_instance).

   * For a list of specifications, see [VCI specifications](https://docs.byteplus.com/en/docs/vke/VCI-instance-types).


<span id=".6K6h6LS55pa55byP"></span>
## Billing method

VCI applies the **pay\-as\-you\-go** billing method. It is a postpaid mode in which you use resources first and pay later. For billing details and unit prices, see [pay-as-you-go](https://docs.byteplus.com/en/docs/vke/Pay-as-you-go).

<span id=".6K6h6LS55ZGo5pyf"></span>
## Billing cycle

The billing cycle is accurate down to seconds, and bills are settled on an hourly basis.
