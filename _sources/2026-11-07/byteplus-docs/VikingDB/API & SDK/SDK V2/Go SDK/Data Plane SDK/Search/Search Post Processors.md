---
title: "Search Post Processors"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Search_Post_Processors"
---

**Position of current search capability in the search paradigm:** 

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSIxMDg1cHgiIGhlaWdodD0iMzU1cHgiIHZpZXdCb3g9Ii0wLjUgLTAuNSAxMDg1IDM1NSI+PGRlZnMvPjxnPjxyZWN0IHg9IjEwMiIgeT0iMiIgd2lkdGg9IjQyMCIgaGVpZ2h0PSIyNDAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA2MiAxMjIgTCAxMTUuNjMgMTIyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMTIwLjg4IDEyMiBMIDExMy44OCAxMjUuNSBMIDExNS42MyAxMjIgTCAxMTMuODggMTE4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZWxsaXBzZSBjeD0iMzIiIGN5PSIxMjIiIHJ4PSIzMCIgcnk9IjMwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA1OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEyMnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5xdWVyeTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAyNDIgMTIyIEwgMjYyIDEyMiBMIDI1MiAxMjIgTCAyNjUuNjMgMTIyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjcwLjg4IDEyMiBMIDI2My44OCAxMjUuNSBMIDI2NS42MyAxMjIgTCAyNjMuODggMTE4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIxMjIiIHk9IjkyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEyMnB4OyBtYXJnaW4tbGVmdDogMTIzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPuajgOe0ojwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAzOTIgMTIyIEwgNDI1LjYzIDEyMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDQzMC44OCAxMjIgTCA0MjMuODggMTI1LjUgTCA0MjUuNjMgMTIyIEwgNDIzLjg4IDExOC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMjcyIiB5PSI5MiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEyMnB4OyBtYXJnaW4tbGVmdDogMjczcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPmZpbHRlciDov4fmu6Q8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjEwMiIgeT0iOSIgd2lkdGg9IjEwMCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogOThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxOXB4OyBtYXJnaW4tbGVmdDogMTAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPuS4jeWujOWFqOmhuuW6j+aJp+ihjDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA1MDIgMTIyIEwgNTM1LjYzIDEyMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDU0MC44OCAxMjIgTCA1MzMuODggMTI1LjUgTCA1MzUuNjMgMTIyIEwgNTMzLjg4IDExOC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGVsbGlwc2UgY3g9IjQ2NyIgY3k9IjEyMiIgcng9IjM1IiByeT0iMzUiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNjhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMjJweDsgbWFyZ2luLWxlZnQ6IDQzM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5wb3N0X3Byb2Nlc3M8YnIgLz5faW50cHV0X2xpbWl0PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI1NDIiIHk9IjIiIHdpZHRoPSIyOTAiIGhlaWdodD0iMjQwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNjkyIDU5IEwgNzIyIDU5IEwgNzIyIDEyMiBMIDc0NS42MyAxMjIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA3NTAuODggMTIyIEwgNzQzLjg4IDEyNS41IEwgNzQ1LjYzIDEyMiBMIDc0My44OCAxMTguNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjU3MiIgeT0iMjkiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0iI2ZmZTU5OSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA1OXB4OyBtYXJnaW4tbGVmdDogNTczcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPuWIhuaVsOWKoOadg+iejeWQiDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA2OTIgMTkyIEwgNzIyIDE5MiBMIDcyMiAxMjIgTCA3NDUuNjMgMTIyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzUwLjg4IDEyMiBMIDc0My44OCAxMjUuNSBMIDc0NS42MyAxMjIgTCA3NDMuODggMTE4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSI1NzIiIHk9IjE2MiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZmZlNTk5IiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE5MnB4OyBtYXJnaW4tbGVmdDogNTczcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPumikeeOh+aOp+WItjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNTQyIiB5PSI5IiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA5OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE5cHg7IG1hcmdpbi1sZWZ0OiA1NDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+5ZCO572u5aSE55CG566X5a2QPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDY5MiAxMjIgTCA3NDUuNjMgMTIyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzUwLjg4IDEyMiBMIDc0My44OCAxMjUuNSBMIDc0NS42MyAxMjIgTCA3NDMuODggMTE4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSI1NzIiIHk9IjkyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmU1OTkiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTIycHg7IG1hcmdpbi1sZWZ0OiA1NzNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+5YWz6ZSu6K+N6L+H5rukPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDgxMiAxMjIgTCA4NTUuNjMgMTIyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gODYwLjg4IDEyMiBMIDg1My44OCAxMjUuNSBMIDg1NS42MyAxMjIgTCA4NTMuODggMTE4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZWxsaXBzZSBjeD0iNzgyIiBjeT0iMTIyIiByeD0iMzAiIHJ5PSIzMCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA1OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEyMnB4OyBtYXJnaW4tbGVmdDogNzUzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPnJlcmFuay48YnIgLz5pbnB1dF9saW1pdDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA5ODIgMTIyIEwgMTAxNS42MyAxMjIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxMDIwLjg4IDEyMiBMIDEwMTMuODggMTI1LjUgTCAxMDE1LjYzIDEyMiBMIDEwMTMuODggMTE4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSI4NjIiIHk9IjkyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTIycHg7IG1hcmdpbi1sZWZ0OiA4NjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+UmVyYW5rPGJyIC8+KOS7heeUqOS6juWkmuaooeaAgeajgOe0oik8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxlbGxpcHNlIGN4PSIxMDUyIiBjeT0iMTIyIiByeD0iMzAiIHJ5PSIzMCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMjJweDsgbWFyZ2luZy1sZWZ0OiAxMDIzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPmxpbWl0PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI5MDkiIHk9IjI5MiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0idmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzAycHg7IG1hcmdpbi1sZWZ0OiA5MTBweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+5Y+v6YCJPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI5MDkiIHk9IjMxMiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMyMnB4OyBtYXJnaW4tbGVmdDogOTEwcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPuW/hemAiTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iOTUyIiB5PSIyOTUiIHdpZHRoPSIzMCIgaGVpZ2h0PSIxNSIgcng9IjIuMjUiIHJ5PSIyLjI1IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9Ijk1MiIgeT0iMzE0LjUiIHdpZHRoPSIzMCIgaGVpZ2h0PSIxNSIgcng9IjIuMjUiIHJ5PSIyLjI1IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9Ijg5MiIgeT0iMzMyIiB3aWR0aD0iNTciIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA1NXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDM0MnB4OyBtYXJnaW4tbGVmdDogODkzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPuW9k+WJjeeOr+iKgjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iOTUyIiB5PSIzMzQuNSIgd2lkdGg9IjMwIiBoZWlnaHQ9IjE1IiByeD0iMi4yNSIgcnk9IjIuMjUiIGZpbGw9IiNmZmU1OTkiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjwvZz48L3N2Zz4=" />

