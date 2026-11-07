---
title: "Order management"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-orders"
---

Log in to the BytePlus console and go to [Billing Center-Order management](https://console.byteplus.com/finance/order), where you can view the information of all created orders, and pay for or cancel orders that have been created and are pending payment. <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260914115441-616983180399.png) </span>

<span id=""></span>
### **1. Search and Filter Criteria**

You can search for orders using the following search and filter criteria.


* Order number: Enter an order number to view the specified order.

* Creation time (UTC+8): Select a start date and an end date to view orders created within this time range. By default, orders from the past one month are queried.

* Product: Select a product to filter orders of the corresponding product.

* Order type: Select an order type to filter orders of different order types.

* Order status: Select an order status to filter orders in different order statuses.


<span id=""></span>
### **2. Table Field Descriptions**

The order list displays information such as Customer order number, product, order type, creation time, update time, status, and gross amount.


|**Concept** |**Description** |
|---|---|
|Customer order number |The unique identifier of an order. |
|Product |Displays the name of the product corresponding to the order. |
|Order type |The type of the order. <br><br>There are 12 types: Purchase, Trial, Change config, Renew, Extend, End trial, Cancel, RI adjustment(RI adjustment), Temporary upgrade, Manual adjustment, Attribute Adjustment, Resource transfer. |
|Creation time (UTC+8) | The time when the order is created. |
|Update time (UTC+8) | The time when the status is updated. |
|Status |The current status of the order. <br><br>There are 8 statuses: **Pending Payment**, **Paid**, **Canceled**, **Refunded**, **Partially Refunded**, **Pending Refund**, **Refund Failed**, and **In payment** |
|Gross amount |The gross (list\-price) amount of the order. |
|After\-tax amount payable (pricing currency) |The after\-tax amount payable in the pricing currency for the order. |
|After\-tax amount payable (settlement currency) |The after\-tax amount payable in the settlement currency for the order. |
|Actions |For orders with the **Pending Payment** status, you can perform the **Pay Now** and **Cancel Order** actions; for orders with other statuses, you can only click the order number to perform the **View Details** action. |


<span id=""></span>
### **3. Order Details**

Order details are used to display the transaction information related to each order action. Each order has corresponding order details. For Change Config, Reserved Instance Adjustment, and consecutive Temporary Upgrade orders, both the old configuration information before the change and the new configuration information after the change must be displayed; therefore, multiple order detail records may appear.

After an order is placed, the resource service delivery process of this order transaction is recorded separately based on this transaction action. This resource service is called an "instance".

&nbsp;

Click an order number to open the order details page, which is displayed in the following two cases.

**3.1. The order details page for the Purchase, Renewal, Trial, and End trial order types is as follows:** <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260914115442-190840911592.png) </span>

**3.2. The order details page for the Change Config, Cancel, RI adjustment, and Temporary Upgrade order types is as follows:** <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260914115441-508561014335.png) </span>

<span id=""></span>
### **4.Concept description**

The descriptions of order related concepts are as follows:


|**Concept** |**Description** |
|---|---|
|Payable amount |Gross amount \- Discount amount \- Coupon deduction + Tax |
|Gross amount |The gross (list\-price) amount of the order. |
|Discount amount |The total discount amount of all the sub\-orders in an order. |
|Coupon deduction |The total coupon deducted amount of all the sub\-orders in an order. |
|Tax |The total tax to be paid for all the sub\-orders in an order. |
|Amount paid |The actual amount. |
|Type / Order Type |The type of the order. <br><br>There are 12 types: Purchase, Trial, Change config, Renew, Extend, End trial, Cancel, RI adjustment(RI adjustment), Temporary upgrade, Manual adjustment, Attribute Adjustment, Resource transfer. |
|Created time (UTC+8) |The time when an order is created. |
|Payment Method |The payment method of an order:<br><br><br>* **Pre\-payment**: Need to make a payment when activating a service. The service is accessible only after the payment is completed.<br><br>* **Post\-payment**: No need to make a payment when activating a service. The gross amount and order amount is 0. The final amount is calculated according to how many units of the product the user has used, and a bill will be created. |
|Order owner account |Represents the owner of the current order. For example, if A places an order to B, the order owner account is B |
|Buyer |Represents the party placing the order. For example, if A buys from B, the buyer account is A. |
|Seller |Represents the seller of the order. In consignment or resale scenarios, the seller account is the partner account. |
|Payer |Represents the party paying for the order. For example, if a financial escrow sub\-account uses the main account’s funds, the payer account is the main account. |
|Product |The product the order is for. |
|Configuration |The parameter configuration of the product. |
|Purchased Duration |The product's validity period you purchase. |
|Start / End time (UTC+8) |The start time and end time of the validity period. |
|Instance ID |The unique identification of an instance.<br><br>An instance is the minimum unit of a product configured with required parameters. It is also the virtual representation of a product. For example, the VOD service or a cloud server can be an instance. |
