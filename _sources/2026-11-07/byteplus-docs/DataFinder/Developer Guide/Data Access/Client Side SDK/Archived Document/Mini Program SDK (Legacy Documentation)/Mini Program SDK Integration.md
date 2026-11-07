---
title: "Mini Program SDK Integration"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Mini_Program_SDK_Integration_"
---

<span id="48f08aac"></span>
# Document guide

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSIxMDg1cHgiIGhlaWdodD0iNDI1cHgiIHZpZXdCb3g9Ii0wLjUgLTAuNSAxMDg1IDQyNSI+PGRlZnMvPjxnPjxwYXRoIGQ9Ik0gMjEyIDMyIEwgMjg1LjYzIDMyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjkwLjg4IDMyIEwgMjgzLjg4IDM1LjUgTCAyODUuNjMgMzIgTCAyODMuODggMjguNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjIiIHk9IjIiIHdpZHRoPSIyMTAiIGhlaWdodD0iNjAiIGZpbGw9IiM2NjY2ZmYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIwOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTdweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICNGRkZGRkY7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGZvbnQtd2VpZ2h0OiBib2xkOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5QcmVyZXF1aXNpdGVzPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDUwMiAzMiBMIDU3NS42MyAzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDU4MC44OCAzMiBMIDU3My44OCAzNS41IEwgNTc1LjYzIDMyIEwgNTczLjg4IDI4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyOTIiIHk9IjIiIHdpZHRoPSIyMTAiIGhlaWdodD0iNjAiIGZpbGw9IiM2NjY2ZmYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIwOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiAyOTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogI0ZGRkZGRjsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgZm9udC13ZWlnaHQ6IGJvbGQ7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkdldCB0byBrbm93IHRoZSBwcmVjYXV0aW9ucyBmb3IgYWNjZXNzPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDc5MiAzMiBMIDg2NS42MyAzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDg3MC44OCAzMiBMIDg2My44OCAzNS41IEwgODY1LjYzIDMyIEwgODYzLjg4IDI4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSI1ODIiIHk9IjIiIHdpZHRoPSIyMTAiIGhlaWdodD0iNjAiIGZpbGw9IiM2NjY2ZmYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIwOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiA1ODNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxN3B4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogI0ZGRkZGRjsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgZm9udC13ZWlnaHQ6IGJvbGQ7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlNESyBpbnRlZ3JhdGlvbjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iODcyIiB5PSIyIiB3aWR0aD0iMjEwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjNjY2NmZmIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAyMDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogODczcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTdweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICNGRkZGRkY7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGZvbnQtd2VpZ2h0OiBib2xkOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5UcmFja2luZyBwb2ludCB2ZXJpZmljYXRpb248L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMTA3IDE4MiBMIDEwNyAyMTMuMTMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxMDcgMjE4LjM4IEwgMTAzLjUgMjExLjM4IEwgMTA3IDIxMy4xMyBMIDExMC41IDIxMS4zOCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjIiIHk9IjEwMiIgd2lkdGg9IjIxMCIgaGVpZ2h0PSI4MCIgcng9IjEyIiByeT0iMTIiIGZpbGw9IiNkNGUxZjUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIwOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE0MnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5UaGUgZ3JvdXAgaGFzIGJlZW4gY3JlYXRlZCBhbmQgY29ubmVjdGVkIHRvIHRoZSBhcHBsaWNhdGlvbiwgYW5kIHRoZSBkZXZlbG9wbWVudCBlbmdpbmVlciBhbHJlYWR5IGhhcyB0aGUgY29ycmVzcG9uZGluZyBncm91cCBwZXJtaXNzaW9uczwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMiIgeT0iMjE5LjUiIHdpZHRoPSIyMTAiIGhlaWdodD0iODIuNSIgcng9IjEyLjM4IiByeT0iMTIuMzgiIGZpbGw9IiNkNGUxZjUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIwOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDI2MXB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5PYnRhaW4gdGhlIGFwcCBJRCBhbmQgb3RoZXIgaW5mb3JtYXRpb24gcmVxdWlyZWQgZm9yIGRhdGEgcmVwb3J0aW5nPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDM5NyAxODIgTCAzOTcgMjAyIEwgMzk3IDE5OS41IEwgMzk3IDIxMy4xMyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDM5NyAyMTguMzggTCAzOTMuNSAyMTEuMzggTCAzOTcgMjEzLjEzIEwgNDAwLjUgMjExLjM4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMjkyIiB5PSIxMDIiIHdpZHRoPSIyMTAiIGhlaWdodD0iODAiIHJ4PSIxMiIgcnk9IjEyIiBmaWxsPSIjZDRlMWY1IiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAyMDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNDJweDsgbWFyZ2luLWxlZnQ6IDI5M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5VbmRlcnN0YW5kIHRoZSBkYXRhIGZvcm1hdHMgc3VwcG9ydGVkIGJ5IGV2ZW50IGFuZCBhdHRyaWJ1dGUgcGFyYW1ldGVycyB3aGVuIHJlcG9ydGluZyBkYXRhPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDM5NyAzMDIgTCAzOTcgMzM1LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMzk3IDM0MC44OCBMIDM5My41IDMzMy44OCBMIDM5NyAzMzUuNjMgTCA0MDAuNSAzMzMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyOTIiIHk9IjIxOS41IiB3aWR0aD0iMjEwIiBoZWlnaHQ9IjgyLjUiIHJ4PSIxMi4zOCIgcnk9IjEyLjM4IiBmaWxsPSIjZDRlMWY1IiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAyMDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyNjFweDsgbWFyZ2luLWxlZnQ6IDI5M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5VbmRlcnN0YW5kIHRoZSBjdXJyZW50IGxpc3Qgb2Ygc3VwcG9ydGVkIHByZXNldCBldmVudHMgYW5kIGF0dHJpYnV0ZXM8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjI5MiIgeT0iMzQyIiB3aWR0aD0iMjEwIiBoZWlnaHQ9IjgwIiByeD0iMTIiIHJ5PSIxMiIgZmlsbD0iI2Q0ZTFmNSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMjA4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzgycHg7IG1hcmdpbi1sZWZ0OiAyOTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+VW5kZXJzdGFuZCB0aGUgY3VycmVudGx5IHN1cHBvcnRlZCB1c2VyIGlkZW50aWZpY2F0aW9uIHR5cGVzPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDY5MiAxODIgTCA2OTIgMjE1LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNjkyIDIyMC44OCBMIDY4OC41IDIxMy44OCBMIDY5MiAyMTUuNjMgTCA2OTUuNSAyMTMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSI1OTIiIHk9IjEwMiIgd2lkdGg9IjIwMCIgaGVpZ2h0PSI4MCIgcng9IjEyIiByeT0iMTIiIGZpbGw9IiNkNGUxZjUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE5OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE0MnB4OyBtYXJnaW4tbGVmdDogNTkzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkludHJvZHVjaW5nIFNESzwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA2OTIgMzAyIEwgNjkyIDM0MC42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDY5MiAzNDUuODggTCA2ODguNSAzMzguODggTCA2OTIgMzQwLjYzIEwgNjk1LjUgMzM4Ljg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iNTkyIiB5PSIyMjIiIHdpZHRoPSIyMDAiIGhlaWdodD0iODAiIHJ4PSIxMiIgcnk9IjEyIiBmaWxsPSIjZDRlMWY1IiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxOThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyNjJweDsgbWFyZ2luLWxlZnQ6IDU5M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5Jbml0aWFsaXplIFNESzwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNTkyIiB5PSIzNDciIHdpZHRoPSIyMDAiIGhlaWdodD0iNzUiIHJ4PSIxMS4yNSIgcnk9IjExLjI1IiBmaWxsPSIjZDRlMWY1IiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxOThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzODVweDsgbWFyZ2luLWxlZnQ6IDU5M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5JbnZva2UgU0RLIHJlbGF0ZWQgQVBJcyB0byBpbXBsZW1lbnQgcmVsYXRlZCBmdW5jdGlvbnM8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9Ijg3MiIgeT0iMTAyIiB3aWR0aD0iMjEwIiBoZWlnaHQ9IjgwIiByeD0iMTIiIHJ5PSIxMiIgZmlsbD0iI2Q0ZTFmNSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMjA4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTQycHg7IG1hcmdpbi1sZWZ0OiA4NzNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+VHJhY2tpbmcgcG9pbnRzIGRhdGEgdmVyaWZpY2F0aW9uPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48L2c+PC9zdmc+" />

