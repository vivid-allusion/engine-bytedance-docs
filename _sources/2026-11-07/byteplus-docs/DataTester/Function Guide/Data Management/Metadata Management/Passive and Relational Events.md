---
title: "Passive and Relational Events"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Passive-and-Relational-Events"
---

<span id="_1-概述"></span>
# 1. Overview

Active and passive events are based on the active triggering and passive affected behavior descriptions of "users". In some business scenarios, users may be both the initiator and the influencer of behavior. The behavior triggered by the behavior initiator is called an "active event", and the behavior influenced by the behavior influencer is called a "passive event". When active events and passive events have a corresponding relationship and appear in pairs, they are called "relational events".

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI2NzZweCIgaGVpZ2h0PSIzMDRweCIgdmlld0JveD0iLTAuNSAtMC41IDY3NiAzMDQiPjxkZWZzLz48Zz48ZWxsaXBzZSBjeD0iMjEzIiBjeT0iMTExIiByeD0iNDAiIHJ5PSI0MCIgZmlsbD0iIzdlYTZlMCIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMTFweDsgbWFyZ2luLWxlZnQ6IDE3NHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjRkZGRkZGOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Zm9udCBzdHlsZT0iZm9udC1zaXplOjIwcHgiPlVzZXIgQTwvZm9udD48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxlbGxpcHNlIGN4PSI2MzMiIGN5PSIxMTEiIHJ4PSI0MCIgcnk9IjQwIiBmaWxsPSIjN2VhNmUwIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA3OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDExMXB4OyBtYXJnaW4tbGVmdDogNTk0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICNGRkZGRkY7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxmb250IHN0eWxlPSJmb250LXNpemU6MjBweCI+VXNlciBCPGJyIC8+PC9mb250PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAxMyAxMTEgTCAxNjQuNzYgMTExIiBmaWxsPSJub25lIiBzdHJva2U9IiM3ZWE2ZTAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxNzAuNzYgMTExIEwgMTYyLjc2IDExNSBMIDE2NC43NiAxMTEgTCAxNjIuNzYgMTA3IFoiIGZpbGw9IiM3ZWE2ZTAiIHN0cm9rZT0iIzdlYTZlMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDEzIDMxIEwgMTc2LjgzIDgwLjM0IiBmaWxsPSJub25lIiBzdHJva2U9IiM3ZWE2ZTAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxODIuNTcgODIuMDcgTCAxNzMuNzYgODMuNTkgTCAxNzYuODMgODAuMzQgTCAxNzYuMDcgNzUuOTMgWiIgZmlsbD0iIzdlYTZlMCIgc3Ryb2tlPSIjN2VhNmUwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMTMgMTkxIEwgMTc2LjgzIDE0MS42NiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjN2VhNmUwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMTgyLjU3IDEzOS45MyBMIDE3Ni4wNyAxNDYuMDcgTCAxNzYuODMgMTQxLjY2IEwgMTczLjc2IDEzOC40MSBaIiBmaWxsPSIjN2VhNmUwIiBzdHJva2U9IiM3ZWE2ZTAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMTIuNjYiIHk9IjE0OC40MSIgd2lkdGg9IjE1MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiB0cmFuc2Zvcm09InJvdGF0ZSgtMTUsODcuNjYsMTU4LjQxKSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSlyb3RhdGUoLTE1IDg3LjY2IDE1OC40MSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE0OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE1OHB4OyBtYXJnaW4tbGVmdDogMTRweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogI0ZGRkZGRjsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGZvbnQgY29sb3I9IiMwMDAwMDAiIHN0eWxlPSJmb250LXNpemU6MTZweCI+QWZmZWN0ZWQgYnkgRXZlbnQgYzwvZm9udD48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjEyLjY2IiB5PSI5MSIgd2lkdGg9IjE1MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTQ4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTAxcHg7IG1hcmdpbi1sZWZ0OiAxNHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjRkZGRkZGOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Zm9udCBjb2xvcj0iIzAwMDAwMCIgc3R5bGU9ImZvbnQtc2l6ZToxNnB4Ij5BZmZlY3RlZCBieSBFdmVudCBiPC9mb250PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMjMiIHk9IjMxIiB3aWR0aD0iMTUwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHRyYW5zZm9ybT0icm90YXRlKDE1LDk4LDQxKSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSlyb3RhdGUoMTUgOTggNDEpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxNDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA0MXB4OyBtYXJnaW4tbGVmdDogMjRweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogI0ZGRkZGRjsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGZvbnQgY29sb3I9IiMwMDAwMDAiIHN0eWxlPSJmb250LXNpemU6MTZweCI+QWZmZWN0ZWQgYnkgRXZlbnQgYTwvZm9udD48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjI2NyIgeT0iOTEiIHdpZHRoPSIxMjAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEwMXB4OyBtYXJnaW4tbGVmdDogMjY4cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTZweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICNGRkZGRkY7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxmb250IGNvbG9yPSIjMDAwMDAwIj5UcmlnZ2VyIGV2ZW50IDI8L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDI1MyAxMTEgTCA0MDQuNzYgMTExIiBmaWxsPSJub25lIiBzdHJva2U9IiM3ZWE2ZTAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA0MTAuNzYgMTExIEwgNDAyLjc2IDExNSBMIDQwNC43NiAxMTEgTCA0MDIuNzYgMTA3IFoiIGZpbGw9IiM3ZWE2ZTAiIHN0cm9rZT0iIzdlYTZlMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDQzMyAxMTEgTCA1ODQuNzYgMTExIiBmaWxsPSJub25lIiBzdHJva2U9IiM3ZWE2ZTAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA1OTAuNzYgMTExIEwgNTgyLjc2IDExNSBMIDU4NC43NiAxMTEgTCA1ODIuNzYgMTA3IFoiIGZpbGw9IiM3ZWE2ZTAiIHN0cm9rZT0iIzdlYTZlMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDI0MyAxNDEgTCA0MDUuMSAxODguNjgiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzdlYTZlMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDQxMC44NSAxOTAuMzcgTCA0MDIuMDUgMTkxLjk1IEwgNDA1LjEgMTg4LjY4IEwgNDA0LjMxIDE4NC4yNyBaIiBmaWxsPSIjN2VhNmUwIiBzdHJva2U9IiM3ZWE2ZTAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA0MzMgMTkxIEwgNTk2LjgzIDE0MS42NiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjN2VhNmUwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNjAyLjU3IDEzOS45MyBMIDU5Ni4wNyAxNDYuMDcgTCA1OTYuODMgMTQxLjY2IEwgNTkzLjc2IDEzOC40MSBaIiBmaWxsPSIjN2VhNmUwIiBzdHJva2U9IiM3ZWE2ZTAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAyNDEuMjggODIuNzIgTCA0MDUuMTEgMzMuMzgiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzdlYTZlMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDQxMC44NiAzMS42NCBMIDQwNC4zNSAzNy43OCBMIDQwNS4xMSAzMy4zOCBMIDQwMi4wNSAzMC4xMiBaIiBmaWxsPSIjN2VhNmUwIiBzdHJva2U9IiM3ZWE2ZTAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA0MzMgMzIuNzIgTCA1OTYuODEgODAuNDEiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzdlYTZlMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDYwMi41NyA4Mi4wOSBMIDU5My43NyA4My42OSBMIDU5Ni44MSA4MC40MSBMIDU5Ni4wMSA3Ni4wMSBaIiBmaWxsPSIjN2VhNmUwIiBzdHJva2U9IiM3ZWE2ZTAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMjY3IiB5PSIxNDQiIHdpZHRoPSIxMjAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgdHJhbnNmb3JtPSJyb3RhdGUoMTUsMzI3LDE1NCkiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpcm90YXRlKDE1IDMyNyAxNTQpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNTRweDsgbWFyZ2luLWxlZnQ6IDI2OHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjRkZGRkZGOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Zm9udCBjb2xvcj0iIzAwMDAwMCI+VHJpZ2dlciBldmVudCAzPGJyIC8+PC9mb250PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMjUzIiB5PSI0MSIgd2lkdGg9IjEyMCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiB0cmFuc2Zvcm09InJvdGF0ZSgtMTUsMzEzLDUxKSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSlyb3RhdGUoLTE1IDMxMyA1MSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDUxcHg7IG1hcmdpbi1sZWZ0OiAyNTRweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogI0ZGRkZGRjsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGZvbnQgY29sb3I9IiMwMDAwMDAiPlRyaWdnZXIgZXZlbnQgMTwvZm9udD48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjQ0MyIgeT0iMzUiIHdpZHRoPSIxNTAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgdHJhbnNmb3JtPSJyb3RhdGUoMTUsNTE4LDQ1KSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSlyb3RhdGUoMTUgNTE4IDQ1KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTQ4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNDVweDsgbWFyZ2luLWxlZnQ6IDQ0NHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjRkZGRkZGOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Zm9udCBjb2xvcj0iIzAwMDAwMCIgc3R5bGU9ImZvbnQtc2l6ZToxNnB4Ij5BZmZlY3RlZCBieSBFdmVudCAxPC9mb250PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNDMzIiB5PSI5MSIgd2lkdGg9IjE1MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTQ4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTAxcHg7IG1hcmdpbi1sZWZ0OiA0MzRweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogI0ZGRkZGRjsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGZvbnQgY29sb3I9IiMwMDAwMDAiIHN0eWxlPSJmb250LXNpemU6MTZweCI+QWZmZWN0ZWQgYnkgRXZlbnQgMjwvZm9udD48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjQzMyIgeT0iMTQ3IiB3aWR0aD0iMTUwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHRyYW5zZm9ybT0icm90YXRlKC0xNSw1MDgsMTU3KSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSlyb3RhdGUoLTE1IDUwOCAxNTcpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxNDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNTdweDsgbWFyZ2luLWxlZnQ6IDQzNHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjRkZGRkZGOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Zm9udCBjb2xvcj0iIzAwMDAwMCIgc3R5bGU9ImZvbnQtc2l6ZToxNnB4Ij5BZmZlY3RlZCBieSBFdmVudCAzPGJyIC8+PC9mb250PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMTEiIHk9IjIyMSIgd2lkdGg9IjE1MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTQ4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjMxcHg7IG1hcmdpbi1sZWZ0OiAxMnB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDIycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjRkZGRkZGOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Zm9udCBjb2xvcj0iIzAwMDAwMCIgc3R5bGU9ImZvbnQtc2l6ZToyMnB4Ij5QYXNzaXZlIEV2ZW50PC9mb250PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAzMzQgMjQxIEwgMzM0IDI3MSBMIDUyMCAyNzEgTCA1MTkuOTUgMjQwIiBmaWxsPSJub25lIiBzdHJva2U9IiM3ZWE2ZTAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHJlY3QgeD0iMjU5IiB5PSIyMjEiIHdpZHRoPSIxNTAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE0OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIzMXB4OyBtYXJnaW4tbGVmdDogMjYwcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMjJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICNGRkZGRkY7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxmb250IGNvbG9yPSIjMDAwMDAwIiBzdHlsZT0iZm9udC1zaXplOjIycHgiPkFjdGl2ZSBFdmVudDwvZm9udD48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjQzNyIgeT0iMjIxIiB3aWR0aD0iMTUwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxNDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMzFweDsgbWFyZ2luLWxlZnQ6IDQzOHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDIycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjRkZGRkZGOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Zm9udCBjb2xvcj0iIzAwMDAwMCIgc3R5bGU9ImZvbnQtc2l6ZToyMnB4Ij5QYXNzaXZlIEV2ZW50PC9mb250PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMzMzIiB5PSIyODEiIHdpZHRoPSIxODAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE3OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDI5MXB4OyBtYXJnaW4tbGVmdDogMzM0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMjJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICNGRkZGRkY7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxmb250IGNvbG9yPSIjMDAwMDAwIiBzdHlsZT0iZm9udC1zaXplOjIycHgiPlJlbGF0aW9uYWwgRXZlbnQ8L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIzIiB5PSIzIiB3aWR0aD0iMTcwIiBoZWlnaHQ9IjIwOCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjZmZiNTcwIiBzdHJva2Utd2lkdGg9IjMiIHN0cm9rZS1kYXNoYXJyYXk9IjkgOSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjI1MyIgeT0iMyIgd2lkdGg9IjE2MCIgaGVpZ2h0PSIyMDgiIGZpbGw9Im5vbmUiIHN0cm9rZT0iI2ZmYjU3MCIgc3Ryb2tlLXdpZHRoPSIzIiBzdHJva2UtZGFzaGFycmF5PSI5IDkiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSI0MzMiIHk9IjMiIHdpZHRoPSIxNjAiIGhlaWdodD0iMjA4IiBmaWxsPSJub25lIiBzdHJva2U9IiNmZmI1NzAiIHN0cm9rZS13aWR0aD0iMyIgc3Ryb2tlLWRhc2hhcnJheT0iOSA5IiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PC9nPjwvc3ZnPg==" />

