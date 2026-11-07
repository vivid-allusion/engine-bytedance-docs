---
title: "Overview"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/parameter-template-overview"
---

Document Database for MongoDB provides a parameter template function. When you need to configure one or more identical parameter values for MongoDB instances of the same database version, you can use the parameter template function to centrally manage parameters and quickly apply the parameters in the template to the target instance to improve the efficiency of parameter management and instance configuration.

<span id=".5Y-C5pWw5qih5p2_57G75Z6L"></span>
## Type of parameter template

Document Database for MongoDB supports two types of parameter templates: **Customized template** and **System template**. The table below specifies the differences between the two types of templates in terms of use cases, quantitative restrictions, and supported operations for your reference.


|Type of parameter template |Customized templates |System templates |
|---|---|---|
|Usage scenario |Place one or more parameter configurations in a parameter template according to your service requirements. Batch applies these configurations to instances of the same database version to improve the efficiency of parameter management and instance configuration. |Document Database for MongoDB provides a default parameter template for each database version, which includes all parameters and default parameter values supported by the version. You can use the system parameter template to quickly restore all parameters of the instance to their default values. |
|Quantity limits |* Each root account of BytePlus can create up to 100 customized parameter templates in each region by default.<br><br>* Each parameter template can be applied to up to 10 instances at one time. |* Currently, only replica set instances support the parameter template feature. MongoDB provides the following system parameter templates for replica set instances:<br><br>   * MongoDB_Replica_4_2_Default<br><br>   * MongoDB_Replica_4_4_Default<br><br>   * MongoDB_Replica_5_0_Default<br><br>   * MongoDB_Replica_6_0_Default<br><br>   * MongoDB_Replica_8_0_Default<br><br>   * MongoDB_Replica_8_3_Default<br><br>* Each parameter template can be applied to up to 10 instances at one time. |
|Supported operations |* [Creating parameter template](https://docs.byteplus.com/en/docs/mongodb/create-parameter-template)<br><br>* [Editing parameter template](https://docs.byteplus.com/en/docs/mongodb/edit-parameter-template)<br><br>* [Copying parameter template](https://docs.byteplus.com/en/docs/mongodb/copy-parameter-template)<br><br>* [Exporting as parameter template](https://docs.byteplus.com/en/docs/mongodb/export-parameter-template)<br><br>* [Deleting parameter template](https://docs.byteplus.com/en/docs/mongodb/delete-parameter-template) |* [Copying parameter template](https://docs.byteplus.com/en/docs/mongodb/copy-parameter-template)<br><br>* [Applying parameter template](https://docs.byteplus.com/en/docs/mongodb/apply-parameter-template) |
