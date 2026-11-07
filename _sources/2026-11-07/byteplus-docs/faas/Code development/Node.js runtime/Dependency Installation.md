---
title: "Dependency Installation"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Node_js_runtime_Dependency_Installation"
---

For the Node.js runtime, the Function Service supports two methods: online installation of dependencies and packaging dependencies with code for upload. This topic introduces these two methods of dependency installation.

<span id="online-installation-of-dependencies-recommended"></span>
## Online Installation of Dependencies (Recommended)

Install dependencies online through the Function Service console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The Function Service will check the <code>package.json</code> file in the root directory of the code package and attempt to install packages based on the dependencies listed in <code>package.json</code>:</div>



* <div data-tips="true" data-tips-type="tip">If a <code>package-lock.json</code> file exists, dependencies are installed using the npm install command.</div>


* <div data-tips="true" data-tips-type="tip">If a <code>yarn.lock</code> file exists, dependencies are installed using the yarn install command.</div>


* <div data-tips="true" data-tips-type="tip">If both do not exist, npm install is used by default to install dependencies.</div>


1. Create a Node.js runtime function, for specific actions refer to [Creating event functions](https://docs.byteplus.com/en/docs/faas/Creating_event_functions).

2. Switch to the **Code** tab of the target function, and configure dependency information in the `package.json` file. Note that you must follow the [Official syntax specifications](https://docs.npmjs.com/cli/v10/configuring-npm/package-json).

3. Click **Install dependencies**, and the system begins installing dependencies online.

   All dependencies will be installed in the `node_modules` directory.


<span id="package-dependencies-and-code-together-and-uploading"></span>
## Package dependencies and code together and uploading

By using dependency management tools (npm/yarn/pnpm), install dependencies locally and then package them together with the function code for uploading.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When packaging, the entry file index.js must be in the <code>.zip</code> package's root directory. If you package and upload the entire folder in a <code>.zip</code> package, it will fail to create the function because the entry file cannot be found in the root directory after extraction.</div>


* <div data-tips="true" data-tips-type="warning">The Zip package size must not exceed 256 MiB.</div>


* <div data-tips="true" data-tips-type="warning">Due to differences in the runtime environments, confirm that the Node version is compatible with your function's runtime version. Run <code>node -v</code> in the local environment to view the version.</div>


1. In the local project root directory `package.json`, configure the dependencies information according to the [official syntax specification](https://docs.npmjs.com/cli/v10/configuring-npm/package-json).

   Example:

   ```json
   {
     "name": "package-name",
     "version": "1.0.0",
     "description": "",
     "main": "index.js",
     "scripts": {
       "test": "echo \"Error: no test specified\" && exit 1"
     },
     "author": "",
     "dependencies": {
       "axios": "1.6.0",
       "p-limit": "6.1.0",
       "cookie": "0.6.0",
       "yargs": "17.7.2",
       "mocha": "10.7.0"
     }
   }
   ```
   

2. In the local project root directory, run the following command to install dependency packages.


```bash
npm install # Install the dependencies you need

#or
yarn install # You can use any package manager
#or
pnpm install # You just need to make sure node_modules and package.json are available
```



3. Run the following command to package all files in the root directory into a deployment.zip .zip file.


```bash
# This example only illustrates with deployment.zip, the actual filename is not restricted
zip -r ./deployment.zip .
```



4. Upload the deployment.zip file to the function Service console for Deployment, for details refer to [Creating event functions](https://docs.byteplus.com/en/docs/faas/Creating_event_functions).