<span id="典型场景：社交应用"></span>
## Typical scenario: social applications

**Scenario 1:**  User A follows User B.

User A is the initiator of the attention behavior, triggering an active event, and User B is the influencer of the attention behavior, passively accepting an event.

Active Event: User A follows User B

Passive Event: User B is followed by User A

Active and passive events have a corresponding relationship and appear in pairs in this scenario, resulting in "relational events".

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fcaf5f11773c46ee9800d386e0aec6f2~tplv-goo7wpa0wc-image.image" width="505px" /></div>


**Scenario 2:**  User A sends a message to User B.

Active Event: User A sends a message

Passive event: User B receives a message

**Scenario 3:**  User A sends a red envelope to User B

Active event: User A sent 1 red envelope.

Passive event: User B receives a red envelope

**More scenarios** : like and be liked, comment and be commented, complain and be complained, share content and receive content...

<span id="特殊场景"></span>
## Special scenario

**Scenario description:**  The system pushes a notification to the user, and the customer service pushes a coupon to the user during the complaint resolution process. The program triggers a message to the user.

Because active and passive events are based on the "user", there are no active events in this scenario, and it is not the user who actively triggers the behavior.

Users are the recipients of behavior and are affected passively, with only passive events.

Passive event: user receives notification/user receives coupon/user receives push message

