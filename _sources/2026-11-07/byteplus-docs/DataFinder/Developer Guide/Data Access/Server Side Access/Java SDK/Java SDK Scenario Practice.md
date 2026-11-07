---
title: "Java SDK Scenario Practice"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Java_SDK_Scenario_Practice"
---

<span id="23b6fb0c"></span>
# Use custom local_time_ms

Datafinder analyzes the event occurrence time, which is calculated based on the occurrence time of the reported event on the client (i.e. local_time_ms). For example, if a user purchases an event at 2022\-09\-01 23:58:00, but the event is not actually received by Datafinder until 2022\-09\-02 00:03:00 due to network latency or other reasons, then at the time of analysis, the event is still considered to have occurred 2022\-09\-01 time, not 2022\-09\-02.

Use interface:

```Java
/**
  * function description: asynchronous sending of events
  *
  *  @param  appId        application id
  *  @param  custom       user custom public parameters
  *  @param  eventName    event name
  *  @param  eventParams  event parameters
  *  @param  userUniqueId user uuid
  *  @param  localTimeMs  event occurrence time, milliseconds
  *  @return:  void
  *  @date:  2020/8/26 12:24
  */
void sendEvent(String userUniqueId, int appId, Map<String, Object> custom, String eventName, Map<String, Object> eventParams,long localTimeMs);

/**
  * function description: send single event
  *
  *  @param  header      event public property, you can build a header by calling HeaderV3.Builder().build() 
  *  @param  eventName   event name
  *  @param  eventParams event parameters
  *  @param  localTimeMs  event occurrence time, milliseconds
  *  @return:  void
  *  @date:  2020/9/28 22:00
  */
void sendEvent(Header header, String eventName, Map<String, Object> eventParams,long localTimeMs);
```


<span id="94a7ee87"></span>
# High performance scenario

