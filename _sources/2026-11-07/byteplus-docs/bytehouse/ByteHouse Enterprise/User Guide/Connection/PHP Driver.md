---
title: "PHP Driver"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/php-driver"
---

This article explains how to connect to and access ByteHouse Cloud Data Warehouse in the PHP development environment.

ByteHouse is compatible with the following open\-source ClickHouse PHP Drivers:


* Connection via HTTP method: smi2/phpClickHouse (This article has been validated with driver version 1.5, PHP version 8.3.4)


<span id="8d9c3d4a"></span>
## Prerequisites

To access the connection information required for ByteHouse, please refer to [Get cluster connection information](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information) to obtain it.

<span id="ca428fe0"></span>
## Usage method

This section introduces the basic usage of connecting to ByteHouse through the smi2/phpClickHouse program, where you can obtain the latest documents and release version information on the program's [Github main page](https://github.com/smi2/phpClickHouse) or [Packagist](https://packagist.org/packages/smi2/phpclickhouse).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">smi2/phpClickHouse software version 1.5 or higher requires PHP 7.3 or higher.</div>


<span id="a18ca5eb"></span>
### Program installation

```Plain
composer require smi2/phpclickhouse

// Install hyperf 3.1 skeleton
// https://hyperf.wiki/3.1/#/zh-cn/quick-start/install
composer create-project hyperf/hyperf-skeleton 
```


<span id="7ae578b1"></span>
## Connect to ByteHouse

Refer to the example code below to connect to ByteHouse, and make sure to fill in the `$config` field according to the information obtained from the premise conditions.

```PHP
<?php

declare(strict_types=1);
/**
 * This file is part of Hyperf.
 *
 * @link     https://www.hyperf.io
 * @document https://hyperf.wiki
 * @contact  group@hyperf.io
 * @license  https://github.com/hyperf/hyperf/blob/master/LICENSE
 */

namespace App\Controller;

use ClickHouseDB\Client;

class IndexController extends AbstractController
{
    public function queryBH()
    {
        $user = $this->request->input('user', 'Hyperf'); // Fill it in with the actual user name
        $password = $this->request->input('password', ''); // Fill it in with the actual password
        $host = $this->request->input('host', ''); // Fill it in with the actual Host
        $query = $this->request->input('query', 'select * from system.clusters'); // sql clause

        $config = [
            'host' => "$host",
            'port' => '8123',
            'username' => "{$user}",
            'password' => "$password",
            'https' => false
        ];
        $db = new Client($config);
        $db->database('default');
        $db->setTimeout(10);       // 10 seconds
        $db->setConnectTimeOut(5); // 5 seconds

        $statement = $db->select($query); 
        $json = json_encode($statement->rows()); //Return the query array
        return [
            'query' => "{$query}",
            'result' => "$json"
        ];
    }
}
```