<span id="_2-分析"></span>
# 2. Analysis

<span id="转化分析"></span>
## Conversion analysis

<span id="用户互关的场景"></span>
### Scenarios where users pay attention to each other

Relationship event


|**Event ID** |**Event name** |**User ID** |**Target Object ID** |**Initiating object ID** |**Is it passive?**  |**Is it related?**  |**Semantics** |
|---|---|---|---|---|---|---|---|
|1 |subscribe |A |B |null |No |Yes |A pays attention to B |
|2 |$inactive_subscribe |B |null |A |Yes |Yes |B is followed by A |
|3 |subscribe |B |A |null |No |No |B pays attention to A |


When we want to count the proportion of backlinks, we need to use passive events, and build the funnel as follows:

Step 1: $inactive_subscribe, associate initiating object ID

Step 2: subscribe and associate the target object ID (since the associated property of the list type is not currently supported, the user needs to report the ID of a target object by himself in this scenario).

Other conditions: Group by user ID.

<span id="_3-事件和属性变更"></span>
# 3. Events and property changes

Relational events and passive events have a few more preset properties to distinguish them from active events. The main differences are shown in the following table:


| |Event name |Preset properties |Display name |Preset property type |Value selection description |
|---|---|---|---|---|---|
|Active events (relationships) |event_name |$target_uuid_list |Passive Event UUID |list |Manually report user ID |
| | |$inline |Is it a relational event? |string |True, and any other value |
|Passive events (relationships) |$inactive_ |$inactive |Is it a passive event? |string |True, and any other value |
| | |$inline |Is it a relational event? |string |True, and any other value |
| | |$source_uuid |active event UUID |string |UUID of the corresponding associated event |
|Passive events (manual) |custom |$inactive |Is it a passive event? |string |True, and any other value |


