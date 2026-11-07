---
title: "When running pipeline with private resource pool it stays in environment preparation stage"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/When_running_pipeline_with_private_resource_pool_it_stays_in_environment_preparation_stage"
---

The storage class used by your private resource pool may not meet the requirements. You need to delete the existing private resource pool, re\-create a file storage NAS\-type storage class with a capacity greater than 50 GB, and use this storage class to re\-create the private resource pool.

Private resource pool storage class requirements:


* Only NAS file storage classes are supported. The private resource pool requires storage classes that support ReadWriteMany. Cloud disk storage classes do not support ReadWriteMany and must not be used.

* The capacity of the file storage NAS must be at least 50 GB. NAS is used to store cache and intermediate products generated during pipeline compilation and build processes. Insufficient capacity may lead to the loss of these products.
