---
title: "ListBillOverviewByProd"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/ListBillOverviewByProd"
---

**ListBillOverviewByProd \- Queries bill overview by product**

<span id="request-parameters"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Example Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListBillOverviewByProd |Operation to be performed. Value: ListBillOverviewByProd. |
|Version |String |Yes |2022/1/1 |The API version. Value: 2022\-01\-01. |
|PayerID |Array of Long |No |[2100057673] |The ID of the payer account. |
|OwnerID |Array of Long |No |[2100057673] |The ID of the owner account. |
|Offset |Integer |No |10 |The offset. |
|Limit |Integer |Yes |10 |The limit. Valid values: 1 to 300. |
|BillPeriod |String |Yes |2023\-08 |The accounting period, in the format of YYYY\-MM. The accounting period must be a month within the last 24 months. The earliest month to which the accounting period can be set is 2022\-01, when the new version of the bill service was launched. |
|IgnoreZero |Integer |No |1 |Specifies whether to ignore data with zero prices after discount. The value 0 indicates no and 1 indicates yes. Default value: 0. |
|NeedRecordNum |Integer |No |1 |Specifies whether to calculate the total number of records in the queried list, which is used for pagination on the frontend. The value 1 indicates yes and 0 indicates no. Default value: 0. |
|BillingMode |Array of String |No |[1] |The billing mode. The value 1 indicates Yearly/monthly, 2 indicates pay\-as\-you\-go billing, 3 indicates based on contract billing, and 4 indicates based on fulfillment billing. If this parameter is not specified, bills of all billing modes will be queried. |
|BillCategoryParent |Array of String |No |[consume] |The bill category. Valid values: consume, refund, and transfer. If this parameter is not specified, bills of all bill categories will be queried. |
|Product |Array of String |No |[ECS] |The name of the product. If this parameter is not specified, bills of all products will be queried. |


<span id="response-parameters"></span>
## Response parameters


|**Parameter** |**Type** |**Example Value** |**Description** |
|---|---|---|---|
|List |Array of BillOverviewByProd | |The list of bills sorted by product. |
|Total |Integer |100 |The total number. |
|Limit |Integer |100 |The step size. |
|Offset |Integer |0 |The offset. |


BillOverviewByProd contains the following parameters:


|**Parameter** |**Type** |**Example Value** |**Description** |
|---|---|---|---|
|BillPeriod |String |2023\-08 |The accounting period. |
|PayerID |String |2100153894 |The ID of the payer account. |
|PayerUserName |String |Doooo |The name of the payer account. |
|PayerCustomerName |String |Beijing Volcano Engine Technology Co., Ltd |The customer name of the payer account. |
|SellerID |String |3423 |The ID of the seller account. |
|SellerUserName |String |Volcano Engine |The name of the seller account. |
|SellerCustomerName |String |Beijing Volcano Engine Technology Co., Ltd |The customer name of the seller account. |
|OwnerID |String |2100153894 |The ID of the owner account. |
|OwnerUserName |String |Doooo |The name of the owner account. |
|OwnerCustomerName |String |Beijing Volcano Engine Technology Co., Ltd |The customer name of the owner account. |
|BusinessMode |String |Regular business |The business type. |
|Product |String |ECS |The English name of the product. |
|ProductZh |String |云服务器 |The Chinese name of the product. |
|BillingMode |String |2 |The billing mode. |
|BillCategoryParent |String |consume |The bill category. |
|OriginalBillAmount |String |168.74 |The original price. |
|PreferentialBillAmount |String |148.500779 |The discounted amount. |
|RoundBillAmount |String |0.559221 |The rounded down amount. |
|DiscountBillAmount |String |19.68 |The price after discount. |
|CouponAmount |String |0 |The coupon value. |
|PayableAmount |String |19.68 |The amount payable. |
|PaidAmount |String |0 |The paid amount. |
|UnpaidAmount |String |0 |The unpaid amount. |
|SettlementType |String |non\-settle |The settlement type. Valid values: settle, non\-settle, and quota\-settle. |
|CreditCarriedAmount |String |0 |The deducted amount via refund to credit card. |
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
