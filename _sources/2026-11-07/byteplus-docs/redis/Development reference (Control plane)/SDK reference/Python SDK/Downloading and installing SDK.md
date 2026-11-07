---
title: "Downloading and installing SDK"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/download-install-python-sdk"
---

This topic describes how to download and install Redis Python SDK.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Python 2.7 or a later version is installed.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can run <code>python --version</code> command to check the current Python version.</div>


<span id=".c2RrLeS4i-i9veWcsOWdgA=="></span>
## SDK download address

For the Redis Python SDK source code address, refer to [Redis Python SDK](https://github.com/byteplus-sdk/byteplus-python-sdk-v2/tree/main/byteplussdkredis).

<span id=".5a6J6KOFLXNkaw=="></span>
## Install SDK

You can install the SDK in one of the following ways:


* Install the SDK using the `pip` command.

   ```Python
   pip install byteplus-python-sdk-v2
   ```
   

* Download the Redis Python SDK source code and install it with [Setuptools](https://pypi.org/project/setuptools/) tool. Run the corresponding commands to install it based on your business needs:

   * Run the following command to install the SDK for a specific user.

      ```Python
      python setup.py install --<username>
      ```
      

   * Run the following command to install the SDK for all users.

      ```Python
      sudo python setup.py install
      ```
