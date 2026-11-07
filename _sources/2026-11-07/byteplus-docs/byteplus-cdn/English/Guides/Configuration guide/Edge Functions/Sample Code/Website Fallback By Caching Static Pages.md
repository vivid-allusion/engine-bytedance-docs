---
title: "Website Fallback By Caching Static Pages"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/Implement_Website_Fallback_By_Caching_Static_Pages"
---

This example demonstrates how to implement fallback by caching static pages of a website. If the website is inaccessible, the cached static pages can be returned to users as a fallback.

The static pages of the website will be stored in Edge KV. Edge KV uses key\-value pairs as storage units, and there is a storage capacity limit for each key\-value pair (currently 128 KB). If the size of a single static page exceeds 128 KB, the function will split the website's static pages and then store them as multiple key\-value pairs in Edge KV. After the function retrieves the key\-value pair data from Edge KV, it will also cache the key\-value pair data in local memory. If the content of the next user request hits the local cache, the content in the local cache will be returned directly.

The function listens to both cron events and fetch events:


* cron event: The function periodically retrieves the latest static pages of the website and updates the chunked data in Edge KV.

* fetch event: The function assembles the chunked data into a website static page and returns it to the user.


<span id="preparation"></span>
## Preparation

To use this example, you need to complete the following preparations.

<span id="step-1-set-the-website-url-to-be-cached-in-the-example-code"></span>
### Step 1: Set the website URL to be cached in the example code

Set the website URL to cache in the config.js file of the example code, such as https://www.example.com. You can set one or multiple URLs. For example:

```JavaScript
  ORIGIN: sparrowOrigin([
  "https://www.example.com/page1",
  "https://www.example.com/page2",
  "https://www.example.com/page3",  
  ]),
```


<span id="step-2-create-a-namespace"></span>
### Step 2: Create a namespace

