---
title: "AI Dubbing"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/ai-liveinterpret-simultaneous-audio-and-video-interpretation"
---

The AI Dubbing feature integrates advanced technologies such as the Doubao simultaneous interpretation model, multilingual subtitles, voice cloning, and lip sync. This feature can process the human voice in your live stream audio into multilingual content, effectively enhancing the audience's viewing experience in noisy or muted environments, or in cross\-language scenarios, and helping your content reach a broader global audience. This topic describes how to use the AI Dubbing feature through the BytePlus MediaLive console.

## Architecture

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90b1efb646914de0a42c64fd86b75a19~tplv-goo7wpa0wc-topic.webp)

This architecture diagram shows the overall processing flow of AI Dubbing in stream push scenarios, mainly including the following stages:

1. **Audio source separation**: Extracts human voice and background sound from the live stream to provide clean audio for subsequent processing.

2. **Speech recognition and translation**: Uses the Doubao simultaneous interpretation model to recognize human voice content and generate multilingual subtitles.

3. **Voice cloning**: The dubbed audio retains the original voice timbre, optimizes volume, and performs noise reduction.

4. **Lip sync**: Adjusts the speaker's lip movements in real time and synchronizes them with the dubbed audio, achieving a highly realistic effect.

5. **Audio fusion**: Naturally blends the cloned human voice with background sound to improve the overall audio quality.

6. **Audio and video synthesis**: Combines the processed audio and subtitles to generate the final output, achieving a natural multilingual live stream effect.

## Highlights

* **Immersive experience**: Combines voice cloning and lip\-sync technologies to deliver realistic dubbing and facial movements, significantly enhancing the naturalness of the video.

* **Low latency**: Adapted for live streaming scenarios, providing an end\-to\-end low\-latency experience.

* **Flexible usage methods**: Select the appropriate features based on your scenario.

   |Scenario |Recommended features |Mode selection |Description |
   |---|---|---|---|
   |Provide basic subtitles for the live stream, making it convenient to watch in muted or noisy environments. |Original ASR subtitles |**Original (ASR) Subtitles** |Overlay source subtitles over the video using speech recognition. |
   |Enable cross\-language text communication to reach a global audience. |Subtitle translation |**AI Dubbing** or **Real\-Time Interpretation** |Overlay translated subtitles over the video using speech recognition, while retaining the original sound. |
   |Provide a dubbing\-style translation experience, similar to watching a dubbed film. |Dubbed audio |**AI Dubbing** or **Real\-Time Interpretation** |Provide dubbed audio and replace the original sound. In **Real\-Time Interpretation** mode, you can choose to overlay the dubbed audio on the original sound or directly replace the original sound. |
   |Provide an immersive human interpreter experience to enhance professionalism. |Dubbed audio + lip sync |**AI Dubbing** |Based on dubbed audio, AI technology synchronizes the speaker's lip movements with the dubbed audio, creating a highly realistic effect. |

## Scenarios

* **Barrier\-free viewing**

   Generate source subtitles for people with hearing impairments, supporting accessible viewing experiences in silent environments such as offices and libraries, as well as in noisy environments such as subways and shopping malls.

* **Cross\-border business and global communication**

   Applicable to various scenarios such as cross\-border e\-commerce livestreams, product launches, international conferences, educational training, and speeches by non\-native speakers, facilitating cross\-language communication and market expansion.

* **Entertainment and sports**

   Supports overseas event broadcasting and domestic event internationalization to meet real\-time streaming needs and promote global distribution of event content.

## Billing

