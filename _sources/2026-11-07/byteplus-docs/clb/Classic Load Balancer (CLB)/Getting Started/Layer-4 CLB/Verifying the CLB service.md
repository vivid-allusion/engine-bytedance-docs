---
title: "Verifying the CLB service"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Layer-4-CLB-05"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

This topic introduces how to verify that the layer 4 Classic Load Balancer (CLB) service can provide service normally.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. View and record the EIP of the CLB instance on the CLB Instances page.

2. Use a local browser to visit `http://EIP of the CLB instance:listening port`. If the backend service page deployed on the backend server is displayed, it means the layer 4 CLB should forward the access request to the backend server for processing properly.
