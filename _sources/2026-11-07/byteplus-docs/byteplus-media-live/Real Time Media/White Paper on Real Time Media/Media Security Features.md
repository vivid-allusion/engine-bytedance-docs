---
title: "Media Security Features"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-media-security-features"
---

<span id="3eed6a91"></span>
## DTLS/SRTP/SRTCP encryption and decryption switch control

DTLS/SRTP/SRTCP encryption is determined by `<proto>` on the `m=` line in the SDP.


* When `<proto>` is `SAVPF`, it indicates encryption;

* When `<proto>` is `AVPF`, it indicates no encryption.


<span id="7ecbe474"></span>
### Sample SDP encryption

```Plain
m=audio 9 UDP/TLS/RTP/SAVPF 111 103
m=video 9 UDP/TLS/RTP/SAVPF 96 97
a=fingerprint:sha-256 92:4D:B6:E3:6A:17:8A:48:B2:9D:D4:D5:F1:1F:AE:9B:31:9D:98:0F:72:99:53:78:38:8F:09:81:65:62:DC:68
......
```


`<proto>` `UDP/TLS` specifies the use of DTLS for key exchange.

<span id="1aea6802"></span>
### Sample non\-encrypted SDP

There are no `a=fingerprint:sha-256` line markers in unencrypted SDP text.

```Plain
m=video 1  RTP/AVPF 102 125
m=audio 9  RTP/AVPF 96 103
.......
```
