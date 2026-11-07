---
title: "How do I fix slow public network image pushes caused by proxy settings?"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/What-do-I-do-when-image-pushes-over-the-internet-are-slow-after-I-configure-a-proxy"
---

## Issue description:

After a proxy is configured on the client, image pushes to Trial Edition and Enterprise Edition instances over the public network may become slower.

## Solution:

Check where the network proxy is configured. Try removing the proxy configuration and pushing the image again. Then verify whether the issue is caused by the proxy settings. Use the following methods to check whether a network proxy is configured.

### Docker

* Check whether a network proxy is configured for the Docker client.

   `cat ~/.docker/config.json`

* Check whether a network proxy is configured for the Docker service.

   `cat {Docker Service configuration path}`

   > **tip**

   > You can get the Docker service configuration path by running `systemctl status docker`.

* Check whether a network proxy is configured in the `http-proxy.conf` file.

   `cat /etc/systemd/system/containerd.service.d/http-proxy.conf`

### Containerd

* Check whether a network proxy is configured for the Containerd service.

   `cat {Container Service configuration path}`

   > **tip**

   > You can get the Containerd service configuration path by running `systemctl status containerd`.

* Check whether a network proxy is configured in the `http-proxy.conf` file.

   `cat /etc/systemd/system/containerd.service.d/http-proxy.conf`
