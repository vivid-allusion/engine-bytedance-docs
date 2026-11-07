---
title: "SDP示例"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rtm-SDP-example-zh-CN"
---

<span id="51a42d7d"></span>
## SDP发起

```Plain
v=0
o=- 1933070330123933231 2 IN IP4 127.0.0.1
s=-
t=0 0
a=pli-relay
a=group:BUNDLE audio video
a=msid-semantic: WMS ff6d570f-8964-4e32-a6fc-282b9678efc0
m=audio 9 RTP/AVPF 111 114 115 116 8 117 0 118 119 120 121
c=IN IP4 0.0.0.0
a=rtcp:9 IN IP4 0.0.0.0
a=ice-ufrag:C8jR
a=ice-pwd:IBkzSrk9J6v****QWQaSoGYn
a=ice-options:trickle renomination
a=mid:audio
a=extmap:1 urn:ietf:params:rtp-hdrext:ssrc-audio-level
a=sendrecv
a=rtcp-mux
a=rtpmap:111 opus/48000/2
a=rtcp-fb:111 rrtr
a=rtcp-fb:111 transport-cc
a=rtcp-fb:111 nack
a=fmtp:111 minptime=10;useinbandfec=1
a=rtpmap:114 rtx/48000/2
a=fmtp:114 apt=111
a=rtpmap:115 opus/16000
a=rtcp-fb:115 rrtr
a=rtcp-fb:115 transport-cc
a=rtcp-fb:115 nack
a=fmtp:115 minptime=10;useinbandfec=1
a=rtpmap:116 rtx/16000
a=fmtp:116 apt=115
a=rtpmap:8 PCMA/8000
a=rtcp-fb:8 rrtr
a=rtcp-fb:8 transport-cc
a=rtcp-fb:8 nack
a=rtpmap:117 rtx/8000
a=fmtp:117 apt=8
a=rtpmap:0 PCMU/8000
a=rtcp-fb:0 rrtr
a=rtcp-fb:0 transport-cc
a=rtcp-fb:0 nack
a=rtpmap:118 rtx/8000
a=fmtp:118 apt=0
a=rtpmap:119 bdfec/48000/2
a=rtpmap:120 red/48000/2
a=rtpmap:121 rtx/48000/2
a=fmtp:121 apt=120
a=ssrc-group:FID 91054504 2287352107
a=ssrc:91054504 cname:+7O0EaAUNid/TJH/
a=ssrc:91054504 msid:ff6d570f-8964-4e32-a6fc-282b9678efc0 ff6d570f-8964-4e32-a6fc-282b9678efc0a0
a=ssrc:91054504 mslabel:ff6d570f-8964-4e32-a6fc-282b9678efc0
a=ssrc:91054504 label:ff6d570f-8964-4e32-a6fc-282b9678efc0a0
a=ssrc:2287352107 cname:+7O0EaAUNid/TJH/
a=ssrc:2287352107 msid:ff6d570f-8964-4e32-a6fc-282b9678efc0 ff6d570f-8964-4e32-a6fc-282b9678efc0a0
a=ssrc:2287352107 mslabel:ff6d570f-8964-4e32-a6fc-282b9678efc0
a=ssrc:2287352107 label:ff6d570f-8964-4e32-a6fc-282b9678efc0a0
m=video 9 RTP/AVPF 96 97 98 99 101 102 103
c=IN IP4 0.0.0.0
a=rtcp:9 IN IP4 0.0.0.0
a=ice-ufrag:C8jR
a=ice-pwd:IBkzSrk9J6v****QWQaSoGYn
a=ice-options:trickle renomination
a=mid:video
a=extmap:2 urn:ietf:params:rtp-hdrext:toffset
a=extmap:3 http://www.webrtc.org/experiments/rtp-hdrext/abs-send-time
a=extmap:4 urn:3gpp:video-orientation
a=extmap:5 http://www.ietf.org/id/draft-holmer-rmcat-transport-wide-cc-extensions-01
a=extmap:6 http://www.webrtc.org/experiments/rtp-hdrext/playout-delay
a=extmap:7 http://www.webrtc.org/experiments/rtp-hdrext/video-content-type
a=extmap:8 http://www.webrtc.org/experiments/rtp-hdrext/video-timing
a=extmap:10 http://tools.ietf.org/html/draft-ietf-avtext-framemarking-07
a=extmap:12 http://www.webrtc.org/experiments/rtp-hdrext/color-space
a=sendrecv
a=rtcp-mux
a=rtcp-rsize
a=rtpmap:96 H264/90000
a=rtcp-fb:96 goog-remb
a=rtcp-fb:96 transport-cc
a=rtcp-fb:96 ccm fir
a=rtcp-fb:96 nack
a=rtcp-fb:96 nack pli
a=rtcp-fb:96 rrtr
a=fmtp:96 level-asymmetry-allowed=1;packetization-mode=1;profile-level-id=42e01f
a=rtpmap:97 rtx/90000
a=fmtp:97 apt=96;packetization-mode=1
a=rtpmap:98 H265/90000
a=rtcp-fb:98 goog-remb
a=rtcp-fb:98 transport-cc
a=rtcp-fb:98 ccm fir
a=rtcp-fb:98 nack
a=rtcp-fb:98 nack pli
a=rtcp-fb:98 rrtr
a=rtpmap:99 rtx/90000
a=fmtp:99 apt=98;packetization-mode=1
a=rtpmap:101 red/90000
a=fmtp:101 packetization-mode=1
a=rtpmap:102 rtx/90000
a=fmtp:102 apt=101;packetization-mode=1
a=rtpmap:103 bdfec/90000
a=fmtp:103 packetization-mode=1
a=ssrc-group:SIM 1211486230 1342709036 2464424174
a=ssrc-group:FID 1211486230 1366852466
a=ssrc-group:FID 1342709036 665872642
a=ssrc-group:FID 2464424174 2118976071
a=ssrc:1211486230 cname:+7O0EaAUNid/TJH/
a=ssrc:1211486230 msid:ff6d570f-8964-4e32-a6fc-282b9678efc0 ff6d570f-8964-4e32-a6fc-282b9678efc0v0
a=ssrc:1211486230 mslabel:ff6d570f-8964-4e32-a6fc-282b9678efc0
a=ssrc:1211486230 label:ff6d570f-8964-4e32-a6fc-282b9678efc0v0
a=ssrc:1342709036 cname:+7O0EaAUNid/TJH/
a=ssrc:1342709036 msid:ff6d570f-8964-4e32-a6fc-282b9678efc0 ff6d570f-8964-4e32-a6fc-282b9678efc0v0
a=ssrc:1342709036 mslabel:ff6d570f-8964-4e32-a6fc-282b9678efc0
a=ssrc:1342709036 label:ff6d570f-8964-4e32-a6fc-282b9678efc0v0
a=ssrc:2464424174 cname:+7O0EaAUNid/TJH/
a=ssrc:2464424174 msid:ff6d570f-8964-4e32-a6fc-282b9678efc0 ff6d570f-8964-4e32-a6fc-282b9678efc0v0
a=ssrc:2464424174 mslabel:ff6d570f-8964-4e32-a6fc-282b9678efc0
a=ssrc:2464424174 label:ff6d570f-8964-4e32-a6fc-282b9678efc0v0
a=ssrc:1366852466 cname:+7O0EaAUNid/TJH/
a=ssrc:1366852466 msid:ff6d570f-8964-4e32-a6fc-282b9678efc0 ff6d570f-8964-4e32-a6fc-282b9678efc0v0
a=ssrc:1366852466 mslabel:ff6d570f-8964-4e32-a6fc-282b9678efc0
a=ssrc:1366852466 label:ff6d570f-8964-4e32-a6fc-282b9678efc0v0
a=ssrc:665872642 cname:+7O0EaAUNid/TJH/
a=ssrc:665872642 msid:ff6d570f-8964-4e32-a6fc-282b9678efc0 ff6d570f-8964-4e32-a6fc-282b9678efc0v0
a=ssrc:665872642 mslabel:ff6d570f-8964-4e32-a6fc-282b9678efc0
a=ssrc:665872642 label:ff6d570f-8964-4e32-a6fc-282b9678efc0v0
a=ssrc:2118976071 cname:+7O0EaAUNid/TJH/
a=ssrc:2118976071 msid:ff6d570f-8964-4e32-a6fc-282b9678efc0 ff6d570f-8964-4e32-a6fc-282b9678efc0v0
a=ssrc:2118976071 mslabel:ff6d570f-8964-4e32-a6fc-282b9678efc0
a=ssrc:2118976071 label:ff6d570f-8964-4e32-a6fc-282b9678efc0v0
a=bdfec-type:rsfec
a=rsfec-version:1
```


