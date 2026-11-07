---
title: "FAQ about using the command line for Base64 encoding"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/FAQs-about-using-the-command-line-for-base64-encoding"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

When you use Linux command\-line tools on macOS to Base64\-encode username and password, the system automatically adds a newline character `(\n)` at the end. If you directly use Base64\-encoded content, the program or business may fail to run.

<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution

If you need to Base64\-encode passwords and similar data by using Linux command\-line tools, we recommend that you use the following command:

```bash
echo -n ${your_password} | base64
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Replace <code>${your_password}</code> with your actual password. For example: <code>echo -n password123 | base64</code>.</div>