When the user marks the current event as a relational event in the active event ($inline is "true"), the system automatically generates the corresponding passive event. System\-generated passive events will set an additional preset property: "$source_uuid" to trigger the user's uuid for the active event.

<span id="_4-常见问题"></span>
# 4. Frequently Asked Questions

<span id="_4-1-如何区分主被动事件？"></span>
## 4.1 How to distinguish between active and passive events?

The value of the passive event property $inactive is true. Note that the data type of this property is currently string, not boolean.

When a relational event is reported, the system automatically generates a passive event. The passive event automatically generated by the system will not only have the above preset properties, but also include the two properties of $inline = "true" and $source_uuid (the value is the corresponding active event uuid), and the event name will automatically add "$inactive_" prefix.

<span id="_4-2-被动事件是否会对账单数据计算产生影响？"></span>
## 4.2 Will passive events affect the calculation of billing data?

Passive events are counted by default when calculating event volume consumption, but not when calculating MAU and DAU. Passive events that are disabled do not consume.

<span id="_4-3-上报关系事件时，如果-target-uuid-list中包含多个-uuid，是否会生成多个被动事件？"></span>
## 4.3 When reporting a relational event, if $target_uuid_list contains multiple uuids, will multiple passive events be generated?

Yes. $target_uuid_list is a list property that supports multiple uuids. The system automatically generates a corresponding passive event for each user affected by the event.

