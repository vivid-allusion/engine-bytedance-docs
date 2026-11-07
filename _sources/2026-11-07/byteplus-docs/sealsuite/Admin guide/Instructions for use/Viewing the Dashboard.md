---
title: "Viewing the Dashboard"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/viewing-the-dashboard"
---

The data **Dashboard** is a centralized data visualization hub designed to provide you with deep insights into your organization's endpoint, security, and network posture. It consolidates various charts and data reports to help you make data\-driven management decisions and assess risks.

<span id="dc946e2c"></span>
# Endpoint Posture

The **Endpoint** tab provides statistical information about all endpoint devices across your organization.


* The dashboard displays key metrics such as **Total Devices**, **Active Device Statistics**, **OS Distribution**, **Top 20 Software Statistics**, **Client Version Distribution**, and resource utilization for disk, CPU, and memory.

* Use the filters at the top of the page to narrow the data by **Device Group**, **Device Status**, or **Department**.

* Click on any bar or donut chart to drill down into a detailed view of that specific data point.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f03a8bba20714c8db58ce38ed629b419~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f187526696c482abef6d079aee67c52~tplv-goo7wpa0wc-image.image) </span>

<span id="b54ec8e6"></span>
# Security Posture

The **Security** tab provides dashboards for AI Application Security, Data Loss Prevention, Endpoint Antivirus, and other security metrics.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Data will only appear on these dashboards after you have enabled the relevant security policies and a security event has been triggered.</div>



|**Module** |**Description** |
|---|---|
|AI App Security |This dashboard provides an overview of AI application usage and risks.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Data is sourced from the Data Loss Prevention, Internet Access Control, and Application Security modules. If you have not purchased one of these modules, some data may be missing.</div><br><br><br><br>* View a 180\-day overview, including total AI app exfiltrations, total users accessing AI apps, total risky employees, and total prompts sent.<br><br>* Use the date filter in the **AI App Risk Discovery** section to analyze exfiltration statistics.<br><br>* Use the date filter in the **AI App Access Data** section to analyze access statistics.<br><br>* Click **Control Policy** on the right side of the dashboard to navigate to the corresponding policy configurations.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f5c2490efaf4f9babf954121da46c0d~tplv-goo7wpa0wc-image.image) </span> |
|DLP |This dashboard provides statistics on data loss prevention activities.<br><br><br>* Filter the data by department, role, or a specific time range.<br><br>* View key metrics such as policy coverage, sensitive file counts, alert events, and risky employees.<br><br>* Click **Export Report** in the top\-right corner to download the current dashboard data.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/968576c520d54cc8817a584ae0e5acf5~tplv-goo7wpa0wc-image.image) </span> |
|Anti\-Virus |This dashboard provides statistics on antivirus activities.<br><br><br>* Filter the data by department or role.<br><br>* View key metrics such as policy coverage, scan tasks, and at\-risk devices and employees.<br><br>* Click **Export Report** to download the current dashboard data.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6bbcb1abbec4acd9c1294809e6f8872~tplv-goo7wpa0wc-image.image) </span> |
|Others |This section includes statistics on general endpoint risks and external device usage. You can filter the data by a specific time range.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0515e0cc77fa4769bfca3d8ff16df4d1~tplv-goo7wpa0wc-image.image) </span> |


<span id="5edc5ec9"></span>
# Network Posture

The **Network** tab provides connection and usage statistics for your organization's Network Access Control and VPN services.

<span id="63923f49"></span>
## **VPN**

This dashboard displays connection and bandwidth usage data for your VPN gateways, including line charts for daily peak concurrency, bandwidth consumption, and average daily connection time per user.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d391bb2274224636afe8a93fcc728cd1~tplv-goo7wpa0wc-image.image) </span>


* In the **VPN Daily Peak** section, you can filter by time period or a specific VPN gateway.

* In the **Bandwidth Usage** and **Average Daily Connection per User** sections, you can filter by time period or search for a specific department, role, or employee.


<span id="3faa0763"></span>
## **Network admission status**

This dashboard provides connection and usage statistics for your corporate network, focusing on daily peak data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/77289df6bd67409faf85f5c3a27490aa~tplv-goo7wpa0wc-image.image) </span>


* **Office Network Peak:**  A line chart that displays peak usage over a selected time period, including peak online devices and peak online accounts.

* **View by Category:**  You can switch between **Employee Wi\-Fi**, **Guest Wi\-Fi**, and **IoT devices** to view data for each specific scenario.

* **Data Filtering:**  Filter the data by a time range (e.g., last 7 days or a custom range) and by a specific RADIUS service.