Search post\-processing operators are a **post\-processing capability (PostProcess)**  provided by VikingDB, used for further filtering and optimization of candidate data after **recall and scalar filtering** in search, ensuring that the final returned search results are more accurate and efficient.

In VikingDB, post\-processing operators can be used for:


* **Scalar weight fusion:**  Fusion sorting based on business requirements combined with data temporal/spatial information, fusing scores from multiple custom business metrics to generate a final ranking score that better aligns with business needs, ensuring recall ranking results meet business expectations.

* **Precise result filtering:**  Set filtering rules through regex matching based on business requirements, such as filtering products containing specific characteristic text information, ensuring users obtain valid search results.

* **Data quality improvement:**  Use regex matching to perform format validation on search results, filter data containing special characters, illegal content, or advertising information, ensuring returned content meets standards and improving data standardization.

* **Search result balancing:**  Set frequency limits for specific fields to prevent certain values from dominating search results, such as overexposure of popular brands, popular authors, or specific categories, ensuring diversity and fairness in search results.


**Post\-processing operators are common search parameters that can be applied to vector search, multimodal search, and other capabilities.** 

<span id="request-parameters"></span>
# Request Parameters

Based on vector search requests, you can specify the **`postProcessOps`**, **`postProcessInputLimit`** sub\-parameters in the `search` request parameters to configure post\-processing operators.


