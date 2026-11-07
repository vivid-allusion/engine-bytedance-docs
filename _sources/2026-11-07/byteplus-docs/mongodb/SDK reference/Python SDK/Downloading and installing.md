---
title: "Downloading and installing"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/download-install-python-sdk"
---

This topic describes how to download and install the MongoDB Python SDK.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign up and verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* As per the regulations in the Chinese mainland, you must have completed real name registration before you can activate and use cloud services in regions in the Chinese mainland through BytePlus. For more details, refer to [Real name registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration).

* Before accessing the Document Database for MongoDB API using the BytePlus Python SDK, please confirm that you have enabled the MongoDB service in the [BytePlus Console](https://console.byteplus.com/home).

* If Python v2.7 or higher has been installed, you can check the current Python version with the `python version`.


<span id=".c2RrLeS4i-i9veWcsOWdgA=="></span>
## SDK download link

For the MongoDB Python SDK source code address, refer to [MongoDB Python SDK](https://github.com/byteplus-sdk/byteplus-python-sdk-v2/tree/main/byteplussdkmongodb).

<span id=".5a6J6KOFLXNkaw=="></span>
## Installing the SDK

You can install the SDK in any of the following ways:


* Install the SDK with the `pip` command.

   ```Python
   pip install byteplus-python-sdk-v2
   ```
   

* Download the MongoDB Python SDK source code and install it with the [Setuptools.](https://pypi.org/project/setuptools/) tool. You can run the following commands based on business needs:

   * Run the following command to install the SDK for specified users.

      ```Python
      python setup.py install --<username>
      ```
      

   * Run the following command to install the SDK for all users.

      ```Python
      sudo python setup.py install
      ```
