---
title: "Typical Application Scenarios"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Typical-Application-Scenarios"
---

Feature Flag has a wealth of usage scenarios, providing targeted solutions for various roles such as R & D, operation, operation and maintenance, and QA.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bcc5e4d3db8a4a7a923bd500eb99251d~tplv-goo7wpa0wc-image.image) </span>

<span id="一-缓解上线发布风险"></span>
# 1. Mitigate launch risk

The new function release can gradually expand the grey release, first let a small number of users experience the new function, observe the user feedback and data performance, and then initially expand the quantity, and find the hidden problems in time to quickly stop the loss.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4605ee53b58842c69762d6f60b3e4fb9~tplv-goo7wpa0wc-image.image) </span>


* Blue\-Green Releases: For software releases that have two identical production environments (with the advantage of easy failover and avoiding release downtime), FeautreFlag provides the ability to roll back all features without having to issue a single feature in a larger release, exposing specific segments of the internal QA/tester, external beta tester, or user base to new features for specific users.

* Canary Release: Many organizations test/use the Canary version simultaneously, which is a package\-level job, so FeatureFlag is required to turn on/off the functionality of each section.

* Progressive delivery: Flexible release schedule management + critical operations audits + release rollbacks provide the foundation for reducing the risk of new feature explosion radius, and feature flags pair feature flags with operational and customer data to monitor new code rollouts in real time.

* Production testing: Testing code directly in production is one of the most reliable ways to verify that Features are working properly. Feature flags allow a small group of users to perform functional QA and performance tests directly in the production environment, providing a safe and effective way to scale. If something goes wrong, the error tracking and performance monitoring data will alert the user to the corresponding function, and any Flag can be turned off immediately without the need to roll back the code.

* Beta testing: Usually run by product managers or engineers, it attempts to validate the performance, usability, and functional parameters of new features. It is a critical stage in the software release lifecycle, giving development teams the opportunity to run controlled user tests. Usually before alpha testing by QA and dogfooding personnel.


**Typical Scenario 1 AB test Safe and Fast Total**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/854efb0bc3f44500ae47e1a4f804128d~tplv-goo7wpa0wc-image.image) </span>

**Typical scenario 2 new feature grey release reduces risk**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69a0d3b726ed441ca1002f3f99492741~tplv-goo7wpa0wc-image.image) </span>

<span id="二-减少开发周期"></span>
# 2. Reduce development cycles


* Continuous Delivery: Adopting a trunk\-based development process (the only way to ensure that shared branches are always freeable is to hide unfinished functionality behind a default closed flag, build new functionality by turning off that flag and deploying it to the master server at any time, preventing merge conflicts before new functionality is complete), reduce the amount of code deployed and released, speed up deployment and reduce release risk.

* Dark Launch: A launch strategy in which new features are deployed without exposing them to the user, turned on when ready, Feature Flag simplifies the process of dark launch features. Wrap the code in a flag, keep the flag closed, and release new features.

* Microservice transformation: Large feature changes across services often have dependencies, and leveraging FeatureFlag to turn functionality on and off makes the transition to a microservice structure safe and controlled.


**Typical scenario, multi\-feature parallel continuous development to improve iterative efficiency**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/37b478b8a6b34d6c857badb7d58e58b6~tplv-goo7wpa0wc-image.image) </span>

<span id="三-精细化运营"></span>
# 3. Refined operation


* Function personalization: Different functions can be displayed according to the characteristics of different groups of people, such as Android users recommending QQ login, iOS users recommending WeChat login, and improving the personalized experience of different groups of people

* Differentiated operation: When operating activities, differentiated operation strategies can be adopted for different regions and groups of people to achieve fine operation of segmented groups of people

* Customized publishing: Feature Flag supports a variety of crowd methods such as public attributes, user grouping, portrait grouping, and event flow circle people, and supports user\-defined crowd audiences to meet the targeted publishing needs of business customization.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e578d488b5c4ca3805b8f4ffe3dadf9~tplv-goo7wpa0wc-image.image) </span>

**Typical scene, thousands of people and thousands of faces refined operation**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa0c062df9f34359b283b0cd0c2d04af~tplv-goo7wpa0wc-image.image) </span>