|Operator |Applicable Field Type |Description |Example |
|---|---|---|---|
|score_fusion |string |Score fusion operator, used to fuse scores from specified temporal/spatial scalars. |`Scala <br> { <br> "op": "score_fusion", <br> "fusion_by": "add", <br> "addition_score_weight": 0.6, // The weight of the additional score is 0.6; the weight of the ANN score is 1-0.6=0.4 <br> "addition_score": [ <br> { <br> "factor": 1.0, <br> "base_value_from": "scalar_field", <br> "field": "f_sales" <br> }, <br> { <br> "factor": -10.0, // Products with more complaints should have lower scores <br> "base_value_from": "scalar_field", <br> "field": "f_complain" <br> } <br> ] <br> { <br>` |
|string_contain |string |Keyword matching filter operator. Indicates the field content contains the pattern. |`JSON <br> { <br> "op": "string_contain", <br> "field": "name", <br> "pattern": "bar" <br> } <br>` |
|string_match |string |Regex matching filter operator. |`JSON <br> { <br> "op": "string_match", <br> "field": "name", <br> "pattern": "^[0-9A-Za-z_]+$" <br> } <br>` |
|enum_freq_limiter |string |Frequency control operator. Used to ensure that in a single recall result, the total count of a specific value does not exceed the `threshold` number of times. |`JSON <br> { <br> "op": "enum_freq_limiter", <br> "field": "city" <br> "threshold": 5 <br> } <br>` |


<span id="score-fusion-operator-introduction"></span>
# Score Fusion Operator Introduction

Score weighted fusion (Score Fusion) is a powerful search post\-processing capability that allows fusing scores from multiple custom business metrics on top of vector search (ANN) scores, generating a final ranking score that better aligns with business needs. The final ranking and scores of `search` results are calculated based on this. This feature tightly combines vector similarity with business logic through a flexible weighted formula.

<span id="core-formula"></span>
## Core Formula

The final score calculation follows this core formula:

`final_score = origin_score * (1 - weight) + addition_score * weight`


* **origin_score**: The original vector search (ANN) score.

* **addition_score**: Additional score items, summed from a set of custom business metric scores, allowing injection of multi\-dimensional business logic such as timeliness, popularity, authority, user ratings, etc.

* **weight**: Weight used to adjust the influence of addition_score, with a value range of `(0, 1)`. Default value is 0.5.

* Additionally, note that normalization is enabled by default, scaling `origin_score` and `addition_score` to the `(0,1)` interval. When you need to fuse raw scores with different distributions and business scores, it is recommended to enable this feature for more stable and predictable results. The normalized score calculation formula is as follows:


`final_score = normed1(origin_score) * (1 - weight) + normed2(addition_score) * weight`

<span id="calculation-method-for-addition-score"></span>
## Calculation Method for addition_score

`addition_score` is an accumulated value derived from summing one or more `addition_item_score`:

`addition_score = Σ (addition_item_score)`

Each `addition_item_score` represents an independent business bonus item, calculated as:

`addition_item_score = factor * base_value`


* **factor**: Multiplier used to scale or reverse the influence of `base_value`. Can be set to a positive number for bonuses, or a negative number for downgrading or penalties. Default is 1.

