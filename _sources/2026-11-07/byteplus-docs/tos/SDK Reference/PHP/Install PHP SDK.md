---
title: "Install PHP SDK"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Install-the-php-sdk"
---

This article explains how to install the TOS PHP SDK.

<span id=".546v5aKD5YeG5aSH"></span>
## Environment


* The TOS PHP SDK supports PHP version 5.6 and above; this document uses PHP 5.6 as an example.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Since TOS provides an HTTP protocol interface, your PHP environment needs to enable the cURL and OpenSSL extensions through <code>php.ini</code> to send HTTP or HTTPS requests.   </div>
   

* Supported operating systems: Linux, macOS, and Windows.


<span id=".5rqQ56CB5LiL6L29"></span>
## Source code download


* For the TOS PHP SDK source code, see: [GitHub](https://github.com/volcengine/ve-tos-php-sdk).

* Version revision history: [CHANGELOG](https://github.com/volcengine/ve-tos-php-sdk/blob/main/CHANGELOG.md).


<span id=".5a6J6KOF5pa55byP"></span>
## Installation methods

You can install the SDK using the following methods:

<span id=".77yI5o6o6I2Q77yJ5L2_55SoLXBocC3nmoTljIXnrqHnkIblt6XlhbctY29tcG9zZXI="></span>
### (Recommended) Use PHP's package manager composer

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">composer version V1 stopped supporting on September 1, 2025; please use composer version V2.</div>



1. Run the following command to upgrade Composer from V1.x to V2.x.

   ```PHP
   // Download the specified version of Composer 2
   curl -sS https://getcomposer.org/installer | php -- --version=2.7.6
   // Install to the global PATH
   sudo mv composer.phar /usr/bin/composer
   // Verify
   composer --version
   ```
   

2. Directly run `composer require volcengine/ve-tos-php-sdk`, or add the following dependency in `composer.json` and then run `composer install`.

   ```json
   {
       "require": {
         "volcengine/ve-tos-php-sdk": "^2.1"
       }
   }
   ```
   

3. After successful installation, TOS PHP SDK will be included in the `vendor/` directory; you can import dependencies in your code as follows.

   ```php
   // Assume the script integrating the SDK and the vendor/ directory are under the same parent directory
   require_once __DIR__ . '/vendor/autoload.php';
   ```
   


<span id=".5L2_55SoLXRvcy1waHAtc2RrLeeahC1waGFyLeaWh-S7tg=="></span>
### Use the phar file of TOS PHP SDK


1. Select the corresponding version on GitHub and directly download the packaged phar file.

2. Import dependencies in your code as follows.

   ```php
   // Assume the script integrating the SDK and the TOS PHP SDK source code are under the same parent directory when using source installation
   require_once __DIR__  .  '/ve-tos-php-sdk-2.x.x.phar';
   ```
   


<span id=".5L2_55SoLXRvcy1waHAtc2RrLea6kOeggQ=="></span>
### Use TOS PHP SDK source code


1. Select the corresponding version on GitHub and download the source code directly.

2. After downloading, the TOS PHP SDK source code includes the `autoload.php` file, which can be used to include dependencies in the code as follows.

   ```php
   // Assume the script integrating the SDK and the TOS PHP SDK source code are under the same parent directory when using source installation
   require_once __DIR__  .  '/autoload.php';
   ```
