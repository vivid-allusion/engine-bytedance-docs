---
title: "Thread Synchronization"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-thread-synchronization"
---

<span id="Special Effect Version"></span>
## Special Effects

For functions related to image special effects, such as face beautification, filters, makeup, and stickers, the entire life cycle—including initialization, special effects processing and destruction—must be performed in the GL thread, because special effects rendering depends on the OpenGL context.

<span id="Basic Algorithm Version"></span>
## Basic Algorithm

Basic algorithm functions, such as portrait detection, gesture detection, body keypoints, segmentation, and portrait comparison do not depend on the OpenGL context, so they are not required to be executed in the GL thread. However, to ensure data synchronization, the entire life cycle of each algorithm—including initialization, detection, and destruction—must be in the same thread.