<span id="_5-数据上报"></span>
# 5. Data reporting

We provide methods for automatically generating a corresponding passive event when a user triggers an active event.

In order to distinguish between active and passive events, we have added the event public property $inactive. When $inactive is true, the corresponding event is a passive event.


|**Property name** |**Data type** |**Value range** |
|---|---|---|
|$inactive |string |"True" passive event<br><br>"False" active event<br><br>Other times, it is a non\-passive event and can also be considered an active event |


<span id="android"></span>
## Android

<span id="自动生成关系事件"></span>
### Automatically generate relational events

Example code: "Associated Events"

```Plain
new ActionButton (
    "关联事件", //Related events
    new Action ()
    {
        @Override public void doAction ()
        {
            JSONObject param = new JSONObject ();
            try {
                param.put ( "video_id", Generator.getRandomNum ( 0, 10000000 ) );
                param.put ( "category", "主动被动事件" ); //active and passive events
                param.put ( "author_id", Generator.getRandomNum ( 0, 10000 ) );
                param.put ( "$inline", "true" );
                JSONArray uuid_list = new JSONArray ();
                for (int i = 0; i < Generator.getRandomNum ( 0, 10 ); i++)
                {
                    uuid_list.put ( Generator.getRandomNum ( 10000, 99999 ) );
                }
                param.put ( "$target_uuid_list", uuid_list );
            }
            catch (JSONException e)
            { e.printStackTrace (); }
            AppLog.onEventV3 ( "like", param );
        }
    }
)
```


<span id="手动上报被动事件"></span>
### Manually report passive events

Example code: "Passive events"

```Plain
new ActionButton (
    "被动事件", //passive events
    new Action ()
    {
        @Override public void doAction ()
        {
            JSONObject param = new JSONObject ();
            try {
                param.put ( "video_id", Generator.getRandomNum ( 0, 10000000 ) );
                param.put ( "category", "主动被动事件" ); //active and passive events
                param.put ( "author_id", Generator.getRandomNum ( 0, 10000 ) );
                param.put ( "$inactive", "true" );
            }
            catch (JSONException e)
            { e.printStackTrace (); }
            AppLog.onEventV3 ( "like", param );
        }
    }
)
```


<span id="ios"></span>
## iOS

<span id="示例代码：-主动事件"></span>
### Example code: "Active Events"

```Plain
[BDAutoTrack eventV3:@"like" params:@{
    @"video_title": @"Lady Gaga on Oscar",
    @"category" : @"主动被动事件", //active and passive events
    @"$inactive" : @"false"
}];
```


<span id="自动生成关系事件"></span>
### Automatically generate relational events

Example code: "Associated Events"

```Plain
[BDAutoTrack eventV3:@"like" params:@{
    @"video_title": @"Lady Gaga on Oscar",
    @"category" : @"主动被动事件", //active and passive events
    @"$inactive" : @"true",
    @"$inline": @"true",
    @"$target_uuid_list" : @[@"123", @"456", @"789"]
}];
```