Only AI Dubbing fees are charged. AI Dubbing is billed based on the **actual stream push duration** of the task. For more information, see [AI Dubbing](https://docs.byteplus.com/docs/byteplus-media-live/ai_dubbing).

> **Warning**

> You can only experience the **Demo video** for free. Other demo methods will incur corresponding fees.

## Workflow

The complete workflow of AI Dubbing is as follows. There are two types of addresses involved:

* BytePlus MediaLive address: Refers to the address whose domain name has been bound to your current account.

* Third\-party platform address: Refers to the address from other cloud providers or live platforms such as TikTok.

![](data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSIxMzg1cHgiIGhlaWdodD0iMjQ1cHgiIHZpZXdCb3g9Ii0wLjUgLTAuNSAxMzg1IDI0NSI+PGRlZnMvPjxnPjxyZWN0IHg9IjIiIHk9IjIiIHdpZHRoPSIyNzUiIGhlaWdodD0iMjQwIiByeD0iMzYiIHJ5PSIzNiIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMzIiIHk9IjYyIiB3aWR0aD0iMjIwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIxOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDkycHg7IG1hcmdpbi1sZWZ0OiAzM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Zm9udCBzdHlsZT0iZm9udC1zaXplOjIwcHgiPlRoaXJkLXBhcnR5IHBsYXRmb3JtIHB1bGwgc3RyZWFtIGFkZHJlc3M8L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIzMiIgeT0iMTYyIiB3aWR0aD0iMjIwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIxOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE5MnB4OyBtYXJnaW4tbGVmdDogMzNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGZvbnQgc3R5bGU9ImZvbnQtc2l6ZToyMHB4Ij5CeXRlUGx1cyBNZWRpYUxpdmUgcHVsbMKgc3RyZWFtIGFkZHJlc3M8L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIzMiIgeT0iMjIiIHdpZHRoPSIyMjAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIxOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiAzM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2Pjxmb250IHN0eWxlPSJmb250LXNpemU6MTlweCI+UHVsbCBzdHJlYW0gYWRkcmVzczwvZm9udD48L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNDQyIDEzMiBMIDI4OC4zNyAxMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyODMuMTIgMTMyIEwgMjkwLjEyIDEyOC41IEwgMjg4LjM3IDEzMiBMIDI5MC4xMiAxMzUuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNTcyIDEzMiBMIDY1MiAxMzIgTCA2NTIgMTMyLjYgTCA3MTkuNTQgMTMyLjU2IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzI0Ljc5IDEzMi41NiBMIDcxNy43OSAxMzYuMDYgTCA3MTkuNTQgMTMyLjU2IEwgNzE3Ljc5IDEyOS4wNiBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjQ0MiIgeT0iMTAyIiB3aWR0aD0iMTMwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEyOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEzMnB4OyBtYXJnaW4tbGVmdDogNDQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxmb250IHN0eWxlPSJmb250LXNpemU6MjBweCI+VGFzazwvZm9udD48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjMyMiIgeT0iOTIiIHdpZHRoPSI3MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNjhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMDJweDsgbWFyZ2luLWxlZnQ6IDMyM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Zm9udCBzdHlsZT0iZm9udC1zaXplOjIwcHgiPlB1bGw8L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDEwMjIgMTIyIEwgMTIwNS42MyAxMjIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxMjEwLjg4IDEyMiBMIDEyMDMuODggMTI1LjUgTCAxMjA1LjYzIDEyMiBMIDEyMDMuODggMTE4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSI3MzIiIHk9IjIiIHdpZHRoPSIyOTAiIGhlaWdodD0iMjQwIiByeD0iMzYiIHJ5PSIzNiIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMTIxMiIgeT0iMiIgd2lkdGg9IjE3MCIgaGVpZ2h0PSIyNDAiIHJ4PSIyNS41IiByeT0iMjUuNSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTY4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTIycHg7IG1hcmdpbi1sZWZ0OiAxMjEzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxmb250IHN0eWxlPSJmb250LXNpemU6MjBweCI+TGl2ZSBwbGF5ZXI8L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI3NjQuNSIgeT0iNzIiIHdpZHRoPSIyMjcuNSIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAyMjZweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMDJweDsgbWFyZ2luLWxlZnQ6IDc2NnB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Zm9udCBzdHlsZT0iZm9udC1zaXplOjIwcHgiPlRoaXJkLXBhcnR5IHBsYXRmb3JtIHB1c2ggc3RyZWFtIGFkZHJlc3M8L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI3NjQuNSIgeT0iMTUyIiB3aWR0aD0iMjI1IiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIyM3B4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE4MnB4OyBtYXJnaW4tbGVmdDogNzY2cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxzcGFuIHN0eWxlPSJmb250LXNpemU6MjBweCI+Qnl0ZVBsdXMgTWVkaWFMaXZlIHB1c2ggc3RyZWFtIGFkZHJlc3M8L3NwYW4+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI3NjQuNSIgeT0iMjIiIHdpZHRoPSIxOTcuNSIgaGVpZ2h0PSIzMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTk2cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzdweDsgbWFyZ2luLWxlZnQ6IDc2NnB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Zm9udCBzdHlsZT0iZm9udC1zaXplOjIwcHgiPlB1c2ggc3RyZWFtIGFkZHJlc3M8L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2MTIiIHk9IjkyIiB3aWR0aD0iODAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDc4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTAycHg7IG1hcmdpbi1sZWZ0OiA2MTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGZvbnQgc3R5bGU9ImZvbnQtc2l6ZToyMHB4Ij5QdXNoPC9mb250PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMTA2MiIgeT0iNzIiIHdpZHRoPSI5MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogODhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA4MnB4OyBtYXJnaW4tbGVmdDogMTA2M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Zm9udCBzdHlsZT0iZm9udC1zaXplOjIwcHgiPkxpdmUgc3RyZWFtaW5nPC9mb250PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==)

1. Pull the source stream

   The task will pull the source stream based on the pull stream address you provide and perform translation.

   > **Warning**

   > You can pull the source stream using the pull stream address from BytePlus MediaLive or other cloud providers, but you cannot use the pull stream address from certain live platforms like TikTok to pull the source stream.

2. Push the stream

   The task pushes the new translated live stream to the push stream address. You can use the push stream address from BytePlus MediaLive, other cloud providers, or live platforms such as TikTok to push the new translated live stream.

3. Watch the live stream

   The audience uses a player to pull and watch the new translated live stream.

## Prerequisites

* **Account preparation**: You have access to a BytePlus account and have activated the [BytePlus MediaLive](https://console.byteplus.com/live/main/overview) service. For more information, see [Signing up for a BytePlus account](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account) and [Activating the MediaLive service](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started#da5a6a63).

* **Scenario preparation**: Complete the relevant preparations according to your scenario.

   * **Scenario 1: Quick demo experience**

      To quickly experience the feature, ensure the following:

      * Your network connection is stable.

      * Prepare the following according to the way you start a live stream:

         * **Web push**: A functioning camera and microphone.

         * **Upload video**: An MP4 video file with a size not exceeding 100 MB.

         * **Online address**: A valid pull stream address, supporting HLS, FLV, or RTMP formats. You can generate the address using the [address generator](https://console.byteplus.com/live/main/locationGenerate).

   * **Scenario 2: Create an AI Dubbing task**

      To create a task for actual live streaming scenarios, complete the following steps.

      1. Ensure that the domain names for stream pushing and pulling have been added under the same domain name space. For more information, see [Adding a domain name](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain).

         > **Warning**

         > This step is required only when using the push and pull stream addresses from BytePlus MediaLive.

      2. Prepare the **Pull Stream URL** and **Push Stream URL**.

         * **Pull Stream URL**: Used for pulling the source stream, which supports RTMP or FLV formats.

            * To use a pull stream address from BytePlus MediaLive as the **Pull Stream URL**, use the same `AppName` and `StreamName`, and generate a pair of addresses using the [address generator](https://console.byteplus.com/live/main/locationGenerate). This pair includes the pull stream address used as the **Pull Stream URL** and the push stream address for pushing the source stream.

            * To use a pull stream address from other cloud providers as the **Pull Stream URL**, get a valid pull stream address.

            > **Warning**

            > Pull stream addresses from certain live platforms like TikTok cannot be used as the **Pull Stream URL**.

         * **Push Stream URL**: Used for pushing the new translated live stream, which supports the RTMP format.

            * To use a push stream address from BytePlus MediaLive as the **Push Stream URL**, use the same `AppName` and `StreamName`, and generate a pair of addresses using the [address generator](https://console.byteplus.com/live/main/locationGenerate). This pair includes the push stream address used as the **Push Stream URL** and the pull stream address for pulling the new live stream.

            * To use a push stream address from other cloud providers or a live platform such as TikTok as the **Push Stream URL**, get a valid push stream address. To push the stream to TikTok or other live platforms, refer to the corresponding official documentation or contact their customer service to get the push stream address.

      > **Note**

      > The push stream address to push the source stream and the pull stream address to pull the new translated live stream are not restricted by protocol. You can select the appropriate protocol based on actual needs.

## Experiencing the demo

Complete the following steps to experience the AI Dubbing effect. If the effect meets expectations, you can create a task to enable translated live streaming. For more information, see [Creating an AI Dubbing task](https://docs.byteplus.com/docs/byteplus-media-live/ai-liveinterpret-simultaneous-audio-and-video-interpretation#0946c25d).

1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live/main/si_v2).

2. In the left navigation bar, click **AI Dubbing**.

3. Click **AI Dubbing Demo**.

4. Select any of the following methods to start a live stream as needed.

   |Method to start a live stream |Description |
   |---|---|
   |Web push |Suitable for scenarios where a live stream is started from a local device, such as a camera and microphone. |
   |Upload video |Suitable for scenarios where translation is performed on existing local video files, such as recorded courses, promotional videos, and more. |
   |Online address |Suitable for scenarios where content is pulled from external live sources, such as live streams from other live platforms or CDN origin, and translated. |
   |Demo video |Suitable for quickly understanding and experiencing translation. |

   > **Warning**

   > Except for **Demo video**, all other demo methods for starting a live stream **are billed at the standard rate**. Therefore, to simply experience the effect, we recommend that you use the **Demo video**.

5. Configure parameters according to the selected method for starting a live stream.

   > **Note**

   > If you select the **Demo video** method, you can directly enter preview mode without further configuration.

   |Configuration item |Applicable method to start a live stream |Description |Configuration details |
   |---|---|---|---|
   |Select mode |* **Web push**<br><br>* **Upload video**<br><br>* **Online address** |Select the translation mode. Different modes provide different effects and latency. |* **Subtitle + Dubbing + Lip Sync**: Translates speech, clones voice timbre, and synchronizes lip movements to provide an immersive experience.<br><br>* **Subtitle + Dubbing**: Translates speech and clones voice timbre, but does not adjust lip movements.<br><br>* **Subtitle only**: Only generates and displays translated subtitles. |
   |Set the translation language |* **Web push**<br><br>* **Upload video**<br><br>* **Online address** |Select the source language and target language.<br><br>> **Warning**<br><br><br><br>* > The demo experience supports fewer languages than a created task.<br><br><br>* > The source and target languages must be different.<br> |* **Original**: Select the source language. You can select **Chinese** or **English**.<br><br>* **Translate as**: Select the target language for translation. You can select **Chinese** or **English**. |
   |Set up the camera and microphone |**Web push** |Select audio and video input devices. |* **Camera**: Select the camera to use from the list.<br><br>* **Microphone**: Select the microphone to use from the list. |
   |Upload local video file |**Upload video** |Upload a local video file. |Select a video to upload. Only the MP4 format is supported, and the file size cannot exceed 100 MB. |
   |Live stream address |**Online address** |Enter the playback URL for the live stream. |Enter a valid pull stream address in HLS, FLV, or RTMP formats.<br><br>> **Note**<br><br><br>> The address cannot directly contain multibyte characters, such as Chinese characters. If you need to include them, you must URL\-encode these characters before entering the address.<br> |
   |Experience duration |* **Web push**<br><br>* **Upload video**<br><br>* **Online address** |Select the experience duration. |Select a duration of **10**, **60**, or **120** minutes. The task will automatically stop when the selected duration ends. |

6. After completing the configuration, click **Start AI Dubbing** at the bottom of the page to begin translation. Ensure that the live content includes clear and stable human voice audio.

   * The **Original** area displays the original input.

   * The **Output** area will automatically start playback once translation is complete.

      During playback, you can click the **Pause** or **Play** icon to control the playback for the **Original** or **Output** area.

      You can click **Stop** **AI Dubbing** at the bottom of the page at any time to stop translation.

   > **Warning**

   > Except for **Demo video**, all other demo methods for starting a live stream are **charged at the standard rate**. Therefore, please **stop translation** promptly to avoid unnecessary charges.

## Creating an AI Dubbing task

During the task duration, when you start pushing the stream, the task will automatically pull the live stream for translation. The new translated live stream will then be pushed to the specified push stream address, enabling the translated live streaming. For example, you can use OBS to start a live stream. After translation, you can stream the translated content on TikTok. For more information, see [Are there any best practices for streaming translated content?](https://docs.byteplus.com/docs/byteplus-media-live/ai-liveinterpret-simultaneous-audio-and-video-interpretation#e98319a7).

Complete the following steps to create a task.

1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live/main/si_v2).

2. In the left navigation bar, click **AI Dubbing**.

3. Click **New Task**.

4. On the page that appears, complete the following configuration and click **Create**.

   |Configuration item |Description |
   |---|---|
   |Title |Task title. Length must be 1–20 characters. Supports Chinese, uppercase and lowercase English letters, digits (0–9), underscores (_), and hyphens (\-).<br><br>> **Warning**<br><br><br>> This title must be unique among all running tasks.<br> |
   |Relay time |Set the task's start and end time, that is, the duration during which the task runs.<br><br><br>* During this period, when you start pushing the stream, the task will automatically pull the live stream for translation and push the new translated live stream to the push stream address.<br><br>* The task automatically stops pushing the new live stream when the task ends, the source stream disconnects, or stream pulling fails.<br><br><br>For example, if you set the relay time to 3 days, you can live stream for 2 hours each day. Each live stream will use this task configuration for translation, and billing will be based on the actual stream push duration of 6 hours (3 days × 2 hours/day).<br><br>> **Note**<br><br><br>> The maximum relay time cannot exceed 7 days.<br> |
   |Pull Stream URL |The address from which the task pulls the source stream. RTMP and FLV formats are supported.<br><br>> **Note**<br><br><br>> The address cannot directly contain multibyte characters, such as Chinese characters. If you need to include them, you must URL\-encode these characters before entering the address.<br> |
   |Push Stream URL |The push stream address, which supports the RTMP format. The task will push the new translated live stream to this address.<br><br>> **Note**<br><br><br><br>* > The address cannot directly contain multibyte characters, such as Chinese characters. If you need to include them, you must URL\-encode these characters before entering the address.<br><br><br>* > To play a new translated live stream on TikTok or other third\-party platforms, ensure that the push stream address of the third\-party platform is used (for example, the push stream address of the TikTok live room). For information on how to get the push stream address, refer to the official documentation of the third\-party platform or contact their official customer service.<br> |
   |Mode |Select from the following modes as needed.<br><br><br>* **AI Dubbing**: Subtitles, dubbed audio, and video are fully synchronized. Supports the lip sync feature. Suitable for scenarios such as conference live streaming where high synchronization and immersion are required. This mode introduces some latency.<br><br>* **Real\-Time Interpretation**: Low latency, but video may not be synchronized with subtitles and dubbed audio. Suitable for scenarios such as event live streaming where low latency is required.<br><br>* **Original (ASR) Subtitles**: Only the source subtitles are needed. Translation is not involved. Suitable for viewing in muted or noisy environments. |
   |Processing Delay |The delay time for translation to complete.<br><br>The recommended values for different modes are as follows:<br><br><br>* **AI Dubbing** (value range: 1–60 seconds)<br><br>   * For lip sync, dubbed audio, and subtitles: 20<br><br>   * For dubbed audio and subtitles: 12<br><br>   * For subtitles only: 8<br><br>* **Real\-Time Interpretation** (value range: 0\-20 seconds): 2\-3. With this delay, the video, subtitles, and dubbed audio can be better synchronized.<br><br>* **Original (ASR) Subtitles** (value range: 0\-20 seconds)<br><br>   * When **Writing Method** is **Whole Sentence**: 15<br><br>   * When **Writing Method** is **Live Streaming**: 2\-3<br><br><br>> **Note**<br><br><br>> If the subtitles appear earlier than the video or original sound, reduce the delay time as needed to align the subtitles with the video or original sound, and vice versa.<br> |
   |Translation language / Original Language |* For **AI Dubbing** or **Real\-Time Interpretation** mode: Select the source and target languages. The source language supports Chinese and English. The target language supports Chinese, English, Japanese, Spanish, Indonesian, Portuguese, French, and German.<br><br>   > **Note**<br>   <br><br>   > The source and target languages must be different.<br>   <br><br>* For **Original (ASR) Subtitles** mode<br><br>   * When **Writing Method** is **Whole Sentence**: The source language supports Chinese, English, Japanese, Spanish, Indonesian, Portuguese, French, German, and Korean.<br><br>   * When **Writing Method** is **Live Streaming**: The source language supports Chinese and English. |
   |Write SEI |Whether to write subtitles into SEI messages in the live stream. When enabled, the player can receive the subtitles from the SEI messages.<br><br>> **Note**<br><br><br><br>* > This field is displayed in either of the following cases:<br><br><br>   * > **AI Dubbing** mode is selected.<br><br><br>   * > **Original (ASR) Subtitles** mode is selected and **Writing Method** is set to **Whole Sentence**.<br><br><br>* > MediaLive uses `100` as the SEI `type` value when writing subtitles into SEI messages. If your stream pushing tool or app also writes custom SEI messages into the stream, avoid using the same SEI `type` value. Otherwise, the player may identify the custom data as subtitles.<br> |
   |Lip Sync |Whether to enable the lip sync feature. Once enabled, the speaker's lip movements will synchronize with the dubbed audio, making the live stream more immersive.<br><br>> **Note**<br><br><br>> This feature can only be enabled when the dubbed audio feature is enabled in **AI Dubbing** mode.<br> |
   |Dubbed Audio |Whether to enable the dubbed audio feature.<br><br>> **Note**<br><br><br>> This feature can only be enabled in **AI Dubbing** or **Real\-Time Interpretation** mode.<br><br><br>After enabling the feature, complete the following configuration.<br><br><br>* **Voice Settings**: Currently, only **Clone From Source** is supported, which retains the original voice timbre.<br><br>* **Noise Reduction**: When enabled, the background noise such as electrical noise and environmental noise in dubbed audio is effectively reduced, improving the clarity of the final output audio.<br><br>   > **Warning**<br>   <br><br>   * > You can only enable or disable noise reduction in **AI Dubbing** mode, or when you select **Keep only translated audio** in **Real\-Time Interpretation** mode.<br>   <br><br>   * > Enabling noise reduction may cause background sound to disappear.<br>   <br><br>* **Original sound configuration**: Select how to handle the original sound of the live stream, which determines whether the audience hears mixed audio or pure dubbed audio.<br><br>   * **Automatic overlay translation of original sound**: Overlay the dubbed audio while retaining the original sound. Commonly used in scenarios such as live streams of sports events where it is necessary to retain the sense of presence at the venue. In this case, adjusting the volume of the original sound is supported.<br><br>   * **Keep only translated audio**: The original sound is completely removed, and only the dubbed audio is output. Applicable to scenarios where the original sound does not need to be heard. In this case, adjusting the volume of the background sound (non\-human voice) is supported.<br><br>   > **Note**<br>   <br><br>   > You can only configure the original sound in **Real\-Time Interpretation** mode.<br>   <br><br>* **Volume Balance**: When enabled, the system automatically adjusts the output audio volume to maintain a stable and comfortable level, effectively preventing sudden changes in volume or harsh explosive sounds, and significantly enhancing the audience's listening experience. |
   |Subtitle |Whether to enable the subtitles feature. When enabled, subtitles will be displayed on the video.<br><br>You can configure the number of display lines, subtitle order (source subtitles on top or bottom), margin, font size, font, and more for source and translated subtitles. For example,<br><br><br>* **Subtitle format**: Set which subtitles are displayed.<br><br>   * **Original + Translation**: Display bilingual subtitles. The display order of subtitles is determined by **Subtitle sorting**.<br><br>   * **Translation**: Only display translated subtitles.<br><br>   * **Original**: Only display source subtitles.<br><br>* **Lines of subtitles**: Set the maximum number of lines displayed for the subtitles in each language.<br><br>   > **Note**<br>   <br><br>   > When displaying bilingual subtitles, this configuration applies to both the source and translated subtitles. For example, if **2 lines** is selected, both the source and translated subtitles will display up to 2 lines each, so the subtitles will occupy a total of 4 lines of screen space.<br>   <br><br>   * **1 line**: Each language's subtitles display up to one line. Content may be truncated.<br><br>   * **2 lines**: Each language's subtitles display up to two lines. Content may be truncated.<br><br>   * **Auto**: Automatically wraps lines based on the total number of subtitle characters and the maximum number of characters per line to ensure complete content display.<br><br>* **Maximum characters per line**: The maximum number of characters per line. When **Lines of subtitles** is set to **1 line** or **2 lines**, and the total number of characters in the source or translated subtitles exceeds the display range, the content will be truncated. For example, if the maximum number of characters per line for translated subtitles is 10, **Lines of subtitles** is set to **2 lines**, and the total number of characters in the translated subtitles exceeds 20, any content after the 20th character will be truncated.<br><br>   > **Note**<br>   <br><br>   * > The system calculates the maximum number of characters that can be displayed per line based on factors such as the **Maximum characters per line**, **Left & right margins**, **Font**, **Font** **Size**, and screen resolution you configured.<br>   <br><br>   * > Each character, letter, symbol, or digit counts as one character.<br>   <br><br>* **Writing Method**: The display mode of source subtitles.<br><br>   * **Whole Sentence**: The subtitles will be displayed one complete sentence at a time. The system waits until a sentence is finished, then displays the entire subtitles corresponding to the audio segment all at once. This method ensures contextual completeness and reading continuity, providing an experience similar to watching movie subtitles.<br><br>   * **Live Streaming**: Subtitles are displayed character by character or word by word, without waiting for the sentence to finish. This method prioritizes real\-time performance, allowing the audience to see the text almost simultaneously with the audio, similar to voice input on a mobile phone.<br><br>   > **Note**<br>   <br><br>   > You can only configure the display mode of source subtitles in **Original (ASR) Subtitles** mode.<br>    |
   |Glossary |Add proprietary vocabulary and expected translations, such as brand names, personal names, product names, or feature names. The system uses the glossary as a reference for the translation model to improve the translation accuracy of proprietary vocabulary, **but the expected translations may not be used every time**. If mistranslations persist after you configure the glossary, add possible mistranslations and their correct translations in **Corrections** to forcibly correct translated subtitles.<br><br>Use the format `original text:translation`, and separate multiple entries with English commas (,). For example, `赛事直播:sports live streaming,实时字幕:real-time subtitles`.<br><br>> **Warning**<br><br><br><br>* > You can only configure the glossary in **AI Dubbing** or **Real\-Time Interpretation** mode, and the glossary applies only to **translated subtitles**.<br><br><br>* > In each `original text:translation` entry, the original text and translation cannot contain English commas (,).<br><br><br>* > The total number of characters in the **Glossary** text box cannot exceed 30,000.<br> |
   |Hot word bank |Add hotwords, such as product names or popular phrases, as a reference for the speech recognition model to improve recognition accuracy. **Hotwords may not be recognized accurately every time**. Hotwords must match the source language and be separated by line breaks.<br><br>The total number of characters in the **Hot word bank** text box cannot exceed 30,000. If recognition errors persist after you configure hotwords, add possible recognition errors and their corrected forms in **Corrections** to forcibly correct original ASR subtitles.<br><br>> **Note**<br><br><br>> You can only configure hotwords in **Original (ASR) Subtitles** mode.<br> |
   |Corrections |Configure subtitle text that must be forcibly corrected. Add possible incorrect forms and their corrected forms one by one. Each incorrect form or corrected form must be 1 to 50 characters long. You can add up to 60 corrections. We recommend that you adjust them based on actual results.<br><br>When the system matches an incorrect form, it forcibly replaces the incorrect form with the corrected form.<br><br><br>* **Original (ASR) subtitles**: Correct recognition errors. For example, if **MediaLive** is incorrectly recognized as **media life**, you can add the following correction: media life (**Subtitle**) \> MediaLive (**Correct**).<br><br>* **Translated subtitles**: Correct mistranslations. **Corrections modify only translated subtitles and do not modify source subtitles or dubbed audio**. For example, if **LiveCore** is mistranslated as **核心直播**, you can add the following correction: 核心直播 (**Translation**) \> LiveCore (**Correct**).<br><br><br>> **Warning**<br><br><br>> Corrections match text only and do not determine the context. Use corrections only when the configured text can be clearly identified as incorrect. The corrected form must not contain the corresponding incorrect form. For example, if you configure **stream** \> **live stream**, and the subtitle already correctly displays **live stream**, the system still replaces **stream** with **live stream**, resulting in **live live stream**.<br> |
   |Preview |Test the subtitle effects online according to the UI prompts.<br><br>> **Note**<br><br><br><br>* > The source stream size selected here is used only for preview and will not change the source stream's resolution. The orientation of the output stream for the task is inherited from the source stream.<br><br><br>* > There are no restrictions on the size, format, or other attributes of the background image uploaded here.<br> |
   |Callback address |The URL used to receive callback messages. The URL must start with `http://` or `https://`, be publicly accessible, and contain 1–100 characters. For more information about AI Dubbing callback messages, see [AI Dubbing](https://docs.byteplus.com/docs/byteplus-media-live/docs-callback-description#ai-dubbing). |

5. During the relay duration of the task, use your stream pushing tool (such as OBS) to start pushing the stream. Ensure that the live content includes clear and stable human voice audio. The task will automatically pull the live stream for translation and push the new translated live stream to the push stream address.

6. If you push the new translated live stream to TikTok or other third\-party platforms, the audience can directly watch the live stream on the third\-party platform.

   You can also use any of the following methods to pull the translated content using a pull stream address with the same `AppName` and `StreamName` as the push stream address.

   |Method |Scenario |Description |
   |---|---|---|
   |Third\-party stream pulling tool |No SDK development resources. |Configure the pull stream address in the third\-party stream pulling tool to play the live stream. For more information, refer to the corresponding official documentation or consult official customer support. |
   |Player SDK for Web |Watch the live stream in a web browser. |Integrate the Player SDK for Web and play the live stream on your website or web app. For more information, see [Integrating the Player SDK for Web](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1). |
   |Client SDK |Watch the live stream in your own mobile app. |Integrate the client SDK and play the live stream in a mobile app. For more information, see:<br><br><br>* iOS: [Integrating the Player SDK for iOS](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios)<br><br>* Android: [Integrating the Player SDK for Android](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-android)<br><br>* Flutter: [Integrating the Player SDK for Flutter](https://docs.byteplus.com/docs/byteplus-media-live/integrating-the-player-sdk-for-flutter)<br><br>* React Native: [Integrating the Player SDK for React Native](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-rn) |
   |BytePlus MediaLive console |For quick preview and debugging during development or testing. |On the [Web pull page](https://console.byteplus.com/live/main/webPullStream/play) in the console, enter the pull stream address to quickly verify playback. For more information, see [Pulling a stream through the console](https://docs.byteplus.com/docs/byteplus-media-live/docs-web-pull).<br><br>> **Note**<br><br><br>> Only supports playing FLV, HLS, and RTM streams.<br> |

7. (Optional) In the task list, click **Preview** to enter the **Video Preview** page and view the video after translation is complete.

   You can control the AI Dubbing feature at any time by clicking **EnabledSubtitle** or **CloseSubtitle**. This operation will not interrupt the stream pushed to the push stream address. AI Dubbing is still billed based on the actual stream push duration.

   * **CloseSubtitle**: Disable translation to push the original content without translation.

   * **EnabledSubtitle**: Enable translation to push the translated content.

      For example, during a live stream for English speakers, you can enable translation when non\-English speakers are speaking, and then disable translation after their speech ends.

   > **Warning**

   * > You can run up to 2 tasks simultaneously under each account. To run more tasks simultaneously, please contact [technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980).

   * > Tasks cannot be restarted after they end. You can copy the task to quickly create a new task with the same configuration, and set a new relay time for the new task.

## FAQ

### Are there any best practices for streaming translated content?

Taking the most common scenario **using OBS to start a live stream and pushing the translated content to TikTok** as an example, the complete process is as follows.

> **Note**

> AI Dubbing does not restrict the stream pushing method. You can also start a live stream using a mobile phone or other methods. This example uses OBS to start a live stream.

1. Add the domain names for stream pushing and pulling under the same domain name space. For more information, see [Adding a domain name](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain).

2. Use the [address generator](https://console.byteplus.com/live/main/locationGenerate) to generate the push stream address for OBS to push the stream.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d68335b38334d1db72b46564d0bd5ab~tplv-goo7wpa0wc-topic.webp)

   * To use the RTMP protocol to push the stream, get the **OBS push stream address** and **OBS Streaming Key**.

   * To use the RTMPS protocol to push the stream, get the **OBS push stream address** and **OBS Streaming Key**, and modify the protocol header from `rtmp` to `rtmps` in the **OBS push stream address**.

   * To use the SRT protocol to push the stream, get the **TS over SRT address** or **RTMP over SRT address**.

3. In the OBS **Settings** dialog box, select **Custom...**  from the **Service** drop\-down list and configure the **Server** and **Stream Key** under the **Stream** tab.

   * To use the RTMP or RTMPS protocol to push the stream, complete the following configuration.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3858db6f3e7446f1945a8e23794e6182~tplv-goo7wpa0wc-topic.webp)

      * **Server**: The **OBS push stream address** obtained in the previous step, for example, `rtmp://push.example.com/live/`.

         > **Note**

         > To use the RTMPS protocol to push the stream, ensure that the protocol header of the **OBS push stream address** has been changed to `rtmps`.

      * **Stream Key**: The **OBS Streaming Key** obtained in the previous step, for example, `test?expire=17770****6&sign=84ad24cea1fc6e186****0ceb5315bfb`.

   * To use the SRT protocol to push the stream, use the **TS over SRT address** or **RTMP over SRT address** obtained in the previous step as the **Server**, and leave **Stream Key** blank.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5151957f11c04f93a37efbd642e4cc9f~tplv-goo7wpa0wc-topic.webp)

   > **Note**

   > There are no restrictions on stream pushing protocols, but when using OBS for stream pushing, only RTMP, RTMPS, and SRT protocols are currently supported.

4. On the [Address generator](https://console.byteplus.com/live/main/locationGenerate) page, use the same `AppName` and `StreamName` as the push stream address generated in Step 2 to generate a pull stream address using the RTMP or FLV protocol, which will be used as the **Pull Stream URL** for the task.

5. On the [AI Dubbing](https://console.byteplus.com/live/main/si_v2) page, create a task. Note the following when you configure the task.

   * **Pull Stream URL**: The pull stream address generated in Step 4.

   * **Push Stream URL**: A valid push stream address that uses the RTMP protocol for the TikTok live room. For information on how to get the push stream address, refer to TikTok official documentation or contact TikTok official customer service.

6. During the relay duration of the task, use OBS to start pushing the stream. Ensure that the live content includes clear and stable human voice audio. Then, the task will automatically pull the live stream for translation, and the new translated live stream will be pushed to the push stream address of TikTok. The audience can then watch the translated content in the corresponding TikTok live room.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ca866bb1b9c496ab841151aea729e8e~tplv-goo7wpa0wc-topic.webp)

### Which should I choose: the AI Dubbing task or the AI Dubbing mode of subtitle configuration?

The AI Dubbing task and the AI Dubbing mode of subtitle configuration use the same translation model and deliver identical translation results. Please select the appropriate mode based on your specific scenario.

* If the following scenarios apply, we recommend that you choose the AI Dubbing task:

   * **Event\-oriented**: Translation is needed for a single or a few important events, such as product launches or international conferences.

   * **Manual control required**: You want to enable translation only during specific periods in the live stream, such as when non\-native speakers are speaking.

   * **Low latency required**: For live streaming scenarios with high demands for low latency, such as sports events, you can choose the **Real\-Time Interpretation** mode to reduce latency.

* If you have a large number of live rooms that require translation to be enabled regularly and automatically, we recommend that you choose the AI Dubbing mode of subtitle configuration. For more information, see [Managing subtitle configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-manage-subtitle-configuration).

### My live stream only has subtitles but no audio. Can I use the AI Dubbing feature?

No, you cannot. The AI Dubbing feature only supports recognizing and translating human voice content, but cannot translate based on source subtitles.

### My live stream is aimed at a global audience. How can I provide subtitles in different languages for them?

You can create multiple tasks, use the same **Pull Stream URL** to pull the source stream, and set different target languages and **Push Stream URL**s for each task. When the audience switches between language channels of the player, the player pulls different live streams in different languages.

### My live stream involves multiple languages. For example, the host speaks Chinese, but sings Japanese songs during the live stream. Can all of this be translated into English?

No, this is not supported. Currently, automatic detection of the live stream language is not supported. Translation only works between the source and target languages configured in the task. In such cases, we recommend that you set the source language to the host’s primary language, such as Chinese. In this example, only the Chinese content will be translated into English, while the Japanese songs will remain untranslated.

### Can I adjust the volume of the dubbed audio?

No, you cannot. You can only adjust the original sound volume or background sound (non\-human voice) volume through the **Original sound configuration** in **Real\-Time Interpretation** mode. The volume of the dubbed audio can be adjusted by the audience.

### Can I perform transcoding and other operations while performing translation?

Yes, you can. After translation is complete, the task will generate a new live stream. As long as you use the BytePlus MediaLive push stream address as the **Push stream URL** for the task, you can perform any regular processing on the live stream, such as transcoding, recording, and more.

Take **transcoding** as an example. Suppose the push stream address is `rtmp://push.example.com/live/test`, proceed as follows:

1. **Add transcoding configuration**: Under the **domain name space** where the domain name for stream pushing (`push.example.com`) belongs, use the same `AppName` (**live**) as the push stream address to add the transcoding configuration. For more information, see [Managing transcoding configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding).

2. **Get the transcoded stream address**: On the [Address generator](https://console.byteplus.com/live/main/locationGenerate) page, complete the following configuration to generate the transcoded stream address.

   * **Select the domain name**: Select the domain name for stream pulling. This domain name for stream pulling must belong to the same domain name space as your domain name for stream pushing (`push.example.com`).

   * **AppName** and **StreamName**: Enter the same `AppName` (**live**) and `StreamName` (**test**) as the push stream address.

3. **Pull the stream for playback**: Use the obtained transcoded stream address to pull the transcoded stream, so you can play the translated and transcoded live content.

### Why is it not possible to play translated live content, or why does playback stop after a short period?

Unstable stream pushing of the source stream can cause issues such as playback failures or stuttering during playback. Please check the stream pushing status of your source stream.

### Why was the translation not successful?

Ensure that the source language matches the language in the source stream audio, and that the target language is the language required by the audience. Also, ensure that the live content contains clear and stable human voice audio.

### Can I export subtitle files?

No, you cannot. BytePlus MediaLive currently does not support exporting subtitle files.

### Why can I still hear the original sound?

Please check the following items one by one:

* **Check whether the dubbed audio feature is enabled**: The dubbed audio will only be provided after you enable the dubbed audio feature. Otherwise, only the original sound will be output.

* **Check the original sound configuration in Real\-Time Interpretation mode**: If you do not want to hear the original sound, you can select **Keep only translated audio**.

* **Check the task status**: On the [AI Dubbing](https://console.byteplus.com/live/main/si_v2) page, ensure that the task status is **Running**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1074bb2673bb4e16ab54257253d4a897~tplv-goo7wpa0wc-topic.webp)

* **Check whether translation is enabled**: On the [AI Dubbing](https://console.byteplus.com/live/main/si_v2) page, click **Preview**. On the **Video Preview** page, ensure that **EnabledSubtitle** is selected.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e67e46ffaa584c3c844bc0e67952f7f0~tplv-goo7wpa0wc-topic.webp)

### What happens if multiple tasks use the same push stream address?

We recommend that you configure a separate push stream address for each task to ensure the stability and predictability of the live content.

If you configure the same push stream address for different tasks with similar relay times, the content played on that push stream address will be the translated content of the task that first successfully pushes the stream.

For example, the source stream of task A is a press conference, and the source stream of task B is an e\-commerce livestream. Both tasks use the same push stream address for a TikTok live room. If task B completes stream pushing earlier than task A, the TikTok live room will play the e\-commerce livestream.