If the user already has their own event tracking, or their own server level services are particularly large, in order to avoid each service integrating the DataFinder SDK, the business can uniformly report their business tracking to a Kafka topic, and then start a new integrated SDK service to consume business tracking information. Use the API provided by the SDK to report the event tracking information to the DataFinder. The process is as follows:

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI3MDRweCIgaGVpZ2h0PSIyNjVweCIgdmlld0JveD0iLTAuNSAtMC41IDcwNCAyNjUiPjxkZWZzLz48Zz48cGF0aCBkPSJNIDEyMiAzMiBMIDE2MiAzMiBMIDE2MiAxMzIgTCAxOTMuNzYgMTMyIiBmaWxsPSJub25lIiBzdHJva2U9IiM4MDgwODAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxOTkuNzYgMTMyIEwgMTkxLjc2IDEzNiBMIDE5My43NiAxMzIgTCAxOTEuNzYgMTI4IFoiIGZpbGw9IiM4MDgwODAiIHN0cm9rZT0iIzgwODA4MCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyIiB5PSIyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjN2VhNmUwIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE0cHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5CdXNpbmVzcyBldmVudCB0cmFja2luZzwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAxMjIgMTMyIEwgMTkzLjc2IDEzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjODA4MDgwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMTk5Ljc2IDEzMiBMIDE5MS43NiAxMzYgTCAxOTMuNzYgMTMyIEwgMTkxLjc2IDEyOCBaIiBmaWxsPSIjODA4MDgwIiBzdHJva2U9IiM4MDgwODAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMTAyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjN2VhNmUwIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMzJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNHB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+QnVzaW5lc3MgZXZlbnQgdHJhY2tpbmc8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMTIyIDIzMiBMIDE2MiAyMzIgTCAxNjIgMTMyIEwgMTkzLjc2IDEzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjODA4MDgwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMTk5Ljc2IDEzMiBMIDE5MS43NiAxMzYgTCAxOTMuNzYgMTMyIEwgMTkxLjc2IDEyOCBaIiBmaWxsPSIjODA4MDgwIiBzdHJva2U9IiM4MDgwODAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMjAyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjN2VhNmUwIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMzJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNHB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+QnVzaW5lc3MgZXZlbnQgdHJhY2tpbmc8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjIwMiIgeT0iMTAyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjY2NjY2NjIiBzdHJva2U9IiM0ZDRkNGQiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMzJweDsgbWFyZ2luLWxlZnQ6IDIwM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE0cHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5LYWZrYTp0b3BpYzwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA0MDIgMTMyIEwgMzMwLjI0IDEzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjODA4MDgwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMzI0LjI0IDEzMiBMIDMzMi4yNCAxMjggTCAzMzAuMjQgMTMyIEwgMzMyLjI0IDEzNiBaIiBmaWxsPSIjODA4MDgwIiBzdHJva2U9IiM4MDgwODAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA1MjIgMTMyIEwgNTkzLjc2IDEzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjODA4MDgwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNTk5Ljc2IDEzMiBMIDU5MS43NiAxMzYgTCA1OTMuNzYgMTMyIEwgNTkxLjc2IDEyOCBaIiBmaWxsPSIjODA4MDgwIiBzdHJva2U9IiM4MDgwODAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iNDAyIiB5PSIxMDIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNjY2NjY2MiIHN0cm9rZT0iIzRkNGQ0ZCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEzMnB4OyBtYXJnaW4tbGVmdDogNDAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTRweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkZpbmRlciBzZXJ2ZXIgc2lkZSBTREsgZXZlbnQgdHJhY2tpbmc8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNjAyIDEzMiBDIDYxMC4wOSAxMTYuODggNjI0LjI1IDEwNS45NiA2NDAuOSAxMDIgTCA2ODAuOCAxMDIgQyA2OTIuNSAxMDcuMzggNzAwIDExOS4xIDcwMCAxMzIgQyA3MDAgMTQ0LjkgNjkyLjUgMTU2LjYyIDY4MC44IDE2MiBMIDY0MC45IDE2MiBDIDYyNC4yNSAxNTguMDQgNjEwLjA5IDE0Ny4xMiA2MDIgMTMyIFoiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzRkNGQ0ZCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA5NnB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEzMnB4OyBtYXJnaW4tbGVmdDogNjAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTRweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRhdGFGaW5kZXI8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjE0MiIgeT0iMTAyIiB3aWR0aD0iNDAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTEycHg7IG1hcmdpbi1sZWZ0OiAxNDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNHB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgYmFja2dyb3VuZC1jb2xvcjogI2ZmZmZmZjsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+UmVwb3J0PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI1NDIiIHk9IjEwMiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDExMnB4OyBtYXJnaW4tbGVmdDogNTQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTRweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlJlcG9ydDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMzQyIiB5PSIxMDIiIHdpZHRoPSI0MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMTJweDsgbWFyZ2luLWxlZnQ6IDM0M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE0cHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5Db25zdW1lPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48L2c+PC9zdmc+" />

In this case, users usually report all the information about event tracking, including the event tracking time, to Kafka. If the local_time_ms is not set when using the server level SDK, the event occurrence time will be considered as the SDK processing time, which is generally different from the event tracking occurrence time. When the system is busy and the kafaka topic lags, this difference is even greater, causing the amount of events seen on the DataFinder at the same time to vary more than expected.

<span id="a6751e5b"></span>
# Check the reporting delay


1. The server level is reported to the applog service, which can be viewed on the granafa of the service:

   ```Plain
   http://{IP}:{port}/d/applog/applog?refresh=1m&orgId=1
   ```
   

2. The average delay can be obtained by curl.

   Domain needs to be replaced with real values; app_id, user_unique_id are also replaced with real app_id, user_unique_id.

