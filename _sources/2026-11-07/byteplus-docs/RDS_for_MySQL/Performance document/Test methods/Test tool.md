---
title: "Test tool"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/test_tools"
---

This topic describes the tools used to stress test RDS for MySQL.

<span id=".5rWL6K-V5bel5YW3"></span>
### Test tool

Sysbench is a modular, scriptable open\-source multi\-threaded benchmarking tool. It can simulate database business workloads and evaluate the performance of systems and databases under different configurations and parameters via metrics such as throughput, event rate and latency.

<span id=".5a6J6KOF5L6d6LWW5YyF"></span>
### Installing dependency packages

```Bash
yum -y install make automake libtool pkgconfig libaio-devel mariadb-devel openssl-devel
```


<span id=".5rWL6K-V5bel5YW35LiL6L29"></span>
### Downloading the test tool

Sysbench GitHub link: [Sysbench github](https://github.com/akopytov/sysbench).

This topic uses Sysbench version 1.0.20 as an example.

```Bash
# Use wget to obtain the compressed package of version 1.0.20.
wget https://codeload.github.com/akopytov/sysbench/tar.gz/1.0.20
# Decompress the package
tar -xzvf 1.0.20
```


<span id=".5rWL6K-V5bel5YW35a6J6KOF"></span>
### Installing the test tool

```Bash
# Go to the installation directory after decompression
cd sysbench-1.0.20
# Run the autogen.sh script to generate the configure script
./autogen.sh
# Run the configure script to check the System configuration
./configure
# Compile the code
make -j
# Install the compiled files
make install
# Check if the installed Version is correct
sysbench --version
```
