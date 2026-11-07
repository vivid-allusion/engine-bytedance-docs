---
title: "Setting up the development environment"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/setting-up-environment"
---

This topic describes how to set up the development environment for getting started with Message Queue for Kafka.

<span id="1 准备账号"></span>
## Step 1: Create a BytePlus account

Before you activate Message Queue for Kafka, you must create a BytePlus account and complete the enterprise real\-name authentication. If you want to create and use a **pay\-as\-you\-go** Kafka instance, make sure that the total value of your account balance is no less than CNY 100.


1. Create a BytePlus account.

2. Complete the enterprise real\-name authentication.


<span id="2 创建私有网络和子网"></span>
## Step 2: Create a VPC and a subnet

By default, internal access is enabled for a Kafka instance. Virtual Private Cloud (VPC) offers an isolated virtual network environment, and the Kafka instance can be accessed only from the VPC. Make sure that at least one VPC and one subnet are available in the Region in which you want to create a Kafka instance. If no VPCs and subnets are available, create one.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Take note of the following items when you create a VPC:</div>



* <div data-tips="true" data-tips-type="tip">To ensure successful access, the VPC and your Kafka instance must be deployed in the same Region.</div>


* <div data-tips="true" data-tips-type="tip">Security groups and relevant rules must be configured based on your business requirements.</div>


* <div data-tips="true" data-tips-type="tip">The subnet must contain at least six internal IP addresses that are not used.</div>



<span id="62f9c1e8"></span>
## Step 3: Create an Elastic Compute Service instance

If you want to access a Kafka instance from a VPC, first buy an Elastic Compute Service (ECS) instance in the same Region. In addition, configure the VPC, install a Java Development Kit (JDK), and configure environment variables for the ECS instance. If you want to access a Kafka instance over the internet, your ECS instance or self\-managed data center must be accessible over the internet.


1. Create an ECS instance.

2. Log on to the ECS console and set up your Java development environment.

3. Download an open source Kafka toolkit.

   In the following example, Kafka version 2.2.2 is used.

   ```Bash
   wget https://archive.apache.org/dist/kafka/2.2.2/kafka_2.11-2.2.2.tgz
   ```
