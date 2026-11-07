---
title: "Overview"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/flink_overview"
---

<span id="_1-概述"></span>
## **1 Overview**

Apache Flink is a distributed computing framework for stateful computing on both bounded and unbounded streams, supporting both stream processing and batch processing application types. Flink not only provides real\-time computing capabilities that simultaneously support **high throughput**, **low latency**, and **exactly\-once** semantics, but also offers the ability to process batch data based on a streaming computation engine, thereby truly achieving **stream\-batch unification**.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_4abcd02b09d151b433292bd6b41b4582) </span>

<span id="_2-使用场景"></span>
## **2 Use cases**

The most common business use cases for Flink in the industry can be summarized as follows:


1. **Real\-time ETL & index building:**  Mainly involves real\-time extraction, aggregation, and cleaning of data through real\-time computation, such as in real\-time monitoring platforms or real\-time dashboard scenarios;

2. **Real\-time statistics and analysis**: For example, in real\-time data warehouse scenarios;

3. **Real\-time machine learning (ML)** : As user growth slows, the conversion rate of traditional T+1 offline recommendation engines declines, so recommendation engines are evolving toward real\-time. By using real\-time sample stitching and real\-time incremental models to improve conversion rate, ByteDance's internal Douyin, Toutiao, Ad Network, and TikTok ad recommendations all make extensive use of Flink's capabilities (to be introduced later);

4. **Real\-time event processing/decision\-making (CEP)** : Mainly used in scenarios such as real\-time monitoring, risk control, refined operations, and personalized marketing. For example, in the financial sector for online loan real\-time financial risk control, and in the security sector for big data real\-time security risk control based on situational awareness.
