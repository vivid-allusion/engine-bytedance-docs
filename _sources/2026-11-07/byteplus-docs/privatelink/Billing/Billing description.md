---
title: "Billing description"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Billing-rules"
---

<span id=".5qaC6L-w"></span>
## Overview

The payer account for the PrivateLink service is determined by the endpoint service. It defaults to the endpoint account. Only some BytePlus services support having the endpoint service account act as the payer.

PrivateLink supports the pay\-as\-you\-go billing method. Pay\-as\-you\-go is a metering method where you activate and release resources on demand at any time without purchasing a large amount of resources in advance.

<span id=".6K6h6LS56KeE5YiZ"></span>
## Billing rules

PrivateLink currently charges Endpoint Instance Fees and Traffic Processing Fees, which are settled on an hourly basis.

The overall billing formula is: **PrivateLink cost = Endpoint instance fee + Traffic processing fee.** 


|Billing items |Formula |Billing description |
|---|---|---|
|Endpoint instance fee |Endpoint Instance Fee = Instance Unit Price (USD/instance/hour) × Peak Number of AZs in the Endpoint (instances) × Usage Duration (hours) |* One Availability Zone within an Endpoint counts as one billing instance. The instance unit price refers to the price per billing instance per billing cycle.<br><br>* The method for determining **the maximum number of billable Availability Zones** (AZs) differs based on the payer account.<br><br>   * Payer account is the Endpoint Account: This refers to the peak number of AZs within the endpoint at any given moment during a billing cycle.<br><br>   * Payer account is the Endpoint Service Account: This refers to the sum of the peak number of AZs across all endpoints associated with the endpoint service at any given moment during a billing cycle.<br><br>* **Usage Duration**: Billing starts from the successful creation of the order. Usage lasting less than one hour is billed as a full hour.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Adding/removing AZs to/from an endpoint or deleting an endpoint will change the number of AZs, which may cause the PrivateLink charges to change.</div><br> |
|Traffic processing fee |Traffic Processing Fee = Traffic Unit Price (USD/GB) × Processed Traffic (GB) |* **Traffic unit price** refers to the price for processing 1 GB of data on PrivateLink connections.<br><br>* The **Processed traffic** volume is defined differently depending on the payer account.<br><br>   * Payer account is the Endpoint Account: The total bidirectional traffic (inbound + outbound) passing through the endpoint per billing cycle.<br><br>   * Payer account is the Endpoint Service Account: The total bidirectional traffic (inbound + outbound) passing through the endpoint service per billing cycle. |


<span id=".6LWE5rqQ5Lu35qC8"></span>
## Resource pricing

You can check the price of PrivateLink resources on the [Price calculator](https://www.byteplus.com/en/pricing?product=PrivateLinkGateway&tab=2) page. The Price Calculator provides reference prices. The specific cost shall be based on the actual order result in the [PrivateLink console](https://console.byteplus.com/pl/endpoint).
