---
title: "Cumulative Trend of Report Pages"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Cumulative-Trend-of-Report-Pages"
---

<span id="一-什么是多天累积"></span>
# 1. What is multi\-day accumulation?

Multi\-day cumulative data is the cumulative value of the corresponding indicators combined over multiple days within the selected experimental date range.

<span id="二-为什么要用多天累积数据"></span>
# 2. Why use multi\-day data accumulation?

Accumulating data over multiple days can improve confidence strategies and enhance experimental sensitivity.


* With multi\-day cumulative data, multi\-day confidence levels can be calculated directly, thus enabling precise control of confidence recall based on selected confidence levels.

* Accumulating data over multiple days allows the experiment to obtain more samples, which means that the test sensitivity of the experiment continues to improve as the experiment progresses.


<span id="三-计算过程举例"></span>
# 3. Example of calculation process

Multi\-day original data sources are aggregated by person, and the sample index values are accumulated and calculated using the aggregated standard deviation for statistical calculation.

For example, the following two tables represent the behavior statistics of three users over two days.

day 1


|uuid |read/u |
|---|---|
|uuid1 |13 |
|uuid2 |2 |
|uuid3 |8 |


day 2


|uuid |read/u |
|---|---|
|uuid1 |6 |
|uuid2 |0 |
|uuid3 |12 |


The corresponding multi\-day merger result is:


|uuid |read/u |
|---|---|
|uuid1 |19 |
|uuid2 |2 |
|uuid3 |20 |
