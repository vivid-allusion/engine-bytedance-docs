---
title: "Unsubscription rules"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management"
---

<span id="ebb43571"></span>
## Unsubscription rules

**Prepaid instance unsubscription**: The BytePlus Console \- Billing Center \- Unsubscription Management path supports the unsubscription of prepaid instances only, with two options available: seven\-day unconditional full refund (seven\-day refund), and non\-seven\-day refund. Refunds are applicable solely to payments made in cash (including credit control balance) by the user and exclude amounts covered by coupons. Upon successful unsubscription, the refund will be processed through the original payment method (see *Refund Flow* for details). For product unsubscription, please navigate to BytePlus Console \- Billing Center \- Unsubscription Management.

**Postpaid instance unsubscription**: To unsubscribe postpaid services, please visit the product Console or submit a support ticket to initiate the unsubscription process.

Note: If the refund amount has been invoiced, you are required to prepare the necessary documentation for invoice return. You can submit the invoice return request through BytePlus Console \- Billing Center \- Invoice Management or any other methods supported by BytePlus. Provide the relevant documents for invoice return when you request a service unsubscription. We will proceed with the refund after verifying that the documents are accurate.

<span id="97db1fd1"></span>
## I. Seven\-Day Unconditional Refund Policy

<span id="afd4d008"></span>
### Seven\-day unconditional refund rules


1. Annual or monthly subscriptions eligible for this policy are entitled to a full, unconditional refund within seven days of purchase.

2. Resource packages eligible for this policy also qualify for a full, unconditional refund if they remain unused within seven days of purchase. Used resource packages cannot be unsubscribed.

3. Subscriptions that have been renewed, changed, or adjusted if it is a Reserved Instance within the first seven days are not eligible for a full, unconditional refund.

4. Each account is entitled to one full, unconditional refund per product per calendar year (January 1 \- December 31) under this policy.

5. Expired instances cannot be unsubscribed.

6. Instances that are subject to compulsory binding must be unsubscribed as a whole.

7. For products purchased during promotions, if the refund policy conflicts with the promotional rules, the latter prevails.

8. For prepaid instances purchased and paid for by the primary account during the custody period, any remaining value will be refunded to the primary account upon unsubscription. Prepaid instances that are either purchased before the custody period and unsubscribed during it, or purchased during the custody period and unsubscribed after the custody ends, are not refunded if unsubscribed.

9. Prepaid instances purchased before entering into a consignment or resale agreement are eligible for unsubscription without refund during the term of said agreement; similarly, prepaid instances purchased during the term of a consignment or resale agreement are only eligible for unsubscription without refund after termination of the agreement.

10. Post\-tax refundable total = Pre\-tax refundable total + (Pre\-tax refundable total \* Tax rate at the time of order) = Pre\-tax real value of order + (Pre\-tax real value of order \* Tax rate at the time of order)


<span id="2a09ed89"></span>
## II. Non\-seven\-Day Refund Policy

<span id="ef52e8cd"></span>
### Non\-seven\-day refund rules


1. Refund amount calculation:

   1. Pre\-tax refundable total = Pre\-tax real value of order \- Monthly list price at purchase \* [Used duration (days)/(365/12)] \* Applicable discount

   2. Post\-tax refundable total = Pre\-tax refundable total + (Pre\-tax refundable total \* Tax rate at the time of order)

2. Pre\-tax real value of the order: This refers to the actual amount paid by the client, which includes all amounts paid in cash or through credit control balance.

   * For new purchases, renewals, and adjustments to Reserved Instances, the pre\-tax real value equals to the pre\-tax payable amount.

   * Pre\-tax real value of instance after change: It will be employed in calculations of the pre\-tax real value for any subsequent change and of the remaining value for a refund.

      * Pre\-tax real value of instance after change = Payable total for current change + Pre\-tax remaining real value before change

      * Pre\-tax remaining real value before change = min

      * Pre\-tax remaining real value of original order = Pre\-tax real value of original order \* (Remaining duration/Total order duration), measured to the second

3. Expired instances cannot be unsubscribed.

4. Instances that are subject to compulsory binding must be unsubscribed as a whole.

5. For products purchased during promotions, if the refund policy conflicts with the promotional rules, the latter prevails.

6. For prepaid instances purchased and paid for by the primary account during the custody period, any remaining value will be refunded to the primary account upon unsubscription. Prepaid instances that are either purchased before the custody period and unsubscribed during it, or purchased during the custody period and unsubscribed after the custody ends, are not refunded if unsubscribed.

7. Prepaid instances purchased before entering into a consignment or resale agreement are eligible for unsubscription without refund during the term of said agreement; similarly, prepaid instances purchased during the term of a consignment or resale agreement are only eligible for unsubscription without refund after termination of the agreement.

8. Special notes:

   * For non\-seven\-day refunds, we measure usage daily. Any usage less than a full day is rounded up to one full day.

   * Applicable discount: The refund will reflect a discount rate applicable based on the actual used duration, as outlined at purchase.

   * **Example**

   Consider a scenario where a client acquired a monthly subscription instance of RabbitMQ message queue on November 1, 2021 for a duration of 6 months. The monthly list price was USD 100.00, with a 20% discount for a 6\-month commitment. This lowered the total cost from USD 600.00 to USD 480.00. After applying a coupon of USD 100.00, the pre\-tax payable amount was USD 380.00, which was also the pre\-tax real value. The client paid USD 380.00 in cash. At the time of the order, the tax rate was 8%, so the total payment was USD 410.40. The subscription will expire on May 1, 2022.

   Having used the instance for 5 days, the client canceled the subscription on November 5, 2021 using the non\-seven\-day refund option. Then:

   Pre\-tax refundable total = Pre\-tax real value of order \- Monthly list price at the time of purchase \* [Used duration (days)/(365/12)] \* Applicable discount \* 1.5 = USD 380 \- 100 \* [5/(365/12)] \* 1 \* 1.5 = USD 355.34

   Post\-tax refundable total = USD 355.34 + (355.34 \* 8%) = USD 383.77


<span id="b76fa99c"></span>
## III. Non\-refundable Products


* Instances under temporary upgrade cannot be unsubscribed.


<span id="7d1daff3"></span>
## IV. Unsubscription Procedure


1. Access the Billing Center \- Unsubscription Management page.

2. Select the Seven\-Day Unconditional Refund or Non\-seven\-day Refund tab.

3. You can unsubscribe one individual instance or multiple instances in batch as needed.

* **For individual unsubscription**: Select the instance you wish to unsubscribe and click the Unsubscribe button to proceed to the Unsubscription Confirmation page.

* **For bulk unsubscription**: In the list, select the instances you wish to unsubscribe and click the Bulk Unsubscribe button at the bottom left of the list to proceed to the Unsubscription Confirmation page.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a93695e3ed59a40e049d3cfe9d85aeee.png) </span>


4. Unsubscription Confirmation: You can view the pre\-tax refundable total of the instance(s) being unsubscribed. After checking the confirmation prompt (if any), click Confirm Unsubscription.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e8bd08dfbfa3e682eb6f8ff82ef573ee.png) </span>


5. Unsubscription Details: Once the unsubscription request is successfully processed, clicking on the order number will redirect you to the unsubscription order details.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dbd5644dce0c4600ba16b861b455e82d~tplv-goo7wpa0wc-image.image" width="1290px" /></div>
