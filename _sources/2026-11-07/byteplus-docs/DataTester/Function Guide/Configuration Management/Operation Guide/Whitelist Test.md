---
title: "Whitelist Test"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Whitelist-Test"
---

<span id="一、功能简介"></span>
# Introduction to functions

Before the experiment is officially launched, it is usually necessary to select a few users to enter the testing phase to observe whether the experiment can normally obtain the data to be collected, or whether there are bugs on the client side. Users who participate in this step are called "whitelisted users". The added whitelist is mainly used to debug Features and check whether whitelisted users can hit Experiments/Features.

<span id="二、如何使用"></span>
# How to use


* Function entrance: [feature list] \- Click [feature name] to display the created whitelist test list, and you can create a new whitelist test.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f21efee851e4a23850da67528e1d651~tplv-goo7wpa0wc-image.image) </span>

* Main usage scenarios:

   * **Scenario 1:**  Feature creator adds whitelist for test validation during creation

      * The whitelist does not need to be published to take effect

   * **Scenario 2:**  After a feature is created and before it is published, QA staff tests and verifies the feature

      * The whitelist does not need to be published to take effect

      * QA can easily add whitelist

   * **Scenario 3:**  After the Feature is released, if there is an online problem, quickly roll back. After rolling back, I want to reproduce the problem of this version

      * The version that has been rolled back can support whitelisting testing.

   * **Scenario 4:**  For the same Feature ① The logic to be tested is different/② Different people conduct their own test verification, such as wanting to test the case of Android effective value 1 or Android effective value 2 respectively, which is no problem, that is, which strategy is used

      * For Features, you can add whitelist test and verification first, and then use it as a correct version if there is no problem.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eac08ec0c2f84e69a405af1081c270bb~tplv-goo7wpa0wc-image.image) </span>

* Specific operation:

* Feature Details Add a separate whitelist test feature

* You can perform whitelist testing for existing versions or modify new content yourself

* Whether to support whitelisting needs to meet audience rules 2 test scenarios

* After submitting the test, the whitelist will take effect; if the whitelist fails, the user needs to take the initiative to cancel the test

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e79ed2d7d274cc1adc130c9a1df918d~tplv-goo7wpa0wc-image.image) </span>

* Function introduction:

   *  **① Test Name:**  Fill in a name for this whitelist test

   *  **② Test version:**  Users can choose to test the existing version, or modify the variants and effective rules for whitelist testing

   *  **③ Expiration time:**  Select the expiration date (to hours and seconds), only the date within 7 days can be selected.

      * Example: Currently 2022.03.24, selectable date range 03.24\-03

      * Note: After selecting a certain day, the default will expire at 23:59:59 on the same day.

   *  **④ Whitelist:**  that is, add corresponding whitelists for different audience rules

      * The top shows custom variables and variant information, and the bottom shows audience rules and whitelist text boxes

      * **Custom Variables & Variant Information and Audience Rules:**  Consistent with Editing Features, supports user modification (including: adding edit custom variables, adding and deleting edit variants/variant names, adding and deleting edit audience rules).

      * **Whitelist text box:**  Each publishing rule (including the default publishing rule) corresponds to a whitelist text box

      * **Test whitelist drop\-down selection:**  Support drop\-down selection of a group of user whitelists, maintain and edit a group of whitelists[User Testing Whitelist](https://docs.byteplus.com/docs/DataTester/User-Testing-Whitelist)

   * After adding the whitelist and writing the content of the test, click the [Submit Test] button below, that is, the save is successful and the test is entered, and the whitelist will take effect (return to the whitelist test list page)
