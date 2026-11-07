---
title: "Dimensions and Metrics"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Dimensions_and_Metrics"
---

<span id="5b047ffd"></span>
# Dimensions and metrics

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d57b628c4e544e07a78103346d9632ab~tplv-goo7wpa0wc-image.image) </span>

Fields have two roles: dimension and metric.


* A dimension segments the data being analyzed, representing the perspective from which the data is viewed. It is a non\-aggregated field, such as date, author UID, and so on.

* A metric measures data using different aggregation methods. In most cases, it is a number, such as the number of submissions by an author. For example, to view the number of students in each course category, "course category" can be set as the dimension, and "number of students" (that is, the sum of students) can be set as the metric.


<span id="2209fd69"></span>
# **Application of dimensions and metrics in different business scenarios**

A field may serve as a dimension or a metric in different scenarios.

Detail table example:


* Each time an author makes a submission, one record is generated.

* 2,230 rows of data were filtered from 2020\-1\-6 to 2020\-1\-8.



|Date |Author UID |Number of submissions |…… |
|---|---|---|---|
|2020\-01\-08 |71539701417 |1 | |
|2020\-01\-08 |71539701417 |1 | |
|2020\-01\-07 |71539701417 |1 | |
| |…… | | |
|2020\-01\-08 |9744333079 |1 | |
|2020\-01\-07 |9744333079 |1 | |
| |…… | | |
|2020\-01\-08 |8779307635 |1 | |
|2020\-01\-07 |8779307635 |1 | |


**Scenario 1 Number of submissions per day**

View the total number of submissions per day.


* Dimension: date

* Metric: number of submissions, aggregation method is sum



|Date |Number of submissions |
|---|---|
|2020\-01\-08 |780 |
|2020\-01\-07 |700 |
|2020\-01\-06 |750 |


**Scenario 2 Number of submissions per author per day**

View the total number of submissions per author per day.


* Dimension: date, author UID

* Metric: number of submissions, aggregation method is sum



|Date |Author UID |Number of submissions |
|---|---|---|
|2020\-01\-08 |71539701417 |280 |
|2020\-01\-08 |9744333079 |400 |
|2020\-01\-08 |8779307635 |100 |
|2020\-01\-07 |71539701417 |200 |
|2020\-01\-07 |9744333079 |420 |
|2020\-01\-07 |8779307635 |80 |
|2020\-01\-06 |71539701417 |220 |
|2020\-01\-06 |9744333079 |420 |
|2020\-01\-06 |8779307635 |110 |


**Scenario 3 Number of submitting authors**

During 2020\-1\-6 to 2020\-1\-8, how many authors submitted


* Metric: author UID, aggregation method is distinct count



|Number of submitting authors |
|---|
|3 |


&nbsp;