<span id="手动上报被动事件"></span>
### Manually report passive events

Example code: "Passive events"

```Plain
[BDAutoTrack eventV3:@"like" params:@{
    @"video_title": @"Lady Gaga on Oscar",
    @"category" : @"主动被动事件", //active and passive events
    @"$inactive" : @"true"
}];
```


<span id="jssdk"></span>
## JSSDK

<span id="示例代码：-主动事件"></span>
### Example code: "Active Events"

```Plain
window.collectEvent('like', {
   from: "index",
   category: "主动被动事件", //active and passive events
   $inactive: "false" 
});
```


<span id="自动生成关系事件"></span>
### Automatically generate relational events

Example code: "Associated Events"

```Plain
window.collectEvent('like', {
   from: "index",
   category: "主动被动事件", //active and passive events
   $inactive: "true" ,
   $inline: "true",
   $target_uuid_list: ["123","456","789"]
});
```


<span id="手动上报被动事件"></span>
### Manually report passive events

Example code: "Passive events"

```Plain
window.collectEvent('like', {
   from: "index",
   category: "主动被动事件", //active and passive events
   $inactive: "true" ,
});
```


<span id="小程序-sdk"></span>
## Mini Program SDK

<span id="示例代码：-主动事件"></span>
### Example code: "Active Events"

```Plain
app.$$Rangers.event('like', {
    from: "index",
   category: "主动被动事件", //active and passive events
   $inactive: "false",
})
```


<span id="自动生成关系事件"></span>
### Automatically generate relational events

Example code: "Associated Events"

```Plain
app.$$Rangers.event('like', {
   from: "index",
   category: "主动被动事件", //active and passive events
   $inactive: "true" ,
   $inline: "true",
   $target_uuid_list: ["123","456","789"]
});
```


<span id="手动上报被动事件"></span>
### Manually report passive events

Example code: "Passive events"

```Plain
app.$$Rangers.event('like', {
   from: "index",
   category: "主动被动事件", //active and passive events
   $inactive: "true" 
});
```


<span id="http-api-服务端上报"></span>
## HTTP API server level reporting

<span id="示例代码：-主动事件"></span>
### Example code: "Active Events"

```Plain
{
    "user": {
        // It is recommended to first report the user_unique_id of the user on the client side, and then use it on the server side
        "user_unique_id": " 74481585297"   //user unique identifier
    },
    "header": {
        "app_channel": "App Store"   //App channel
    },
    "events": [
        {
            "event": "like",    //event name
            "params": "{
                \"category\":\"主动被动事件\", //active and passive events
                \"$inactive\":\"false\"
             }",    // event properties
            "local_time_ms": 1489573628001   //event happen time timestamp
        }
    ]
}
```


<span id="自动生成关系事件"></span>
### Automatically generate relational events

Example code: "Associated Events"

```Plain
{
    "user": {
        // It is recommended to first report the user_unique_id of the user on the client side, and then use it on the server side
        "user_unique_id": " 74481585297"   //user unique identifier
    },
    "header": {
        "app_channel": "App Store"   //App channel
    },
    "events": [
        {
            "event": "like",    //event name
            "params": "{
                \"category\":\"主动被动事件\", //active and passive events
                \"$inactive\":\"true\",
                \\"$inline\\":\\"true\\",
                \"$target_uuid_list\":[\"123\",\"456\",\"789\"]
             }",    // event properties
            "local_time_ms": 1489573628001   //event happen time timestamp
        }
    ]
}
```


<span id="手动上报被动事件"></span>
### Manually report passive events

Example code: "Passive events"

```Plain
{
    "user": {
        // It is recommended to first report the user_unique_id of the user on the client side, and then use it on the server side
        "user_unique_id": " 74481585297"   //user unique identifier
    },
    "header": {
        "app_channel": "App Store"    //App channel
    },
    "events": [
        {
            "event": "like",    //event name
            "params": "{
                \"category\":\"主动被动事件\", //active and passive events
                \"$inactive\":\"true\"
             }",    // event properties
            "local_time_ms": 1489573628001   //event happen time timestamp
        }
    ]
}
```
