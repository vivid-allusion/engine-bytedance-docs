---
title: "What is an ECS Hostname Record"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/_N_NJT"
---

To ensure that the hostname clearly describes its specific purpose, you can customize the hostname of an [ECS instance](https://www.byteplus.com/en/product/ecs) when purchasing an ECS instance or modifying the hostname of an ECS instance after purchasing the ECS instance. For example, the default hostname of an ECS instance might be `iv-ybo19qc2zqijuuub***`. To ensure the hostname describes the actual purpose of the ECS instance, you can change the hostname to `ecs-game-app-huabei1`.

BytePlus PrivateZone can automatically generate a DNS record based on the hostname of each ECS instance, known as a hostname record. Each hostname record corresponding to an ECS instance points to the internal IP address of that ECS instance. This way, you can access the ECS instance through the hostname record. For example, you create a domain `private.zone`, associate your VPC with this domain, and add the hostname `ecs-game-app-huabei1`. BytePlus PrivateZone can then automatically generate a hostname record from the hostname `ecs-game-app-huabei1`. Consequently, you can access the ECS instance corresponding to the hostname through `ecs-game-app-huabei1.private.zone`.