3. You can execute the following commands multiple times:

   ```Bash
   curl -o /dev/null -s -w 'Total: %{time_total}s\n'   --location --request POST '${domain}/sdk/log' \
   --header 'User-Agent: DataRangers Java SDK' \
   --header 'Content-Type: application/json' \
   --data '{
       "app_type": "app",
       "_format_name": "datarangers_svc_app_log_v3_server_sdk_1.5.6",
       "app_id": 10000000,
       "header": {
           "aid": 10000000,
           "custom": {
               "client": "fdaf",
               "__sdk_platform": "datarangers_sdk_1.5.6-release"
           },
           "device_id": 0,
           "timezone": 8,
           "tz_offset": 28800,
           "tz_name": "Asia/Shanghai",
           "user_unique_id": "dkqfn5ku9zk8",
           "app_id": 10000000
       },
       "user_unique_id": "xxxx",
       "event_v3": [
           {
               "event": "补贴查询",
               "params": {
                   "cardNum": "cardNum",
                   "year": "2021"
               },
               "local_time_ms": 1637734994778,
               "datetime": "2021-12-15 14:23:14"
           }
       ]
   }'
   ```
   

4. More ways to curl:

   ```Bash
   curl -w "@curl-format.txt" -o /dev/null -s  --location --request POST '${domain}/sdk/log' \
   --header 'User-Agent: DataRangers Java SDK' \
   --header 'Content-Type: application/json' \
   --data '{
       "app_type": "app",
       "_format_name": "datarangers_svc_app_log_v3_server_sdk_1.5.6",
       "app_id": {replace with the real app_id},
       "header": {
           "custom": {
               "client": "fdaf",
               "__sdk_platform": "datarangers_sdk_1.5.6-release"
           },
           "device_id": 0,
           "timezone": 8,
           "tz_offset": 28800,
           "tz_name": "Asia/Shanghai",
           "user_unique_id": "{replace with the real user_unique_id}", 
           "app_id": {replace with the real app_id}
       },
       "user_unique_id": "xxx",
       "event_v3": [
           {
               "event": "补贴查询",
               "params": {
                   "cardNum": "cardNum",
                   "year": "2021"
               },
               "local_time_ms": 1637734994778,
               "datetime": "2021-12-15 14:23:14"
           }
       ]
   }'
   ```
   

   The content of the curl\-format.txt file is:

   ```Plain
        time_namelookup:  %{time_namelookup}s\n
               time_connect:  %{time_connect}s\n
        time_appconnect:  %{time_appconnect}s\n
       time_pretransfer:  %{time_pretransfer}s\n
          time_redirect:  %{time_redirect}s\n
     time_starttransfer:  %{time_starttransfer}s\n
                        ----------\n
             time_total:  %{time_total}s\n
   ```
   


<span id="8e1ee5ae"></span>
# How to handle data that fails to be sent

By default, the data that fails to be sent will be written to the error\-datarangers.log file in the `eventSavePath`(default is logs/) directory. The following is the general processing method:


1. If partial failure is tolerated, it will not be dealt with.

2. Custom failure handling logic, such as sending failed messages to another kafka\-topic, and then compensating for consumption after the system is restored.

3. Cooperate with the provided logagent (only privatized, contact the account manager to obtain) to monitor failed files and make up for failed reports.


Spring injection callback:

```Java
@Configuration
public class SdkConfiguration {

//  @Bean
  public Callback callback() {
    return new Callback() {

      @Override
      public void onFailed(FailedData failedData) {
      // handle  failed data
      // cause   exception is anomalous information
      // message is the complete message for reporting
        System.out.println(failedData.getCause());
        System.out.println(failedData.getException());
        System.out.println(failedData.getMessage());
      }
    };
  }
}
```


Or set one when initializing the collector:

```Java
EventCollector appEventCollector =  new AppEventCollector("app", dataRangersSDKConfigPropertiesInfo, new Callback() {
  @Override
  public void onFailed(FailedData failedData) {
    // handle the failed data
  }
})
```


<span id="8acfa9a5"></span>
# Report performance debugging

If it is found that the reported QPS does not meet the requirements, it can be handled:


1. Extended services app_log services.

2. Debug the relevant configuration of SDK:

   1. Increase the number of threadCount, you can report the delay, simple and quick estimate ( **not necessarily a linear relationship** ): `1s/delay * threadCount * batchSize`.

   2. Use batch reporting.

3. Contact DataFiner operations to expand.
