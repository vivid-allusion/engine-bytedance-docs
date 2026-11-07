---
title: "Public resource pool"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Public_resource_pool"
---

The public resource pool is the environment provided by Continuous Delivery for running build tasks, meeting your daily build and packaging needs. This document introduces content related to the public resource pool.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The public resource pool cannot be modified.</div>


* <div data-tips="true" data-tips-type="tip">The public resource pool has limits on single account execution time and the number of concurrent pipeline runs. For details, see <a href="https://docs.byteplus.com/en/docs/cp/Limit">usage limits</a>. If your usage quota is exceeded, you can use the private resource pool.</div>



<span id=".5pSv5oyB6K-t6KiA5Y-K54mI5pys"></span>
## Supported languages and versions

The public resource pool comes pre\-installed with the following image versions for compilation, build, or command execution:


|Language |Tier |
|---|---|
|Java |JDK 7、JDK 8 、JDK 11、JDK 17、JDK 21 |
|Java Maven |3.6.3 |
|Java Gradle |7.4.2 |
|Python |2.7、3.6、3.8、3.10、3.11、3.12 |
|Go |1.12.4、1.15.1、1.16.13、1.17.3、1.18.8、1.20、1.21.4 |
|Node.js |6.17.1、8.17.0、10.24.1、12.22.5、 14.17.5、16.14.0、18.20.4、20.11.0 |
|Bash |4.4.12 |
