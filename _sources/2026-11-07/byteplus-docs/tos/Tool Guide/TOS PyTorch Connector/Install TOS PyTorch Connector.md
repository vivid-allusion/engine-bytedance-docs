---
title: "Install TOS PyTorch Connector"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Install_TOS_PyTorch_Connector"
---

This article describes the environment requirements and installation of the TOS PyTorch Connector.

<span id="4265b41e"></span>
## Environment requirements


* Operating system: Linux x86\-64.

* Python: 3.8~3.13.

* PyTorch: \>=2.0.


<span id="a32c7fa9"></span>
## Installation steps

You need to successfully install the TOS PyTorch Connector in your Python environment.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The installation involves downloading and compiling related dependencies, which may take some time. Please be patient.</div>



&nbsp;

1. Install by running the following command with `pip`.


```bash
pip install -v tostorchconnector
```



2. After installation, run the `pip show tostorchconnector` command to verify the installation status. The appearance of the following information indicates a successful installation.


```YAML
Name: tostorchconnector
Version:
Summary: TOS connector integration for PyTorch
Home-page:
Author:
Author-email:
License:
Location: /usr/local/lib/python3.10/dist-packages
Requires: torch, tos, tosnativeclient
Required-by:
```


<span id="aacc7816"></span>
## Next steps

[Configure TOS PyTorch Connector](https://docs.byteplus.com/docs/tos/Configure_TOS_PyTorch_Connector)
