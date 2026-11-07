---
title: "Preparation for Experiments"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Preparation-for-Experiments"
---

**Before A/B testing, you need to connect to the application, specify the type of experiment, design the experiment, and finally create the experiment in the BytePlus A/B test.** 

<span id="一、接入应用"></span>
## 1. Access application

A/B testing supports client side, web side, server side and other access methods. Please refer to the following documents to complete the SDK access, data and streaming service access according to the type of application you need to access.

Data access work is generally completed by R & D personnel, you can [Data Access Overview](https://docs.byteplus.com/docs/DataTester/Data-Access-Overview) understand how to access, or you can directly view the Data Transmission Service instructions of each client side and server side through the following.

**Client side SDK**


* [iOS SDK Integration](https://docs.byteplus.com/docs/DataTester/iOS-SDK-Integration)

* [Android SDK Integration](https://docs.byteplus.com/docs/DataTester/Android-SDK-Integration)

* [Web/JavaScript SDK Integration](https://docs.byteplus.com/docs/DataTester/Web-JavaScript-SDK-Integration)

* [WeChat Mini Program SDK Integration (Universal)](https://docs.byteplus.com/docs/DataTester/WeChat-Mini-Program-SDK-Integration-Universal)


**Server side SDK**


* [Server Side SDK Overall Description](https://docs.byteplus.com/docs/DataTester/Server-Side-SDK-Overall-Description)

* [Java SDK](https://docs.byteplus.com/docs/DataTester/Java-SDK)

* [Python SDK](https://docs.byteplus.com/docs/DataTester/Python-SDK)

* [Go SDK](https://docs.byteplus.com/docs/DataTester/Go-SDK)

* [Traffic Shunt Agent](https://docs.byteplus.com/docs/DataTester/Traffic-Shunt-Agent)

* [HTTP API](https://docs.byteplus.com/docs/DataTester/HTTP-API)


<span id="二、明确实验类型"></span>
## 2. Identify the type of experiment

You need to identify client side and server side experiments before selecting a specific category.

<span id="服务端实验"></span>
### Server side experiment

Server side experiment refers to the experiment that obtains the experimental packet information through the server side and controls the configuration to take effect or be delivered.

**Applicable scenarios:** 


* Some functions can only be controlled by the server side, such as information delivery algorithms (such as what users will see in the feed stream after opening Jinri Toutiao), product functions controlled by server side logic (such as push), etc.

* The experimental configuration takes effect when the APP is not required to be invoked. The client side has enough time to make a request to the server side, obtain the experimental configuration, and then present the policy to the user.


**Server side experiments include:** 


* **Programming experiment:**  AB test through code programming, widely used in front\-end optimization, policy optimization and back\-end algorithm optimization of various experimental scenarios. See [Programming Experiment](https://docs.byteplus.com/docs/DataTester/Programming-Experiment).

* **Push experiment:**  Push notification experiments can test the title, content, click action, etc. of push notifications. When you want to send a notification message to your existing users or start a new marketing notification, but you are unsure how effective it will be, you create a push notification experiment to find the ideal notification copy and message presentation by testing various notification experiment groups in your selected user base. See [Push Notification Experiment](https://docs.byteplus.com/docs/DataTester/Push-Notification-Experiment).


<span id="客户端实验"></span>
### Client side experiment

Client side experiment refers to the experiment in which the client side obtains the experimental grouping information and controls the configuration to take effect.

**Applicable scenarios:** 


* Some functions can only be controlled by the client side, such as the client's UI style, interaction function design, etc.

* When the APP is invoked, the configuration needs to take effect. For example, we want to conduct A/B experiments on the opening page of the APP. As soon as the user opens the APP, the client side needs to show the opening interface to the user. In this case, the client side may not have time to request configuration parameters from the server side.


**Client side experiments include:** 


* **Programming experiments:**  AB test through code programming, widely used in front\-end optimization, policy optimization and back\-end algorithm optimization for a variety of experimental scenarios, see [Programming Experiment](https://docs.byteplus.com/docs/DataTester/Programming-Experiment).

* **Visual experiment:**  Through WYSIWYG online editing (such as editing elements and attributes such as pictures, text, colors, positions, etc.), in the scenario of Web/H5 page optimization, reduce the cost of product and operator using A/B experiment tools, eliminating coding. See [Visual Experiment](https://docs.byteplus.com/docs/DataTester/Visual-Experiment).

* **Multi\-link experiment:**  Also known as the Split URL experiment, your users will visit different versions of the link based on the experimental splitting results. See [Multi-Link Experiment](https://docs.byteplus.com/docs/DataTester/Multi-Link-Experiment).


<span id="三、准备基本信息"></span>
## 3. Prepare basic information

Before designing an A/B experiment, prepare the following information:


1. **Ask a question:**  Why is my registration page conversion rate not high enough? Or why is my recommender system click/exposure ratio not ideal?

2. **Establish an experimental hypothesis:**  make registered button copy more attractive? Or replace a set of recommended models?

3. **Preparation plan:**  different button copy, button clicks and page entry traffic statistics, or different recommendation models, recommended content clicks and traffic statistics entering the For You feed surface.

4. **To test this hypothesis:**  build a different button copy as experimental group B, go live at the same time as control group A, show it to two parts of users with the same attributes, and get statistics.

5. **Analysis of the data yielded preliminary results:**  if experimental group B succeeded in increasing the conversion rate, then this hypothesis was validated. Otherwise, you need to return to the second step to make other assumptions.


In addition to this, you also need to determine the name of the experiment, the type of experiment, and the estimated duration of the experiment.


|**Experimental basic information** ||
|---|---|
|**Name of experiment** |Registration page Registration button Copywriting test |
|**Experimental description (problems, objectives, and hypotheses)**  |Problem: The conversion rate of the registration page is not high enough<br><br>Objective: To increase the conversion rate of registration pages<br><br>Hypothesis: Changing the button copy from "Register" to "Go Explore" will increase the conversion rate of the registration page |
|**Type of experiment** |Client side experiment |
|**Experiment duration** |14 Days |


<span id="四、选择关注指标"></span>
## 4. Select metrics of concern

After clarifying the basic information of the experiment, you need to determine a core metric that determines the success or failure of the experiment, and a must\-see metric that needs to be monitored during the experiment.


* **Core metrics:**  Whether the decision\-making experiment function meets the expected "direct effect metrics", also known as "success metrics". Only one metric can be set as the core metric of an experiment, and the experimental data can be viewed in the experiment report. For example, the optimization experiment of "button copy" was established, and "button click through rate" was the core metric of the experiment.

* **Must\-see metrics:**  must guard the business line metrics, the experimental function may not have a direct causal relationship to it, can not directly bring improvement, but generally can not have a significant negative impact on it.


For more metric definitions, see [Experimental Metric](https://docs.byteplus.com/docs/DataTester/Experimental-Metric) list.

<span id="五、设置实验版本-实验组"></span>
## 5. Set up the experimental version/experimental group

After determining the metrics of concern, it is necessary to set the parameters of the experimental control version and the experimental version. Under the premise that there are only two experimental versions, the parameter combinations of the two experimental groups are allowed to be the same, that is, the AA experiment is started.

**Experimental parameters:**  Configurative mapping of experimental business policies and functions. The experimental parameters determine what policies are in effect for each experimental grouping, so you need to configure the experimental parameters when creating an experiment.

**Contrast version:**  Generally, the control group takes an online raw strategy.

**Experimental group:**  Adopt a new strategy.

**Parameter value:**  The parameter value determined for the experimental group and the control group, and the behavior of the users divided into this group will be marked with this parameter value.

In order to improve the effectiveness of related recommendations, a new recall strategy is designed for related recommendations.

Original strategy: content\-based collaborative filtering

New strategy: user\-based collaborative filtering

Then the configurable mapping relationship of the agreed policy in development is as follows:

```plain
collaborative_filtering="content" ——Representing content-based collaborative filtering
collaborative_filtering="user" ——Representing user-based collaborative filtering
```


<span id="六、分配流量、设置目标受众"></span>
## 6. Allocate traffic and set target audiences

Finally, you need to determine the proportion of traffic required for the experiment as a whole and the traffic weights for each experimental group (usually evenly distributed), and determine whether the experiment should join a mutual exclusion group.

**The proportion of traffic:**  The proportion of traffic in the overall group in this experiment.

**Mutual exclusion group:**  also called mutual exclusion layer, experimental layer. All experiments in a mutual exclusion group do not share users, and if one user/device enters Experiment A, it does not enter other experiments in that mutual exclusion group.

<span id="七、诊断实验"></span>
## 7. Diagnostic tests

After starting the experiment, if the user cannot enter the experiment, you can check the following information to solve the problem. For more details, see [Experimental Diagnosis Tool](https://docs.byteplus.com/docs/DataTester/Experimental-Diagnosis-Tool).


|Reason |Explain in detail |
|---|---|
|The experimental status is closed. |The experiment has been closed, and no user can access it. |
|Mutual exclusion layer hit rule |Whitelist users, hit other experiments on the same level. |
|Does not belong to the traffic range |The user shunting result does not belong to the traffic interval of the experiment. The current experimental allocation total traffic is < experimental assigned traffic percentage \>, and the user belongs to the remaining traffic space. |
|The experimental state is suspended |When the experiment was suspended, the user, although in the traffic zone, was unable to hit. |
|The experimental status is preview/debugging |The experiment was in a debugging state at the time, and the user was not a whitelisted user and could not be hit. |
|The experimental state is frozen |The experiment was frozen at the time, and the user did not expose the experiment before freezing. Although it belonged to the traffic range, it was unable to hit. |
|Traffic filter conditions do not meet |The user does not meet the audience filter criteria and cannot be hit.<br><br>Eg. The user "OS = Windows" does not meet the filter "OS = MAC/Android" and cannot hit. |
|Miss multilink experiment |The user request URL misses the target URL of the multilink experiment. |


<span id="更多"></span>
## More


* [Optimization Plan](https://docs.byteplus.com/docs/DataTester/Optimization-Plan): By formulating business optimization plans, managing optimization goals, and binding related experiments, we can help you design experiments more systematically and track results.
