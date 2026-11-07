---
title: "Adding or replacing key pairs within instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Adding-or-replacing-key-pairs-for-instances"
---

You can associate a Linux instance with only one key pair in the console. Within a Linux instance, you can manually edit the ~/.ssh/authorized_keys file to add multiple key pairs to the instance. This way, you can log in to the instance by using different key pairs. You can also refer to the following steps to replace the existing key pairs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you need only one key pair, we recommend that you associate the key pair with the instance in the console. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Binding-key-pairs-to-instances">Associating key pairs with instances</a>.</div>


* <div data-tips="true" data-tips-type="tip">After you replace or delete a key pair within an instance, the key pair is disassociated from the instance. To permanently delete the key pair, you need to disassociate the key pair from the instance in the console and make sure that the key pair is not associated with any other instance. For information about how to disassociate a key pair from an instance in the console, see <a href="https://docs.byteplus.com/en/docs/ecs/Unbinding-key-pairs-from-instances">Disassociating key pairs from instances</a>.</div>



<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

You have obtained the public key information of the target key pair. For more information, see [Viewing public key information](https://docs.byteplus.com/en/docs/ecs/Viewing-public-keys).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Use an existing key pair to [log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to open the ~/.ssh/authorized_keys file.

   `vim .ssh/authorized_keys`

3. Press `i` to enter the edit mode.

4. Add or replace public key information.

   * **Add public key information**: Add new public key information below the existing public key information. This way, you can log in to the same instance by using multiple key pairs.

      If the public key file contains multiple public keys, you can log in to the instance by using any corresponding private key.

      ```Plain Text
      ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCxxxxxxMluApvIRol1fqXDJtdeesXwVXFOySC4PzRrehfN1Us2huWo03jS7F6f164PNQDehdxxxxxx+aWBBqsZtcEKUKqVY9Vleuyt8zHHtMq8I0GBxxxxxx+T1WQCQJKe7zxxxxxx/XfNF1lBdyuKbLOAA65fWP4ca8xxxxxx/lUyOiCZxIz4EU8NaJPsK0eprwGXQcitvBZCMx7APNFNixxxxxx/eALjqfh8jo1E5t1uy7C38EPxtST7xxxxxx/HIsmlCM2xVdiJSLiTgXWY9fRvMP1BVXD7Pv0xxxxxx/V118XYkiV0rj0XqtzT7IYlFVKxxxxxx/SoJWJiWHd/
      ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDxxxxxxZAnJLM5fSFq1s7WRcB3d0HjDVwPiq2P2ye3vEvKnMcyN0M8F3UYeUhcorPPvODrCvQxxxxxxo8ACtarHnDICdgIW066jKfbPCJI7zRxxxxxx+y24mR4xHJzQUR4wZjbPsDWZPS9cVXBJJJpro5G74z0WVKO2lkjGWJtL6g4lVJgcccAynAxxxxxx+B+g1GD0iqNpM8dOtVxxxxxx+qufC7h2y8NO7Ssi2raCubKsJHcFmqxxxxxx+VTLfWq8CEZ7Vixxxxxx/foL1++TjMIypmfOeZ1pgegW269yS6THmkxxxxxxQ5eFKbWzfkDkRBGrq5rxxxxxx/0QO5V
      ```
      

   * **Replace public key information**: Delete the existing public key information and add new public key information. That is, associate a new key pair with the instance.

      You can also directly delete the existing public key information to disassociate the key pair from the instance.

      ```Plain Text
      ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDxxxxxxZAnJLM5fSFq1s7WRcB3d0HjDVwPiq2P2ye3vEvKnMcyN0M8F3UYeUhcorPPvODrCvQxxxxxxo8ACtarHnDICdgIW066jKfbPCJI7zRxxxxxx+y24mR4xHJzQUR4wZjbPsDWZPS9cVXBJJJpro5G74z0WVKO2lkjGWJtL6g4lVJgcccAynAxxxxxx+B+g1GD0iqNpM8dOtVxxxxxx+qufC7h2y8NO7Ssi2raCubKsJHcFmqxxxxxx+VTLfWq8CEZ7Vixxxxxx/foL1++TjMIypmfOeZ1pgegW269yS6THmkxxxxxxQ5eFKbWzfkDkRBGrq5rxxxxxx/0QO5V                
      ```
      

5. Press `Esc` to exit the edit mode, enter `:wq`, and then press Enter to save and exit the file.


<span id=".57uT5p6c6aqM6K-B"></span>
## Result verification

After you complete the above operations within the instance, if you can log in to the instance by using the new private key, the key pair has been added or replaced.
