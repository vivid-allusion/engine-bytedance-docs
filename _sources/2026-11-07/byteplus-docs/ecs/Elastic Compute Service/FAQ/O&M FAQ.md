---
title: "O&M FAQ"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/O-and-M-FAQs"
---

<span id=".6YCa6L-H5om56YeP5L2c5Lia5omn6KGM5q2j56Gu55qEV2luZG93cyBQb3dlclNoZWxs5oiWQmF06ISa5pys5Li65L2V5oql6ZSZ4oCc5LiN5piv5YaF6YOo5oiW5aSW6YOo5ZG95Luk77yM5Lmf5LiN5piv5Y-v6L-Q6KGM55qE56iL5bqP5oiW5om55aSE55CG5paH5Lu24oCd77yf"></span>
## Why do I receive an error message saying "This is not an internal or external command, nor a runnable program or batch file" when the cloud assistant executes a correct Windows PowerShell or Bat script?


* **Possible cause:** 

   Scripts transferred by the cloud assistant to your instance are encoded in UTF\-8 by default, whereas Windows CMD uses GBK by default. Therefore, this issue may be caused by Chinese characters in your Windows script.

* **Solutions:** 

   * Solution 1:

      Add the following command at the first line of your script:

      ```Plain Text
      chcp 437
      ```
      

   * Solution 2:

      Replace Chinese characters in the script with English characters.


<span id="qSQ4aBH3"></span>
## Why does the execution timeout occur when I call the cloud assistant by executing the `nohup {cmd} &` command?

When the Cloud assistant executes the nohup command, it needs to perform redirection for the command output. Otherwise, the Cloud assistant will wait for IO, thus causing the execution timeout.

Use the redirection symbol `>`to specify the output file. Format: `nohup {cmd} & > output.log 2>&1 &`.
