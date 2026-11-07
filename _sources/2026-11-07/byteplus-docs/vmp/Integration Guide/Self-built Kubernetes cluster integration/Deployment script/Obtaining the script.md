---
title: "Obtaining the script"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Obtaining-a-script"
---

You can deploy collectors, Grafana, and exporters by using the deployment script. This topic describes how to obtain the deployment script.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* To obtain and use the script, you need to use wget, echo, curl, and sed in your local environment (Linux/Mac). Make sure that these command\-line tools are installed on your system.

* Your local environment (Linux/Mac) can access the Internet.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

Run the following command in your local environment (Linux/Mac) to obtain the installation script and grant executable permissions:

```bash
wget https://vmp-release-cn-beijing.tos-cn-beijing.volces.com/shell/install.sh && chmod +x install.sh
```
