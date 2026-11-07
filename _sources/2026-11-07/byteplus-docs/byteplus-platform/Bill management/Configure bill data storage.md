---
title: "Configure bill data storage"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/bill_storage_tos"
---

<span id="feature-overview"></span>
### Feature overview


1. After you set up the Bill Storage TOS, BytePlus will synchronize billing files to the bucket or folder specified by your TOS.

2. Subscribable billing data types: Monthly bill PDF, billing item bill details, billing item bills summary by day, billing item bills summary by billing cycle, instance bill details, instance bills summary by day, instance bills summary by billing cycle, split bill details, split bills summary by day, split bills summary by billing cycle, cost bill details, cost bill summary by day of allocation, cost bill summary by month of allocation, bill, and cost analysis report template.

3. Daily subscribed billing data is for reference only and should not be used as the basis for reconciliation. For reconciliation purposes, refer to the final monthly billing data.

4. Notes: Scenarios such as delayed billing, refunds, and bill changes may occur during the month. It is recommended to pull the billing files after 10:00 AM on the 4th calendar day of the following month for fee bills and after 10:00 AM on the 5th calendar day of the following month for split bills and cost bills. (If the billing mode is set to contract billing, pull the fee bills on the 5th working day of the following month and the split bills and cost bills on the 6th working day of the following month.)

5. File naming: UID_File name_YYYYMMDD (for monthly data, YYYYMM). For the file names of each bill type, refer to the notes at the end of the documentation.

6. Notes: (1) Subscribed billing files are generally stored to TOS by no later than 24:00 the next day. (2) Except for monthly bill PDF, all other billing data types are in ZIP format.


<span id="HksNh07m"></span>
### Procedure


1. Account authorization: This authorization allows the billing service to deliver files to your TOS bucket. Go to [Billing center > ](https://console.byteplus.com/finance/bill/detail)[Bill details](https://console.byteplus.com/finance/bill/detail) and click Configure bill data storage at the top right corner. If authorization is required, click Authorize service in the prompt box to jump to the cross\-service access request page. After authorization, you can return to the Bill details page.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260623112614-649694783623.png) </span>


&nbsp;

2. Enter the settings page: After authorization is completed, click Configure bill data storage to enter the billing data storage settings page.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260623112617-319066945583.png) </span>


&nbsp;

3. Add subscription items: On the billing data storage settings page, click Add subscription item at the top left of the list. Select the billing data type to store and the starting billing cycle for pushing, and enter the bucket name for subscription. Note: You may select January 2022 and later as the starting billing cycle to resend historical bills. For daily new billing data, the platform will generate files for the subscribed bills and synchronize them to your TOS bucket every day.

   <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260623112719-631842311206.png) </span>

4. View subscription items: In the list below, you can view the subscription items added.

5. Edit/Delete subscription items: Click Edit or Delete on the right side of the list to edit or delete the corresponding subscription items for billing data storage TOS.

6. Manage delivered files: On the [TOS console](https://console.byteplus.com/tos), you can view and manage the stored subscription files. For operation guidelines, refer to: [TOS File Management](https://docs.byteplus.com/en/docs/tos/docs-uploading-a-file).

7. Names of delivered files for each billing data type:



|**Billing data type** |**File name** |**Description** |
|---|---|---|
|Monthly bill PDF |MonthBill |Consistent with the monthly bill PDF exported from the bill details page. |
|Bill |Bill |Consistent with the complete bill CSV table exported from the bill details page. |
|Billing item bill details |ChargeItemDetail |Consistent with the complete table content in the bill details page when Items= Billing Item and Period = Details. |
|Billing item bills summary by day |ChargeItemDetailDaily<br><br> |Consistent with the complete table content in the bill details page when Items= Billing Item and Period = By Day. |
|Billing item bills summary by billing cycle |ChargeItemDetailMonthly |Consistent with the complete table content in the bill details page when Items= Billing Item and Period = Billing cycle. |
|Instance bill details |InstanceDetail |Consistent with the complete table content in the bill details page when Items = Instance and Period = Details. |
|Instance bills summary by day |InstanceDetailDaily<br><br> |Consistent with the complete table content in the bill details page when Items = Instance and Period = By Day. |
|Instance bills summary by billing cycle |InstanceDetailMonthly<br><br> |Consistent with the complete table content in the bill details page when Items = Instance and Period = Billing cycle. |
|Split bill details |SplitItemDetail<br><br> |Consistent with the complete table content in the split bills page when Period = Details. |
|Split bills summary by day |SplitItemDetailDaily<br><br> |Consistent with the complete table content in the split bills page when Period = By Day. |
|Split bills summary by billing cycle |SplitItemDetailMonthly<br><br> |Consistent with the complete table content in the split bills page when Period = Billing cycle. |
|Cost bill details |AmortizedCostBillDetail |Consistent with the complete table content on the cost bills \> cost details page. |
|Cost bill summary by day of allocation |AmortizedCostBillDaily |Consistent with the complete table content on the cost bills \> cost details page. |
|Cost bill summary by month of allocation |AmortizedCostBillMonthly<br><br> |Consistent with the complete table content on the cost bills \> cost overview page. |
|Cost analysis report template |CostAnalyse<br><br> |Consistent with the statistical report content on the cost analysis report template page. |
