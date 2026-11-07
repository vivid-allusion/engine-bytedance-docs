---
title: "General-purpose specifications"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/VCI-General-purpose"
---

General\-purpose VCI specifications provide balanced vCPU, memory, and network capabilities that can meet application requirements in most scenarios.

Refer to the introduction below to select a general\-purpose VCI specification that matches your actual business needs.


|Instance family |Description |
|---|---|
|[General computing power u1](https://docs.byteplus.com/en/docs/vke/VCI-General-purpose#.6YCa55So566X5Yqb5Z6LLXUx) (vci.u1) |This instance family masks differences in back\-end processors and provides scheduling control capabilities based on actual back\-end physical resource utilization levels. It is applicable to various types and scales of enterprise applications, websites, servers, and similar scenarios. |
|[General-purpose n3i](https://docs.byteplus.com/en/docs/vke/VCI-General-purpose#.6YCa55So5Z6LLW4zaQ==) (vci.n3i) |Next\-generation general\-purpose VCIs built on DPU (Data Processing Unit) architecture of BytePlus, offering significantly enhanced computing, network, and storage performance. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="tip">Supported specifications vary by regions and availability zones. For details, see <a href="https://docs.byteplus.com/en/docs/vke/VCI-Regions-and-Availability-Zones">Regions and availability zones</a>.</div>


<span id=".6YCa55So566X5Yqb5Z6LLXUx"></span>
## General computing power u1

<span id=".54m554K5"></span>
### Features


|Type |Performance |
|---|---|
|Computing |* Uses Intel® Xeon® scalable processors.<br><br>* Available processor\-to\-memory ratios are `1:2`, `1:4`, and `1:8`. |
|Storage |* Supports ESSD cloud disks, with a maximum of 16 cloud disks mountable (including one system disk).<br><br>* Storage I/O performance is correlated with instance specifications: a higher specification delivers stronger performance. |
|Network |Network performance is correlated with instance specifications: a higher specification delivers stronger performance. |


<span id=".6YCC55So5Zy65pmv"></span>
### Application scenarios


* Enterprise\-level applications of various types and scales.

* Websites and application servers.

* Data analytics and computing.

* Computing clusters and memory\-dependent data processing.


<span id=".5L2_55So5pa55byP"></span>
### Usage method

For instructions on using general computing power type u1 instances, see [Creating general-purpose instances](https://docs.byteplus.com/en/docs/vke/Create_General_purpose_instance).

<span id=".6KeE5qC85YiX6KGo"></span>
### Specification list

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta \- Apply for Trial</strong></a>]: Some specifications in the general\-purpose computing power u1 instance family are in the beta stage. To use them, submit an application.</div>



|<div style="text-align: center"><br>Instance specification</div><br> |<div style="text-align: center"><br>vCPU</div><br> |<div style="text-align: center"><br>Memory</div><br><br><br><div style="text-align: center"><br>(GiB)</div><br> |<div style="text-align: center"><br>Network bandwidth</div><br><br><br><div style="text-align: center"><br>(Gbit/s)</div><br> |<div style="text-align: center"><br>Packets per second</div><br><br><br><div style="text-align: center"><br>(10k PPS)</div><br> |<div style="text-align: center"><br>Connections</div><br><br><br><div style="text-align: center"><br>(10k)</div><br> |<div style="text-align: center"><br>Cloud disk IOPS</div><br><br><br><div style="text-align: center"><br>(10k)</div><br> |<div style="text-align: center"><br>Cloud disk bandwidth</div><br><br><br><div style="text-align: center"><br>(Gbit/s)</div><br> |
|---|---|---|---|---|---|---|---|
|<div style="text-align: center"><br>vci.u1.0.25c\-0.5gi</div><br> |<div style="text-align: center"><br>0.25</div><br> |<div style="text-align: center"><br>0.5</div><br> |<div style="text-align: center"><br>0.1</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>0.2</div><br> |<div style="text-align: center"><br>0.1</div><br> |
|<div style="text-align: center"><br>vci.u1.0.25c\-1gi</div><br> |<div style="text-align: center"><br>0.25</div><br> |<div style="text-align: center"><br>1</div><br> |<div style="text-align: center"><br>0.1</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>0.2</div><br> |<div style="text-align: center"><br>0.1</div><br> |
|<div style="text-align: center"><br>vci.u1.0.5c\-1gi</div><br> |<div style="text-align: center"><br>0.5</div><br> |<div style="text-align: center"><br>1</div><br> |<div style="text-align: center"><br>0.2</div><br> |<div style="text-align: center"><br>5</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>0.3</div><br> |<div style="text-align: center"><br>0.2</div><br> |
|<div style="text-align: center"><br>vci.u1.0.5c\-2gi</div><br> |<div style="text-align: center"><br>0.5</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>0.2</div><br> |<div style="text-align: center"><br>5</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>0.3</div><br> |<div style="text-align: center"><br>0.2</div><br> |
|<div style="text-align: center"><br>vci.u1.0.75c\-1.5gi</div><br> |<div style="text-align: center"><br>0.75</div><br> |<div style="text-align: center"><br>1.5</div><br> |<div style="text-align: center"><br>0.3</div><br> |<div style="text-align: center"><br>5</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>0.4</div><br> |<div style="text-align: center"><br>0.3</div><br> |
|<div style="text-align: center"><br>vci.u1.0.75c\-3gi</div><br> |<div style="text-align: center"><br>0.75</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>0.3</div><br> |<div style="text-align: center"><br>5</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>0.4</div><br> |<div style="text-align: center"><br>0.3</div><br> |
|<div style="text-align: center"><br>vci.u1.1c\-1gi (beta)</div><br> |<div style="text-align: center"><br>1</div><br> |<div style="text-align: center"><br>1</div><br> |<div style="text-align: center"><br>0.5</div><br> |<div style="text-align: center"><br>6</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>0.5</div><br> |<div style="text-align: center"><br>0.5</div><br> |
|<div style="text-align: center"><br>vci.u1.1c\-2gi</div><br> |<div style="text-align: center"><br>1</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>0.5</div><br> |<div style="text-align: center"><br>6</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>0.5</div><br> |<div style="text-align: center"><br>0.5</div><br> |
|<div style="text-align: center"><br>vci.u1.1c\-4gi</div><br> |<div style="text-align: center"><br>1</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>0.5</div><br> |<div style="text-align: center"><br>6</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>0.5</div><br> |<div style="text-align: center"><br>0.5</div><br> |
|<div style="text-align: center"><br>vci.u1.1c\-8gi</div><br> |<div style="text-align: center"><br>1</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>0.5</div><br> |<div style="text-align: center"><br>6</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>0.5</div><br> |<div style="text-align: center"><br>0.5</div><br> |
|<div style="text-align: center"><br>vci.u1.1.25c\-2.5gi</div><br> |<div style="text-align: center"><br>1.25</div><br> |<div style="text-align: center"><br>2.5</div><br> |<div style="text-align: center"><br>0.6</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>0.5</div><br> |<div style="text-align: center"><br>0.6</div><br> |
|<div style="text-align: center"><br>vci.u1.1.25c\-5gi</div><br> |<div style="text-align: center"><br>1.25</div><br> |<div style="text-align: center"><br>5</div><br> |<div style="text-align: center"><br>0.6</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>0.5</div><br> |<div style="text-align: center"><br>0.6</div><br> |
|<div style="text-align: center"><br>vci.u1.1.5c\-3gi</div><br> |<div style="text-align: center"><br>1.5</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>0.7</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>0.5</div><br> |<div style="text-align: center"><br>0.7</div><br> |
|<div style="text-align: center"><br>vci.u1.1.5c\-6gi</div><br> |<div style="text-align: center"><br>1.5</div><br> |<div style="text-align: center"><br>6</div><br> |<div style="text-align: center"><br>0.7</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>0.5</div><br> |<div style="text-align: center"><br>0.7</div><br> |
|<div style="text-align: center"><br>vci.u1.2c\-2gi (beta)</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>1</div><br> |<div style="text-align: center"><br>10</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>1.0</div><br> |<div style="text-align: center"><br>1.0</div><br> |
|<div style="text-align: center"><br>vci.u1.2c\-4gi</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>1</div><br> |<div style="text-align: center"><br>10</div><br> |<div style="text-align: center"><br>6</div><br> |<div style="text-align: center"><br>1.0</div><br> |<div style="text-align: center"><br>1.0</div><br> |
|<div style="text-align: center"><br>vci.u1.2c\-8gi</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>1</div><br> |<div style="text-align: center"><br>10</div><br> |<div style="text-align: center"><br>6</div><br> |<div style="text-align: center"><br>1.0</div><br> |<div style="text-align: center"><br>1.0</div><br> |
|<div style="text-align: center"><br>vci.u1.2c\-16gi</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>1</div><br> |<div style="text-align: center"><br>10</div><br> |<div style="text-align: center"><br>6</div><br> |<div style="text-align: center"><br>1.0</div><br> |<div style="text-align: center"><br>1.0</div><br> |
|<div style="text-align: center"><br>vci.u1.4c\-4gi (beta)</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>25</div><br> |<div style="text-align: center"><br>6</div><br> |<div style="text-align: center"><br>2.0</div><br> |<div style="text-align: center"><br>1.5</div><br> |
|<div style="text-align: center"><br>vci.u1.4c\-8gi</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>25</div><br> |<div style="text-align: center"><br>12</div><br> |<div style="text-align: center"><br>2.0</div><br> |<div style="text-align: center"><br>1.5</div><br> |
|<div style="text-align: center"><br>vci.u1.4c\-16gi</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>25</div><br> |<div style="text-align: center"><br>12</div><br> |<div style="text-align: center"><br>2.0</div><br> |<div style="text-align: center"><br>1.5</div><br> |
|<div style="text-align: center"><br>vci.u1.4c\-32gi</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>25</div><br> |<div style="text-align: center"><br>12</div><br> |<div style="text-align: center"><br>2.0</div><br> |<div style="text-align: center"><br>1.5</div><br> |
|<div style="text-align: center"><br>vci.u1.8c\-8gi (beta)</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>50</div><br> |<div style="text-align: center"><br>12</div><br> |<div style="text-align: center"><br>3.0</div><br> |<div style="text-align: center"><br>2.0</div><br> |
|<div style="text-align: center"><br>vci.u1.8c\-16gi</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>50</div><br> |<div style="text-align: center"><br>30</div><br> |<div style="text-align: center"><br>3.0</div><br> |<div style="text-align: center"><br>2.0</div><br> |
|<div style="text-align: center"><br>vci.u1.8c\-32gi</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>50</div><br> |<div style="text-align: center"><br>30</div><br> |<div style="text-align: center"><br>3.0</div><br> |<div style="text-align: center"><br>2.0</div><br> |
|<div style="text-align: center"><br>vci.u1.8c\-64gi</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>50</div><br> |<div style="text-align: center"><br>30</div><br> |<div style="text-align: center"><br>3.0</div><br> |<div style="text-align: center"><br>2.0</div><br> |
|<div style="text-align: center"><br>vci.u1.16c\-16gi (beta)</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>5</div><br> |<div style="text-align: center"><br>90</div><br> |<div style="text-align: center"><br>50</div><br> |<div style="text-align: center"><br>4.0</div><br> |<div style="text-align: center"><br>3.0</div><br> |
|<div style="text-align: center"><br>vci.u1.16c\-32gi</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>5</div><br> |<div style="text-align: center"><br>90</div><br> |<div style="text-align: center"><br>50</div><br> |<div style="text-align: center"><br>4.0</div><br> |<div style="text-align: center"><br>3.0</div><br> |
|<div style="text-align: center"><br>vci.u1.16c\-64gi</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>5</div><br> |<div style="text-align: center"><br>90</div><br> |<div style="text-align: center"><br>50</div><br> |<div style="text-align: center"><br>4.0</div><br> |<div style="text-align: center"><br>3.0</div><br> |
|<div style="text-align: center"><br>vci.u1.16c\-128gi</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>128</div><br> |<div style="text-align: center"><br>5</div><br> |<div style="text-align: center"><br>90</div><br> |<div style="text-align: center"><br>60</div><br> |<div style="text-align: center"><br>4.0</div><br> |<div style="text-align: center"><br>3.0</div><br> |
|<div style="text-align: center"><br>vci.u1.24c\-24gi (beta)</div><br> |<div style="text-align: center"><br>24</div><br> |<div style="text-align: center"><br>24</div><br> |<div style="text-align: center"><br>9</div><br> |<div style="text-align: center"><br>150</div><br> |<div style="text-align: center"><br>75</div><br> |<div style="text-align: center"><br>5.0</div><br> |<div style="text-align: center"><br>4.0</div><br> |
|<div style="text-align: center"><br>vci.u1.24c\-48gi</div><br> |<div style="text-align: center"><br>24</div><br> |<div style="text-align: center"><br>48</div><br> |<div style="text-align: center"><br>9</div><br> |<div style="text-align: center"><br>150</div><br> |<div style="text-align: center"><br>75</div><br> |<div style="text-align: center"><br>5.0</div><br> |<div style="text-align: center"><br>4.0</div><br> |
|<div style="text-align: center"><br>vci.u1.24c\-96gi</div><br> |<div style="text-align: center"><br>24</div><br> |<div style="text-align: center"><br>96</div><br> |<div style="text-align: center"><br>9</div><br> |<div style="text-align: center"><br>150</div><br> |<div style="text-align: center"><br>75</div><br> |<div style="text-align: center"><br>5.0</div><br> |<div style="text-align: center"><br>4.0</div><br> |
|<div style="text-align: center"><br>vci.u1.24c\-192gi</div><br> |<div style="text-align: center"><br>24</div><br> |<div style="text-align: center"><br>192</div><br> |<div style="text-align: center"><br>9</div><br> |<div style="text-align: center"><br>150</div><br> |<div style="text-align: center"><br>75</div><br> |<div style="text-align: center"><br>5.0</div><br> |<div style="text-align: center"><br>4.0</div><br> |
|<div style="text-align: center"><br>vci.u1.32c\-32gi (beta)</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10</div><br> |<div style="text-align: center"><br>180</div><br> |<div style="text-align: center"><br>100</div><br> |<div style="text-align: center"><br>8.0</div><br> |<div style="text-align: center"><br>5.0</div><br> |
|<div style="text-align: center"><br>vci.u1.32c\-64gi (beta)</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>10</div><br> |<div style="text-align: center"><br>180</div><br> |<div style="text-align: center"><br>100</div><br> |<div style="text-align: center"><br>8.0</div><br> |<div style="text-align: center"><br>5.0</div><br> |
|<div style="text-align: center"><br>vci.u1.32c\-128gi (beta)</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>128</div><br> |<div style="text-align: center"><br>10</div><br> |<div style="text-align: center"><br>180</div><br> |<div style="text-align: center"><br>100</div><br> |<div style="text-align: center"><br>8.0</div><br> |<div style="text-align: center"><br>5.0</div><br> |
|<div style="text-align: center"><br>vci.u1.32c\-256gi (beta)</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>256</div><br> |<div style="text-align: center"><br>10</div><br> |<div style="text-align: center"><br>180</div><br> |<div style="text-align: center"><br>100</div><br> |<div style="text-align: center"><br>8.0</div><br> |<div style="text-align: center"><br>5.0</div><br> |


<span id=".6YCa55So5Z6LLW4zaQ=="></span>
## General\-purpose n3i

<span id=".54m554K5"></span>
### Features


|Type |Performance |
|---|---|
|Computing |* Uses 4th generation Intel® Xeon® scalable processors (Sapphire Rapids) with a base frequency of 2.6 GHz.<br><br>* Available processor\-to\-memory ratios are `1:2`, `1:4`, and `1:8`. |
|Storage |* Supports ESSD cloud disks, with a maximum of 16 cloud disks mountable (including one system disk).<br><br>* Storage I/O performance is correlated with instance specifications: a higher specification delivers stronger performance. |
|Network |Network performance is correlated with instance specifications: a higher specification delivers stronger performance. |


<span id=".6YCC55So5Zy65pmv"></span>
### Application scenarios


* General application scenarios such as MySQL databases, Redis databases, NGINX applications, and MQ middleware.

* High network packet transmission scenarios, including video bullet comment systems and telecommunication service forwarding.

* Computing\-intensive scenarios such as data analytics, batch computing, video encoding and decoding, video rendering, and high\-performance scientific and engineering applications.

* CPU\-based deep learning and training scenarios, including AI inference and training, as well as training for small and medium\-sized deep learning models.


<span id=".5L2_55So5pa55byP"></span>
### Usage method

For instructions on using general\-purpose n3i instances, see [Creating general-purpose instances](https://docs.byteplus.com/en/docs/vke/Create_General_purpose_instance).

<span id=".6KeE5qC85YiX6KGo"></span>
### Specification list


|<div style="text-align: center"><br>Instance specification</div><br> |<div style="text-align: center"><br>vCPU</div><br> |<div style="text-align: center"><br>Memory</div><br><br><br><div style="text-align: center"><br>(GiB)</div><br> |<div style="text-align: center"><br>Network bandwidth</div><br><br><br><div style="text-align: center"><br>base/burst</div><br><br><br><div style="text-align: center"><br>(Gbit/s)</div><br> |<div style="text-align: center"><br>Packets per second</div><br><br><br><div style="text-align: center"><br>(10k PPS)</div><br> |<div style="text-align: center"><br>Connections</div><br><br><br><div style="text-align: center"><br>(10k)</div><br> |<div style="text-align: center"><br>Cloud disk IOPS</div><br><br><br><div style="text-align: center"><br>base/burst</div><br><br><br><div style="text-align: center"><br>(10k)</div><br> |<div style="text-align: center"><br>Cloud disk bandwidth</div><br><br><br><div style="text-align: center"><br>base/burst</div><br><br><br><div style="text-align: center"><br>(Gbit/s)</div><br> |
|---|---|---|---|---|---|---|---|
|<div style="text-align: center"><br>vci.n3i.1c\-2gi</div><br> |<div style="text-align: center"><br>1</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>1/max. 4</div><br> |<div style="text-align: center"><br>20</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>0.6/max. 2</div><br> |<div style="text-align: center"><br>0.5/max. 2</div><br> |
|<div style="text-align: center"><br>vci.n3i.1c\-4gi</div><br> |<div style="text-align: center"><br>1</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>1/max. 4</div><br> |<div style="text-align: center"><br>20</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>0.6/max. 2</div><br> |<div style="text-align: center"><br>0.5/max. 2</div><br> |
|<div style="text-align: center"><br>vci.n3i.1c\-8gi</div><br> |<div style="text-align: center"><br>1</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>1/max. 4</div><br> |<div style="text-align: center"><br>20</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>0.6/max. 2</div><br> |<div style="text-align: center"><br>0.5/max. 2</div><br> |
|<div style="text-align: center"><br>vci.n3i.2c\-4gi</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>2.5/max. 12</div><br> |<div style="text-align: center"><br>60</div><br> |<div style="text-align: center"><br>6</div><br> |<div style="text-align: center"><br>1.5/max. 6</div><br> |<div style="text-align: center"><br>1.5/max. 6</div><br> |
|<div style="text-align: center"><br>vci.n3i.2c\-8gi</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>2.5/max. 12</div><br> |<div style="text-align: center"><br>60</div><br> |<div style="text-align: center"><br>6</div><br> |<div style="text-align: center"><br>1.5/max. 6</div><br> |<div style="text-align: center"><br>1.5/max. 6</div><br> |
|<div style="text-align: center"><br>vci.n3i.2c\-16gi</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>2.5/max. 12</div><br> |<div style="text-align: center"><br>60</div><br> |<div style="text-align: center"><br>6</div><br> |<div style="text-align: center"><br>1.5/max. 6</div><br> |<div style="text-align: center"><br>1.5/max. 6</div><br> |
|<div style="text-align: center"><br>vci.n3i.4c\-8gi</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>4/max. 12</div><br> |<div style="text-align: center"><br>100</div><br> |<div style="text-align: center"><br>12</div><br> |<div style="text-align: center"><br>3/max. 6</div><br> |<div style="text-align: center"><br>2/max. 6</div><br> |
|<div style="text-align: center"><br>vci.n3i.4c\-16gi</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>4/max. 12</div><br> |<div style="text-align: center"><br>100</div><br> |<div style="text-align: center"><br>12</div><br> |<div style="text-align: center"><br>3/max. 6</div><br> |<div style="text-align: center"><br>2/max. 6</div><br> |
|<div style="text-align: center"><br>vci.n3i.4c\-32gi</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>4/max. 12</div><br> |<div style="text-align: center"><br>100</div><br> |<div style="text-align: center"><br>12</div><br> |<div style="text-align: center"><br>3/max. 6</div><br> |<div style="text-align: center"><br>2/max. 6</div><br> |
|<div style="text-align: center"><br>vci.n3i.8c\-16gi</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>6/max. 12</div><br> |<div style="text-align: center"><br>160</div><br> |<div style="text-align: center"><br>30</div><br> |<div style="text-align: center"><br>4/max. 8</div><br> |<div style="text-align: center"><br>3/max. 6</div><br> |
|<div style="text-align: center"><br>vci.n3i.8c\-32gi</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>6/max. 12</div><br> |<div style="text-align: center"><br>160</div><br> |<div style="text-align: center"><br>30</div><br> |<div style="text-align: center"><br>4/max. 8</div><br> |<div style="text-align: center"><br>3/max. 6</div><br> |
|<div style="text-align: center"><br>vci.n3i.8c\-64gi</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>6/max. 12</div><br> |<div style="text-align: center"><br>160</div><br> |<div style="text-align: center"><br>30</div><br> |<div style="text-align: center"><br>4/max. 8</div><br> |<div style="text-align: center"><br>3/max. 6</div><br> |
|<div style="text-align: center"><br>vci.n3i.16c\-32gi</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>12/max. 30</div><br> |<div style="text-align: center"><br>300</div><br> |<div style="text-align: center"><br>50</div><br> |<div style="text-align: center"><br>6/max. 8</div><br> |<div style="text-align: center"><br>5/max. 6</div><br> |
|<div style="text-align: center"><br>vci.n3i.16c\-64gi</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>12/max. 30</div><br> |<div style="text-align: center"><br>300</div><br> |<div style="text-align: center"><br>50</div><br> |<div style="text-align: center"><br>6/max. 8</div><br> |<div style="text-align: center"><br>5/max. 6</div><br> |
|<div style="text-align: center"><br>vci.n3i.16c\-128gi</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>128</div><br> |<div style="text-align: center"><br>12/max. 30</div><br> |<div style="text-align: center"><br>300</div><br> |<div style="text-align: center"><br>50</div><br> |<div style="text-align: center"><br>6/max. 8</div><br> |<div style="text-align: center"><br>5/max. 6</div><br> |
|<div style="text-align: center"><br>vci.n3i.24c\-48gi</div><br> |<div style="text-align: center"><br>24</div><br> |<div style="text-align: center"><br>48</div><br> |<div style="text-align: center"><br>16/max. 30</div><br> |<div style="text-align: center"><br>450</div><br> |<div style="text-align: center"><br>75</div><br> |<div style="text-align: center"><br>7.5/NA</div><br> |<div style="text-align: center"><br>6/NA</div><br> |
|<div style="text-align: center"><br>vci.n3i.24c\-96gi</div><br> |<div style="text-align: center"><br>24</div><br> |<div style="text-align: center"><br>96</div><br> |<div style="text-align: center"><br>16/max. 30</div><br> |<div style="text-align: center"><br>450</div><br> |<div style="text-align: center"><br>75</div><br> |<div style="text-align: center"><br>7.5/NA</div><br> |<div style="text-align: center"><br>6/NA</div><br> |
|<div style="text-align: center"><br>vci.n3i.24c\-192gi</div><br> |<div style="text-align: center"><br>24</div><br> |<div style="text-align: center"><br>192</div><br> |<div style="text-align: center"><br>16/max. 30</div><br> |<div style="text-align: center"><br>450</div><br> |<div style="text-align: center"><br>75</div><br> |<div style="text-align: center"><br>7.5/NA</div><br> |<div style="text-align: center"><br>6/NA</div><br> |
|<div style="text-align: center"><br>vci.n3i.32c\-64gi</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>24/NA</div><br> |<div style="text-align: center"><br>600</div><br> |<div style="text-align: center"><br>100</div><br> |<div style="text-align: center"><br>10/NA</div><br> |<div style="text-align: center"><br>6/NA</div><br> |
|<div style="text-align: center"><br>vci.n3i.32c\-128gi</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>128</div><br> |<div style="text-align: center"><br>24/NA</div><br> |<div style="text-align: center"><br>600</div><br> |<div style="text-align: center"><br>100</div><br> |<div style="text-align: center"><br>10/NA</div><br> |<div style="text-align: center"><br>6/NA</div><br> |
|<div style="text-align: center"><br>vci.n3i.32c\-256gi</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>256</div><br> |<div style="text-align: center"><br>24/NA</div><br> |<div style="text-align: center"><br>600</div><br> |<div style="text-align: center"><br>100</div><br> |<div style="text-align: center"><br>10/NA</div><br> |<div style="text-align: center"><br>6/NA</div><br> |
