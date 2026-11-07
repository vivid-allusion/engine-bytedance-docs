---
title: "What is A/B Testing?"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/What-is-A-B-Testing"
---

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d2287f2d82eb4e45b425b54d0e1d00c2~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A/B testing is also known as A/B experimentation.</div>


<span id="一-什么是a-b实验"></span>
# 1. What is A/B testing?

<span id="_1-a-b实验的基本思想"></span>
## 1. The basic idea of A/B testing

The basic idea of the A/B testing is:

We take **a small part** of the online traffic (lower risk), divide it completely **randomly** into the original strategy A and the new strategy B (excluding interference), and then combine certain **statistical methods** to obtain an accurate estimate of the relative effect of the two strategies (quantification results).

This set of experimental methods based on small samples meets the requirements of **low risk**, **anti\-interference** and **quantification results**, so it is widely used in both Internet product research & development and scientific research.

<span id="_2-a-b实验的应用一"></span>
## 2. First application of A/B testing

> Instead of saying 'I have an idea', what if you said 'I have a new **hypothesis** , let's go **test** it, see if it's valid, ask how quickly can we **validate** it.' And if it's not valid, **move on** to the next one. —— Satya Nadella CEO, Microsoft


Microsoft CEO *Satya Nadella*'s response to hypothesis testing in a Business Insider interview succinctly describes Microsoft's data\-driven culture based on **experiment\-analysis\-decision**.

In fact, Microsoft is also one of the first technology companies in the world to adopt A/B testings to evaluate every major feature, from Bing's search ranking to MSN's interaction design, data\-driven decision\-making is ubiquitous, avoiding a lot of risk and generating considerable returns for Microsoft every year.

The graph below, from the bing side, shows the explosive growth of the number of experiments running simultaneously on Microsoft's experimental platform over the past decade.

<span>![图片](https://p9-volceps.byteimg.com/tos-cn-i-0000/1117ca140446482393c64509de9bb8fb~tplv-noop.image?width=700&height=422) </span>

<span id="_3-a-b实验的应用二"></span>
## 3. Second application of A/B testing

In addition, it is worth noting that this set of experimental methods based on hypothesis testing is not pioneered by technology companies. Its impact is far more profound than we imagined, and its reliability has been well validated.

For example, in the medical field, every new drug development is accompanied by a series of animal experiments and clinical tests, and the effects of these experiments are evaluated using similar but more rigorous hypothesis testing methods. Only drugs that are ultimately determined to be safe and effective will enter the market and benefit patients.

The figure below shows an excerpt from a report on the effectiveness of a radiation therapy in the treatment of breast cancer. The **95% CI** (95% confidence interval) and **p** (p\-value) in the red box are statistical terms commonly used in hypothesis testing.

<span>![图片](https://p9-volceps.byteimg.com/tos-cn-i-0000/06b9f98855e949068c6d64e2bdde8320~tplv-noop.image?width=482&height=554) </span>

<span id="二-为什么要开启ab实验？"></span>
# 2. Why should we start A/B testing?

Nowadays, the era of the barbaric growth of most Internet products has passed, and the demographic dividend has reached its peak. Product strategies need to shift from the fast and rough way of horse racing to the refined operation mode of deep cultivation and meticulous cultivation. To achieve refined operation, data should be used as a driven factor.

What is data\-driven? Imagine the following scenarios:


1. Staff A directly modified the online strategy of the product with his rich experience. After a week, he found that the effect did not increase but decreased, so he took it offline.

2. Staff B and Staff C launched two product functions at the same time. After a week, the product data declined. They both thought it was the other party's problem, and no one accepted to take the blame.

3. Staff D launched a new strategy, and then entered the holiday week of November. User interaction declined. Staff D felt that it must be the holiday that ruined his hard work, but he couldn't explain it and had nowhere to complain.

4. Staff E worked hard for a whole year to develop 365 different functions and take them online, but when he wrote a summary at the end of the year, he couldn't write down how much and on what aspects he had contributed to.


Presumably, whether it is research and development or product operation staff, you don't want to fall into the above awkward situations after hard work, so data\-driven business growth is necessary.

So what is the causal relationship between data changes and product actions?

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c58160cb3644c7cb14c9123f7d2fbf4~tplv-goo7wpa0wc-image.image) </span>

Suppose that an Internet company carries millions of DAUs, and a large number of new features are waiting to be launched every day. On the one hand, business personnel cannot bear the serious consequences of any of the wrong features directly affecting the user experience. On the other hand, business personnel hope to be able to isolate and quantify the impact of each feature.

Therefore, we need to design and adhere to **a data\-driven approach**, so that business personnel can evaluate new features at a **lower risk**, accumulate experience through active trial; and the methods we designed have the ability to **exclude interference of other factors** (such as other features developed simultaneously and time factors, etc.); finally, in addition to "good" or "bad", we hope that this method can also give **quantitative ** results.

In order to solve the above problems, the commonly used methodology is **small flow randomized experiments**, which is often referred to as **A/B testing.** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c4df56719ee4d8e8c8faf5c5761d87b~tplv-goo7wpa0wc-image.image) </span>
