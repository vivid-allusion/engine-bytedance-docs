---
title: "Installing the C SDK"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Install-the-c-sdk"
---

This document provides an overview of the environment, download location, and installation procedures for the TOS C SDK.

<span id=".546v5aKD5YeG5aSH"></span>
## Development Environment Preparation

This document is based on TOS C SDK 2.1.0. The development environment requirements are as follows:

<span id="3ddd12a6"></span>
### Installing Dependency Libraries


* Install the CMake tool (version 2.6.0 or later is recommended). For the download link, refer to [CMake](https://cmake.org/download/). The typical installation procedure is as follows:

   ```Bash
   ./configure
   make
   make install
   ```
   

* Install libcurl (version 7.32.0 or later is recommended). For the download link, please refer to [ libcurl](https://curl.se/download.html?spm=5176.doc32132.2.7.23MmBq). Typical installation methods are as follows:

   ```Bash
   ./configure
   make
   make install
   ```
   

* Install apr (version 1.5.2 or later is recommended). For the download link, please refer to [ apr](https://apr.apache.org/download.cgi?spm=5176.doc32132.2.9.23MmBq&file=download.cgi). The typical installation procedure is as follows:

   ```Bash
   ./configure
   make
   make install
   ```
   

* Install apr\-util (version 1.5.4 or later is recommended). For the download link, please refer to [apr-util](https://apr.apache.org/download.cgi?spm=5176.doc32132.2.10.23MmBq&file=download.cgi). During installation, you need to specify the `--with-apr` option. A typical installation method is as follows:

   ```Bash
   ./configure --with-apr=/your/apr/install/path
   make
   make install
   ```
   

* Install cJSON (version 1.7.18 or later is recommended). For the download link, see [cJSON](https://github.com/DaveGamble/cJSON). Typical installation methods are as follows:

   ```Bash
   ./configure
   make
   make install
   ```
   


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The TOS C SDK utilizes <a href="https://apr.apache.org/">APR</a> (Apache Portable Runtime)'s <a href="https://apr.apache.org/docs/apr/1.5/group__apr__pools.html">memory pool mechanism</a> for memory management. When using the TOS C SDK, your business code can also employ APR for memory management to prevent memory leaks. If your business code does not use APR for memory management, you must manually handle memory allocation and deallocation to prevent memory leaks.</div>


<span id=".5LiL6L295Zyw5Z2A"></span>
## Download Link


* Latest source code address: [Source Code Address](https://github.com/volcengine/ve-tos-c-sdk)

* Revision History: [Version Record](https://github.com/volcengine/ve-tos-c-sdk/blob/main/CHANGELOG.md)

* Historical Version Address: [Historical Version](https://github.com/volcengine/ve-tos-c-sdk/releases)


<span id=".5a6J6KOF5pa55byP"></span>
## Installation Method

<span id="ac3a1dbb"></span>
### Source Code Installation

Download the source code from [GitHub](https://github.com/volcengine/ve-tos-c-sdk). Typical compilation commands are as follows:

```Bash
cmake .
make
make install
```