* **base_value**: Base score, the raw value of business metrics. It can be sourced in two ways:

   1. **Direct value (** **`scalar_field`** **)** : Directly use the numeric value of the scalar field in the document as `base_value`. Suitable for scenarios like "likes count", "sales volume" where business value can be directly quantified.

   2. **Decay function (** **`decay_func`** **)** : Based on the value of the scalar field, calculate a `base_value` within the `(0,1)` interval through a decay function (Gaussian, exponential, linear). Suitable for scenarios related to proximity to a certain "center point", such as "publish time".


Through this layered design, the score weighted fusion feature provides a highly flexible and powerful tool to optimize the ranking of search results, making them not only relevant but also more business\-value oriented.

<span id="score-fusion-parameter-configuration"></span>
## score_fusion Parameter Configuration


|Parameter Name |Type |Required |Sub\-parameter |Type |Required |Description |
|---|---|---|---|---|---|---|
|op |string |Yes | | | |Fill in `score_fusion` |
|fusion_by |string |Yes | | | |Fill in `add` or `multiply`. Indicates the algorithm for fusing the original score origin_score (vector search score or keyword search score) with custom additional scores (addition_score).<br><br><br>* `add`: Final `score = (1-addition_score_weight) * origin_score + addition_score_weight * addition_score`<br><br>* `multiply`: Final `score = origin_score * addition_score` |
|addition_score_weight |float |No | | | |Weight used to adjust the influence of addition_score, value range (0,1), open interval, default value 0.5. Takes effect when fusion_by is `add`. |
|addition_score |list |Yes | | | |Additional score items, summed from a set of custom business metric scores, allowing injection of multi\-dimensional business logic such as timeliness, popularity, authority, user ratings, etc.<br><br>Custom addition_score content. The final addition_score value is obtained by accumulating the values of each addition_item. |
| | | |factor |float |No |Coefficient. Defaults to 1 if not filled. Cannot be 0, absolute value cannot exceed 1000000 |
| | | |base_value_from |string |Yes |Fill in `scalar_field` or `decay_func`<br><br><br>* `scalar_field`: Directly take value from scalar field. Supports scalar fields of float32 or int64 type in the dataset.<br><br>* `decay_func`: Calculate decay function using scalar field. Supports scalar fields of float32, int64, date_time, or geo_point type in the dataset. |
| | | |field |string |Yes |Value field. Supported field types see description of `base_value_from`. |
| | | |func |string |Required when `base_value_from` is `decay_func` |Type of decay function. Only takes effect when `base_value_from` is filled with `decay_func`.<br><br><br>* `linear`: Linear decay function<br><br>* `exp`: Exponential decay function<br><br>* `gauss`: Gaussian decay function |
| | | |scale |any |Required when `base_value_from` is `decay_func` |Characterizes the decay amplitude of the decay function. Indicates that when the input parameter value is scale, the decay function result is 0.5. Only takes effect when `base_value_from` is filled with `decay_func`. For time and geography related input formats, refer to [20250813【Technical Solution】Vector Library - Support for Temporal and Spatial Type Fields](https://bytedance.larkoffice.com/wiki/KKbHwd4mTiNIWDkh5vVc7whinhh)<br><br><br>* When field is a float32 or int64 type field, fill scale with float.<br><br>* When field is a date_time type field, fill scale with time period format.<br><br>* When field is a geo_point type field, fill scale with geographic distance format. |
| | | |origin |any |Optional when `base_value_from` is `decay_func` |Reference value for the decay function. Only takes effect when `base_value_from` is filled with `decay_func`.<br><br><br>* When field is a float32 or int64 type field, fill origin with float, or defaults to 0 if not filled<br><br>* When field is a date_time type field, fill origin with date_time format, or defaults to the real\-time time of the current search if not filled.<br><br>* When field is a geo_point type field, origin is required and must be in geo_point format. |
| | | |offset |any |Optional when `base_value_from` is `decay_func` |Tolerance distance for the decay function. Only takes effect when `base_value_from` is filled with `decay_func`.<br><br><br>* When field is a float32 or int64 type field, fill offset with float, or defaults to 0 if not filled.<br><br>* When field is a date_time type field, fill offset with time period format, or defaults to 0 if not filled.<br><br>* When field is a geo_point type field, fill offset with geographic distance format, or defaults to 0 if not filled. |
| | | |decay |float |No |Value range (0, 1), open interval. Used in conjunction with scale. Default 0.5. |
|normalize_for_origin_score |Normalize (parameter structure see below) |No | | | |Normalization configuration for origin_score. If not filled, normalization using `arctan` is used by default, with arctan_factor=1, arctan_offset=0 |
|normalize_for_addition_score |Normalize (parameter structure see below) |No | | | |Normalization configuration for addition_score. If not filled, normalization using `arctan` is used by default, with arctan_factor=1, arctan_offset=0 |



* **Normalize Parameter Structure**



|Parameter Name |Type |Required |Description |
|---|---|---|---|
|enable |bool |Yes |Whether to perform normalization. Default is true.<br><br>If false, normalization is not performed, and the following parameters do not take effect. |
|func |string |No |Normalization function. Takes effect if enable=true, values are `min_max` or `arctan`, default `arctan`.<br><br><br>* `min_max`: result = (x \- min_value) / (max_value \- min_value)<br><br>* `arctan`: result = (arctan(arctan_factor \* (x \- arctan_offset)) / π) + 0.5 |
|arctan_factor |float |No |Default 1. Only takes effect when normalization function is `arctan`. Cannot be 0, absolute value cannot exceed 1000000 |
|arctan_offset |float |No |Default 0. Only takes effect when normalization function is `arctan`. |


<span id="what-is-a-decay-function"></span>
## What is a Decay Function?

There are 3 main types: *Linear decay function, Exponential decay function, Gaussian decay function*, but their **input parameters** and **output** forms are completely consistent.

<span id="input-parameters"></span>
#### **Input Parameters**


|Parameter Name |Type |Value Range |Required |Meaning |
|---|---|---|---|---|
|distance |float |(\-∞,﹢∞) |Yes |Scalar field value. For example, the timestamp field value of a piece of data is 1750671188. |
|origin |float |(\-∞,﹢∞) |No |Origin. The reference baseline. When calculating the function, the actual distance is abs(distance \- origin). For example, using the time of search as a baseline, can be set to time.now().timestamp() |
|scale |float |(0, ﹢∞) |Yes |Scale. Defines the distance from origin + offset, at which distance the calculated score will equal the decay parameter. The larger the scale, the slower the decay. |
|decay |float |(0,1) |No |Decay parameter. Defines how to proportionally score documents based on the given distance. When the actual distance value is scale, the decay function value is exactly decay. The closer decay is to 1, the slower the decay. Default 0.5. |
|offset |float |[0,﹢∞) |No |Offset amount. The decay function will only calculate the decay function for documents with distances greater than the defined offset. Default value is 0. |


<span id="decay-characteristics"></span>
#### Decay Characteristics

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cdd0de8589f444e3bd6b62ac1a9d8562~tplv-goo7wpa0wc-image.image) </span>

