---
title: "SourceMap upload and reverse mapping"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/SourceMap_upload_and_reverse_mapping"
---

Sourcemap is an information file that stores location information. In other words, each position in the transformed code corresponds to a position in the original code. With the Sourcemap file, when an error occurs, the debugging tool will display the original code directly instead of the transformed code. Upload Sourcemap files and use Sourcemap for code deobfuscation

<span id=".U291cmNlbWFwIOeuoeeQhueahOS9jee9rg=="></span>
## sourcemap management


* Sourcemap management

* Version details page

   The version details page can be accessed from the **JavaScript error details** page by clicking **manage sourcemap**.


<span id=".5aaC5L2V5LiK5LygU291cmNlbWFw"></span>
## Upload Sourcemap


* (Recommended, webpack plugin) Use @apm\-insight\-web/upload\-sourcemaps\-webpack\-plugin to automatically upload

* (Recommended, Vite plugin) Use @apm\-insight\-web/upload\-sourcemaps to build a Vite plugin for automatic upload

* Use @apm\-insight\-web/upload\-sourcemaps to automatically upload

* Manually upload using the platform


<span id=".5L2_55SoIHVwbG9hZC1zb3VyY2VtYXBzLXdlYnBhY2stcGx1Z2luICjmjqjojZAp"></span>
### (Recommended, webpack plugin) Use upload\-sourcemaps\-webpack\-plugin


1. At the top of the **manage sourcemap** page, obtain the API_KEY and API_TOKEN required for authentication.

2. Run the following command to install the add\-on.

   ```bash
   npm install @apm-insight-web/upload-sourcemaps-webpack-plugin --save-dev
   ```
   

3. Add the following script in `webpack.config.js`. Use the plugin.

   ```js
   const UploadSourcemapsPlugin = require('@apm-insight-web/upload-sourcemaps-webpack-plugin').default;
   
   const config = {
     plugins: [
       new UploadSourcemapsPlugin({
         app_id: 123456,
         paths: ['./dir1', './dir2'],  // Path containing sourcemap files; we will upload symbol table files to the platform from this path. Currently, only single-level directories are supported.
         release: "1.0.1", // Your sourcemap version must match your sdk version. This field is optional; if not specified, the default value is empty.
         appKey: "你的 API_KEY", // API Key obtained from the sourcemap management page, used for authentication
         appSecret: "你的 API_TOKEN", // API token obtained from the sourcemap management page, used for authentication
         host: "open.apmplus.cn-beijing.volces.com", // For Asia Pacific (Johor), enter open.apmplus.ap-southeast-1.volces.com
       }),
     ],
   }
   ```
   


<span id="2c4118dd"></span>
### (Recommended, Vite plugin) Use @apm\-insight\-web/upload\-sourcemaps to build and use a Vite plugin


1. At the top of the **Manage sourcemap** page, obtain the API_KEY and API_TOKEN required for authentication.

2. Run the following command to install the add\-on. You can also select global installation.


```Bash
npm install @apm-insight-web/upload-sourcemaps --save-dev
```



3. Use @apm\-insight\-web/upload\-sourcemaps to build a Vite plugin


```TypeScript
import { UploadSourcemapsCommand } from '@apm-insight-web/upload-sourcemaps'
import { Plugin } from 'vite'

interface Options {
  paths?: string[]
  app_id: string
  host?: string
  env?: string
  release?: string
  appSecret: string
  appKey: string
}

const uploadSourcemapsPlugin = function(options: Options): Plugin {
  return {
    name: 'vite-upload-sourcemaps-plugin',
    apply: 'build',
    closeBundle: async () => {
      let { paths } = options
      const { host, env, release, app_id, appSecret, appKey } = options
      if (!paths || !Array.isArray(paths) || !paths.length) {
        paths = ['./dist/assets']
      }
      try {
        await UploadSourcemapsCommand.upload({
          paths,
          app_id,
          host,
          env,
          release,
          appSecret,
          appKey,
        })
      // eslint-disable-next-line @typescript-eslint/no-unused-vars, no-empty
      } catch (e) {
      }
    },
  }
}
```



4. Add the plugin and use it in `vite.config.ts`.


```TypeScript
export default defineConfig({
  plugins: [uploadSourcemapsPlugin({
      app_id: '123456',
      paths: ['./dist/assets'],  // Path containing sourcemap files; we will upload symbol table files from it to the platform. Currently, only single-level directories are supported.
      release: "1.0.1", // Your sourcemap version must match the sdk version. This field is optional; if left blank, the default is empty.
      appKey: "你的 API_KEY", // Api Key obtained from the sourcemap management page, used for authentication
      appSecret: "你的 API_TOKEN", // API token obtained from the sourcemap management page, used for authentication
      host: "open.apmplus.cn-beijing.volces.com", // For Asia Pacific (Johor), enter open.apmplus.ap-southeast-1.volces.com
  })],
  build:{
    sourcemap:true
  }
})
```


