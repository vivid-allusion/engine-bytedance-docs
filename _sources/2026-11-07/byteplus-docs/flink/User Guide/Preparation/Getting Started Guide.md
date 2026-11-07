---
title: "Getting Started Guide"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Getting_Started_Guide"
---

To help you quickly experience Flink, the quick start guide introduces the task development process and the necessary preparations before starting task development.

<span id="d645b2e0"></span>
## Experience Process


1. Initialization

   When the main account first logs into the Flink console, it does not have permission to use any feature and must complete the service initialization first. For detailed operations, please refer to [Service Initialization](https://docs.byteplus.com/docs/flink/Service_Initialization).

2. Preparations

   Before experiencing the Flink task process, the following preparations must be completed:

   * [Import Project](https://docs.byteplus.com/docs/flink/Import_Project_From_BytePlus): The main account can create multiple isolated and independent project spaces.

   * [Member Management](https://docs.byteplus.com/docs/flink/Member_Management): The main account should enter the project and add project members, such as project administrators, developers, operation and maintenance personnel, etc.

   * [Create Resource Pool](https://docs.byteplus.com/docs/flink/Create_Resource_Pool): Tasks developed within the project require computing resources for running and debugging. Thus, the main account or project administrators need to create a resource pool within the project beforehand.

3. Task Development

   * On the Flink console, task development is primarily performed using Jupyter, currently supporting four types of tasks: Flink Stream SQL, Flink Stream JAR, Flink Batch SQL, and Flink Batch JAR. The quick start guide details the development process for Stream type tasks. For more information, see [Create Flink SQL Job](https://docs.byteplus.com/docs/flink/Create_Flink_SQL_Job) and [Create Flink JAR Jobs](https://docs.byteplus.com/docs/flink/Create_Flink_JAR_Jobs).
