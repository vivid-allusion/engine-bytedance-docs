---
title: "Install TLS SDK for C++"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/install_tls_sdk_for_c"
---

Before you use a Torch Log Service (TLS) SDK to perform operations, install the SDK. This topic describes how to install TLS SDK for C++.

<span id="开发环境要求"></span>
## Development environment

Make sure that the current development environment meets the following requirements:


|Environment |Description |
|---|---|
|Linux |Linux distributions such as Debian and CentOS |
|C++ compiler |C++11 or later |


<span id="安装c-sdk"></span>
## Installing TLS SDK for C++

To install TLS SDK for C++:


1. Install the dependencies.

   1. Install the C++ Protobuf library. The following sample code installs Protobuf 3.21.10:

      ```sql
      wget https://github.com/google/protobuf/releases/download/v3.21.10/protobuf-3.21.10.tar.gz
      tar zxvf protobuf-3.21.10.tar.gz
      cd protobuf-3.21.10
      ./configure
      make
      make check
      make install
      ```
      

   2. Install the C++ OpenSSL library. Install the library from [OpenSSL source code](https://github.com/openssl/openssl), or run the following command:

      ```cpp
      # For Ubuntu and Debian
      sudo apt-get install libssl-dev
      # For CentOS 7
      yum install openssl-devel
      # For RedHat and Fedora
      sudo dnf install openssl-devel
      ```
      

   3. Install the C++ LZ4 library. For more information, refer to the [LZ4 documentation](https://github.com/lz4/lz4).

2. Install TLS SDK for C++.

   1. Download the latest version of TLS SDK for C++. Get the project source code from https://github.com/volcengine/ve\-tls\-cpp\-sdk.

   2. Switch to the source code directory of TLS SDK for C++, and run the following command to install the SDK:

   ```cpp
   ./genpb.sh
   mkdir build
   cd build
   cmake ../
   sudo make
   sudo make install
   ```