<span id="3038f6a4"></span>
## SDP应答

```Plain
o=- 0 0 IN IP4 127.0.0.1
s=parker
t=0 0
a=pli-relay
a=group:BUNDLE audio video
a=msid-semantic: WMS
a=bdfec-type:rsfec
m=audio 1 RTP/AVPF 111 114 119 120 121
c=IN IP4 0.0.0.0
a=rtcp:1 IN IP4 0.0.0.0
a=candidate:0 1 tcp 1526726655 192.0.2.1 8108 typ host tcptype passive generation 0
a=candidate:1 1 udp 2130706431 192.0.2.1 50001 typ host generation 0
a=candidate:2 1 udp 2130706431 192.0.2.1 50000 typ host generation 0
a=ice-ufrag:HYnbBcITqqadiFhC
a=ice-pwd:twilEHmwQgJLv****GbyrCbeSHPgieHj
a=ice-options:trickle renomination
a=setup:active
a=sendrecv
a=extmap:1 urn:ietf:params:rtp-hdrext:ssrc-audio-level
a=mid:audio
a=rtcp-mux
a=rtpmap:111 opus/48000/2
a=rtcp-fb:111 rrtr
a=rtcp-fb:111 nack
a=fmtp:111 minptime=10;useinbandfec=1
a=rtpmap:114 rtx/48000/2
a=fmtp:114 apt=111
a=rtpmap:119 bdfec/48000/2
a=rtpmap:120 red/48000/2
a=rtpmap:121 rtx/48000/2
a=fmtp:121 apt=120
m=video 1 RTP/AVPF 96 97 101 102 103
c=IN IP4 0.0.0.0
a=rtcp:1 IN IP4 0.0.0.0
a=candidate:0 1 tcp 1526726655 192.0.2.1 8108 typ host tcptype passive generation 0
a=candidate:1 1 udp 2130706431 192.0.2.1 50001 typ host generation 0
a=candidate:2 1 udp 2130706431 192.0.2.1 50000 typ host generation 0
a=ice-ufrag:HYnbBcITqqadiFhC
a=ice-pwd:twilEHmwQgJLv****GbyrCbeSHPgieHj
a=ice-options:trickle renomination
a=setup:active
a=sendrecv
a=extmap:2 urn:ietf:params:rtp-hdrext:toffset
a=extmap:3 http://www.webrtc.org/experiments/rtp-hdrext/abs-send-time
a=extmap:4 urn:3gpp:video-orientation
a=extmap:5 http://www.ietf.org/id/draft-holmer-rmcat-transport-wide-cc-extensions-01
a=extmap:6 http://www.webrtc.org/experiments/rtp-hdrext/playout-delay
a=extmap:10 http://tools.ietf.org/html/draft-ietf-avtext-framemarking-07
a=mid:video
a=rtcp-mux
a=rtpmap:96 H264/90000
a=rtcp-fb:96 goog-remb
a=rtcp-fb:96 transport-cc
a=rtcp-fb:96 ccm fir
a=rtcp-fb:96 nack
a=rtcp-fb:96 nack pli
a=rtcp-fb:96 rrtr
a=fmtp:96 level-asymmetry-allowed=1;packetization-mode=1;profile-level-id=42e01f
a=rtpmap:97 rtx/90000
a=fmtp:97 apt=96;packetization-mode=1
a=rtpmap:101 red/90000
a=fmtp:101 packetization-mode=1
a=rtpmap:102 rtx/90000
a=fmtp:102 apt=101;packetization-mode=1
a=rtpmap:103 bdfec/90000
a=fmtp:103 packetization-mode=1
```
