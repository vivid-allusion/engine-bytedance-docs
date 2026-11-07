---
title: "ListBillDetail"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/ListBillDetail"
---

**ListBillDetail \- Queries bill details**

<span id="request-parameters"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Example Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListBillDetail |Operation to be performed. Value: ListBillDetail. |
|Version |String |Yes |2022/1/1 |The API version. Value: 2022\-01\-01. |
|PayerID |Array of Long |No |[2100057673] |The ID of the payer account. |
|OwnerID |Array of Long |No |[2100057673] |The ID of the owner account. |
|Product |Array of String |No |[ECS] |The name of the product. If this parameter is not specified, bills of all products will be queried. |
|BillingMode |Array of String |No |[1] |The billing mode. The value 1 indicates Yearly/monthly, 2 indicates pay\-as\-you\-go billing, 3 indicates based on contract billing, and 4 indicates based on fulfillment billing. If this parameter is not specified, bills of all billing modes will be queried. |
|BillCategory |Array of String |No |[consume\-use] |The bill category. Valid values: consume\-use, consume\-new, consume\-renew, consume\-formalize, consume\-modify, consume\-trial, refund\-terminate, refund\-modify, transfer\-manual, and transfer\-system. If this parameter is not specified, bills of all bill categories will be queried. |
|Offset |Integer |No |10 |The offset. |
|Limit |Integer |Yes |10 |The limit. Valid values: 1 to 300. |
|BillPeriod |String |Yes |2023\-08 |The accounting period, in the format of YYYY\-MM. The accounting period must be a month within the last 24 months. The earliest month to which the accounting period can be set is 2022\-01, when the new version of the bill service was launched. |
|ExpenseDate |String |No |2023/3/15 |The expense date. This parameter is supported when the value of GroupPeriod is 1. The month of the expense date must be the same as the accounting period. |
|GroupTerm |Integer |No |0 |The statistical dimension. The value 0 indicates billable item, 1 indicates instance, 2 indicates product, and 3 indicates account. |
|GroupPeriod |Integer |No |0 |The statistical period. The value 0 indicates accounting period, 1 indicates day, and 2 indicates details. |
|InstanceNo |String |No |i\-ycjlq77tdg8rx6ib4v1s |The IDs of the instances to be queried. If this parameter is not specified, bills of all instances will be queried. |
|IgnoreZero |Integer |No |1 |Specifies whether to ignore data with zero prices after discount. The value 0 indicates no and 1 indicates yes. Default value: 0. |
|NeedRecordNum |Integer |No |1 |Specifies whether to calculate the total number of records in the queried list, which is used for pagination on the frontend. The value 1 indicates yes and 0 indicates no. Default value: 0. |


<span id="response-parameters"></span>
## Response parameters


|**Parameter** |**Type** |**Example Value** |**Description** |
|---|---|---|---|
|List |Array of BillDetail | |The list of bill details. |
|Total |Integer |100 |The total number. |
|Limit |Integer |100 |The step size. |
|Offset |Integer |0 |The offset. |


BillDetail contains the following parameters:


