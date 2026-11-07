---
title: "Container storage"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-container-storage-correctly"
---

This topic describes considerations, configuration recommendations, and best practices for using container storage resources in VKE, including PersistentVolume (PV), PersistentVolumeClaim (PVC), and StorageClass (SC).

<span id=".5oyC6L295a-56LGh5a2Y5YKoLXB2LeeahOadg-mZkOivtOaYjg=="></span>
## Permission details for mounting TOS PVs

Mounting TOS PVs in Linux requires root access by default. To allow users with other permissions than root permissions to modify TOS PV configuration, you can add the `additional_args` field in the static TOS PVs, as in the `additional_args: "-o allow_other"` example. The following code provides a complete example of a PV configuration:

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-tos
spec:
  accessModes:
    - ReadWriteMany
  capacity:
    storage: 1Gi
  csi:
    driver: tos.csi.volcengine.com
    volumeHandle: pv-tos
    volumeAttributes:
      # Replaced by the url of your region.
      url: "http://tos-s3-cn-beijing.volces.com"
      # Replaced by the bucket name you want to use.
      bucket: "csi-test"
      # Replaced by the subPath in bucket you want to use.
      path: /test
      # You can specify any other options used by the s3fs command in here.
      additional_args: "-o allow_other"
    nodePublishSecretRef:
      # Replaced by the name and namespace of your secret.
      name: tos-secret
      namespace: kube-system
```
