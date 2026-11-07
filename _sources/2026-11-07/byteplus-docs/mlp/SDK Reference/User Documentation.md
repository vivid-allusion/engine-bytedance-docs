---
title: "User Documentation"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/User_Documentation"
---

The Machine Learning Platform provides the Python SDK `volcengine-ml-platform` for users to access the Machine Learning Platform on any machine with internet connectivity. This SDK currently supports functions such as model registration, service deployment, and experiment management.

<span id="相关概念"></span>
# Related Concepts


* AK / SK

* Region

* Command Line Tool (volc)


See in [Common concepts](https://docs.byteplus.com/docs/mlp/76491)

<span id="安装"></span>
# Installation

Use the following command to install the latest version of the SDK:

```bash
git clone http://github.com/volcengine/ml-platform-sdk-python
cd ml-platform-sdk-python && python -m pip install .
```


<span id="配置-ak-sk"></span>
# Configure AK/SK

Before officially using the SDK, you need to first complete the local configuration of AK/SK for your Byteplus account; otherwise, identity verification will fail when using the SDK to access the Machine Learning Platform.


1. Log in to the Byteplus console and go to [Key Management] to view the AK/SK of the current account.

   * If the current account is a sub\-account, it needs to have the IAM policy of `AccessKeyFullAccess`.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c12dfd612a14d2591fef213e73bcfb0~tplv-goo7wpa0wc-image.image) </span>


2. It is recommended to use the volc command\-line tool to configure AK/SK. Like the SDK, this tool is also a way to access the machine learning platform without using the console page. For details on installing this tool, see [Command-Line Tool (volc)](https://www.volcengine.com/docs/6459/72394). After installing the command\-line tool, configure AK/SK and region interactively via `volc configure`.

   ```Plain
   volc configure
   volc access key [********yM2I]: Enter the user's AK
   volc secret access key [********TQ==]: Enter the user's SK
   volc region [cn-beijing]: █ Enter the region, supporting cn-beijing, cn-shanghai, cn-guangzhou, cn-beijing2, ap-southeast-1
   ```
   

* Method 2: If you do not want to install the command\-line tool additionally, you can manually create two files, `config` and `credentials`, in the `~/.volc` directory and correctly fill in the region and AK/SK.

   * `~/.volc/config`

   ```Plain
   [default] 
   region = cn-beijing Fill in the region where you are located, supporting cn-beijing, cn-shanghai, cn-guangzhou, cn-beijing2, ap-southeast-1
   ```
   

   * `~/.volc/credentials`

   ```Plain
   [default]
   access_key_id = ****** Fill in the user's AK
   secret_access_key = ****** Fill in the user's SK
   ```
   

* Method 3: Configure AK/SK and region via environment variables.

   ```Bash
   export VOLC_ACCESSKEY=**** Fill in the user's AK
   export VOLC_SECRETKEY=**** Fill in the user's SK
   export VOLC_REGION=**** Fill in the region, supports cn-beijing, cn-shanghai, cn-guangzhou, cn-beijing2, ap-southeast-1
   ```
   


<span id="使用-sdk"></span>
# Use SDK

How to use the SDK to access the machine learning platform and complete actions such as model registration, service deployment, and experiment management: see the following examples for details.


* Model Management and Service Deployment:

   * [Sample code](https://github.com/volcengine/ml-platform-sdk-python/tree/main/samples)

* Experiment Management:

   * [README](https://github.com/volcengine/ml-platform-sdk-python/tree/main/volcengine_ml_platform/tracking/README.md)

   * [Sample code](https://github.com/volcengine/ml-platform-sdk-python/tree/main/samples/tracking)
