---
title: "Billing of image"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Imagebilling"
---

This topic describes the billing methods for images, billing method changing, and presents billing examples.

<span id="WRfXVOqU"></span>
## Overview

Fees may be incurred when you use images. The billing varies based on the type of images you use. For more information, see the following table.


|**Types** |**Billing note** |
|---|---|
|[Public images](https://docs.byteplus.com/en/docs/ecs/Public-image-overview) |Public images are images with legitimate copyrights provided by BytePlus, including self\-developed image veLinux, third\-party open\-source images, and commercial images.<br><br><br>* veLinux and third\-party open\-source images do not incur image license fees.<br><br>* For use of commercial images, you need to pay certain image license fees, including:<br><br>   * **Windows Server**:<br><br>      License fees are charged for images only in some regions. The amount depends on the number of instance vCPUs. Please refer to the actual order settlement page.<br><br>   * **Red Hat Enterprise Linux**:<br><br>      License fees are charged for images in all [regions](https://docs.byteplus.com/en/docs/ecs/Regions-and-Availability-Zones). The amount depends on the number of instance vCPUs. The unit price is as follows:<br><br>      * 1 ~ 8 vCPUs:<br><br>         * Pay\-as\-you\-go: 0.015 USD/vCPU/hour<br><br>         * Subscription: 10.15 USD/vCPU/month<br><br>      * 9 ~ 27 vCPU：<br><br>         * Pay\-as\-you\-go: 0.011 USD/vCPU/hour<br><br>         * Subscription: 7.61 USD/vCPU/month<br><br>      * 128 vCPUs and above:<br><br>         * Pay\-as\-you\-go: 0.01 USD/vCPU/hour<br><br>         * Subscription: 6.6 USD/vCPU/month<br><br>   * **SUSE Linux Enterprise Server：** <br><br>      License fees are charged for images in all [Regions](https://docs.byteplus.com/en/docs/ecs/Regions-and-Availability-Zones). The amount depends on the number of instance vCPUs. The unit price is as follows:<br><br>      * 1 ~ 2 vCPU：<br><br>         * Pay\-as\-you\-go: 0.064 USD/instance/hour<br><br>         * Subscription: 24.46 USD/instance/month<br><br>      * 3 ~ 4 vCPU：<br><br>         * Pay\-as\-you\-go: 0.127 USD/instance/hour<br><br>         * Subscription: 50.15 USD/instance/month<br><br>      * 5 vCPU and above:<br><br>         * Pay\-as\-you\-go: 0.152 USD/instance/hour<br><br>         * Subscription: 58.62 USD/instance/month<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Under the "Subscription" billing model, the Red Hat Enterprise Linux and SUSE Linux Enterprise Server images only offer monthly prices. If you purchase an ECS instance by year and select this Public Image, BytePlus will charge based on the monthly price corresponding to the vCPU number of the instance. <a href="https://docs.byteplus.com/en/docs/ecs/Imagebilling#fiTT8TWY">Learn more</a>.</div><br> |
|[Custom image](https://docs.byteplus.com/en/docs/ecs/Custom_image_overview) |You can create a custom image based on an instance or by importing a local image file.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You are not charged when you create a custom image for an instance, import a custom image, or copy a custom image. By default, BytePlus creates a snapshot for a custom image. If you retain the custom image, you are charged the snapshot storage fee. For more information about billing details, see <a href="https://docs.byteplus.com/en/docs/ecs/Snapshot_billing">Snapshot billing</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When you import a local image file, if you use the BytePlus official license to activate the image, you are charged image license fees when you create instances by using the image. For the specific amount, refer to the actual order settlement page.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When you create an instance by using a custom image derived from a chargeable image, you are charged the image fee. The billing rules are the same as those of the source chargeable image. For the specific amount, refer to the actual order settlement page.</div><br> |
|[Share an image](https://docs.byteplus.com/en/docs/ecs/Sharing-or-canceling-sharing-image) |Shared images are images shared by other BytePlus accounts. If a shared image is a chargeable image, when you create an instance by using this shared image, you also need to pay for it under the sharing account. In this scenario, the billing rule is same as that for the source chargeable image. |


<span id="3NauVgls"></span>
## Billing method

For Elastic Compute Service (ECS) images, two billing methods are available: Pay\-as\-you\-go and Subscription.


|Billing method |Description |
|---|---|
|Pay\-as\-you\-go |A post\-payment billing method, which allows you to pay after use, with the billing cycle precise to the second. |
|Subscription |A prepaid model, where payment is made upfront prior to usage, with the subscription duration measured in months. |


<span id="WcrYbAqL"></span>
## Billing method change

When you change the billing method of an instance, the billing method of the image used by the instance is also changed.

<span id="fiTT8TWY"></span>
## Fee calculation example

The following table outlines the calculation process for public image license fees under different billing methods. Assume the Region is **Asia Pacific (Johor)** , purchase**1**instance**4**of vCPU specification, and use the image **Windows Server 2019 Data Center Edition 64\-bit English version**, **Red Hat 9.3 64 bit ** , or **SUSE 15 SP5 64 bit**.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The prices in the following table are only for example purposes. Actual fees depend on the instance type and capacity. See the fee results displayed when you place order in the <a href="https://console.byteplus.com/ecs/region:ecs+cn-shanghai/instance">ECS console</a>.</div>



|Selected image |Billing formula |Billing method |Unit price and billing cycle |Fee  **(USD)**  |
|---|---|---|---|---|
|Windows Server 2019 Datacenter Edition 64 bit English |Fee = Image unit price \* Number of vCPUs \* Billing duration/Subscription duration |Pay\-as\-you\-go |* Image unit price: 0.0413 USD/hour/vCPU<br><br>* Billing cycle: 30 days |0.0413 \* 4 \* 30 \* 24 = 118.944 |
|||Subscription |* Image unit price: 32.5669 USD/vCPU/month<br><br>* Subscription duration: 1 month |32.5669 \* 4 \* 1 = 130.2676 |
|Red Hat 9.3 64 bit ||Pay\-as\-you\-go |* Image unit price: 0.015 USD/hour/vCPU |0.015 \* 4 \* 30 \* 24 = 43.2 |
|||Subscription |* Image unit price: 10.15 USD/vCPU/month<br><br>* Billing cycle: 1 month |10.15 \* 4 \* 1 = 40.6 |
||||* Image unit price: 10.15 USD/vCPU/month<br><br>* Billing cycle: 1 year |10.15 \* 4 \* 1 \* 12 = 487.2 |
|SUSE 15 SP5 64 bit |Fee = Image unit price \* Number of instances \* Billing duration/Subscription duration |Pay\-as\-you\-go |* Image unit price: 0.127 USD/instance/hour<br><br>* Billing cycle: 30 days |0.127 \* 1 \* 30 \* 24 = 91.44 |
|||Subscription |* Image unit price: 50.15 USD/instance/month<br><br>* Billing cycle: 1 month |50.15 \* 1 \* 1 = 50.15 |
||||* Image unit price: 50.15 USD/instance/month<br><br>* Billing cycle: 1 year |50.15 \* 1 \* 12 = 601.8 |