<span id="formula-introduction"></span>
#### Formula Introduction

```Python
import numpy as np

def gaussian_decay(origin, scale, decay, offset, distance):
    """Gaussian decay function"""
    adjusted_dist = max(0, abs(distance - origin) - offset)
    sigma_square = (scale ** 2) / (-2*np.log(decay))
    exponent = -(adjusted_dist ** 2) / (2 * sigma_square)
    return np.exp(exponent)


def exp_decay(origin, scale, decay, offset, distance):
    """Exponential decay function"""
    adjusted_dist = max(0, abs(distance - origin) - offset)
    lambda_val = np.log(decay) / scale
    return np.exp(lambda_val * adjusted_dist)


def linear_decay(origin, scale, decay, offset, distance):
    """Linear decay function"""
    adjusted_dist = max(0, abs(distance - origin) - offset)
    slope = (1 - decay) / scale
    return max(0, 1 - slope * adjusted_dist)

# Geographic distance decay function:
# Basically the same as above, the abs(distance - origin) part becomes the distance from the geographic coordinate point to the center coordinate point.
```


<span id="score-fusion-request-examples"></span>
# Score Fusion Request Examples

<span id="example-1-fusion-by-sales-complaint-quantity"></span>
## **Example 1: Fusion by sales/complaint quantity**

