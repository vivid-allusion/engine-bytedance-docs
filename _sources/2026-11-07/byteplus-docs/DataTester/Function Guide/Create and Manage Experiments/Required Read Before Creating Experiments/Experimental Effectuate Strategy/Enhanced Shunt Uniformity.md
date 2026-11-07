---
title: "Enhanced Shunt Uniformity"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Enhanced-Shunt-Uniformity"
---

The programming experiment has added the function of "Enhanced Shunt Uniformity". After turning on the function switch, you can enhance the uniformity of the experimental traffic between each version of the experiment in the traffic circle before the experiment starts, that is, before the experiment starts, ensure that the corresponding experimental metrics are not significantly different in each experimental version, in order to improve the reliability of the experimental results.

<span id="df23999e"></span>
# Configuration for enhanced shunt uniformity

In the second step of programming the experiment creation, you can configure whether to turn on the Enhanced Shunt Uniformity switch when setting the effective policy for the experiment.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73e9c53bd0164ccc936e085832105a0c~tplv-goo7wpa0wc-image.image) </span>

After turning on the switch, you can choose whether the uniform shunt method is "by metric value" or "by cluster" ("by cluster" is only supported by client side experiments).

<span id="b07d36a7"></span>
## Uniform diversion according to index value


* Parameter configuration instructions

   
   |Parameter |Configuration instructions |
   |---|---|
   |Metrics<br><br>to be leveled |* Select the metric that needs to be evenly distributed in the drop\-down box, and the metric selected here will later default to the focus metric of the experiment. At the beginning of the experiment, these leveled metrics did not differ significantly in the traffic distribution between the experimental versions.<br><br>* Currently, a maximum of 3 metrics are supported. |
   |Select a time range |Set the time range for uniform shunting. |
   |Heavy random stop condition |Set the conditions for restochastic, which is to run the simulated shunt multiple times to find the best shunt method under the conditions.<br><br><br>* Maximum number of runs: To prevent repeated random infinite loops, set the maximum number of runs.<br><br>* P\-value: Set the p\-value threshold for judging that the difference is not significant before the experiment. |
   

* Uniform split logic: The experimental metrics configured here did not differ significantly across experimental versions before the experiment began.


<span id="f90d2d14"></span>
## Uniform shunting by cluster (client\-side experiment support only)


* Parameter configuration instructions

   
   |Parameter |Configuration instructions |
   |---|---|
   |Select cohorts |Select the population that needs to be evenly distributed in the drop\-down box. Subsequent to the start of the experiment, the population selected here will be evenly distributed among each experimental version. |
   |Heavy random stop condition |Set the conditions for restochastic, which is to run the simulated shunt multiple times to find the best shunt method under the conditions.<br><br><br>* Maximum number of runs: To prevent repeated random infinite loops, set the maximum number of runs.<br><br>* P\-value: Set the p\-value threshold for judging that the difference is not significant before the experiment. |
   

* Uniform shunt logic: The population configured here is evenly distributed across experimental versions.


<span id="1c35860b"></span>
# Check the state of heavy randomization before the experiment

After the experiment is created, during the debugging stage before the experiment starts, the experimental traffic will be uniformly distributed according to the above configuration. You can view the current heavy randomization state in the experiment details.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df4afbda960b4888aab327e78d0a40c3~tplv-goo7wpa0wc-image.image) </span>

When the condition of heavy random stops is reached, the experiment can be officially started.
