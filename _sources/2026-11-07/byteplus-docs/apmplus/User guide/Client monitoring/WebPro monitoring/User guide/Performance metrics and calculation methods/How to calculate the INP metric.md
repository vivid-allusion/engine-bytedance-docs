---
title: "How to calculate the INP metric"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/How_to_calculate_the_INP_metric"
---

<span id="4518a250"></span>
## What is the INP metric

<span id="6cc0e6e8"></span>
### Metric descriptions

Interaction to Next Paint (INP) observes the delay time for all user clicks, taps, and keyboard interactions with the webpage throughout the page lifecycle, and reports the longest duration. A lower INP means that the page consistently responds quickly to most user interactions.

<span id="2f87ada4"></span>
### metric baseline

To ensure a good user experience with responsive performance, it is recommended to measure the **75th percentile** of actual recorded web page load times:


* An INP of **200 milliseconds** or less means your web page **has good responsiveness**.

* If INP is between **200 milliseconds** and **500 milliseconds**, it means that your web page's responsiveness **needs improvement**.

* An INP greater than **500 milliseconds** indicates that the webpage **responds slowly**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a61c410a35fa4d65bccc2cd441619891~tplv-goo7wpa0wc-image.image) </span>

<span id="7bcc9620"></span>
## How to calculate the INP metric

The calculation method for INP is to observe all interactions between the user and the webpage.

For most websites, the operating system reports the interaction with the longest delay time as INP. However, for web pages with a high level of interactivity, random minor faults may result in exception high latency in interactions on other responsive websites. The more interaction there is, the greater the likelihood of this situation occurring. To address this issue and better measure the actual response speed of these type webpages, we ignore the highest interaction out of every 50 interactions. Because the vast majority of web experiences involve fewer than 50 interactions, the browser almost always reports the worst interaction. Then, the operating system will continue to report the 75th percentile of all webpage views, which will further remove outliers and provide a more representative user experience.

Interaction refers to a set of event handling scripts that are triggered during the same logical user gesture. For example, the "tap" interaction on touchscreen devices includes several events, such as `pointerup`, `pointerdown`, and `click`. Interactivity can be enabled by JavaScript, CSS, form elements, other built\-in browser controls, or combinations of these elements. Interaction latency time includes the period from when the user begins interacting to the moment the next frame displays visual feedback, and is determined by the maximum duration of the set of event handling scripts that drive the interaction. For more information about how to measure INP, see ["What is interaction?"](https://web.dev/articles/inp?hl=zh-cn#whats_in_an_interaction).

<span id="eb51093d"></span>
## How does the platform apply the INP metric

<span id="e1e3f838"></span>
### PID aggregation

<span id="d0cfc648"></span>
### Metrics overview

<span id="c5c8d4f6"></span>
### page list

<span id="ff401ca8"></span>
### data explore

<span id="ce2b22ee"></span>
### custom dashboard

<span id="2fec3e53"></span>
### Monitoring alert

<span id="901297b5"></span>
## Reference materials

https://web.dev/articles/inp
