---
title: "Install TLS SDK for Node.js"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/install_tls_sdk_for_nodejs"
---

Before you use Torch Log Service (TLS) SDK for Node.js to call TLS API actions and implement relevant features, install the SDK. This topic describes how to install TLS SDK for Node.js.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Before you begin


* Create and get a BytePlus AccessKey pair.

* The AccessKey pair has the permissions to access all API actions. We recommend that you use an IAM user to call API actions or perform routine O&M. Before you use an IAM user, use a BytePlus account to grant the IAM user the permissions to operate TLS resources.


<span id=".5YeG5aSH5byA5Y-R546v5aKD"></span>
## Preparing a development environment

TLS SDK for Node.js is built in the Node.js environment. Before you integrate the SDK, download and install Node.js. For information on the download URL and relevant operations, visit the [Node.js](https://nodejs.org/en/download/) official website.

<span id=".5a6J6KOFLXNkaw=="></span>
## Installing the SDK


1. Create a project and enter the project directory.

2. Run the following command to initialize the SDK, and configure npm initialization as prompted:

   ```shell
   npm init
   ```
   

   After the initialization, npm automatically creates a configuration file named `package.json`. The file content is as follows:

   ```json
   {
     "name": "nodejs",
     "version": "1.0.0",
     "description": "",
     "main": "index.js",
     "scripts": {
       "test": "echo \"Error: no test specified\" && exit 1"
     },
     "author": "",
     "license": "ISC"
   }
   ```
   

3. Install the SDK using npm.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If a network error occurs when you use npm, we recommend that you use the specified <a href="https://www.npmjs.com/package/@volcengine/openapi">npm image</a>.   </div>
   

   ```shell
   npm install @volcengine/openapi
   ```
   

   After you run the command, the `@volcengine/openapi` information is automatically added to the `package.json` file. File content:

   ```json
   {
     "name": "nodejs",
     "version": "1.0.0",
     "description": "",
     "main": "index.js",
     "scripts": {
       "test": "echo \"Error: no test specified\" && exit 1"
     },
     "author": "",
     "license": "ISC",
     "dependencies": {
       "@volcengine/openapi": "^1.2.2"
     }
   }
   ```
   

4. Build a project using Express.

   This section builds a project using Express as an example. You can use other methods to build a Node.js project as needed.

   1. Run the following npm command to install Express.

      For more information on installing Express, visit the [Express official website](https://www.expressjs.com.cn/starter/installing.html?spm=a2c4g.11186623.0.0.1ccc333dSKBa8P).

      ```shell
      npm install express
      ```
      

   2. Run the following npm command to install [morgan](https://www.npmjs.com/package/morgan?spm=a2c4g.11186623.0.0.1ccc333dSKBa8P):

      ```shell
      npm install morgan
      ```
      

   3. Create a file named `app.js` and add the following code:

      ```javascript
      var express = require('express')
      var morgan = require('morgan')
      var app = express()
      const logger = morgan(function (tokens, req, res) {
        return [
          tokens.method(req, res),
          tokens.url(req, res),
          tokens.status(req, res),
          tokens.res(req, res, 'content-length'), '-',
          tokens['response-time'](req, res), 'ms'
        ].join(' ')
      })
      app.use(logger)
      app.get('/', (req, res) => res.send('Hello World!'))
      app.listen(3001, () => console.log('Listening on port 3001!'))
      ```
      

   4. Run the following command to start the project:

      ```javascript
      node app.js
      ```
      

      The following output is displayed, which indicates that the project is started as expected.

      ```shell
      Listening on port 3001!
      ```
