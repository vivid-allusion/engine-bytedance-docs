---
title: "How do I modify the TOS mount configuration to grant others read and write access to TOS PersistentVolumes?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How_to_modify_the_mount_configuration_of_TOS"
---

TOS is mounted with Linux root privileges by default. You can modify the mount configuration to allow other users to read from and write to TOS PersistentVolumes. To do so, add the` additional_args` field to the static TOS PersistentVolume.

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

The Deployment failed to mount TOS, with an error message indicating a mount failure and a mount device failure.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

TOS is mounted using Linux root privileges by default. The s3fs client cannot directly use the chown command to assign user permissions to the TOS mount point.  Therefore, other users do not have read\-write permissions for TOS PersistentVolumes.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

You can modify the mount configuration to grant other users read and write access to the TOS PersistentVolume by adding the `additional_args` field to the static TOS PersistentVolume. The format for adding the configuration is `additional_args: "-o allow_other -oumask=000"`. The following YAML manifest provides an example PersistentVolume configuration:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">When adding the <code>additional_args</code> field to a static TOS PersistentVolume configuration, note the following:</div>



* <div data-tips="true" data-tips-type="warning">The PersistentVolume must remain unbound to have this field added. The field configuration grants other users read and write access to the TOS PersistentVolume.</div>


* <div data-tips="true" data-tips-type="warning">If the PersistentVolume has already been bound, you must unbind it and delete any remaining <code>spec.claimRef</code> settings before adding this field. Otherwise, the field configuration will not take effect.</div>



```Yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: "pv-tos"
spec:
  accessModes:
    - ReadWriteMany
  capacity:
    storage: 1Gi
  csi:
    driver: tos.csi.volcengine.com
    volumeHandle: pv-tos
    volumeAttributes:
      url: "http://tos-s3-cn-beijing.volces.com"
      bucket: "csi-test"
      path: /test
      additional_args: "-o allow_other -oumask=000" # The additional_args field used to grant other users read and write access to TOS PersistentVolumes.
    nodePublishSecretRef:
      name: tos-secret
      namespace: kube-system
```
