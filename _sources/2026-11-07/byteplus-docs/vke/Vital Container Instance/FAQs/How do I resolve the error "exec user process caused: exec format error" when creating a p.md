---
title: "How do I resolve the error \"exec user process caused: exec format error\" when creating a pod?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-do-I-resolve-the-error-exec-format-error-when-creating-a-pod"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Problem description

The following error occurs during pod creation: `exec user process caused: exec format error`.

<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution

VCI supports images with the AMD64 architecture. If you use an image with the ARM architecture, this error will occur. Switch to an image built for the architecture​.
