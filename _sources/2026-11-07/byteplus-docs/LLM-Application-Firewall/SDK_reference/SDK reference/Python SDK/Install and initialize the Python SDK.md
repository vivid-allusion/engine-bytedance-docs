---
title: "Install and initialize the Python SDK"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Python_installation_and_initialization"
---

The LLM Application Firewall Python SDK enables you to integrate robust security into your Python applications that leverage Large Language Models (LLMs). It protects against common threats like prompt injections and data leakage, ensuring your AI interactions are safe and compliant. This guide provides the complete process for installing and initializing the SDK, which is essential when building secure LLM\-powered services like intelligent chatbots or content creation tools.

<span id="3b8e665d"></span>
## Prerequisites


* Obtain the Access Key ID (AK) and Secret Access Key (SK). You have two options:

   * Go to [BytePlus IAM > Access key management](https://console.byteplus.com/iam/keymanage) to find your existing access key pair.

   * Create a RAM user and generate a new AccessKey pair. For details, refer to [Create a user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user).

* In the LLM Application Firewall console, add an asset and configure its protection policies. For details, refer to [Introduction to protection policies](https://docs.byteplus.com/docs/LLM-Application-Firewall/introduction_to_protection_policy).


&nbsp;

<span id="3fb51ead"></span>
## Environmental requirements

Python 3.7 or later is required (Python 3.9 is recommended).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">Run <strong><code>python3 --version</code></strong> to check the current Python version.</div>


<span id="8d6453b7"></span>
## Important notes

Due to the maximum path length limitation in the Windows operating system, Python installation may fail. You can enable long paths as follows:


1. Press `Win+R`, enter `regedit` to open the Registry Editor.

2. Set the variable `LongPathsEnabled` under the path `\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\FileSystem` to `1`.


<span id="f7243957"></span>
## Install the SDK


1. Use the pip command to install the SDK.

   ```Bash
   pip3 install byteplus-python-sdk-v2
   ```
   

2. Install dependencies.

   * Install the `pydantic` dependency:

      ```Bash
      pip3 install pydantic
      ```
      

   * Install the `requests` dependency:

      ```Bash
      pip3 install requests
      ```
      


<span id="7b687851"></span>
## Initialization

This section describes the initialization parameters and provides sample code.

<span id="6d99cf55"></span>
### Parameter description


|Parameter |Example |Description |
|---|---|---|
|myUrl |https://ap\-southeast\-1.sdk.access\-bp.llm\-shield.omni\-shield.ai<br><br> |* **Parameter description**: The endpoint for the LLM Application Firewall service has the format **`https://`**  **`{region}`**  **`.sdk.access-bp.llm-shield.omni-shield.ai`**, where {region} is the region of your provisioned instance.<br><br>   * ap\-southeast\-1<br><br>   * cn\-hongkong<br><br>* **Finding this value**: You can find the region in the instance management module of the LLM Application Firewall console. |
|ak, sk |* AK : AKLTYWRhNDMw\*\*\*\*<br><br>* SK: TWprNE5XVXlZbc\*\*\*\* |These are the **Access Key ID** and **Secret Access Key** for your BytePlus account. |
|appid |app\-d35p9du8pa51\*\*\*\* |* **Parameter description**: The unique identifier of the asset. After you add an asset in the console, the system automatically generates an AppID.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Caution   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When making SDK calls, only assets integrated via the SDK method are supported.   </div><br>   <br><br>* **Finding this value**: Go to the asset management module in the LLM Application Firewall console to view the AppIDs of assets integrated via SDK. |
|region |ap\-southeast\-1 |* **Parameter description**: This is the region of your LLM Application Firewall instance. It must match the region specified in `myUrl`.<br><br>   * ap\-southeast\-1<br><br>   * cn\-hongkong<br><br>* **Finding this value**: Go to the LLM Application Firewall console instance management module to view the region where the instance is located. |


&nbsp;

&nbsp;

<span id="1e8da51b"></span>
### Sample code

The following is a complete initialization code example:

```Python
from byteplussdkllmshield import *

def main():
    # Replace the parameters with the actual values
    myUrl = "https://ap-southeast-1.sdk.access-bp.llm-shield.omni-shield.ai" # Endpoint of your LLM Application Firewall instance
    ak = "YOUR AK"  # Access Key ID for your BytePlus account
    sk = "YOUR SK"  # Secret Access Key for your BytePlus account
    appid = "app-d40oac7fjl9ffpn3****" # AppID of your asset
    region = "ap-southeast-1"  # Region of the LLM Application Firewall instance

    TIMEOUT = 50  # Timeout (seconds)
```
