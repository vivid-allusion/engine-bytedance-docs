---
title: "About packages"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/About_packages"
---

In the Billing Center, you can view all your packages and their deduction details. A package contains a certain quota for deduction. For example, if the quota of a package is 10GB and you have used 1GB of a product, 1GB will be deducted from the 10\-GB quota.

<span id="11dc58f4"></span>
## Package types

BytePlus provides two types of package: diminishing and periodic. The details of each type are as follows:

**Diminishing package**


* **Billing mode** : pay\-per\-use

* **Attribute** : the number of remaining packages decreases with deduction; packages can be upgraded or re\-configured for but cannot be extended.

* **Unavailability condition** : when there are no available instances, instances expire, or the package expires.


**Periodic package**


* **Billing mode** : pay\-per\-month

* **Attribute** : the number of remaining packages decreases with deduction; the number of packages is set to zero at the end of each reset cycle, and is recovered at the beginning of next reset cycle; packages can be extended, upgraded, or re\-configured; the reset cycle can be set by hour, day, or month.

* **Unavailability condition** : when there are no available instances, instances expire, or the package expires.


<span id="3b71cc25"></span>
## Deduction rules

If you own multiple packages, the deduction orders are as follows:

**Packages with different expiry times**

If the expiry times of packages are different, the package with the nearest expiry time is used. As for monthly packages, the expiry time can be taken as the end time of the current period.

**Packages with the same expiry time**

If the packages have the same expiry time, the deduction orders are as follows:


* If there are both diminishing and periodic packages, periodic packages are deducted first.

* If there is only one type of package, the package with the earliest take\-effect time is deducted first.


<span id="98942b06"></span>
## Deduction time rules

The time rules for deduction are as follows:


* For pay\-per\-hour and pay\-per\-day instances, the platform deducts quota from the package whose validity period covers the hour or day when the instances are used.

* For pay\-per\-month instances, the platform deducts quota from the packages bought within the billing month.
