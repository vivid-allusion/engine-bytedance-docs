---
title: "ListBillOverviewByCategory"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/ListBillOverviewByCategory"
---

**ListBillOverviewByCategory \- Queries bill overview by account**

<span id="request-parameters"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Example Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListBillOverviewByCategory |Operation to be performed. Value: ListBillOverviewByCategory. |
|Version |String |Yes |2022/1/1 |The API version. Value: 2022\-01\-01. |
|BillingMode |Array of String |No |[1] |The billing mode. The value 1 indicates Yearly/monthly, 2 indicates pay\-as\-you\-go billing, 3 indicates based on contract billing, and 4 indicates based on fulfillment billing. If this parameter is not specified, bills of all billing modes will be queried. |
|BillCategoryParent |Array of String |No |[consume] |The bill category. Valid values: consume, refund, and transfer. If this parameter is not specified, bills of all bill categories will be queried. |
|PayerID |Array of Long |No |[2100057673] |The ID of the payer account. |
|OwnerID |Array of Long |No |[2100057673] |The ID of the owner account. |
|BillPeriod |String |Yes |2023\-03 |The accounting period. |


<span id="response-parameters"></span>
## Response parameters


|**Parameter** |**Type** |**Example Value** |**Description** |
|---|---|---|---|
|List |Array of BillOverviewByCategoryByPayerList | |The list of bills sorted by account. |


BillOverviewByCategoryByPayerList contains the following parameters:


|**Parameter** |**Type** |**Example Value** |**Description** |
|---|---|---|---|
|List |Array of BillOverviewByCategory | |The list of bills of an account. |


BillOverviewByCategory contains the following parameters:


|**Parameter** |**Type** |**Example Value** |**Description** |
|---|---|---|---|
|List |Array of BillOverviewByCategoryByPayerList | |The list of bills sorted by account. |
|List |Array of BillOverviewByCategory | |The list of bills of an account. |
|OwnerID |String |2100057673 |The ID of the owner account. |
|PayableAmount |String |0 |The amount payable. |
|UnpaidAmount |String |0 |The unpaid amount. |
|OriginalBillAmount |String |0 |The original price. |
|DiscountBillAmount |String |0 |The price after discount. |
|PaidAmount |String |0 |The paid amount. |
|CouponAmount |String |0 |The coupon value. |
|PayerID |String |2100057673 |The ID of the payer account. |
|SellerID |String |3423 |The ID of the seller account. |
|CreditCarriedAmount |String |0 |The deducted amount via refund to credit card. |
|OwnerUserName |String |weitest009 |The name of the owner account. |
|OwnerCustomerName |String |Junjie 1 |The customer name of the owner account. |
|SettlementType |String |non\-settle |The settlement type. Valid values: settle, non\-settle, and quota\-settle. |
|SubjectName |String |Beijing Volcano Engine Technology Co., Ltd |The subject name. |
|Currency |String |CNY |The currency. |
|PayerCustomerName |String |Junjie 1 |The customer name of the payer account. |
|SellerUserName |String |Volcano Engine |The name of the seller account. |
|SellerCustomerName |String |Beijing Volcano Engine Technology Co., Ltd |The customer name of the seller account. |
|BusinessMode |String |Financial hosting |The business type. |
|BillPeriod |String |2023\-11 |The accounting period. |
|BillCategoryParent |String |consume |The bill category. |
|PayerUserName |String |weitest009 |The name of the payer account. |
|SubjectNo |String |3423 |The subject number. |
|Tax |String |0.84 |The tax in the pricing currency. |
|PosttaxAmount |String |23.43 |The post\-tax payable amount in the pricing currency. |
|PretaxAmount |String |14.23 |The pre\-tax payable amount in the pricing currency. |
|RealValue |String |53.64 |The post\-tax real value in the pricing currency. |
|PretaxRealValue |String |37.45 |The pre\-tax real value in the pricing currency. |
|SettlePosttaxAmount |String |63.75 |The post\-tax payable amount in the settlement currency. |
|SettlePretaxAmount |String |33.54 |The pre\-tax payable amount in the settlement currency. |
|SettleTax |String |65.36 |The tax in the settlement currency. |
|SettleRealValue |String |24.52 |The post\-tax real value in the settlement currency. |
|SettlePretaxRealValue |String |25.64 |The pre\-tax real value in the settlement currency. |
|CountryRegion |String |"SG" |The country or region. |
