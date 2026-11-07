---
title: "FAQ"
product: "Terraform"
product_code: "tf"
section: "Document"
source: "https://docs.byteplus.com/en/docs/tf/FAQs"
---

<span id=".5aaC5L2V5p-l55yLVGVycmFmb3Jt55qE6K-m57uG5pel5b-X77yf"></span>
## How do I view detailed Terraform logs?

Add the `TF_LOG` and `TF_LOG_PATH` environment variables in your operating system. For example, you must run the following commands for the Linux operating system:

```Plain Text
export TF_LOG=TRACE
export TF_LOG_PATH=/var/log/terraform.log
```


<span id=".5aaC5L2V5pu05pawcHJvdmlkZXLniYjmnKzvvJ8="></span>
## How do I upgrade a provider version?

Execute the following command in the working directory to upgrade:

`terraform init -upgrade=true`

<span id=".5aaC5L2V6Ieq5Yqo6KGl5YWodGVycmFmb3Jt5ZG95Luk77yf"></span>
## How do I enable autocompletion for Terraform commands?

Currently, only bash and zsh are supported. After executing the following commands and restarting the session, autocompletion will be enabled:

`terraform -install-autocomplete`
