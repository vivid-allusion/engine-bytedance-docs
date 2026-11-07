---
title: "AB Testing Full Amount"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/AB-Testing-Full-Amount"
---

<span id="一、功能简介"></span>
# Introduction to functions

AB testing full volume refers to solidifying the Feature to the experiment and publishing it online. After the experiment is created, the experimental parameters can be solidified into a Feature and published online. Generally, there are two scenarios:


* Scenario 1: After the conclusion of the experiment is reached, the full amount of a group with good results is put online, that is, by solidifying it into a Feature and publishing it to the full amount (commonly used scenarios).

* Scenario 2: The experiment has not yet come up with which group works well, but this function will continue to be explored in the future, that is, first solidify the experimental parameters into a Feature and manage it in FeatureFlag


<span id="二、如何使用"></span>
# How to use


* **Function entrance**

   * **Entry 1:**  Operation area on the right side of the experimental details page \- \> Initiate curing from the experimental particle size

   * **Entry 2:**  Next to Experiment Details Grouping \- \> Initiate Curing from Experiment Grouping Particle Size

      * "Fast Full" operation next to experimental grouping information

   * Difference: Initiate curing from the experimental particle size, which group needs to be selected for curing; initiate from the experimental group particle size, and select the corresponding group by default

* **Full process: Select the full group \-\> confirm the effective information \-\> publish it online**

   * **Step1 Select the full amount group:**  that is, select which experimental group to solidify (full amount)

      * If solidified from the experimental particle size, you need to choose which group to solidify

      * If the granularity is solidified from the experimental group, the group is selected by default, and the user can change it

      * Support the selection of multiple groups and solidify according to the experimental flow ratio

      * After selecting an experimental group, the AB parameter information of the group is displayed on the left (not editable), and the Feature information generated with the AB parameter is displayed on the right (editable).

   * **Step2 Confirm the effective information:**  that is, confirm whether the effective information of the Feature meets the expectations

      * Please carefully check whether the generated Features and effective rules meet expectations. If not, you can make changes at this step

   * **Step3 Release Feature:**  that is, publish according to the Feature Release Process (the default workflow of the system), and take effect online

      * Follow the corresponding steps step by step

      * See the Release Features for details.
