---
title: "How do I avoid pulling images after using an image cache?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-do-I-avoid-pulling-images-after-using-an-image-cache"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Problem description

After an image cache is used, you may still encounter situations where image pulling is required due to the following reasons:


* The image cache matches based on image tags. If you re\-push an image with the same tag after creating the image cache, image pulling may be triggered.

* You are using the image cache by specifying its ID, but some pod images are not included in the image cache.

* You specify `ImagePullPolicy: Always`. In this case, even if the image is not updated, the system still needs to access the image repository to retrieve metadata such as the image `manifest`.


<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution

If you need to avoid accessing the image repository (for example, the image has been deleted or network issues prevent connection to the repository), you can set `ImagePullPolicy` to `IfNotPresent` or `Never`, and disable the `AlwaysPullImages` admission controller of the cluster. For detailed steps, see the following:


* [AlwaysPullImages](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#alwayspullimages)

* [Image pull policy](https://kubernetes.io/docs/concepts/containers/images/#image-pull-policy)