<span id=".5L2_55SodXBsb2FkLXNvdXJjZW1hcOW3peWFtw=="></span>
### Use upload\-sourcemaps


1. At the top of the **Manage sourcemap** page, obtain the API_KEY and API_TOKEN required for authentication.

2. Run the following command to install the add\-on. You can also choose to install globally.

   ```bash
   npm install @apm-insight-web/upload-sourcemaps --save-dev
   ```
   

3. Use plugins

   * Direct upload (for apps in the Asia Pacific (Johor) region, you need to specify open.apmplus.ap\-southeast\-1.volces.com as the upload domain after \-\-host)

      ```bash
      npx upload-sourcemaps --app_id xxxxxx --paths ./dir1 --app_key <API_KEY> --app_secret <API_TOKEN> --host open.apmplus.cn-beijing.volces.com
      ```
      

   * Specify the release version (optional). (If the app is in the Asia Pacific (Johor) region, after \-\-host, you need to enter open.apmplus.ap\-southeast\-1.volces.com as the upload domain name.)

      release must be a standard string and may contain only English characters separated by underscores (_). Colons (:) and other special characters are not supported.

      ```bash
      npx upload-sourcemaps --app_id xxxxxx --paths ./dir1 --release 1.0.1 --app_key <API_KEY> --app_secret <API_TOKEN> --host open.apmplus.cn-beijing.volces.com
      ```
      


<span id=".6aqM6K-BU291cmNlbWFw5ZCI5rOV5oCn"></span>
## Validate the Sourcemap validity

If you have confirmed that the Sourcemap has been uploaded, the format is correct, and the release mapping is correct, but the result of reverse mapping is still incorrect... You can use the following method to perform a self\-test.


1. Download the corresponding Sourcemap on the platform.

   1. On the specific error page, locate the name of the file with the error and check whether release information is available.

   2. Click **Manage sourcemap**, then in the **SourceMap** management module in the version details, search for the corresponding file name.

   3. Locate the corresponding Sourcemap file, and click **download Sourcemap** in the Actions column.

2. Download the official Mozilla Sourcemap reverse parsing library.

   Download links: https://github.com/mozilla/source\-map.

3. Use the following script to perform reverse decoding.

   ```JavaScript
   var sourceMap = require("source-map");
   var fs = require("fs");
   // Replace here with the sourcemap file you downloaded
   let data = fs.readFileSync("../index.js.5d59fc.js.map").toString();
   const consumer = new sourceMap.SourceMapConsumer(data);
   consumer.then(c => {
     // Replace here with the original error line and column number
     const line = 23,
       column = 112003;
     let s = c.originalPositionFor({ line, column });
     console.log(s);
     console.log(`origin code for line: ${line}, ${column}\n`);
     console.log(
       `======================================================================`
     );
     console.log(
       c
         .sourceContentFor(s.source)
         .split("\n")
         .slice(Math.max(s.line - 10, 0), s.line + 10)
         .join(`\n`)
     );
     console.log(
       `======================================================================`
     );
   });
   ```
   

4. Check output results.

   * Successful output: When output is successful, the reverse\-engineered original code should be visible.

      ```Bash
      $   node   index.js
      origin   code   for   line:   373,   2432186
      ======================================================================
                  });
                  setTimeout(()   =>   {
                        throw   new   Error('local   test,   plz   ignore');
                  },   1000);
            },   []);
            return   (
                  <Provider   store={store}>
                        <Player   />
                  </Provider>
            );
      };
      ======================================================================
      ```
      

      Self\-test results are normal. It is recommended to submit a ticket for feedback.

   * Failure output: All variable attributes in a failure output will be null, and the output source code will report an error.

      ```Bash
      $   node   index.js
      {   source:   null,   line:   null,   column:   null,   name:   null   }
      origin   code   for   line:   373111,   2432186
      ======================================================================
      (node:4136)   UnhandledPromiseRejectionWarning:   Error:   "null"   is   not   in   the   SourceMap.
               ...
      ```
      

      Self\-test results also show that reverse parsing is not possible, indicating that either the Sourcemap or the original file is incorrect. Please check whether the Sourcemap file has been overwritten or the JS file has been reprocessed.