|**Parameter** |**Type** |**Example Value** |**Description** |
|---|---|---|---|
|List |Array of BillDetail | |The list of bill details. |
|ProjectDisplayName |String |default |The project name. |
|DiscountBizUnitPrice |String |1.3 |The discounted price or the discount. |
|DiscountBizUnitPriceInterval |String |1,2,3 |The discounted price range. |
|DiscountBizMeasureInterval |String |0,100,200 |The discounted amount range. |
|EffectiveFactor |String |1 |The effective factor. |
|PriceInterval |String |1,2,3 |The unit price range. |
|MeasureInterval |String |0,100,200 |The amount range to which the unit price applies. |
|BillingMethodCode |String |Billing by total amount per hour |The billing mode. |
|DiscountBizBillingFunction |String |The full progressive unit price. |The discount type. |
|Price |String |640 |The unit price. |
|MarketPrice |String |2.716 |The market price. |
|BillingFunction |String |Fixed unit price |The unit price type. |
|CreditCarriedAmount |String |0 |The deducted amount via refund to credit card. |
|PreferentialBillAmount |String |5.036185 |The discounted amount. |
|InstanceName |String |ECS\-fEaG |The instance name. |
|ConfigName |String |Downgrade |The configuration name. |
|Element |String |BE000232 |The billing unit. |
|Region |String |China (Beijing) |The region. |
|Zone |String |Zone B |The availability zone. |
|Factor |String | |The factor. |
|ExpandField |String |Billing by total amount per hour |The extended field. |
|PriceUnit |String |block |The unit of the unit price. |
|BusiPeriod |String |2023\-08 |The operational period. |
|Count |String |0 |The usage. |
|Unit |String |GB |The unit of usage. |
|BillDetailId |String |Detail7039533873751019820 |The ID of bill details. |
|DeductionCount |String |0 |The deducted amount of the resource package. |
|OriginalBillAmount |String |5.7112 |The original price. |
|RoundAmount |Double |0 |The rounded down amount. |
|DiscountBillAmount |String |0.66 |The price after discount. |
|CouponAmount |String |0 |The coupon value. |
|PayableAmount |String |0.66 |The amount payable. |
|PaidAmount |String |0 |The paid amount. |
|UnpaidAmount |String |0.66 |The unpaid amount. |
|Currency |String |CNY |The currency. |
|SettlementType |String |The settlement type. Valid values: settle, non\-settle, and quota\-settle. |non\-settle |
|Project |String |default |The project. |
|Tag |String | |The tag, in the format of a JSON string containing multiple key\-value pairs. |
|SellingMode |String |0 |The selling mode. The value 0 indicates regular instance and 1 indicates spot instance. |
|SolutionZh |String |测试方案 |The Chinese name of the solution. |
|SubjectName |String |Beijing Volcano Engine Technology Co., Ltd |The subject name. |
|OwnerUserName |String |Doooo |The name of the owner account. |
|BillCategory |String |consume\-use |The bill category. |
|ReservationInstance |String |0 |The selling mode. The value 0 indicates regular instance and 1 indicates elastic reserved instance. |
|ElementCode |String |BE000137 |The billing unit code. |
|RegionCode |String |R000671 |The region code. |
|ZoneCode |String |Zone1 |The availability zone code. |
|FactorCode |String | |The factor code. |
|ConfigurationCode |String |ecs.g1.large |The configuration code. |
|DeductionUseDuration |String |0 |The deducted amount. |
|BillPeriod |String |2023\-08 |The accounting period. |
|ExpenseDate |String |2023/8/14 |The date. |
|PayerID |String |2100153894 |The ID of the payer account. |
|PayerUserName |String |Doooo |The name of the payer account. |
|PayerCustomerName |String |Beijing Volcano Engine Technology Co., Ltd |The customer name of the payer account. |
|SellerID |String |3423 |The ID of the seller account. |
|SellerUserName |String |Volcano Engine |The name of the seller account. |
|SellerCustomerName |String |Beijing Volcano Engine Technology Co., Ltd |The customer name of the seller account. |
|OwnerID |String |2100153894 |The ID of the owner account. |
|OwnerCustomerName |String |Beijing Volcano Engine Technology Co., Ltd |The customer name of the owner account. |
|BusinessMode |String |Regular business |The business type. |
|Product |String |ECS |The English name of the product. |
|ProductZh |String |云服务器 |The Chinese name of the product. |
|BillingMode |String |pay\-as\-you\-go |The billing mode. |
|ExpenseBeginTime |String |2023/8/14 |The start time of consumption. |
|ExpenseEndTime |String | |The end time of consumption. |
|UseDuration |String |0 |The use duration. |
|UseDurationUnit |String |second |The unit of use duration. |
|TradeTime |String |2022/1/1 |The trade time. Example: 2006\-02\-02 15:04:05. |
|BillID |String |Bill7262035879529697551 |The order number or bill number. |
|InstanceNo |String |i\-ycjlq77tdg8rx6ib4v1s |The instance ID. |
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
