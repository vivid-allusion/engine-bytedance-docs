---
title: "Overview of instance launch templates"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Launch-template-overview"
---

An instance launch template is a collection of instance configuration information used for quickly purchasing instances. In a template, you can store all configuration information except the password, including the key pair, instance type, volume, and network. If all configuration information is valid, you can purchase instances with one click, without the need to configure the settings repeatedly.

<span id=".5qih5p2_54mI5pys"></span>
## Template versions

You can create one or more versions for an instance launch template, and each version may store different configuration information. When you purchase an instance by using an instance launch template, you can select any version of the template. If you do not select a version, the default version is used.

By default, the first version of the template is specified as the default version, and you can also specify any version as the default version.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

<span id=".5pWw6YeP55u45YWz"></span>
### Quantity


* Each account can create up to 30 instance launch templates in each region.

* Each instance launch template can have up to 30 versions at the same time.


<span id=".5qih5p2_55u45YWz"></span>
### Template


* After you create an instance launch template, you cannot modify the template. However, you create a new version of the template.

* Instance launch templates do not support project and tag features.


<span id=".54mI5pys55u45YWz"></span>
### Version


* After you create a new version of an instance launch template, the default version of the template remains unchanged. You can manually change the default version.

* Version numbers are assigned sequentially based on the order in which they are created. You cannot manually specify a version number. After you delete a version, the numbers of the remaining versions do not change or shift forward to fill the gap.
