---
title: "Configuration change and unsubscribion instructions"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Configuration_change_and_unsubscribion_instructions"
---

This topic describes the fees for changing the configuration of and unsubscribing from a Milvus for VectorDB instance.

<span id="crvU27gZ"></span>
## **Upgrade fees**


* Pay\-as\-you\-go

   You are charged for pay\-as\-you\-go instances hourly. After you change the configuration, billing follows the new configuration price per hour.

* Subscription

   Subscription instance configuration changes include resource upgrades and downgrades.

   * Upgrade: When you change resource specifications, if the new configuration price (hourly) is greater than or equal to the old configuration price (hourly), the system calculates the price difference based on the upgrade formula.

   * Downgrade: When you change resource specifications, if the new configuration price (hourly) is less than the old configuration price (hourly), the system calculates the price difference based on the downgrade refund formula. If the result is a refund, the system will refund the price difference by using the original payment method. If the result is a charge, the system recalculates using the upgrade formula, and you must pay the price difference.



|**Configuration change type** |**Cost calculation logic** |**Description** |
|---|---|---|
|Upgrade |Total amount due for upgrade orders<br><br>= new configuration fees \- remaining value of old configuration<br><br>= new configuration price (hourly) \* remaining hours \* discount \- old configuration price (hourly) \* remaining hours \* discount |* New configuration hourly price calculation rules:<br><br>   * For daily subscription, the new configuration price (hourly) = daily price/24.<br><br>   * For monthly subscription, the new configuration price (hourly) = monthly price/30/24.<br><br>   * For yearly subscription, the new configuration price (hourly) = subscription price/365/24.<br><br>* Remaining time = [instance expiration time (accurate to seconds) \- order submission time (accurate to seconds) + 1]/3600.<br><br>* Discount: the new configuration discount will be re\-matched with the latest system discount based on the remaining time. The old configuration discount is matched in the original order.<br><br>* Configuration fees = the total cost of all billing items included in this configuration/instance. |
|Downgrade |Total amount due for downgrade orders<br><br>= new configuration fees \- refundable remaining value of the old configuration<br><br>= new configuration price (hourly) \* remaining hours \* discount \- actual value of the order/purchase duration of the order \* remaining duration<br><br>= new configuration price (hourly) \* remaining hours \* discount \- (actual value of the order \- actual value of the order \* used duration/purchase duration of the order \* downgrade refund coefficient)<br><br>= new configuration price (hourly) \* remaining hours \* discount \- (actual value of the order \- actual value of the order \* used duration/purchase duration of the order) \* downgrade refund coefficient |* Calculation rules for new configuration hourly price:<br><br>   * For daily subscription, the new configuration price (hourly) = daily price/24.<br><br>   * For monthly subscription, the new configuration price (hourly) = monthly price/30/24.<br><br>   * For yearly subscription, the new configuration price (hourly) = subscription price/365/24.<br><br>* Remaining duration = [instance expiration time (accurate to seconds) \- order submission time (accurate to seconds) + 1]/3600.<br><br>* Used duration = original purchase duration \- remaining duration, accurate to seconds.<br><br>* Discount: the new configuration discount will be adjusted based on the remaining duration to match the latest system discount.<br><br>* Configuration fees = the sum of all billing item fees included in this configuration/instance.<br><br>* If the refundable remaining value of the old configuration is less than 0, it will be calculated as 0, meaning no remaining value.<br><br>* If the billing rule for the cloud service states no refund for downgrade (based on the cloud product billing documentation), the refund amount after downgrade will be 0.<br><br>* Order true value:<br><br>   * The real value of a new purchase or renewal order is the actual amount paid for the order.<br><br>   * The real value of the instance after reconfiguration: used for recalculating the true value for further reconfiguration and calculating the refundable remaining value.<br><br>      * The real value after reconfiguration = total amount due for this reconfiguration + actual remaining value of the old configuration.<br><br>      * Actual remaining value of the old configuration = min{theoretical remaining value of the old configuration, actual remaining value of the original old order}.<br><br>      * Actual remaining value of the original old order = actual value of the original order \* (remaining duration of the original order/purchase duration of the original order), with duration accurate to seconds. |


<span id="PWJRDz4z"></span>
## **Unsubscription fees**


* Deleting a pay\-as\-you\-go instance is equivalent to unsubscription and does not involve a refund.

* Subscription instances will be refunded based on the unsubscription refund policy.
