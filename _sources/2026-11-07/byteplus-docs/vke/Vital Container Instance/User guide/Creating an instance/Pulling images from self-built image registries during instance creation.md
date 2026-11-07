---
title: "Pulling images from self-built image registries during instance creation"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Pull_images_from_a_self-hosted_Container_Registry_when_creating_an_instance"
---

VCI allows you to pull images from self\-built image registries. When you pull images from a self\-built image registry, image pulling may fail due to protocol differences or certificate verification failures. This topic describes how to create VCIs or image caches by pulling images from a self\-built image registry when the self\-built image registry uses HTTP and self\-signed certificates.

<span id="SNUmGTxM"></span>
## Feature description

VCI supports self\-built image registries in the following scenarios:


* Pull images (including using image caches) during the creation of instances.

* Create image caches.


VCI allows you to pull images from self\-built image registries by using annotations. The following table describes annotations. For more information about VCI annotations, see [Pod annotation descriptions](https://docs.byteplus.com/en/docs/vke/VCI-Pod-annotations).


|Annotation key |Annotation sample value |Description |Required |
|---|---|---|---|
|vci.volcengine.com/insecure\-registries |"registry1,registry:5000,registry:80" |When you pull images from an image registry that uses a self\-signed certificate, certificate verification fails, which results in image pull failure. You can skip TLS authentication to resolve this issue.<br><br>Separate multiple image registries by commas (`,`). If the address of the image registry contains a port number, you also need to enter the port number. |no |
|vci.volcengine.com/plain\-http\-registries |"registry1\-http,registry\-http:5000,registry\-http:80" |Specify HTTP\-accessible image registries, separated by commas (,).  If the image registry address includes a port number, enter the port number as well. |no |


<span id="TMzO5bY7"></span>
## Usage limits


* You can use this method only by using YAML instead of the console.

* Image caches can only be created automatically or manually, not via the CRD method. For details about image caches, see [VCI image caches](https://docs.byteplus.com/en/docs/vke/VCI-Image-Cache).


<span id="TMzO5bY7"></span>
## Procedure

The following sample code shows how to create a Deployment. For detailed instructions, see [Creating general-purpose instances by specifying container vCPUs and memory](https://docs.byteplus.com/en/docs/vke/Creating-a-general-purpose-instance-based-on-specified-container-vCPUs-and-memory). For more information about creating VCIs, see [Creating instances](https://docs.byteplus.com/en/docs/vke/Creating-an-instance).

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      annotations:
        vke.volcengine.com/burst-to-vci: enforce  # Force the use of VCI.
        vke.volcengine.com/preferred-subnet-ids: subnet-3tispp1nai**** # Specify the ID of a subnet. You can specify multiple subnets within the same availability zone. To do so, separate them with commas (,).
        vci.vke.volcengine.com/preferred-instance-family: vci.u1 # Specify the instance family of VCI.
        "vci.volcengine.com/insecure-registries": "registry1,registry:5000,registry:80" # Specify image registries that skip TLS authentication and separate multiple image registries by commas (,).
        "vci.volcengine.com/plain-http-registries": "registry1-http,registry-http:5000,registry-http:80" # Specify image registries that are accessed via HTTP and separate multiple image registries by commas (,).
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: example.com/namespace/repository1:v1 # The address of your self-built image registry. If you need to use a public image, make sure that the cluster can access the public network.
        ports:
        - containerPort: 80
        resources:
          requests:  # Specify the container CPU and memory.
            cpu: "500m"      
            memory: "1024Mi"
          limits:
            cpu: "1"      
            memory: "2048Mi"
```


&nbsp;
