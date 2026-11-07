---
title: "Get Started Quickly"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Get-Started-Quickly_"
---

<span id="名词解释"></span>
## Term explanation

> AB testing everyone is familiar with, here is mainly to explain some new terms of FeatureFlag.


* Feature: Configuration

* Variant: that is, configure the value, one Feature can set multiple variants (values)

* Publish audience: that is, the effective rules


Example: APP login This function supports different login methods (WeChat, QQ, Douyin)


* Feature name: APP login method

* key：app_log_type

* variant

   * Variant 1:1 (WeChat login)

   * Variant 2:2 (QQ login)

   * Variant 3:3 (Douyin login)

* Release audience: Android users default QQ login, iOS users default Douyin login, other default WeChat login


<span id="ab实验和featureflag的关系"></span>
## Relationship between AB testing and FeatureFlag

AB testing and FeatureFlag are tools we build for different scenarios: AB testing used to validate and evaluate the effect of different versions/strategies, while FeatureFlag is used for dynamic configuration, crowd\-directed release, experimental full release, etc.

**Contact**:


* Use AB testing and FeatureFlag with only one product access

* The same downlink, AB testing can be directly solidified to FeatureFlag

* Share a set of request parameters (filter conditions), which can be used after a single registration


**Difference**:


* The two are independent and can coexist

   * For example, the APP login method is normally issued according to the online rules as a commonly used dynamic configuration (for example, the default display of QQ login, WeChat login, Douyin login and other three ways for users to choose); at the same time, an experiment can be opened to verify whether adding a mobile phone number login helps to improve the login rate

* **If both experiments and FeatureFlag are running on the same parameter, priority will be given in case of conflict: Experiment \> Feature.**