<span id="a2399c88"></span>
# Event tracking planning

Before integrating the SDK, you need to perform event tracking planning based on your business analysis, and clarify which events and properties may require event tracking in the business indicators to be analyzed. When planning for event tracking, you need to understand some basic concepts and pre\-information such as event tracking events and properties provided by DataFinder, DataFinder's user identity logic, etc., and combine the capabilities provided by DataFinder to plan your purchase price.

<span id="53f52e34"></span>
## Basic concept


|Basic concept |Concept note |Event tracking planning and SDK integration points |Detailed guidance document |
|---|---|---|---|
|Event, event property, event public property, user property |DataFinder's user behavior data analytics is based on event + user model.<br><br><br>* Event & Event property: One or a type of behavior of the user is called an "event". Event property is the information used to describe the event, such as the form and location of the event that are synchronously collected when the event is triggered. For example, if a user purchases a product, then the user's behavior event is "Purchase", and the event property is "Product Name" , "Product Classification", "Payment Amount", etc .<br><br>* Event public properties: Refers to properties that are not strongly associated with an event and are common to multiple or all events, such as the version number of the application, device information, etc.<br><br>* User & User property: User refers to the person who occurs the event behavior. User properties refer to properties of the user's own state (independent of behavior, such as age, gender, etc.) or user\-related properties related to behavior but do not change frequently (such as VIP level, registration time, etc.). |You need to plan the events, event properties, and user properties to be collected according to the needs of business analysis. When integrating the SDK |Please see the detailed concept introduction [Data Model](https://docs.byteplus.com/docs/DataFinder/Data_Model). |
|Event tracking, full event tracking, custom event tracking |* Event tracking: Through the development of the SDK, the process of writing event logic into the code is called **event tracking**. DataFinder provides you with preset events and event properties that do not require manual event tracking, just turn on the capture switch .<br><br>* Full event tracking: is a kind of preset events and event properties provided by DataFinder. In DataFinder, the full event tracking events collected are bav2b_click button clicks and bav2b_page page browsing. No additional investment in research and development is required, but it will be at the expense of reporting a large amount of data, and only simple PV and UV can be collected, which is a bit'powerless' for the collection of rich business data.<br><br>* Code event tracking: Code event tracking refers to the development engineer who manually writes the code to implement the data collection logic according to the personalized needs of the business. Wide collection range and flexible application. However, it requires investment in research and development and requires certain technical capabilities. |It is usually recommended that you combine the preset events/properties and custom event tracking provided by DataFinder for event tracking planning. |[Event Tracking, Full Event Tracking](https://docs.byteplus.com/docs/DataFinder/Event_Tracking_Full_Event_Tracking) |


<span id="0dfd2056"></span>
## Understanding data reporting requirements (format, quantity restrictions, etc.)

When planning for event tracking, you need to be clear about the data format requirements of the events and properties to be collected and reported, as well as some restrictions on collection and reporting, so as to avoid subsequent failure to meet the requirements due to data formats, which will lead to data collection that cannot be warehoused and cannot be queried and analyzed later.

The data reported by the SDK usually has a fixed format, mainly including `user`, `header`, and `events`.


|Field |Effect |Mini Program Data Sample |
|---|---|---|
|`user` |Store user property data, such as web_id, user_unique_id these important properties. |```TypeScript```<br>```[```<br>```  {```<br>```    events: [```<br>```      {```<br>```        event: 'app_launch',```<br>```        params: '{"path":"pages/index/index",……}',```<br>```        local_time_ms: 1745897787714,```<br>```        session_id: 'd8b28410-6079-42da-***',```<br>```      },```<br>```      {```<br>```        event: 'predefine_pageview',```<br>```        params: '{"scene":1001,……}',```<br>```        local_time_ms: 1745897787756,```<br>```        session_id: 'd8b28410-6079-42da-9f91-5a49d6ffb01f',```<br>```      },```<br>```    ],```<br>```    user: {```<br>```      web_id: '7498573*****',```<br>```      user_unique_id: 'tangseng',```<br>```    },```<br>```    header: {```<br>```      app_id: *******,```<br>```      app_version: '',```<br>```      os_name: 'devtools',```<br>```      os_version: 'iOS 10.0.1',```<br>```      ……```<br>```      custom: {```<br>```        custom_platform: 'miniProduct',```<br>```        mp_platform: '0',```<br>```        mp_platform_app_version: '8.0.5',```<br>```        ……```<br>```      },```<br>```      ……,```<br>```    },```<br>```  },```<br>```]```<br> |
|`header` |Store event public property.<br><br>app_id, os_name These are preset and will be placed directly under the header. If it is the event public property you customize, it will be placed under header.custom. ||
|`events` |Store events and event properties.<br><br>It is an array that supports carrying multiple events.<br><br>Each event has event, params, local_time_ms, session_id fields, where local_time_ms, session_id are automatically generated by the SDK, and event, params are set by the business, event is the event name, and params stores the event property (the value is that the JSON object is serialized). ||


Among them, when you need to report custom events and custom properties, you need to ensure that the data format of the event and property meets the requirements. Please refer to the data format requirements and data reporting restrictions supported by the current DataFinder [Supported Data Formats and Event/Property Classification](https://docs.byteplus.com/docs/DataFinder/Supported_Data_Formats_and_Event_Property_Classification).

Common problem:


* How to report data of nested JSON type?[Example 1: How nested JSON type properties are reported and used for filtering and grouping](https://docs.byteplus.com/docs/DataFinder/Property_Custom_Grouping_and_Properties#1fafd5b2)

* Event property data type transmission error, need to modify how to do?[Q1: Event property data type transmission error, how to modify?](https://docs.byteplus.com/docs/DataFinder/Supported_Data_Formats_and_Event_Property_Classification#q1%EF%BC%9A%E4%BA%8B%E4%BB%B6%E5%B1%9E%E6%80%A7%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B%E4%BC%A0%E8%BE%93%E9%94%99%E8%AF%AF%EF%BC%8C%E9%9C%80%E8%A6%81%E4%BF%AE%E6%94%B9%E6%80%8E%E4%B9%88%E5%8A%9E%EF%BC%9F)

* The data type transmission at each end is inconsistent. How does the system handle it? How to modify?[Q2: The data type transmission at each end is inconsistent. How does the system handle it? How to modify it?](https://docs.byteplus.com/docs/DataFinder/Supported_Data_Formats_and_Event_Property_Classification#q2%EF%BC%9A-%E5%90%84%E7%AB%AF%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B%E4%BC%A0%E8%BE%93%E4%B8%8D%E4%B8%80%E8%87%B4%EF%BC%8C%E7%B3%BB%E7%BB%9F%E5%A6%82%E4%BD%95%E5%A4%84%E7%90%86%EF%BC%9F%E5%A6%82%E4%BD%95%E4%BF%AE%E6%94%B9%EF%BC%9F)


<span id="9fd87708"></span>
## Understanding user identity logic

When planning for event tracking, you need to understand the user identity logic of DataFinder, which is used to combine the user identity logic of your own business to eventually unify the source of user identity data. DataFinder defaults to the **user** as the object of statistical analysis, and defaults to using ssid as the user's unique identification ID to calculate the indicator. At this time, the user's SSID is the default statistical criteria. When your analysis object is a user, it is recommended to keep the default statistical criteria ssid, DataFinder can ID_Mapping the user's device_id/web_id, user_unique_id, etc. mapping, try to restore a real user through a ssid.


* **device_id**, **web_id**, **anonymous_id:**  Can be used as the unique ID of the device, mostly in scenarios where the user's real name ID cannot be obtained.

* **user_unique_id:**  It is the login user ID, which is mostly used in the scenario where the user's real\-name ID can be obtained. Generally, the user ID used in the product business is directly used, such as the login account. When the user_unique_id is not set, in the SaaS version, the system will automatically use device_id/web_id instead.

* **Ssid:**  for the DataFinder user statistics criteria ID, with the device identification device_id/web_id, login state user identification user_unique_id mutual Mapping, can ensure the user anonymity and real\-name status of the ID unity.


See the mapping logic for the three types of IDs and more information about user identities [Supported User Unique Identifiers](https://docs.byteplus.com/docs/DataFinder/Supported_User_Unique_Identifiers).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If there are multiple ID types for the user's real\-name ID in your business, for example, the user's real\-name information can be marked by multiple ID types such as account ID, user's mobile phone number, etc., you can also use the multi\-ID type function, see for details <a href="https://docs.byteplus.com/docs/undefined/6a4ce26a8f7714051e96f4c5">(不发布)Using Multi\-ID Types</a>.</div>



<span id="351948c9"></span>
## Understand the preset events and properties supported by the Mini Program

As mentioned above, in most business analysis scenarios, you need to combine your own business characteristics for custom event tracking planning and integration. Before that, you can first understand the preset events and preset properties currently provided by DataFinder, and combine the existing preset events and property capabilities to further plan the requirements for custom code event tracking.


* See the list of preset events and properties supported by the Mini Program [Mini Program Preset Events and Properties](https://docs.byteplus.com/docs/DataFinder/Mini_Program_Preset_Events_and_Properties).

* At the same time, you also need to pay attention to the list of currently disabled preset properties. When planning custom event tracking and properties in the future, you need to avoid the same name as the disabled properties, otherwise the data will not be reported normally. See for details [Disable Properties List](https://docs.byteplus.com/docs/DataFinder/Disable_Properties_List).


<span id="c3d7ad6a"></span>
## Understand the SDK package structure of the Mini Program

Before planning and integrating the event tracking on the Mini Program side, you can first understand the structure and capability range of the SDK package on the Mini Program side of DataFinder, so that you can have a clearer idea when planning and integrating event tracking. See below for details [参考：SDK包文件结构说明](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_Integration#1d52d44a).

<span id="27b40dbb"></span>
## Typical scene event tracking scheme reference


* [How to Sort out Requirements](https://docs.byteplus.com/docs/DataFinder/How_to_Sort_out_Requirements)

* [How to Design Event Tracking and Collection Scheme?](https://docs.byteplus.com/docs/DataFinder/How_to_Design_Event_Tracking_and_Collection_Scheme)

* [Index system demo](https://bytedance.larkoffice.com/sheets/shtcng6Cp2HHiTGGA2LPIf3Rl5e)


<span id="65a6dca5"></span>
# Preparation

<span id="f4224eb3"></span>
## Step 1 (optional): Create event tracking requirements/Enter custom event tracking

After completing the event tracking planning, it is recommended that you create the event tracking requirements according to the planning and then enter the custom event tracking into the DataFinder to complete the warehousing of the custom event tracking in the DataFinder metadata.


* Event tracking request management: You can manage event tracking requirements through DataFinder's event tracking request management function, and you can continue to maintain and manage requirements in the event tracking request management page to improve management efficiency. See the operation to create event tracking request management [Request Management](https://docs.byteplus.com/docs/DataFinder/Request_Management).

* Custom event tracking entry: You can first create custom event tracking metadata into the DataFinder according to the event tracking plan. For activity details, see [New event](https://docs.byteplus.com/docs/DataFinder/General_Events#_2-1-%E6%96%B0%E5%A2%9E%E4%BA%8B%E4%BB%B6), [Add event properties](https://docs.byteplus.com/docs/DataFinder/Event_Properties#_2-1-%E6%96%B0%E5%A2%9E%E4%BA%8B%E4%BB%B6%E5%B1%9E%E6%80%A7), [Add user properties](https://docs.byteplus.com/docs/DataFinder/User_Properties#533b53ea).


<span id="8c5ac3ed"></span>
## Step 2: Obtain the APPID


* In the SaaS\-cloud native scenario, you can find the corresponding application in "Project Center" \> "Project Management" \> "Project Details", click "Access Data", and view the application ID (APPID) and APP URL of the application in the application details. For details, please refer to [Project Management](https://docs.byteplus.com/docs/DataFinder/Project_Management__).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c52873d5e5ef4d7da390c4c102215d88~tplv-goo7wpa0wc-image.image) </span>


<span id="f22345a9"></span>
## Step 3: Obtain the reporting address and configure the Mini Program whitelist

When reporting data access, you need to confirm your data reporting address according to the current environment type and terminal type, and add the data reporting address to the "request legal domain name" in the background of the Mini Program. If the reporting address is set incorrectly, you will not be able to report and query the data normally in the future.

<span id="c60485e9"></span>
### Get the data reporting address

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Please confirm the type of environment you are currently using before reporting data, and configure the reporting address according to the type of environment. To view the current environment type see <a href="https://docs.byteplus.com/docs/DataFinder/SaaS_Cloud-Native_Privatized_Environments">SaaS Cloud\-Native & Privatized Environments</a>.</div>


* <div data-tips="true" data-tips-type="warning">If you are using a SaaS\-cloud native environment, you also need to confirm the region where your service is located, and report the address according to the region configuration (usually your service will be in Southeast Asia \- Johor region, and some users may use other regions). SaaS\-cloud native users see the region where the service is located <a href="https://docs.byteplus.com/docs/DataFinder/Supported_Regions">Supported Regions</a>.</div>



<span id="c6ceef44"></span>
#### SaaS\-cloud\-native


|End type |SaaS\-cloud native<br><br>(Overseas: Southeast Asia \- Johor) |Overseas BytePlus environment<br><br>(The following SG refers to Singapore) |
|---|---|---|
|Mini Program |* https://gator.uba.ap\-southeast\-1.bytepluses.com<br><br>* To add a whitelist to the Mini Program: https://gator.uba.ap\-southeast\-1.bytepluses.com |* `channel: 'sg'`<br><br>* To add a whitelist to the Mini Program: https://mcs.tobsnssdk.com |


<span id="e4ee0e62"></span>
#### Privatized environment

In the private deployment scenario, you need to obtain the data upload address that you plan and configure when deploying the private environment, and add the data reporting domain name of the private deployment to the "request legal domain name" in the background of the Mini Program. If you are unsure of this address, please contact your project manager or customer success manager.

<span id="bfd65b0d"></span>
### Configure Mini Program Whitelist

For configuration in "Mini Program Background \- Development \- Development Settings \- Server Domain Name", please refer to the corresponding official documentation of the Mini Program, such as the [WeChat Mini Program documentation](https://developers.weixin.qq.com/miniprogram/en/dev/framework/ability/network.html).

<span id="e729856a"></span>
# Integrated SDK

<span id="d42f309d"></span>
## (Optional) Download sample demo

The following provides you with a simple Mini Program development kit as an example demo. The following SDK integration instructions are also based on this demo. You can download the demo file to learn about the integration operations of the Mini Program SDK.

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b17c5a293d2d4a168da47c171de9dd82~tplv-goo7wpa0wc-image.image" name="demo.zip">demo.zip</Attachment>


&nbsp;

<span id="3d277fbe"></span>
## Install the SDK

You can install the Data Transmission Service SDK on the Mini Program side using npm.


|Operation guidance |Operation screen recording |
|---|---|
|```SQL```<br>```npm install @datarangers/sdk-mp```<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Please execute npm related commands in the "end point" panel of the Mini Program developer tools. If you prompt an error message such as command does not exist when executing npm, please install node first (for details on how to install node, please refer to the documentation on node's official website).</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If the project itself does not support the installation of third\-party npm packages, you can use the npm init related command to make the project support the installation of third\-party npm packages.</div><br> |<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49dbfc29c0d74afaad4118847f0bb8d6~tplv-goo7wpa0wc-image.image" controls></video><br> |


<span id="2feae1e4"></span>
## Initializing the SDK: Native Platform

When initializing the SDK, you usually need to call the core API of the SDK (init, conf, event, etc.) to collect and report preset events and property data, collect and report custom events and data, and define user ID identification fields. The following are examples of Mini Program native platform scenarios and TypeScript type projects to gradually demonstrate the code access to initialize the SDK in most scenarios.

<span id="eaa78476"></span>
### Import and initialize

Locate the ingress file, such as app.ts in the demo, and embed the following code to initialize the SDK before the app global configuration in the ingress file.


|Operation guidance |Operation screen recording |
|---|---|
|```TypeScript```<br>```import $$sdk from '@datarangers/sdk-mp';```<br>``````<br>```$$sdk.init({```<br>```    app_id: 1338,```<br>```    log: true,```<br>```});```<br>```$$sdk.send();```<br>``````<br>```App({```<br>```    //...```<br>```});```<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Operation points:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If you are prompted with an error such as "Could not find @datarangers/sdk\-mp", you need to execute "build npm".</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you get an error such as "Export is not supported", you need to check "Compile JS to ES5" in the local settings under the details of developer tools.</div><br> |<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/04445dd55f894ae9aaa92b42225ceaf6~tplv-goo7wpa0wc-image.image" controls></video><br> |



* Involving the core API:

   * Init: Initialize the SDK instance. The init interface needs to specify the appid information of the data report, and configure whether to turn on the log and other initialization parameters. Please refer to the parameter introduction of the full init interface [init](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_API_Description#b83be19a).

   * Send: After the init initialization call, the send method needs to be called before the SDK starts reporting events. No events are reported until the send method is called. See more about the send method [send](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_API_Description#43b682a2).

* More scene practice references:

   * [How to use it in special environments](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_Integration_Scenario_Practice#34266c0b)


<span id="29f56fe4"></span>
### Report a preset event

According to the event tracking plan, if you need to collect the preset event and preset property data supported by the DataFinder, you need to turn on the "Report preset event" switch when initializing the SDK, that is, the value of the configuration `auto_report`field is `true`.


|Operation guidance |Operation screen recording |
|---|---|
|```TypeScript```<br>```import $$sdk from '@datarangers/sdk-mp';```<br>``````<br>```$$sdk.init({```<br>```    app_id: 1338,```<br>```    log: true,```<br>```    auto_report: true,```<br>```});```<br>```$$sdk.send();```<br>``````<br>```App({```<br>```    //...```<br>```});```<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Operation points:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If you prompt an error such as "export is not supported", you can consider checking "do not verify legal domain names,..." in the local settings under the details of the developer tools during the development stage, but you must be sure to configure legal domain names in the WeChat Mini Program management background when going online.</div><br> |<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe7f98550d2d4e43b3f90a6ddb49781e~tplv-goo7wpa0wc-image.image" controls></video><br> |



* Involving the core API:

   * Init: If you need to capture the preset events and properties reported to you by DataFinder, you need to configure the value of the `auto_report`field to `true`in the init interface. Please refer to the parameter introduction of the full init interface [init](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_API_Description#b83be19a).

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The collection application of some preset events needs to set the switch separately, such as full event tracking preset events, etc. For details, please refer to the corresponding preset event description document.      </div>
      

* More scene practice references:

   * [Enable preset event reporting](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_Integration_Scenario_Practice#7ee332b7)

   * [Add custom properties to preset events](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_Integration_Scenario_Practice#5da28458)

   * [Set event public properties](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_Integration_Scenario_Practice#19a0bfde)

   * [Full Event Tracking Preset Events and Properties](https://docs.byteplus.com/docs/DataFinder/Full_Event_Tracking_Preset_Events_and_Properties)


<span id="de8981da"></span>
### Reporting customs events

According to the event tracking plan, if you need to collect and report custom events, you can call the "event" method to set the custom event name and event properties.

Usually we may need to report custom events on multiple pages of the Mini Program. For the convenience of using the SDK instance $$sdk on other pages of the Mini Program, consider mounting the SDK instance $$sdk on the App object. For example, to report a custom event on a page (such as pages/index/index.ts in the demo example), you can get the global object through getApp, then use the $$sdk mounted on it and call the event method.


|Operation guidance |Operation screen recording |
|---|---|
|1. Initialize in the main entry file (app.ts file in the demo), similar to the above steps, and additionally mount the SDK instance $$sdk onto the App object.<br><br>   ```TypeScript```<br>```   import $$sdk from '@datarangers/sdk-mp';```<br>```   ```<br>```   $$sdk.init({```<br>```       app_id: 1338,```<br>```       log: true,```<br>```       auto_report: true,```<br>```   });```<br>```   $$sdk.send();```<br>```   ```<br>```   App({```<br>```       $$sdk,```<br>```       //...```<br>```   });```<br>```   ```<br>   <br><br>2. In a separate page (where type.ts is newly created), use the $$sdk mounted in the main entry file and call the event method to report custom events and event properties.<br><br>   ```TypeScript```<br>```   const app = getApp()```<br>```   ```<br>```   Component({```<br>```       data: {```<br>```           //...```<br>```       },```<br>```       methods: {```<br>```           bindViewTap() {```<br>```               app.$$sdk.event('test', {```<br>```                   abc: 123,```<br>```               });```<br>```           }```<br>```       }```<br>```   });```<br>```   ```<br>    |<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83a6ff4f2c7d42ada3163a7cf63f9572~tplv-goo7wpa0wc-image.image" controls></video><br> |



* Operation points:

   * If the project itself is a Typescript type and you encounter type problems when mounting $$sdk on the app, you can consider extending the type, such as creating a new type.d.ts type file for easy use everywhere, where the type definition is similar to this. (This extension type handling is not necessary, unless the project's type requirements directly affect the compilation.)

      ```TypeScript
      import SDK from '@datarangers/sdk-mp/sdk.d';
      export type NewIAppOption = IAppOption & {
        $$sdk: SDK,
      }
      ```
      

* Involving the core API:

   * Event: Use the event method to report custom events. This method supports single event mode and batch event mode reporting. The above is an example of a single event reporting. For more event interface parameter descriptions and usage examples, please see [event](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_API_Description#68e73ad4).

* More scene practice references:

   * [Set event public properties](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_Integration_Scenario_Practice#19a0bfde)


<span id="bb21600c"></span>
### Set up a custom user

If you need to set a custom user, you can call the config method to set user_unique_id property.

Usually, when a user needs to log in with a real name, the business will use an ID to uniquely identify the user. You can report the user ID of the corresponding business through the config method and report it as the value of the user_unique_id. Usually, this value can be obtained through the service interface, or an existing fixed user identification ID value can be directly read. The following fixed value is reported as an example.


|Operation guidance |Operation screen recording |
|---|---|
|```TypeScript```<br>```import $$sdk from '@datarangers/sdk-mp';```<br>``````<br>```$$sdk.init({```<br>```    app_id: 1338,```<br>```    log: true,```<br>```    auto_report: true,```<br>```});```<br>```$$sdk.send();```<br>``````<br>```App({```<br>```    $$sdk,```<br>```    //...```<br>```    onLaunch() {```<br>```        // ...```<br>```        //Assuming that the set value is tangseng, this value in the real scenario is generally obtained from the service interface of the business```<br>```        $$sdk.config({```<br>```            user_unique_id: 'tangseng'```<br>```        });```<br>```    }```<br>```});```<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can view the storage value of "_<em>tea_cache_tokens</em> ${app_id}" in the Storage panel under the Debugger in the Developer Tools, and you can see the value set to user_unique_id.</div><br> |<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a49ef27c6654be2a6fca5a692c226c3~tplv-goo7wpa0wc-image.image" controls></video><br> |



* The core API is involved: you can set the user's business identity ID through the config method.

* More scene practice references:


<span id="d99c56a0"></span>
### Set up a reporting domain name

If your current environment is a SaaS\-cloud native environment or a private environment, you need to set the data reporting domain name of the corresponding environment, that is, set the channel_domain at initialization. If the settings are incorrect, the data will not be able to be queried and analyzed normally.


|Operation guidance |Operation screen recording |
|---|---|
|```TypeScript```<br>```import $$sdk from '@datarangers/sdk-mp';```<br>``````<br>```$$sdk.init({```<br>```    app_id: 1338,```<br>```    Assuming a cloud-native environment```<br>```    channel_domain: 'https://gator.volces.com',```<br>```    log: true,```<br>```    auto_report: true,```<br>```});```<br>```$$sdk.send();```<br>``````<br>```App({```<br>```    $$sdk,```<br>```    //...```<br>```    onLaunch() {```<br>```        // ...```<br>```        //Assuming that the set value is tangseng, this value in the real scenario is generally obtained from the service interface of the business```<br>```        $$sdk.config({```<br>```            user_unique_id: 'tangseng'```<br>```        });```<br>```    }```<br>```});```<br> |<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/716d94be05f841e1a063b90f4ef0c3f1~tplv-goo7wpa0wc-image.image" controls></video><br> |



* Operation points:

* Involving the core API:


<span id="30617339"></span>
## Initializing the SDK: A Tripartite Framework

If you are not using a native platform, but a Mini Program application developed with a three\-party framework, you can refer to the following SDK initialization schemes for different frameworks for SDK initialization operations. The operation concept is similar to that of the native platform. The operation core points and demonstration screen recordings are as follows.

<span id="783dee12"></span>
### Taro Framework


* Demo download:

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2a48c41a37a4e769dc2d00a1f1a3d7b~tplv-goo7wpa0wc-image.image" name="taro-demo.zip">taro-demo.zip</Attachment>
   

* Initialization example code:

   
   |Operation guidance |Operation screen recording |
   |---|---|
   |```TypeScript```<br>```import { PropsWithChildren } from 'react'```<br>```import { useLaunch } from '@tarojs/taro'```<br>```import './app.scss'```<br>``````<br>```import $$sdk from '@datarangers/sdk-mp';```<br>```$$sdk.init({```<br>```    app_id: 0000, Please use the appropriate app_id```<br>```    Assuming a cloud-native environment```<br>```    channel_domain: 'https://gator.volces.com',```<br>```    log: true,```<br>```    auto_report: true,```<br>```});```<br>```$$sdk.send();```<br>``````<br>```function App({ children }: PropsWithChildren<any>) {```<br>```  useLaunch(() => {```<br>```    console.log('App launched.')```<br>``````<br>```    $$sdk.event('test', {```<br>```      abc: 123,```<br>```    })```<br>```  })```<br>``````<br>```  return children```<br>```}```<br>``````<br>``````<br>```export default App```<br> |<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c1e43ac14304e3e8f8b417b2e292d66~tplv-goo7wpa0wc-image.image" controls></video><br> |
   


<span id="ec0ee2e5"></span>
### uni\-app framework


* Demo download:

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/82e07096081d4965bfc30736e7e63324~tplv-goo7wpa0wc-image.image" name="uniapp-demo.zip">uniapp-demo.zip</Attachment>
   

* Initialization example code:

   
   |Operation guidance |Operation screen recording |
   |---|---|
   |```TypeScript```<br>```import App from './App'```<br>``````<br>```import $$sdk from '@datarangers/sdk-mp';```<br>```$$sdk.init({```<br>```    //This is a demo app_id, please use your own app_id```<br>```    app_id: 0000,```<br>```    Assuming a cloud-native environment```<br>```    channel_domain: 'https://gator.volces.com',```<br>```    log: true,```<br>```    auto_report: true,```<br>```});```<br>```$$sdk.send();```<br>``````<br>```// #ifndef VUE3```<br>```import Vue from 'vue'```<br>```import './uni.promisify.adaptor'```<br>```Vue.config.productionTip = false```<br>```App.mpType = 'app'```<br>```const app = new Vue({```<br>```  ...App```<br>```})```<br>```app.$mount()```<br>```// #endif```<br>``````<br>```// #ifdef VUE3```<br>```import { createSSRApp } from 'vue'```<br>```export function createApp() {```<br>```  const app = createSSRApp(App)```<br>```  return {```<br>```    app```<br>```  }```<br>```}```<br>```// #endif```<br> |<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c77fdcfe650242d885a2592e7a57d857~tplv-goo7wpa0wc-image.image" controls></video><br> |
   


<span id="2c3b047a"></span>
## Initial result verification

When initializing the SDK, you can enable `log: true`, which will print some running status information of the SDK on the console. Can be used to verify whether the initialization was successful


1. In the Console panel of the Mini Program power builder, filter by entering the `emit`keyword in the filter box. If there is a log of `emit $ready`, it means that the SDK initialization is successful.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f869155cd2d749cea7535846a940b67e~tplv-goo7wpa0wc-image.image" width="946px" />   </div>
   

2. In the Network panel, you can see the event report request for the SDK, indicating that the SDK initialization was successful. At the same time, observe that the Request Payload of the request is normal, and the Response Body `message: "success"`indicates that the event was reported successfully.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/849031cd66c94a30842f83f87ea82c30~tplv-goo7wpa0wc-image.image" width="995px" />   </div>
   

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84fec94982c7402da8b172256f85e2ba~tplv-goo7wpa0wc-image.image" width="993px" />   </div>
   

3. In addition, in the Storage panel, you can see the token stored by the SDK, the key is called `__tea_cache_tokens_ ${app_id}`.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/57820fb8ea6f42b282b3d01314aeae41~tplv-goo7wpa0wc-image.image" width="1000px" />   </div>
   


<span id="46f2518e"></span>
# Event tracking data validation

After the event is reported, you can view the specific user's behavior flow on the `user review`page in the `growth analysis platform`, and you can see each event and property. If you can see the corresponding event here, it indicates that the event was successfully reported. By observing the properties of the event, you can confirm whether the corresponding properties were also successfully reported.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6c7a985fb3804a218b26ec91171cf2b2~tplv-goo7wpa0wc-image.image" width="2460px" /></div>


<span id="5a102c32"></span>
# Mini Program SDK API List
