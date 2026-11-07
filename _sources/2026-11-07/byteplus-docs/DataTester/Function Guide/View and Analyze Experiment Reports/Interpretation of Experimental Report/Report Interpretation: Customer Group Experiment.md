---
title: "Report Interpretation: Customer Group Experiment"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Report-Interpretation-Customer-Group-Experiment"
---

After you create and complete the customer group experiment, debug and open the customer group experiment, you can view the experimental index data of the customer group dimension in the experimental report page. This article introduces the interpretation of the relevant data of the main experimental report of the customer group experiment report for you.

<span id="83f8f124"></span>
# Overview of the customer group experiment report page


|Experiment details page |Experiment report page |Data Metrics/Advanced Analytics Page |
|---|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/97424d2795d146758eb465166cf6000a~tplv-goo7wpa0wc-image.image) </span><br><br><br>* You can view the guest group configuration details of the guest group experiment on the **experiment details** page.<br><br>* As depicted in the figure above, the guest group experiment consists of two guest groups: test and test 1. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a044eea25cf04974a6ae436a113debfc~tplv-goo7wpa0wc-image.image) </span><br><br><br>* In the experimental report page, in addition to the experimental conclusions based on the experimental version, the experimental results are also given synchronously in combination with the experimental version + customer group.<br><br>* In the Data Overview section, you are shown the probability of winning for each customer group in each experimental version; and the probability of winning for each experimental version in each customer group.<br><br>* At the same time, a more professional variance analysis table is also provided to facilitate in\-depth data analytics. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0efe5ab870e54c69bef89f55a9b3c2b4~tplv-goo7wpa0wc-image.image) </span><br><br><br>* You can view the metrics data under each customer group for each experimental version in the Data Metrics/Advanced Analytics page.<br><br>* The caliber and interpretation of the index data are similar to those of ordinary A/B experiments. For details, please refer to the report interpretation document of ordinary A/B experiments. |


Of which:


* For an introduction to the data calculation of the winning probability, please refer to the following: [Winning Guest Group & Winning Experimental Version & Winning Probability](https://docs.byteplus.com/docs/DataTester/Report-Interpretation-Customer-Group-Experiment#8299f533).

* For the calculation of ANOVA(Analysis of variance) table data see below [ANOVA table](https://docs.byteplus.com/docs/DataTester/Report-Interpretation-Customer-Group-Experiment#ed2aa218).


<span id="8299f533"></span>
# Winning Guest Group & Winning Experimental Version & Winning Probability


* For each experimental version, the Monte Carlo method is used to obtain the winning probability of each customer group.

* For each customer group, the Monte Carlo method is used to obtain the winning probability of each experimental version.

* Introduction to the calculation method of Monte Carlo method

   In many cases, we need to calculate the probability of winning an event. For example, in a casino, we need to calculate the probability of winning a game in order to decide whether to participate in that game. In investing, we need to calculate the probability of winning an investment strategy in order to decide whether to adopt it.

   The Monte Carlo method is a commonly used method for calculating the probability of winning. It estimates the probability of winning an event by simulating the outcome of a large number of random events.

   In the multi\-guest experimental scenario, the winning probability of each experimental version is obtained as follows.

   1. Modeling. Use the normal distribution to approximate and calculate the mean and variance of the comparison target (experimental version, population) indicators.

   2. Simulation calculation. Take three experimental groups and two groups as an example, compare the winning probabilities of the three experimental groups under population 1.

      * Step 1:3 experimental groups, calculate the mean and variance of each group respectively;

      * Step2: From the above (mean, variance) normal distribution, sample 1 random number respectively, compare which is the largest, such as group 1 is the largest, then group 1 counts plus 1;

      * Step3: Cycle step2 times 100,000 times to get the maximum number of times for group 1 (such as 60,000), the maximum number of times for group 2 (such as 30,000), and the maximum number of times for group 3 (such as 10,000).

   3. Calculate the probability of winning. Group 1 win probability 0.6, Group 2 win probability 0.3, Group 3 win probability 0.1

      Please note that the accuracy of the Monte Carlo method depends on the number of simulations. Usually, the more times the simulation is performed, the higher the accuracy. However, as the number of simulations increases, so does the computation time. Therefore, in practical applications, we need to choose the appropriate number of simulations according to the requirements of the problem and the limitations of computing resources. In our example, the number of simulations is 100,000.


<span id="ed2aa218"></span>
# ANOVA table

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83e972ed46db4b6ca3fb2f465a78160a~tplv-goo7wpa0wc-image.image) </span>

ANOVA table:


* The main analysis objects: **row factors (population)** , **column factors (strategy),**  these two factors.

   * **Line factor (population):**  It is the target group factor of different customer groups.

   * **Column factors (policies):**  that is, factors for different experimental versions.

* Main analysis objectives: to analyze the interaction effect, main effect and simple main effect of the two factors.

   * Interaction effects are used to explore whether there is an interaction between two or more factors, i.e. whether the effect of one factor depends on the level of the other.

   * Main Effect Analysis: Aims to evaluate the impact of individual factors on experimental results, focusing on the overall effect of the factors themselves, without considering the interactions between the factors.

   * Simple principal effects: When interaction effects are significant, a simple principal effects analysis is used to further refine the understanding and explore the effects of a single factor when controlling for a specific level of other factors. Briefly put, it is to consider the effects of each factor at different levels of another factor in the context of considering interaction effects.

* Main analysis data dimensions: including **error squares and SS** , **degrees of freedom df** , **mean square error MS** , **F value** , **P value** , **F critical value** these data fields.

   * Among them, according to the configuration of the guest group experiment, the data aggregated by DataTester is:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4cc44e32352c4934a60e39c89ac88f29~tplv-goo7wpa0wc-image.image) </span>

   * The statistics side summarizes the data into the following standard format:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a3ef761a0ab0465eaf018ad9b5052346~tplv-goo7wpa0wc-image.image) </span>

   * The data from the ANOVA table are calculated as follows:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/04891a40fad64472a6d522aceabab1df~tplv-goo7wpa0wc-image.image) </span>


For more information on ANOVA, see the [What is ANOVA series of documents ](https://support.minitab.com/en-us/minitab/help-and-how-to/statistical-modeling/anova/supporting-topics/basics/what-is-anova/), [Two-way ANOVA II (with interaction) ](https://mengte.online/archives/1322).
