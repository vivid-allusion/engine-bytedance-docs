---
title: "Ray Data backpressure enhancement analysis"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Ray_Data_backpressure_enhancement_analysis"
---

<span id="a7a18d92"></span>
## Background

The concurrency of Ray Data operators is mostly set manually, and automatic detection generally does not meet the requirements for resource utilization. However, manually setting operator concurrency can easily trigger throttling, and it is currently difficult to obtain the reason for throttling. Volcano EMR provides features for analyzing backpressure causes and for adding more backpressure strategies.

<span id="cc511e1d"></span>
## Backpressure trigger conditions

There are four trigger conditions in total:


* **Resource reservation enabled**: DataContext.get_current()data_context.op_resource_reservation_enabled = true (default). Each time a new task is submitted, the system checks whether the required resources are available. All resources are divided into reserved and shared.

* **Resource reservation disabled:**  DataContext.get_current()data_context.op_resource_reservation_enabled = false. Unified resource management

* **Backpressure strategy:**  The open\-source strategy only supports ConcurrencyCapBackpressurePolicy, which checks whether the number of running tasks exceeds the set concurrency limit.

* **Can the operator add input:**  This checks whether there are remaining free slots in the actor pool, mainly by comparing the number of running tasks on the actor with the default number.


<span id="acb7d352"></span>
## Backpressure enhancement

<span id="2f878584"></span>
### Backpressure observability enhancement


* Before enhancement:


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e03e2a820b4d4c9c9d377ab5680a2e00~tplv-goo7wpa0wc-image.image" width="1585px" /></div>



* After enhancement

   * Concurrency backpressure strategy


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/949510af6b544b3d9c6adaaa9264f764~tplv-goo7wpa0wc-image.image" width="2628px" /></div>



* Backpressure in non\-reservation mode


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dfdb09339e574dc0afb8512547fce304~tplv-goo7wpa0wc-image.image" width="2848px" /></div>



* Backpressure in reservation mode


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db7ac2ef425c4b04b055978cc28ba037~tplv-goo7wpa0wc-image.image" width="2832px" /></div>



* Insufficient free slots in the actor


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/747c55ac2e8e40fca83680ff876c1839~tplv-goo7wpa0wc-image.image" width="2848px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae67854e8504409eaeb99c59c158f31d~tplv-goo7wpa0wc-image.image" width="2882px" /></div>


<span id="fe8d4cfe"></span>
### Add backpressure strategies

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a52e6b51991b487eb8955d14634a6e16~tplv-goo7wpa0wc-image.image" width="2950px" /></div>


<span id="086784d8"></span>
## How to optimize execution parameters

Example: Execution chain adjustment

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9bf113b6e1734b8ca8e424bac7a835b6~tplv-goo7wpa0wc-image.image) </span>


1. After submitting the default parameters, it was found that the overall CPU was not utilized (20/46), and the number of ReadBinary tasks could not be increased. The diagram below shows that two types of backpressure were triggered:

   1. New tasks backpressure: Backpressure in resource reservation mode, with excessive shared resource usage.

      1. The shared resource mode should be set to false. op_resource_reservation_enabled = false

   2. Should add input: There are no free slots on the actor, meaning resources are insufficient.

      1. Increase *GPU resources used by BgeEmbeddingMapper*


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0fb15ee2e5b648bc861e65ded75de6a0~tplv-goo7wpa0wc-image.image" width="2896px" /></div>



2. After adjusting the resource reservation parameters in the previous step, it can be seen that CPU resources are basically fully utilized.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc81c642be3a43d093ab5673a669759b~tplv-goo7wpa0wc-image.image" width="2868px" /></div>


However, the CPU value shown in Resources here is only a logical count, not the actual CPU utilization. Actual resource utilization can be viewed through the UI.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/609ef7f24cb14390ab5815ca5206d9d1~tplv-goo7wpa0wc-image.image" width="1652px" /></div>


If CPU utilization is relatively low, you can adjust num_cpus, concurrency, and batch_size to control specific resource utilization. If resource utilization is not high, you can set DEFAULT_MAX_TASKS_IN_FLIGHT to 4.


3. To address memory usage issues, adjust the following two parameters.

* op_resource_reservation_enabled

* DEFAULT_OBJECT_STORE_MEMORY_LIMIT_FRACTION_WO_RESOURCE_RESERVATION
