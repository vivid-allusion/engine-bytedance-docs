---
title: "Description of unsubscription and configuration modification"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/unsubscribe-or-change-instructions"
---

This topic describes the fees for modifying configurations and unsubscribing from SQL Server instances.

<span id=".5Y-Y6YWN6LS555So6K-05piO"></span>
## **Description of configuration modification fees**


* **Pay\-as\-you\-go**

   Pay\-as\-you\-go instances are billed hourly, and after modification of the configuration, they will be billed hourly at the new configuration's price.

* **Subscription**

   Configuration changes for subscription instances are categorized into two types: resource upgrades and resource downgrades.

   * Upgrade: When you modify resource specifications, the change is considered an upgrade if the hourly list price of the new configuration is greater than or equal to that of the original configuration. In this case, the system will calculate the price difference you need to pay between the new and original configurations based on the upgrade formula.

   * Downgrade: When you modify resource specifications, the change is considered a downgrade if the hourly list price of the new configuration is less than that of the original configuration. The system will then calculate the price difference between the new and old configurations based on the downgrade refund formula and refund the amount to your account balance. If you downgrade and renew your instance, the system will first calculate the cost using the downgrade refund formula. If this results in a refund, the price difference between the old and new configurations will be credited to your account balance. If it results in a charge, the system will recalculate the cost using the upgrade formula, and you will need to pay the price difference.

   
   |Type of specification modification |Billing description |
   |---|---|
   |Upgrade |Upgrade order fee<br><br>= New configuration fee \- Remaining value of old configuration<br><br>= New configuration list price (hourly) \* Remaining duration (hours) \* Discount \- Old configuration list price (hourly) \* Remaining duration (hours) \* Discount |
   |Downgrade |Downgrade order fees<br><br>= New configuration fee \- Refundable remaining value of the old configuration<br><br>= List price of the new configuration (hourly) \* Remaining duration (hours) \* Discount \- Actual order value / Subscription duration \* Remaining duration<br><br>= New configuration list price (hourly) \* Remaining duration (hours) \* Discount \- (Actual order value \- Actual order value \* Used duration / Subscription duration \* Downgrade refund coefficient)<br><br>= New configuration list price (hourly) \* Remaining duration (hours) \* Discount \- (Actual order value \- Actual order value \* Used duration / Subscription duration) \* Downgrade refund coefficient |
   


<span id=".6YCA6K6i6LS555So6K-05piO"></span>
## **Unsubscription fees**


* Pay\-as\-you\-go instances are unsubscribed upon deletion and are not eligible for refunds.

* SQL Server subscription instances do not support a 7\-day unconditional unsubscription. For more details on the unsubscription rules, see [Unsubscription management](https://docs.byteplus.com/en/docs/bandwidthpackage/Unsubscription).
