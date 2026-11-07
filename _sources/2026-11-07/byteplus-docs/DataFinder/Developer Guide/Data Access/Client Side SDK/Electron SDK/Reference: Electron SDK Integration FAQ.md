---
title: "Reference: Electron SDK Integration FAQ"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Reference_Electron_SDK_Integration_FAQ"
---

<span id="da29c0eb"></span>
# SDK integration

<span id="df17a2c3"></span>
## How to debug Electron SDK?

Answer: Specific reference [Debugging the Main Process](https://www.electronjs.org/docs/latest/tutorial/debugging-main-process)

DevTools in the Electron browser window can only debug JavaScript executed in that window (i.e., a web page). To provide a way to debug the main process, Electron provides the `--inspect`and `--inspect-brk`switches.

**Command line switch**

Use the following command\-line switch to debug Electron's main process:

`--inspect=[port]`

Electron listens for V8 debug protocol messages on the specified `port`to which the external debugger needs to connect. `Port`defaults to `9229`.

`electron --inspect=9229 your/app`

`--inspect-brk=[port]`

Same as `--inspector`, but pauses on the first line of the JavaScript script.

**External debugger**

You need to use a debugger that supports the V8 debugging protocol


* Connect Chrome by visiting `chrome://inspect`and there select the Electron application that needs to be inspected.


<span id="436c71d1"></span>
# More FAQ

See the FAQ for more information on data access [SDK Integration & Data Reporting](https://docs.byteplus.com/docs/DataFinder/SDK_Integration_Data_Reporting).
