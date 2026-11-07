---
title: "How do I fix image push failures?"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/What-do-I-do-when-I-fail-to-push-an-image"
---

Use different solutions for different error messages.

* If the error message is **unauthorized: unauthorized to access repository**:

   Your account may not have permission to push images to the CR instance or namespace. Contact your business administrators first and ask them to grant the required permissions. After the permissions are granted, try docker push again.

* Check the network connection and ensure network access is normal.
