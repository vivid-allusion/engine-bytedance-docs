---
title: "Test Environment"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/test_environment"
---

This topic describes the test environments, tools, methods, and indexes used for the RDS for MySQL stress tests.

<span id=".5rWL6K-V546v5aKD"></span>
## Test Environment


* **Region:**  China (Beijing)

* **Availability zone:**  Availability Zone A

* **ECS instance:**  The computational type is c4i with 32 cores and 64 G of memory, and the operating system image is the 64\-bit version of CentOS 8.3.

* **RDS MySQL instance:** 

   * Kernel version: MySQL 5.7.44_20260415, MySQL 8.0.43_20260415, and MySQL 8.4.7_20260415.

   * Instance type: Double node.

   * Specification type: General type.

   * Storage type: Local SSD and Cloud ESSD FlexPL.

   * Node specification: 1 core 2 GiB, 2 cores 4 GiB, 4 cores 16 GiB, 8 cores 32 GiB, 16 cores 64 GiB, and 32 cores 128 GiB (The storage type for this specification is Local SSD. Other specifications support Local SSD and Cloud ESSD FlexPL).

   * Parameter templates: Default parameter templates.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Because you must install additional compilation tools for the stress test tools, we recommend you bind the ECS instance to an EIP.</div>
