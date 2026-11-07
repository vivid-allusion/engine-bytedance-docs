---
title: "Manage Access to Objects (PHP SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-access-to-objects-php-sdk"
---

This article describes sample code for obtaining and setting access permissions to an object.

<span id=".YWNsLeivtOaYjg=="></span>
## ACL Description

The access rights (ACLs) of an object take precedence over the access rights of the bucket, and if the object has no access rights set, the access rights of the bucket are followed. Object access is typically set through predefined enumeration values, which are currently supported as follows:


|**access predefined enumeration values** |**describe** |
|---|---|
|Tos\Model\Enum::ACLPrivate |Private. The owner of the object has all permissions, and no other user has permission to operate on the object. |
|Tos\Model\Enum::ACLPublicRead |Public reading. The owner of the object has all permissions, other users only have read permissions to change the object. |
|Tos\Model\Enum::ACLPublicReadWrite |Public reading and writing. All users have read and write access to the object file. |
|Tos\Model\Enum::ACLAuthenticatedRead |The owner of the object has all permissions, and the authenticated user has read access to the object. |
|Tos\Model\Enum::ACLBucketOwnerRead |The object owner has all permissions, and the bucket owner has read permissions on this object. |
|Tos\Model\Enum::ACLBucketOwnerFullControl |Both the bucket owner and the object owner have all the operating rights on the object. |


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

You can set and obtain access permissions to objects through TosClient\- \> putObjectACL and TosClient\- \> getObjectACL, respectively. The example code is as follows:

```php
<?php

// Assuming the use of composer for installation.
require_once __DIR__ . '/vendor/autoload.php';

use Tos\TosClient;
use Tos\Exception\TosClientException;
use Tos\Exception\TosServerException;
use Tos\Model\PutObjectACLInput;
use Tos\Model\GetObjectACLInput;
use Tos\Model\Enum;

try {
    $client = new TosClient([
        'region' => 'your region',
        'endpoint' => 'your endpoint',
        // Get access key from environment variables.
        'ak' => getenv('TOS_ACCESS_KEY'),
        'sk' => getenv('TOS_SECRET_KEY'),
    ]);
    
    // Set object access permissions.
    $input = new PutObjectACLInput('bucket-test',  'key-test');
    $input->setACL(Enum::ACLPublicRead);
    $output = $client->putObjectACL($input);
    echo $output->getRequestId() . PHP_EOL;
    
    // Accessing Object Permissions
    $output = $client->getObjectACL(new GetObjectACLInput($bucket, $key));
    echo $output->getRequestId() . PHP_EOL;
    // Access permission authorization group
    foreach ($output->getGrants() as $grant) {
        echo $grant->getGrantee()->getType() . PHP_EOL;
        echo $grant->getGrantee()->getCanned() . PHP_EOL;
        echo $grant->getPermission() .PHP_EOL;
    }
    // Get object Owner
    echo $output->getOwner()->getID() . PHP_EOL;
    
} catch (TosClientException $ex) {
    echo $ex->getMessage() . PHP_EOL;
} catch (TosServerException $ex) {
    echo $ex->getRequestId() . PHP_EOL;
    echo $ex->getStatusCode() . PHP_EOL;
    echo $ex->getErrorCode() . PHP_EOL;
}
```
