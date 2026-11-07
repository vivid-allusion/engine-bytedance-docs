---
title: "Installing the C++ SDK"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Install-c-sdk"
---

This article introduces the download address and installation method for the TOS C++ SDK.

<span id=".546v5aKD5YeG5aSH"></span>
## Environmental Preparation

Before installing the TOS C++ SDK, ensure that the following dependencies have been installed:


* C++11 or later versions

* CMake version 3.1 or higher

* GCC version 4.8 or later

* Clang version 3.3 and later

* Visual Studio 2019 or later is required in the Windows environment.


<span id=".5LiL6L295Zyw5Z2A"></span>
## Download Link


* Latest source code address: [Source code address](https://github.com/volcengine/ve-tos-cpp-sdk)

* Sample Code Address: [Sample Code](https://github.com/volcengine/ve-tos-cpp-sdk/tree/main/example)

* Version Revision Record: [Revision Record](https://github.com/volcengine/ve-tos-cpp-sdk/blob/main/CHANGELOG.md)

* Historical Version Address: [Historical Version](https://github.com/volcengine/ve-tos-cpp-sdk/tags)


<span id=".5a6J6KOF5pa55byP"></span>
## Installation Method

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The C++ SDK is currently not supported for installation or use on Android or Linux ARM systems.</div>



<Tabs>
<Tab zoneid="gUIfYpTbJf" title="Compiling from Source Code">
<TabTitle>Compiling from Source Code</TabTitle>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The SDK depends on the libcurl and openssl libraries. Before building the SDK, please ensure that both libraries have been installed.</div>



1. Download the source code. You may download the source code using the following methods:

   * Direct download: See the source code address for the TOS C++ SDK at [TOS C++ SDK](https://github.com/volcengine/ve-tos-cpp-sdk). The latest version is determined by the updates in Git.

   * Download via Git: Execute the following command to clone the source code to your local machine.

      ```bash
      git clone https://github.com/volcengine/ve-tos-cpp-sdk
      ```
      

2. Execute the following command to build using CMake version 3.1 or above.

   ```bash
   cd ve-tos-cpp-sdk
   mkdir build
   cd build
   ```
   


</Tab>
<Tab zoneid="VBWHJX5f9I" title="Linux">
<TabTitle>Linux</TabTitle>

1. Execute the following command to install libcurl and openssl.

   ```bash
   # For Ubuntu/Debian systems
   sudo apt-get install libcurl4-openssl-dev libssl-dev
   
   # For Centos7
   yum install libcurl-devel openssl-devel
   
   # For Redhat/Fedora systems
   sudo dnf install libcurl-devel openssl-devel
   ```
   

2. Execute the following commands to compile and install.

   ```bash
   cmake ../ -DCMAKE_INSTALL_PREFIX="custom installation path"
   make
   make install
   ```
   


</Tab>
<Tab zoneid="Wzv9OqKCpr" title="macOS">
<TabTitle>macOS</TabTitle>

On macOS, you can install dependency libraries using the brew package manager.

On macOS systems, the path to the OpenSSL library must be specified. Assuming that OpenSSL is installed in the `/usr/local/Cellar/openssl@3/3.0.0` directory, you can execute the following commands to compile.

```bash
cmake .. -DOPENSSL_ROOT_DIR=/usr/local/Cellar/openssl@3/3.0.0 
         -DOPENSSL_LIBRARIES=/usr/local/Cellar/openssl@3/3.0.0/lib 
         -DOPENSSL_INCLUDE_DIRS=/usr/local/Cellar/openssl@3/3.0.0/include
         -DCMAKE_INSTALL_PREFIX="custom installation path"
make
make install
```



</Tab>
<Tab zoneid="lp5bHKsnOf" title="Windows">
<TabTitle>Windows</TabTitle>

Run the VS Developer Command Prompt as an administrator, then execute the following commands in the build directory to compile and install.

```bash
cmake ../
msbuild ALL_BUILD.vcxproj
msbuild INSTALL.vcxproj
```



</Tab>
</Tabs>


<span id=".6YCa6L-H5rqQ56CB57yW6K-R"></span>
## CMake Compilation Options

<span id="build-shared-lib"></span>
### BUILD_SHARED_LIB

Disabled by default; CMake compiles only static libraries by default. After opening the project, CMake will simultaneously compile both the static and dynamic libraries, and at the same time, the SDK will link to the dynamic library.

```bash
cmake .. -DBUILD_SHARED_LIB=ON
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The BUILD_SHARED_LIB compilation option is currently not supported in the Windows environment.</div>


<span id="build-demo"></span>
### BUILD_DEMO

Disabled by default. After opening the project, CMake will compile the examples in the example folder, which can then be run directly. Refer to the examples in the example folder.

```bash
cmake .. -DBUILD_DEMO=ON
```


<span id="build-unittest"></span>
### BUILD_UNITTEST

Disabled by default. After opening the project, CMake will compile the unit test cases in the test folder. Note that if you need to compile the unit test section, cmake must be greater than version 3.14.

```bash
cmake .. -DBUILD_UNITTEST=ON
```


<span id=".5Y2H57qn5YiwLXYy"></span>
## Upgrade to Version 2

To upgrade to TOS C++ SDK V2, you must modify the client initialization method. Compared to the V1 version, the V2 version has the following characteristics:


* Enhanced interface capabilities: V2 supports a broader range of interfaces and is continuously improved.

* Additional value\-added features are available, with certain V2 interfaces supporting event callbacks, progress notifications, rate limiting, and other value\-added features.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">New features will not be added to Version V1 in the future; we recommend using Version V2.</div>


<span id=".5L-u5pS55YmN"></span>
### Before modification

The initialization of the TosClient client is as follows.

```cpp
#include "TosClient.h"
using namespace VolcengineTos;
int main(void){
    std::string endpoint = "Your Endpoint";
    std::string region = "Your Region";
    
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    InitializeClient();
    
    TosClient client(endpoint, region, accessKey, secretKey);
    /*
   
    */
    CloseClient();
    return 0;
}
```


<span id=".5L-u5pS55ZCO"></span>
### Revised

Initialize the TosClientV2 client as follows.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;
int main(void){
    
    
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    
    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey);
    
    /*
  
    */
    
    CloseClient()
    return 0;
}
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The initialization parameters for the client have changed in the upgrade to V2: the endpoint parameter, which was the first required parameter in Client V1, has been modified to an optional parameter in Client V2. If you still need to specify the endpoint, please refer to <a href="https://docs.byteplus.com/docs/tos/Initialize-client-side-c-sdk">Setting Optional Parameters</a> for detailed steps.</div>