Create a namespace. See [Manage Namespaces](https://docs.byteplus.com/en/docs/byteplus-cdn/doc-manage-namespace). This example assumes your namespace is website\-fallback\-namespace.

<span id="step-3-create-a-cron-trigger"></span>
### Step 3: Create a Cron trigger

Create a Cron trigger. See [Cron](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-cron-triggers) to learn how to create a Cron trigger. The Cron trigger periodically triggers cron events. When a cron event is triggered, the corresponding callback function is executed to write the website's static pages to Edge KV.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Configure the execution frequency of Cron trigger</div>


<div data-tips="true" data-tips-type="tip">Before the function is executed, Edge KV does not store the website's static content. To make the fallback mechanism effective as soon as possible, the website's static content needs to be written to Edge KV quickly. Therefore, it is recommended that you first set the <strong>Scheduling type</strong> of the Cron trigger to <strong>Single point</strong> and set the <strong>Execution frequency</strong> to <strong>Executed every minute</strong>. This way, a cron event is triggered every minute. The callback function corresponding to the cron event will write the website's static pages to Edge KV. If your website corresponds to multiple URLs, the static pages corresponding to these URLs will be written to Edge KV in parallel.</div>


<div data-tips="true" data-tips-type="tip">You can confirm in the Edge Functions console whether the website's static pages have been written to Edge KV. If all the website's static pages have been written to Edge KV, the fallback mechanism can take effect. At this point, you can set the <strong>Execution frequency</strong> of the Cron trigger to a longer time period, such as <strong>Executed every day</strong>. This way, Edge KV will refresh the stored static pages once a day.</div>


<span id="sample-code"></span>
## Sample code

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">This example includes multiple .js files for demonstration purposes. When editing the function code, you need to bundle all .js files into a single .js file and use the content of the bundled file as the content of default.js. The bundled file must comply with ES6 standards.</div>


* <div data-tips="true" data-tips-type="warning">This example does not include the entry file required for bundling, nor does it include the logic for listening to fetch events. You need to create an entry file and call the addEventListener() method in that entry file to listen for both fetch events and cron events. Then, you need to set the callback function for the fetch event to the handle function exported from fetch.js, and set the callback function for the cron event to the cron function exported from cron.js. For example：</div>


   <div data-tips="true" data-tips-type="warning">   ```JavaScript
   const F = require("./fetch.js");
   const C = require("./cron.js");
   
   addEventListener('fetch', (event) => {
     event.respondWith(F.handle(event));
   });
   
   addEventListener('cron', C.cron);
   ```
      </div>
   


This example includes the following .js files:


* [util.js](https://docs.byteplus.com/en/docs/18/36362#util-js): Defines the `formatKey()` method, which generates a Key in the format of `${prefix}-${await sha1(hostname + pathname)}` based on the hostname and path of the webpage URL. `${prefix}` is a fixed value; `${await sha1(hostname + pathname)}` is the SHA1 digest of the concatenated hostname and path. Each Key is used to identify a unique URL.

* [config.js](https://docs.byteplus.com/en/docs/18/36362#config-js): Defines global constants, such as the URL of the website to be cached, the namespace (namespace) of Edge KV, the size of data chunks, etc.

* [chunk_kv.js](https://docs.byteplus.com/en/docs/18/36362#chunk-kv-js): Defines the following methods:

   * `chunkDoWrite()` method: Splits the content of the webpage and stores each chunk in a key\-value pair in Edge KV.

   * `chunkDoRead()` method: Reads key\-value pair data from Edge KV and combines all chunks into complete data.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">chunk_kv.js uses a fixed JSON structure (finger data) to store the chunk information of the webpage data corresponding to a URL, including the total size of the data before chunking, the size of each chunk, UUID, and the timestamp when the data was stored. The finger data is also stored in Edge KV. The key of the finger data in Edge KV is the Key of that URL, and the value is the content of the finger data.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <code>chunkDoWrite()</code> method updates the finger data in Edge KV after writing chunk data to Edge KV; the <code>chunkDoRead()</code> method reads the finger data from Edge KV before reading chunk data from Edge KV.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Each chunk corresponds to a key\-value pair in Edge KV. The Key of the chunk is the key of the key\-value pair; the data of the chunk is the value of the key\-value pair. The Key of each chunk (chunkKey) follows the format <code>_DATA_${key}-${prefix}-${chunkIdx}</code>, where <code>${key}</code> is the key of the Edge KV key\-value pair, and <code>${chunkIdx}</code> is the sequence number of each chunk when the data is split.   </div>
   

* [kv.js](https://docs.byteplus.com/en/docs/18/36362#kv-js): Specifies whether the `setString()` method and `getString()` method use the methods in chunk_kv.js. In the example code, the `setString()` and `getString()` methods use the methods from chunk_kv.js.

* [cron.js](https://docs.byteplus.com/en/docs/18/36362#cron-js): Listens to cron events and triggers the `chunkDoWrite()` method, which splits the webpage data and writes each chunk into a key\-value pair in Edge KV.

* [fetch.js](https://docs.byteplus.com/en/docs/18/36362#fetch-js): Listens to fetch events and triggers the `chunkDoRead()` method, which reads key\-value pairs from Edge KV, merges the read chunk data into complete data, and then returns it to the user.

* [lru.js](https://docs.byteplus.com/en/docs/18/36362#lru-js): After retrieving key\-value pair data from Edge KV, it caches the website content in local memory through the LRU caching mechanism. If the content of the next user request hits the local cache, the function directly returns the content in the local cache.


<span id="util-js"></span>
### util.js

```JavaScript
function isNode() {
  return typeof isSparrow === "undefined" && typeof module !== "undefined";
}

// Used to encode the URL into a uniformed format for KV store to store them
async function sha1(input) {
  const cpt = isNode() ? globalThis.crypto : crypto;
  const raw = new TextEncoder().encode(input);
  const hash = new Uint8Array(await cpt.subtle.digest("SHA-1", raw));
  return Array.from(hash)
    .map((byte) => byte.toString(16).padStart(2, "0"))
    .join("");
}

async function formatKey(prefix, hostname, pathname) {
  return `${prefix}-${await sha1(hostname + pathname)}`;
}

module.exports = {
  isNode: isNode,
  sha1: sha1,
  formatKey: formatKey,
};

```


<span id="config-js"></span>
### config.js

```JavaScript
function sparrowOrigin(mergedOut) {
  if (typeof isSparrow !== "undefined") {
    if (typeof env !== "undefined") {
      const t1 = env.testOrigin1;
      const t2 = env.testOrigin2;
      const t3 = env.testOrigin3;
      const out = [];
      if (t1) out.push(t1);
      if (t2) out.push(t2);
      if (t3) out.push(t3);
      return mergedOut.concat(out);
    }
  }

  return mergedOut;
}

module.exports = {
  NAMESPACE: "website-fallback-namespace",
  KEY_PREFIX: "website-fallback-key",
  ORIGIN: sparrowOrigin([
    // PLACE all your URL inside of it
    // If you place your url as following, https://www.example.com/. The cron
    // just request the URL specified and cache its content with key as 2
    // elements tuple (hostname, pathname). The match will be against this
    // as well.
  ]),
  OVERWRITE_URL_HEADER_NAME: "x-website-fallback-url",

  CHUNK_SIZE: 1024 * 127, // just use 127KB for now
  CHUNK_GC: true, // whether do GC for chunk KV
  CHUNK_KV_DISABLE: false, // disable chunk kv, make sure KV is large enough

  // search policy, allowed value are
  // [0] @exact, ie match hostname and path
  // [1] @root,  ie match hostname and fallback everything back to root
  // [2] @match-and-fallback, ie try exact match first and fallback to root
  // [3] rest, treat it as a URL and use that URL as key and value for KV cache
  SEARCH_POLICY: "@root",

  // Mostly used for testing, specify it as undefined/null to disable this feature
  MANUAL_CRON_PATHNAME: "",
  DONE_STATUS_CODE: 200,
  FAIL_STATUS_CODE: 504,
  RESPONSE_HEADERS: [
    ["content-type", "text/html"], // force to be HTML page for now
  ],
  INFO_HEADER_NAME: "x-bdcdn-website-fallback",
  MEMORY_CACHE_TTL: 30 * 60 * 1000,         // 30 min
  MEMORY_CACHE_SIZE: 1,                     // same as ORIGIN list
  MEMORY_CACHE_BACKOFF_TTL: 10 * 60 * 1000, // 10 mins

  // NODEJS mock test usage, never used by sparrow
  NODE_MOCK_KV_GET_THROW: false,
};

```


<span id="chunk-kv-js"></span>
### chunk_kv.js

```JavaScript
/**
 ** Scheme of splitted chunk to workaround the KV limitation. 128K is too small
 ** for caching a single web page nowadays.
 **
 ** 1) We split the data into multiple chunks and store them into different keys
 **
 ** 2) The original (ns, key) point to a value which is finger data used to
 **    indicate list of chunks. The finger data is just a small JSON snippet
 **    which contains all the needed information for that list of chunks.
 **    The json is as following
 **
 **    {
 **      "total": 123456,  // total size of the data
 **      "chunkSize": 5,   // chunk #
 **      "prefix": abcd,   // a uuid used to locate the corresponding files
 **      "date": "Jan xxx" // a timestamp to indicate when the data stored
 **    }
 **
 **    prefix is a random uuid, and the 3 is used to indicate the chunk data
 **
 **    which is _DATA_key-{prefix}-0, key-{prefix}-1, ..., key-{prefix}-n
 **
 ** 3) The read follows the above scheme to get the data out, and the write
 **    will ONLY update the final finger once all chunk write is done
 **
 **/

const U = require("./util.js");
const C = require("./config.js");

// chunk size, can be defined based on the specific limitation of KV product
let CHUNK_SIZE = C.CHUNK_SIZE;

// whether perform GC, if not the bucket may go beyond the quota limitation
const DoGC = C.CHUNK_GC;

// for testing
const localKV = {};

// Implementation details
//
//  1) We do not use concurrent promise, instead of we try to perform KV
//     operation one by one to avoid load spike which could cause possible
//     issue, ie garbage left inside of the KV namespace. Notes, all the
//     garbage left in the KV namespace requires extra pass to clean up
//
//  2) We try to make everything relatively easy for manual efforts cleanup
//     in case we left too much garbage that makes us unable to do allocation
//     inside of the KV bucket
//
// ----------------------------------------------------------------------------

async function sleep(ms) {
  return new Promise((r, _) => {
    setTimeout(() => {
      r(undefined);
    }, ms);
  });
}

function rndId() {
  return "xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx".replace(/[xy]/g, function (c) {
    let r = (Math.random() * 16) | 0,
      v = c == "x" ? r : (r & 0x3) | 0x8;
    return v.toString(16);
  });
}

function parseFinger(finger) {
  return JSON.parse(finger);
}

function formatFinger(prefix, chunkSize, total) {
  return JSON.stringify({
    total: total,
    chunkSize: chunkSize,
    date: new Date(Date.now()).toString(),
    prefix: prefix,
  });
}

function formatChunkKey(ns, key, prefix, chunkIdx) {
  return `_DATA_${key}-${prefix}-${chunkIdx}`;
}

// KV wrapper, used for test mocking etc ...
async function doRead(ns, key) {
  if (U.isNode()) {
    return localKV[ns + key];
  } else {
    return await KV.get(ns, key, {type: "string"});
  }
}

async function doWrite(ns, key, value) {
  if (U.isNode()) {
    localKV[ns + key] = value;
  } else {
    await KV.set(ns, key, value);
  }
}

async function doRemove(ns, key) {
  if (U.isNode()) {
    localKV[ns + key] = undefined;
  } else {
    await KV.delete(ns, key);
  }
}

// ChunkKV main functions

async function chunkDoRead(ns, key) {
  // (0) read the finger data out
  const finger = await doRead(ns, key);
  if (finger === undefined) {
    console.log("missing finger data");
    return undefined;
  }

  // (1) parse the finger
  const {prefix, total, chunkSize, date} = parseFinger(finger);
  console.log(`data has ${total} bytes and is updated ${date}`);

  // (2) read each chunk accordingly
  const out = [];
  for (let i = 0; i < chunkSize; i++) {
    const chunkKey = formatChunkKey(ns, key, prefix, i);
    console.error(`read chunk ${chunkKey}`);
    const chunk = await doRead(ns, chunkKey);
    out.push(chunk);
  }

  const data = out.join("");

  if (total != data.length) {
    throw new Error(
      `mismatched content: ${ns}:${key} ${date}/${total} != ${data.length}`,
    );
  }

  // (3) chunk is done
  return data;
}

async function gc(ns, key, finger) {
  if (DoGC) {
    const {prefix, chunkSize} = parseFinger(finger);
    const promiseRemove = [];
    for (let i = 0; i < chunkSize; i++) {
      const chunkKey = formatChunkKey(ns, key, prefix, i);
      promiseRemove.push(doRemove(ns, chunkKey));
    }
    try {
      await Promise.all(promiseRemove);
    } catch (e) {
      console.error(`gc failed: ${e.stack}`); // silent the error
    }
  }
}

async function rollback(ns, key, prefix, size) {
  // rollback is done one by one which is better
  for (let i = 0; i < size; i++) {
    const chunkKey = formatChunkKey(ns, key, prefix, i);
    try {
      await doRemove(ns, chunkKey);
    } catch (e) {
      // ignore
    }
  }
}

// read the finger from current ns:key value, the finger is used for GC
async function readGCFinger(ns, key) {
  let oldFinger = undefined;

  if (DoGC) {
    let readFailed = false;

    // [0] first try, try to read from the KV store, we may have issuse
    try {
      oldFinger = await doRead(ns, key);
    } catch (e) {
      console.log("failed to read finger date for GC");
      readFailed = true; // okay, first try failed, then try to perform a retry
    }

    // if the first read failed, notes, must be an exception, perform a retry
    // otherwise just od nothing
    if (readFailed) {
      // try to sleep 1 second and perform another retry here
      await sleep(1000);

      try {
        oldFinger = await doRead(ns, key);
      } catch (e) {
        console.log("**RETRY** failed to read finger data for GC");
      }
    }
  }

  return {oldFinger}; // notes if the GCFinger operation failed
  // then just return undefined
}

// used to update new finger to the ns:key pair
async function updateFinger(ns, key, finger) {
  // [0] first try
  try {
    await doWrite(ns, key, finger);
    return;
  } catch (e) {
    console.error(`finger update failed, retry: ${e.stack}`);
  }

  await sleep(1); // wait 1 second as back-off

  // [1] second try
  try {
    await doWrite(ns, key, finger);
    return;
  } catch (e) {
    console.error(`finger update RETRY failed: ${e.stack}`);
    throw e;
  }
}

async function chunkDoWrite(ns, key, value) {
  if (value.length == 0) {
    throw new Error(`empty value for ${ns} and ${key}`);
  }

  const uuid = rndId(); // uuid

  let chunkSize = Math.floor(value.length / CHUNK_SIZE);
  if (chunkSize * CHUNK_SIZE < value.length) {
    chunkSize += 1;
  }

  console.error(`chunk size ${chunkSize}`);
  let chunkStart = 0;

  // [0] Try to perform the write chunk by chunk. Notes, the write is been
  //     purposely placed as lockstep fashion to avoid any potential mutation
  //     load and throttling.
  try {
    for (let i = 0; i < chunkSize; i++) {
      const chunkKey = formatChunkKey(ns, key, uuid, i);
      const chunkEnd = Math.min(value.length, chunkStart + CHUNK_SIZE);
      console.error(`write chunk ${chunkKey}@(${chunkStart}-${chunkEnd})`);
      await doWrite(ns, chunkKey, value.substring(chunkStart, chunkEnd)),
        (chunkStart = chunkEnd);
    }
  } catch (e) {
    await rollback(ns, key, uuid, chunkSize);
    throw e;
  }

  // [1] Try to finger out the old finger, used for GC later
  const {oldFinger} = await readGCFinger(ns, key);

  // [2] Swap the pointer with the curernt finger, ie write latest finger to
  //     index file to finish write operation. If the following operation can
  //     be done, ie atomically, then we can see latest content
  const finger = formatFinger(uuid, chunkSize, value.length);
  try {
    await updateFinger(ns, key, finger);
  } catch (e) {
    // try to perform a rollback, still best efforts, which delete newly created
    // chunk data
    await rollback(ns, key, uuid, chunkSize);

    // throw the error out again to indicate that we CANNOT finish the write.
    throw e;
  }

  // [3] If oldFinder is been readed out, try to perform a GC. notes the GC
  //     is always best efforts for now
  if (oldFinger !== undefined) {
    await gc(ns, key, oldFinger);
  }
}

module.exports = {
  write: chunkDoWrite,
  read: chunkDoRead,
  localKV: localKV,
  setChunkSize: function (sz) {
    CHUNK_SIZE = sz;
  },
  setGC(gc) {
    DoGC = gc;
  },
};

```


<span id="kv-js"></span>
### kv.js

```JavaScript
// Mock KV away and allow our code to work under *node.js* for unittest
const U = require("./util.js");
const C = require("./config.js");
const CK = require("./chunk_kv.js");

const UseSparrowKV = C.CHUNK_KV_DISABLE; // whether disable chunk kv

let localKV = {};

function kvId(ns, key) {
  return `${ns}@${key}`;
}

async function getString(ns, key) {
  if (U.isNode()) {
    if (C.NODE_MOCK_KV_GET_THROW) {
      throw new Error("mock test");
    }
    const out = localKV[kvId(ns, key)];
    if (out === undefined) {
      throw new Error(`nodekv: key ${key} in namespace ${ns} is not found`);
    }
    return out;
  } else {
    if (UseSparrowKV) {
      return await KV.get(ns, key, {type: "string"});
    } else {
      return await CK.read(ns, key);
    }
  }
}

async function setString(ns, key, value) {
  if (typeof value !== "string") {
    throw new Error(`not type string for namespace ${ns} and key ${key}`);
  }
  if (U.isNode()) {
    localKV[kvId(ns, key)] = value;
  } else {
    if (UseSparrowKV) {
      await KV.set(ns, key, value);
    } else {
      await CK.write(ns, key, value);
    }
  }
}

function initLocalKV(kvMap) {
  if (!U.isNode()) {
    throw new Error("MUST be under node, used for unittest");
  }
  localKV = kvMap;
}

module.exports = {
  getString: getString,
  setString: setString,
  initLocalKV: initLocalKV,
};

```


<span id="cron-js"></span>
### cron.js

```JavaScript
// Cron Part
//
// Triggered by cron and try to get a updated webpage cached inside of the KV
// for future usage.
const U = require("./util.js");
const C = require("./config.js");
const KVStore = require("./kv.js"); // shim for KV, better for testing

async function downloadOnce(input_url) {
  console.error(`1) download ${input_url}`);
  const resp = await fetch(input_url);
  if (resp.status != 200) {
    throw new Error(`response from ${input_url} is ${resp.status}`);
  }
  const text = await resp.text();
  const url = new URL(input_url);
  const key = await U.formatKey(C.KEY_PREFIX, url.hostname, url.pathname);
  console.error(
    `2) upload to KV(${text.length}): ${key}<=>(${url.hostname}:${url.pathname})`,
  );

  await KVStore.setString(
    C.NAMESPACE, // namespace
    key, // key
    text, // value(content)
  );

  console.error(`3) upload done`);
}

// We try our best to make sure download do not throw exception unless we cannot
// control them. This makes sure that our update for all the origin content
// to be best effort oriented
async function download(url) {
  try {
    await downloadOnce(url);
    return;
  } catch (e) {
    console.error(`url ${url}, download error: ${e.stack}`);
  }

  // try another times
  console.error("failed, retry download one more times");

  try {
    await downloadOnce(url);
  } catch (e) {
    console.error(
      `retry failed for url ${url} with error: ${e.stack}, use stale content`,
    );
  }
}

async function cron(event) {
  let allP = [];

  for (const u of C.ORIGIN) {
    allP.push(download(u));
  }

  try {
    await Promise.all(allP);
    return "done";
  } catch (e) {
    console.error(`upload failed: ${e.stack}`);
    return `${e.stack}`;
  }
}

module.exports = {
  cron: cron,
};

```


<span id="fetch-js"></span>
### fetch.js

```JavaScript
// Fallback function that fetchs the value from the KEY-VALUE

const C = require("./config.js");
const U = require("./util.js");
const LRUCache = require("./lru.js");
const KVStore = require("./kv.js");
const cacheTTL = C.MEMORY_CACHE_TTL;
const kvCache = new LRUCache(C.MEMORY_CACHE_SIZE);
const CRON = require("./cron.js");

let allowedOrigin = null;

function tagInfo(tag) {
  if (U.isNode()) {
    return [C.INFO_HEADER_NAME, `${tag}: node`];
  } else {
    return [C.INFO_HEADER_NAME, `${tag}: ${session.requestId}`];
  }
}

function getFailInfo() {
  return tagInfo("fail");
}
function getDoneInfo(appendix) {
  const out = tagInfo("done");
  if (appendix) {
    out[1] = `${out[1]} (${appendix})`;
  }
  return out;
}

function getReqSignature(req) {
  return `[${req.method}][${req.url}]`;
}

function isKnownHostname(hostname) {
  if (allowedOrigin == null) {
    allowedOrigin = [];
    for (const u of C.ORIGIN) {
      const url = new URL(u);
      allowedOrigin.push(url.hostname);
    }
  }
  return allowedOrigin.includes(hostname);
}

async function serveFromKV(request) {
  if (request.method != "GET") {
    throw new Error(`invalid http method: ${request.method}`);
  }

  let url = undefined;

  // (0) figure out URL based on predefined rules
  if (
    C.OVERWRITE_URL_HEADER_NAME &&
    request.headers.has(C.OVERWRITE_URL_HEADER_NAME)
  ) {
    const input = request.headers.get(C.OVERWRITE_URL_HEADER_NAME);
    try {
      url = new URL(input);
    } catch (e) {
      throw new Error(`invalid overwrite URL ${input}`);
      url = new URL(request.url);
    }
  } else {
    url = new URL(request.url);
  }

  // (2) perform the actual serve from KV operation
  return await doServeFromKV(request, url);
}

async function doServeFromKV(request, url) {
  switch (C.SEARCH_POLICY) {
    case "@root":
      return await doKVFetch(request, url.hostname, "/", url.href);

    case "@exact":
      return await doKVFetch(request, url.hostname, url.pathname, url.href);

    case "@match-and-fallback":
      // try both one and get the matched one out
      try {
        return await doKVFetch(request, url.hostname, "/", url.href);
      } catch (e) {
        console.error("strategy(both) fallback");
        return await doKVFetch(request, url.hostname, url.pathname, url.ref);
      }

    default:
      // try to treat the freaking policy as a hostname
      let new_url = null;
      new_url = new URL(C.SEARCH_POLICY);
      return await doKVFetch(
        request,
        new_url.hostname,
        new_url.pathname,
        new_url.href,
      );
  }
}

async function doKVFetch(request, hostname, pathname, href) {
  const key = await U.formatKey(C.KEY_PREFIX, hostname, pathname);
  let data = null;
  let appendix = "";

  // (1) try to get it from the kv in memory cache, will save us from reading
  //     external KV store
  let kvEntry = kvCache.getEntry(key);

  if (kvEntry === undefined || kvEntry.stale) {
    console.error("kvcahe missed, try lookup from KV store");

    // use KVStore to refresh local cache
    try {
      data = await KVStore.getString(C.NAMESPACE, key);
      if (data !== undefined) {
        kvCache.set(key, data, cacheTTL);
      }
      appendix = "KV";
      kvCache.removeStaleEntry(kvEntry);
      kvEntry = undefined;
    } catch (e) {
      console.error(`KV get for ${C.NAMESPACE} and ${key} failed: ${e.stack}`);

      // check whether we have fallback entry to use
      if (kvEntry !== undefined) {
        data = kvEntry.value;
        kvEntry.node.renew(C.MEMORY_CACHE_BACKOFF_TTL); // make it renew
        appendix = "STALE";
      } else {
        data = undefined;
      }
    }

    // no fallback, we can only error out here, it result in a 504
    if (data === undefined) {
      throw new Error(`unknown url: ${href}`);
    }
  } else {
    data = kvEntry.value;
    appendix = "CACHED";
  }

  // (2) generate the response accordingly
  return new Response(data, {
    status: C.DONE_STATUS_CODE,
    headers: C.RESPONSE_HEADERS.concat([getDoneInfo(appendix)]),
  });
}

async function handle(event) {
  const request = event.request;

  // used for test
  if (request.path === C.MANUAL_CRON_PATHNAME && CRON) {
    await CRON.cron({});
    return new Response("Flush done", {status: 200});
  }

  try {
    return await serveFromKV(request);
  } catch (e) {
    console.error(
      `cannot serve from KV for request: ${getReqSignature(request)}: ${e.stack}`,
    );

    return new Response("Gateway Error", {
      status: C.FAIL_STATUS_CODE,
      headers: [getFailInfo()],
    });
  }
}

// Used as library purpose
module.exports = {
  handle: handle, // fetch handler
  cron: CRON.cron, // cron handler
  kvCache: kvCache, // kv cache
};

```


<span id="lru-js"></span>
### lru.js

```JavaScript
class Node {
  constructor(key) {
    this.key = key;
    this.value = null;
    this.prev = null;
    this.next = null;
    this.deadline = null;
  }

  isExpired() {
    return this.deadline < Date.now();
  }

  renew(ttl) {
    this.deadline = Date().now + ttl; // reset to another one
  }
}

class LRUCache {
  constructor(capacity) {
    this.map = new Map();
    this.head = new Node(null);
    this.tail = new Node(null);
    this.head.next = this.tail;
    this.tail.prev = this.head;
    this.capacity = capacity;
  }

  set(key, value, ttl) {
    const node = this.map.get(key);
    const deadline = Date.now() + ttl;

    if (node !== undefined) {
      node.deadline = deadline;
      node.value = value;
      this._moveToFront(node);
      return true;
    } else {
      // add new key-value pair
      if (this.map.size >= this.capacity) {
        this._removeOldest();
      }
      const newNode = new Node(key);
      newNode.deadline = deadline;
      newNode.value = value;
      this.map.set(key, newNode);
      this._addToFront(newNode);
      return false;
    }
  }

  get(key) {
    const node = this.map.get(key);
    if (node !== undefined) {
      if (node.isExpired()) {
        this._removeNode(node);
        this.map.delete(key);
      } else {
        this._moveToFront(node);
        return node.value;
      }
    }
    return undefined;
  }

  // the difference between this API and get is that this will return staled
  // entry and it is up to the user to decide how to treat the stale one
  getEntry(key) {
    const node = this.map.get(key);
    if (node !== undefined) {
      this._moveToFront(node);
      return {
        value: node.value,
        stale: node.isExpired(),
        node: node,
      };
    }
    return undefined;
  }

  removeStaleEntry(entry) {
    if (entry === undefined) return;

    if (entry.node === undefined) {
      throw new Error("not a valid LRU entry");
    }
    if (entry.stale) {
      this.map.delete(entry.key);
      this._removeNode(entry.node);
    }
  }

  size() {
    return this.map.size;
  }

  orderedEntry() {
    let out = [];
    let start = this.head.next;
    let end = this.tail;
    while (start != end) {
      out.push(start.value);
      start = start.next;
    }
    return out;
  }

  remove(key) {
    const node = this.map.get(key);
    if (node) {
      this._removeNode(node);
      this.map.delete(key);
      return true;
    }
    return false;
  }

  evict(cnt) {
    while (this.map.size > 0) {
      this._removeOldest();
      cnt--;
      if (cnt == 0) break;
    }
  }

  clear() {
    this.evict(this.map.size);
  }

  _removeNode(node) {
    const nodePrev = node.prev;
    const nodeNext = node.next;
    nodePrev.next = nodeNext;
    nodeNext.prev = nodePrev;
    node.prev = null;
    node.next = null;
    node.value = null;
  }

  _removeOldest() {
    const oldestNode = this.tail.prev; // remove from list and map
    this.tail.prev = oldestNode.prev;
    oldestNode.prev.next = this.tail;
    this.map.delete(oldestNode.key);
  }

  _moveToFront(node) {
    node.prev.next = node.next; // remove from list
    node.next.prev = node.prev;
    this._addToFront(node); // add to front of list
  }

  _addToFront(node) {
    const headNextNode = this.head.next;
    node.next = headNextNode; // insert after head
    node.prev = this.head;
    this.head.next = node;
    headNextNode.prev = node;
  }
}

module.exports = LRUCache;

```


<span id="related-runtime-apis"></span>
## Related runtime APIs


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent)

* [Request](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Request)

* [Headers](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Headers)

* [fetch()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-fetch)

* [KV](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-EdgeKV-RuntimeAPI)
