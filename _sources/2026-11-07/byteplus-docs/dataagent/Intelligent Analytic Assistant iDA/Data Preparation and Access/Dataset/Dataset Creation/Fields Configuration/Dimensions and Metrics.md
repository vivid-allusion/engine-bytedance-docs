---
title: "Dimensions and Metrics"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Dimensions_and_Metrics_"
---

<span id="5b047ffd"></span>
# Dimensions and metrics

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d57b628c4e544e07a78103346d9632ab~tplv-goo7wpa0wc-image.image) </span>

Fields have two roles: dimensions and metrics.


* A dimension segments the data we analyze and represents the perspective from which we view the data. Dimensions are non\-aggregated fields, such as date, author UID, and so on.

* A metric is used to measure data using different aggregation methods. In most cases, metrics are numbers, such as the number of submissions by an author. For example, to view the number of students in each course category, set "course category" as the dimension and "number of students" (that is, the sum of students) as the metric.


<span id="2209fd69"></span>
# **Application of dimensions and metrics in different business scenarios**

A field may be a dimension or a metric in different scenarios.

Example of a detail table:


* Each time an author submits, one record is generated.

* Filtered 2,230 rows of data from 2020\-1\-6 to 2020\-1\-8



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


**Scenario 1: Number of submissions per day**

View the total number of submissions per day.


* Dimension: date

* Metric: number of submissions, aggregation method: sum



|Date |Number of submissions |
|---|---|
|2020\-01\-08 |780 |
|2020\-01\-07 |700 |
|2020\-01\-06 |750 |


**Scenario 2: Number of submissions per author per day**

View the total number of submissions per day for each author.


* Dimension: date, author UID

* Metric: number of submissions, aggregation method: sum



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


**Scenario 3: Number of submitting authors**

How many authors submitted from 2020\-1\-6 to 2020\-1\-8?


* Metric: author UID, aggregation method: distinct count



|Number of submitting authors |
|---|
|3 |


&nbsp;
