---
title: "Measuring performance for Content Industry"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-content_standard_measuring_performance"
---

After successful deployment of the recommendation models, users can view the model performance on the Insights dashboard on the BytePlus Recommend Console.

<span id="Recommend Standard recommendation model performance metrics"></span>
# Recommend Standard recommendation model performance metrics

Model performance can be measured through the following metrics:


* Click\-through Rate (CTR)

* Stay duration

* Like rate


If users have other core metrics not listed here, contact the BytePlus Recommend team for customized performance tracking.

<span id="Setting up A/B testing in BytePlus Recommend"></span>
# Setting up A/B testing in BytePlus Recommend

Users are recommended to launch a model with A/B testing. This allows for the progressive rolling out of traffic and the performance measuring of different strategies. Users can test\-launch their A/B testing tool with 1% traffic to ensure service stability. After that, they can scale up the traffic to 5% or more to start measuring performance and ensure that metrics calculations are accurate and aligned. Once everything is stable, the tool can then be scaled up to accept full traffic.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In preparation for future console developments on our end, users should specify the traffic_source field under the UserEvents data for the scene deployed in the model. Users will be able to compare and analyze the differences between the variants through the Insight Dashboard.</div>


**EXAMPLE**

Assume that we are looking at the homepage "Recommended for You" scene and that the optimization objective is CVR. There are two recommendation models available:


* Existing platform logic: Model A

* BytePlus Recommend logic: Model B


To measure the increase in volume brought about by Model B, traffic can be split into two groups by user_id:


* Control Group: 20% traffic with Model A running

* Test Group: 20% with Model B running


After running the A/B test for six weeks, you measure the CVR for both groups and compare the differences to identify the better recommendation model.

<span id="Effective A/B testing experimental variants"></span>
# Effective A/B testing experimental variants

A/B testing requires users to set up different experimental variants. Each variant uses a different recommendation service. There usually are two types:


* **Divide by users**: Randomly divides the users into two (or more) groups.

* **Divide by requests**: Randomly divides the requests into two (or more) groups.


We strongly recommend using Divide by users since it is stable and easy for attribution. Users need to ensure that the division remains stable throughout the recommendation process.
