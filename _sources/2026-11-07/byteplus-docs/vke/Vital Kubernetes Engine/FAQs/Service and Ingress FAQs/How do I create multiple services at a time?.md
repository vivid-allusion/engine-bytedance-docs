---
title: "How do I create multiple services at a time?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-do-I-create-Services-in-batches"
---

In cluster migration scenarios, you may need to quickly migrate services that have already been created in an existing cluster to a new cluster. You can complete this by following these steps:


1. Export the YAML files of all services in the existing cluster and save them in the same local directory.

2. Use kubectl to connect to the new cluster.

3. Go to the directory mentioned above and run the following command to create multiple services at a time.

   ```bash
   kubectl apply -f .
   ```
