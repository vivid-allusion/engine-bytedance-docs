---
title: "NLESDK overview"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-nlesdk-overview"
---

The BytePlus Video Editor SDK is not just one SDK; it's a collection of different SDKs. The choice of which sub\-SDKs to include in your project depends on what you need and what features you've purchased.

For example:


* If you only want features related to **shooting**, you should use the Effect SDK and VESDK.

* If you need both **shooting** and **editing** features, then you should use the Effect SDK, VESDK, and NLESDK.


<span id="90eb90dc"></span>
# What is NLE?

Non\-Linear Editing (NLE) is a method for editing video or audio. NLESDK is implemented in a data\-driven manner for audio and video editing. The SDK primarily exposes interfaces through three main components: NLEModel, NLEEditor, and NLEMediaSessionPublic (known as NLEInterface on iOS).


* NLEModel is a data class where all audio and video clip data is stored. In normal circumstances, knowing the data within this class is sufficient to recreate the entire video.

* NLEEditor can be understood as a project for editing. Its core interfaces provided to the outside world include data submission (commit, done), data storage (store), undo, redo, and others.

* NLEMediaSessionPublic (NLEInterface on iOS) exposes all APIs related to audio and video reconstruction. This includes control of playback during video editing previews and interfaces for merging and exporting edited videos.