Assume the dataset is products, with "sales volume" field `f_sales` (int64 type), "complaints" field `f_complain` (int64 type)

Scenario: I want that during recall, products with higher sales volume are prioritized for recall, and products with fewer complaints are prioritized for recall.

**Sales configuration:**  Linear sorting by scalar size is sufficient, so base_value_from is set to scalar_field;

**Complaint configuration:**  Linear sorting by scalar size is sufficient, so base_value_from is set to scalar_field, and since it's negatively correlated, factor should be designed as a negative number;

The corresponding postProcessOps search settings are as follows:

```JSON
[
  {
    "op": "score_fusion",
    "fusion_by": "add",
    "addition_score_weight": 0.6,
    "addition_score": [
      {
        "factor": 1.0,
        "base_value_from": "scalar_field",
        "field": "f_sales"
      },
      {
        "factor": -10.0,
        "base_value_from": "scalar_field",
        "field": "f_complain"
      }
    ]
  }
]
```


**For example,**  there is a piece of data, f_sales=100, f_complain=2, assuming the ANN score is 0.111.

Now set addition_score_weight=0.6.

The calculation is executed as follows:

origin_score = 0.111, assumed to be 0.7 after normalization

addition_score = (1.0 \* 100) + (\-10.0 \* 2) = 80, assumed to be 0.8 after normalization

Then the total score is score = (0.7 \* 0.4) + (0.8 \* 0.6) = 0.76

<span id="example-2-fusion-by-publish-time-like-count"></span>
## **Example 2: Fusion by publish time/like count**

**Scenario:**  Assume the dataset is short videos, with "like count" field `f_like` (int64 type), "work publish time" field `f_publish_date_time` (date_time type). The scenario wants that during recall, videos with more likes are prioritized for recall, and videos with publish times closer to the current time are prioritized for recall.

**Like count weight configuration:**  Linear sorting by scalar size is sufficient, so base_value_from is set to scalar_field;

**Publish time weight configuration:**  Business logic design is needed, so base_value_from is set to decay_func; consider that within 24 hours from the current time, all should be regarded as the latest data, so the time factor is considered the same; the weight at 10 days from current can decay to half, so scale is set to 9d, decay is set to 0.5;

The corresponding postProcessOps search settings are as follows:

```JSON
[
  {
    "op": "score_fusion",
    "fusion_by": "add",
    "addition_score_weight": 0.6,
    "addition_score": [
      {
        "factor": 1.0,
        "base_value_from": "scalar_field",
        "field": "f_like"
      },
      {
        "factor": 2.0,
        "base_value_from": "decay_func",
        "field": "f_publish_date_time",
        "func": "gauss",       // Gaussian decay function
        "origin": "2025-10-01T00:00:00+08:00",  // Reference time.
        "offset": "1d",       // 1 day. Within 1 day from current time, time factor is considered the same.
        "scale": "9d",     // scale and decay parameters together characterize the slope of the decay function. This indicates: when the time distance is 10 days, the decay function value is 0.5.
        "decay": 0.5
      }
    ]
  }
]
```


For example, there is a piece of data, f_like=100, f_publish_date_time="2025\-10\-22T11:23:48+08:00" (the time at that moment), assuming the ANN score is 0.111.

Now set addition_score_weight=0.6.

The calculation is executed as follows:

origin_score = 0.111, assumed to be 0.7 after normalization

addition_score = (1.0 \* 100) + gauss_decay(), assumed to be 0.8 after normalization

Then the total score is score = (0.7 \* 0.4) + (0.8 \* 0.6) = 0.76
