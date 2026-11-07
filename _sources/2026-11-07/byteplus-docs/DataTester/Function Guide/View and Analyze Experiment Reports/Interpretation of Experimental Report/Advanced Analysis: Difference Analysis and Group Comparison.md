---
title: "Advanced Analysis: Difference Analysis and Group Comparison"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Advanced-Analysis-Difference-Analysis-and-Group-Comparison"
---

<span id="一-概述"></span>
# 1. Overview

**Why is a variance analysis necessary?** 

After the experiment is completed, the experimental results are for all the audience groups of the experiment, and the conclusion that the corresponding strategy has positive or negative effects can be obtained through the data. However, a strategy that reaches positive or negative conclusions for all users is not the same as reaching the same conclusion for subdivided users. At this time, we can use group comparison and difference analysis to obtain a conclusion that the experimental strategy is positive/negative for a certain segment of the population.

<span id="二-名词解释"></span>
# 2. Term explanation


* **Group comparison:**  by splitting all users into multiple user groups for comparison

* **Difference analysis:**  using Monte Carlo method, get a strategy for a group of the optimal strategy, and a group of the most suitable for a strategy of the group.

* **Monte Carlo method:**  Monte Carlo method is also called statistical simulation method, statistical test method. It is a numerical simulation method that takes probability phenomena as the research object. It is a calculation method of estimating unknown characteristic quantity by obtaining statistical value by sampling survey method. Monte Carlo is a famous gambling city in Monaco, and the law is named to demonstrate the nature of its random sampling. Therefore, it is suitable for computational simulation experiments on discrete systems. In computational simulation, the stochastic characteristics of the system can be simulated by constructing a probabilistic model similar to system performance and conducting random experiments on a digital computer.


<span id="三-应用场景"></span>
# 3. Application scenario

**Financial product promotion**

Background: There are three kinds of wealth management products: gold, stock fund and bond fund. We conducted experiments with all users, promoted different types of financial products, and analyzed which financial products were most popular with users, thus increasing the investment of the financial products.

Analysis: Through experiments, we found that the purchase rates of gold, stock funds, and bond funds were 3.11%, 7.52%, and 4.38%, respectively. So should we promote equity funds to all users? At this point, we use group comparison to divide users into four groups: under 25, 25\-35, 25\-45, and over 45. After analysis, we found that younger users are more likely to prefer equity funds, while older users are more likely to prefer bond funds. Similarly, we can also find that female users are more willing to pay for gold wealth management products, while male users prefer fund\-based wealth management products.

<span id="四-功能使用"></span>
# 4. Function usage


1. Log into the A/B test console.

2. In the left navigation bar, select **A/B Testing** \> **Experiment List**.

3. Select the specified experiment in the experiment list to enter the experiment details page.

4. On the Experiment Details page, click the **Advanced Analysis** tab and select **Difference Analysis** on the left side of the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a736200a375d4145b51d4202b837d323~tplv-goo7wpa0wc-image.image) </span>

5. Select Specify Metrics on the left side of the page and complete the following configuration for variance analysis.

   
   |Configuration item |Description |
   |---|---|
   |Set query time period |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dbcf9263683741cd9707d8e5d7ffc1c9~tplv-goo7wpa0wc-image.image) </span><br><br><br>1. Choose **from start\-to\-date accumulation**, **flexible accumulation**<br><br>   * **Start\-to\-date accumulation**<br><br>      * Number of users entering the group: accumulated from the first day of the experiment to the current date<br><br>      * Other metrics: cumulative by filter time<br><br>   * **flexible accumulation**<br><br>      * Number of incoming users: accumulated by filter time<br><br>      * Other metrics: cumulative by filter time<br><br>2. Select **day level**, **hour level**, **5 minute level**<br><br>3. Specify a specific time period. |
   |Attribute filtering |Build an attribute filter by selecting an attribute, adding a condition, and setting a range of values.<br><br><br>* Click **Add and condition** to add multiple attribute filter conditions, and the relationship between multiple conditions is and.<br><br>* Click **Add cluster** to add a user cluster as a filter condition, and the relationship between it and other conditions is and.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4953c13e8e844a9fae0e5d519c71904c~tplv-goo7wpa0wc-image.image) </span> |
   |Group comparison |Support adding multiple groups, and set attribute filter conditions for groups to compare groups.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/53626d0be012409b80a4fc85edee3d9f~tplv-goo7wpa0wc-image.image) </span> |
   

6. Click **Query** to view the data display.

   A variance analysis module appears at the bottom of the page to compare the applicability of different experimental strategies to different client bases. Support for viewing experimental versions, user grouping, and group comparison data.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/893ceca32db64b1cad4deefc06eb996a~tplv-goo7wpa0wc-image.image) </span>
