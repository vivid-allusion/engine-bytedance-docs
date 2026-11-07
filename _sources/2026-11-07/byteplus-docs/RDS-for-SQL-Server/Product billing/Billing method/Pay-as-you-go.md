---
title: "Pay-as-you-go"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/pay-as-you-go"
---

Pay\-as\-you\-go is a billing method with which you use first and pay later. You don't need to buy a large quantity of resources in advance, but purchase and release them on demand at any time.

<span id="brief-introduction"></span>
## Brief introduction

The pay\-as\-you\-go method applies to scenarios with significant business growth in a short period of time, such as flash sales. The system generates fees by the second based on the resources you actually use and deducts fees from your account by the hour, so you pay only for what you use. If the purchased resources are no longer in use, you can delete them at any time, and billing will stop instantly.

<span id="fvcbBIc0"></span>
## Purchase prerequisites


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* As per the regulations in the Chinese mainland, you must have completed real name registration before you can activate and use cloud services on nodes in the Chinese mainland through BytePlus.  For more details, refer to [Real name registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration).

* When purchasing an RDS for SQL Server instance with the pay\-as\-you\-go billing method, the total value of your account balance (i.e., cash balance) and vouchers must be greater than 100.00 USD.


<span id="billing-hours"></span>
## Billing hours

Without considering the shutdown of arrears, the billing time of the RDS for SQL Server instance in the entire life cycle is the completion of the instance creation to start billing, and the billing ends when the instance is released.

<span id="settlement-cycle"></span>
## Settlement cycle

The pay\-as\-you\-go billing method of SQL Server instances issue a bill for the previous hour on the hour (subject to UTC + 8:00), and the bill amount is deducted from the account balance.

For example, the unit price of an instance of a certain specification is 0.89 USD per hour, and the settlement fee of the instance is billed according to the usage time and the second level.


* For a usage time of 30 minutes, the cost is calculated as follows: 

   0.89 USD/hour ÷ 3600 seconds × 60 seconds × 30 minutes = 0.445 USD

* For a usage duration of 1 hour and 30 minutes, the cost calculation is as follows::

   0.89 USD/hour ÷ 3600 seconds × 60 seconds × 90 minutes = 1.335 USD


<span id="change-configuration"></span>
## Change configuration

The pay\-as\-you\-go billing method of SQL Server instances support real\-time configuration changes for instances of the same architecture and type. After the instance specification is successfully changed, the latest specification configuration is displayed in the target instance of the instance list. After the instance configuration is successful, the internal configuration is also the latest configuration.

For a pay\-as\-you\-go instance, the fee settlement rules for changing the instance specification are as follows:


* The price of the replacement configuration is the price of the current target specification, and the actual replacement is paid. The price in different periods is slightly different. The specific price is subject to the actual matching situation.

* The replacement configuration order amount is in hours, and the price is accurate to two decimal places.
