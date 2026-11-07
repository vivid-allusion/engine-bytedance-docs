---
title: "Pay-as-you-go"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Pay-as-you-go"
---

Pay\-as\-you\-go is a postpaid billing method. There is no need to purchase massive resources in advance. You can activate and release resources on demand anytime and pay for the FaaS (Function Service) resources actually used.

<span id="billing-description"></span>
## Billing description

The FaaS resource billing items are categorized as below:


* **Number of function requests**: Charged according to the number of times（bits） the function is requested to execute. Formula: `Cost of function requests = Number of requests × unit price`.

* **Resource usage duration**: Charged based on the execution duration of the function resources, that is, from the start of the request execution to the completion of the request. The billing granularity is 1 millisecond, and less than 1 millisecond is charged as 1 millisecond. Function resources are divided into the following types, each type of resource has different costs:

   * Categorized by computing power mode:

      * **GPU instance**: Providing GPU computing power based on NVIDIA graphics cards (elastic/reserved) function instances.

         Formula: `GPU Instance cost = (Memory size × duration unit price + GPU card size × duration-gpu unit price) × Instance execution duration + Number of requests × request unit price + Traffic_BGP (if any) × unit price`

      * **CPU instance**: Function instances (elastic/reserved) equipped with vCPU and memory (MEM) resources.

         Formula: `CPU Instance cost = (vCPU size × duration_vcpu unit price + Memory size × duration_mem unit price) × Instance execution duration + Number of requests × request unit price + Traffic_BGP (if any) × unit price`

   * Categorized by instance type:

      * **Elastic instance**: The system automatically allocates and releases the instance for functions. Same calculation formula as CPU/GPU instances.

      * **Reserved instance**: Function instances that you allocate, release, and manage on your own. Same calculation formula as CPU/GPU instances.

* **Outbound public network traffic**: The outbound traffic cost generated when the function accesses the internet through the default network card. The billing granularity is 1 Byte; less than 1 Byte is charged as 1 Byte. Formula: `Outbound public network traffic cost = Traffic_BGP × price`

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For functions triggered by the API Gateway, data returned after the function execution finishes is not recorded as function outbound traffic; data returned by the API Gateway to the client\-side is recorded and billed as outbound traffic by the API Gateway.   </div>
   

* **Microservices applications billing**: The CPU allocation mode of microservices applications is always occupies CPU, and supports using GPU resources. The platform does not manage the traffic of microservices applications, or charge the fees of invocation counts. The fees of resources are billed as reserved instances.

* **Cloud sandbox billing information**: Cloud sandbox does not charge fees based on the number of invocations. Resource fees are charged based on the lifecycle of reserved instances. For the relevant billing items, see the **Billing items** section below in this article, specifically the **Cloud sandbox** content.


<span id="billing-items"></span>
## Billing items

<span id="JwXMRlEL"></span>
### Function and application


|Billing category |Billing object |Billing item |Unit price (Asia Pacific Johor) |
|---|---|---|---|
|Function request billing |Request |request |0.0000002 USD/Request |
|Resource usage billing |CPU elastic instance |duration_vcpu |0.0000195 USD/vCPU/Second |
|||duration_mem |0.0000045 USD/GiB/Second |
||CPU reserved instance |duration_vcpu_reserved |0.00000975 USD/vCPU/Second |
|||duration_mem_reserved |0.00000225 USD/GiB/Second |
||GPU elastic instance |duration\-gpu |0.0000169 USD/GiB/Second |
|||duration |0.0000213 USD/GiB/Second |
||GPU reserved instance |duration\-gpu\-reserved |0.0000113 USD/GiB/Second |
|||duration\-reserved |0.0000088 USD/GiB/Second |
|Outbound public network traffic |Traffic_BGP |traffic_BGP |0.11 USD/GiB |


<span id="A3MAJE08"></span>
### Cloud sandbox


|Billing category |Billing object |Billing item |Unit price (Asia Pacific Johor) |
|---|---|---|---|
|Resource usage billing |CPU reserved instance |duration_vcpu_reserved |0.00000975 USD/vCPU/Second |
|||duration_mem_reserved |0.00000225 USD/GiB/Second |
|Outbound public network traffic |Traffic_BGP |traffic_BGP |0.11 USD/GiB |


<span id="billing-cycle"></span>
## Billing cycle

The pay\-as\-you\-go Function Service has a billing cycle that is accurate to one millisecond, and the bill generated in this billing cycle is settled hourly. The bill fees will be automatically deducted from your BytePlus account. You can view the bill details in the  [Billing center > Bill management](https://console.byteplus.com/finance/bill/detail).

If the available credit (including account balance and coupons) in your account is less than the amount of the bill to be settled, then you will receive SMS or email notification of insufficient balance.

<span id="billing-example"></span>
## Billing example

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="tip">This section will take functions and applications as the billing examples and give prices for reference only. Prices are subject to change. See the console for the latest prices.</div>


**Example 1: Pay\-as\-you\-go billing for a CPU type Elastic instance**


* Instance specification: 1 vCPU, 2 GiB of memory

* Region: Asia Pacific (Johor)

* Instance execution duration: 1 hour (3600 seconds)

* Number of function requests: 100,000 calls

* Public network access: Function did not access the public network


The total fees are as follows:

`Total cost = (1 vCPU × 0.0000291 USD/vCPU/second + 2 GiB × 0.0000067 USD/GiB/second) × 3600 seconds + 100,000 bits function requests × 0.0000003 USD/Bits = 0.183 USD`

**Example 2: Reserved instance billing for a certain GPU card type**


* Instance specification: NVIDIA GPU (computing power 1 card, video memory 24 GiB, memory 60 GiB)

* Region: Asia Pacific (Johor)

* Instance execution duration: 1 hour (3600 seconds)

* Number of function requests: 100,000 calls

* Public network access: Accessed public network through default network card and generated 1.2 GiB traffic


The total fees are as follows:

`Total cost = (24 GiB × 0.0000113 USD/GiB/second + 60 GiB × 0.0000088 USD/GiB/second) × 3600 seconds + 100,000 bits function requests × 0.0000003 USD/Bits + 1.2 GiB × 0.11 USD/GiB = 3.03912 USD`
