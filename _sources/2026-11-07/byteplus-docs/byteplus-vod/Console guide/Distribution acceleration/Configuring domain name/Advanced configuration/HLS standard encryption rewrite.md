---
title: "HLS standard encryption rewrite"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/hls_standard_encryption_rewrite"
---

The **HLS standard encryption rewrite** feature secures your video assets by dynamically modifying HLS (HTTP Live Streaming) M3U8 manifest files. When enabled, it injects encryption parameters (including the method, key URI, and an authentication token) into the `#EXT-X-KEY` tag of the manifest before it's delivered to the client.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The <strong>HLS standard encryption rewrite</strong> feature applies to <strong>Playback domain</strong> <strong>name</strong>.</div>


<span id="9f49ac05"></span>
## Background Information

HLS (HTTP Live Streaming) is an adaptive bitrate streaming protocol developed by Apple. It operates over HTTP, allowing clients to download a sequence of small video files from a web server. In HLS, the video content is encapsulated in Transport Stream (TS) files. A separate M3U8 manifest file, which is a plain text playlist, controls the playback. The core principle of HLS is to break a continuous video stream into small, downloadable TS file chunks. When a streaming session begins, the client first downloads the M3U8 playlist, which contains the URLs for the individual TS segments, and then proceeds to download them in sequence.

**Common HLS tags:** 


* `#EXTM3U`: The M3U8 file header, which must be the first line of the file.

* `#EXT-X-MEDIA-SEQUENCE`: The sequence number of the first TS segment in the playlist.

* `#EXT-X-TARGETDURATION`: The maximum duration (in seconds) of any media segment in the playlist.

* `#EXT-X-ALLOW-CACHE`: Specifies whether the client is allowed to cache the downloaded segments.

* `#EXT-X-ENDLIST`: Indicates that no more media segments will be added to the playlist file.

* `#EXTINF`: Provides metadata for each media segment, such as its duration. The format is typically `#EXTINF:<duration>,[<title>]`.

* `#EXT-X-VERSION`: The compatibility version number of the M3U8 file.

* `#EXT-X-DISCONTINUITY`: Indicates a discontinuity between the preceding and following media segments.

* `#EXT-X-PLAYLIST-TYPE`: Specifies the type of playlist (e.g., VOD or LIVE).

* `#EXT-X-KEY`: Defines how to decrypt the media segments. For example, `#EXT-X-KEY:METHOD=AES-128,URI="https://example.com/video.key?token=xxx"` specifies that the segments are encrypted with AES\-128 and the key can be fetched from the provided URI. The fetched key is then used to decrypt all subsequent TS files. This is the tag that the HLS Encryption Rewrite feature modifies.


<span id="c4d048d0"></span>
## Technical workflow

The following steps outline the request and decryption flow when this feature is enabled:


1. A client player sends a request for an M3U8 file to a CDN edge node, including an authentication token. Example: `http://example.com/media/index.m3u8?DrmAuthToken=xxx`.

2. The CDN edge node validates the authentication token in the client's request.

3. Upon successful validation, the CDN edge node fetches the original M3U8 file from the origin server and caches it.

4. The CDN edge node rewrites the `#EXT-X-KEY` tag in the M3U8 file, injecting the encryption method, key URI, and appending the authentication token from the initial request. For example: `#EXT-X-KEY:METHOD=AES-128,URI="https://example.com/video.key?DrmAuthToken=xxx"`.

5. The CDN edge node returns the modified M3U8 file to the client.

6. The client parses the modified M3U8 file, extracts the key URI, and sends a request to this URI to fetch the decryption key.

7. The CDN edge node receives the key request, validates the token again, and returns the decryption key to the client.

8. The client proceeds to download the TS video segments listed in the M3U8 file from the CDN.

9. The client uses the fetched key and the specified encryption algorithm to decrypt the TS segments for playback.


<span id="4cad0ff7"></span>
## Configuring HLS standard encryption rewrite


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Distribution acceleration** \> **Domain names** on the left navigation bar.

3. Depending on the type of your domain name, click the **Playback domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **Advanced configuration** tab.

6. Click the **Modify** button at the bottom of the page.

7. Under **HLS standard encryption rewrite**, set **Status** to **Enabled**.

8. (Optional) The default parameter name for the authentication token is `DrmAuthToken`. You can customize this name. Note that the parameter is **case\-sensitive**. Ensure the name configured here exactly matches the parameter name sent in the client's request. For example, if the client sends a `foobar` parameter but the console is configured with `FooBar`, the rewrite will not take effect.

9. Click **Save**.
