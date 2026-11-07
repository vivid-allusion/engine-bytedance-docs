---
title: "Dependency Installation"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Python_runtime_Dependency_Installation"
---

For the Python runtime, the Function Service supports two methods: online installation of dependencies and packaging dependencies with code for upload. This topic introduces these two methods of dependency installation.

<span id="online-installation-of-dependencies-recommended"></span>
## Online Installation of Dependencies (Recommended)

The Function Service will check the requirements.txt file in the root directory of the code package and attempt to install dependency packages using pip install based on the dependencies listed in requirements.txt.


1. Create a Python runtime function, for specific actions refer to [Creating event functions](https://docs.byteplus.com/en/docs/faas/Creating_event_functions).

2. Switch to the **Code** tab of the target function and configure dependency information in the requirements.txt file. Note that you must follow the [Official syntax specifications](https://pip.pypa.io/en/stable/reference/requirements-file-format/).

3. Click **Install dependencies**, and the system begins installing dependencies online.

   All dependencies will be installed in the `site-packages` directory.


<span id="package-dependencies-and-code-together-and-uploading"></span>
## Package dependencies and code together and uploading

By using a dependency management tool, for example, pip, install dependencies locally and then package them together with the function code for uploading.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When packaging, the entry file index.py must be in the .zip package's root directory. If you package and upload the entire folder in a .zip package, it will fail to create the function because the entry file cannot be found in the root directory after extraction.</div>


* <div data-tips="true" data-tips-type="warning">The Zip package size must not exceed 256 MiB.</div>


* <div data-tips="true" data-tips-type="warning">Due to differences in the runtime environments, confirm that the Python version and the installed dependencies are compatible with your function's runtime version. Check the version by executing python \-v in your local environment.</div>


* <div data-tips="true" data-tips-type="warning">The function runs on Debian, you need to install it in the same environment. If the environments are not consistent, it may cause errors in finding the dependencies after upload during runtime.</div>


1. Configure the dependency information in the requirements.txt at the root directory of your local project. Note that you must follow the [Official syntax specifications](https://pip.pypa.io/en/stable/reference/requirements-file-format/).

2. In the local project root directory, run the following command to install dependency packages.

   ```shell
   # Using the `-t` parameter, you can specify the installation directory for the dependency packages. When executing in the project code directory, you can use `-t .` to install in the current directory.
   python -m pip install -r requirements.txt -t .
   ```
   

3. Run the following command to package all files in the root directory into a deployment.zip .zip file.

   ```shell
   # This example only illustrates with deployment.zip, the actual filename is not restricted
   zip -r ./deployment.zip .
   ```
   

4. Upload the deployment.zip file to the function Service console for Deployment. For details, refer to [Creating event functions](https://docs.byteplus.com/en/docs/faas/Creating_event_functions).
