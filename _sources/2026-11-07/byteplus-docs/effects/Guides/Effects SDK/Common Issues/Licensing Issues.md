---
title: "Licensing Issues"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-licensing-issues"
---

<span id="1. Can I use the license file that binds my package name?"></span>
### 1. Can I use the license file that binds my package name?

A: Using the default license and material in our sample (bundle file under resource) for integration testing is recommended. The advantage is that the default license in our sample is fully functional, so you can test and experience all its functions. After the integration test is completed, you can apply for the official license file bound to your package name. You only need to replace the default license and material with the newly provided official ones, which will not affect the previous integration test results. If you want to use the license file bound to your package name for testing, please contact our business representative first and explain your specific reasons.

<span id="2. How do I use the default license in the sample for testing?"></span>
### 2. How do I use the default license in the sample for testing?

A: The license file is bound with the package name "com.bytedance.labcv.demo" in our sample. For the integration test, you need to change its Application ID/Bundle ID to "com.bytedance.labcv.demo" to start the test.

Android: Change the Application ID in Gradle to "com.bytedance.labcv.demo".

iOS: Change the General/Identity/Bundle Identifier to "com.bytedance.labcvdemo" (for iOS, please be sure to use the enterprise developer account, not the personal developer account. In addition, make sure to refresh the enterprise developer account after modifying Bundle ID. Check "automatically manage signing" repeatedly several times until the developer's account is refreshed.)

<span id="3. Are the license and material bound to the SDK version?"></span>
### 3. Are the license and material bound to the SDK version?

A: In principle, both the license and materials are bound to the SDK version, that is, the license and materials applied for/used by the current version can only be used in this version of the SDK, but not in other versions.

<span id="4. When the official license expires, must it be replaced with a new version and will users be forced to update?"></span>
### 4. When the official license expires, must it be replaced with a new version and will users be forced to update?

A: The new license file needs to be replaced when the official license expires, but a new version may not be required. It is recommended to send the new license using a file distribution service. (Generally, mobile Apps will have services to distribute resources—such as pictures and videos—so you can send our license file to the client as a resource. It belongs to the logic in the application layer).

<span id="5. What are the possible reasons for license failure?"></span>
### 5. What are the possible reasons for license failure?

A: To determine the reason for license failure, you can:


1. Check whether the mobile phone system time is correct.

2. Check whether the bundle ID of the Android Application ID/iOS matches the licensed package name.

3. Check whether check_license matches the corresponding version number.


If it is not one of the problems mentioned above, then check the Error type log of the following tag output:


* **Bef _effect_ai**

* **SMASH_E_LOG**

* **EffectSDK**


Double check the corresponding description in [Error Code Table](https://byteplus-docs.readme.io/effects/docs/error-code-table) against the solutions provided.

<span id="6. Can two Apps with different package names but owned by the same customer share the same set of licenses and materials?"></span>
### 6. Can two Apps with different package names but owned by the same customer share the same set of licenses and materials?

A: No, they cannot share. The materials are matched with the licensed package name. For more information, please contact one of our business representatives.
