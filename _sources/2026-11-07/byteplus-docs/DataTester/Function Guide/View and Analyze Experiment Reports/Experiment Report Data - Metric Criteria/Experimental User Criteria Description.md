---
title: "Experimental User Criteria Description"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Experimental-User-Criteria-Description"
---

<span id="概述"></span>
# Overview

The experimental metrics are filtered and calculated according to the users of the hit experiment. Due to the natural differences between the client side experiment and the server level experiment in the shunt triggering and data reporting logic at the end, there are also some differences in the method of determining "the users of the hit experiment (that is, the users entering the group) " when counting the experimental metrics. In order to achieve the same logic in the determination of the "user who hit the experiment" criteria between the client side experiment and the server level experiment, so as to improve the accuracy, DataTester has upgraded the user determination logic of the experimental group, which is mainly explained in this document.

<span id="进组用户口径"></span>
# Incoming user criteria

<span id="前后对比"></span>
## Before and after comparison


| |Before updating<br><br>~ April 2023 |After update<br><br>April 2023~ |
|---|---|---|
|Client side experiment |* Entry decision logic: all people who report ab_version events within a certain period of time<br><br>* Calculation method: When the client side triggers the shunt, it reports the ab_version event at the same time, and only uses the user behavior event tracking log to calculate the experimental metrics |The two remain consistent, the criteria of the server level experiment remains unchanged, and the criteria of the client side experiment is upgraded to complete the unification<br><br><br>* Entry decision logic: People who have reported exposure events since the start of the experiment and who have reported events within a certain period of time<br><br>* Calculation method: Uniformly use the user behavior event tracking log as the left table, AB shunt log AB_Log table as the right table to join calculation experimental metrics<br><br><br>[Note] AB_Log table logic: Use experimental exposure events to record user hits in experiments, support real\-time and sky\-level, sky\-level offline data will be aggregated based on the granularity of people + experimental groups (ie ab_version)<br><br>Statistical basis for exposure events:<br><br><br>* Normal experimental exposure field: abtest_exposure<br><br>* Push experimental exposure field: rangers_push_send |
|Server level experiment |* Entry decision logic: People who have reported exposure events since the start of the experiment and who have reported events within a certain period of time<br><br>* Calculation method: Use the user behavior event tracking log as the left table, the server level record into the group exposure ab_version event table as the right table to join calculation experimental metrics ||
