---
title: Debugging Dispatcher Tools
description: The Dispatcher Tools provides a containerized Apache Web Server environment that can be used to simulate AEM as a Cloud Services' AEM Publish service's Dispatcher locally. Debugging Dispatcher Tools' logs and cache contents can be vital in ensuring the end-to-end AEM application and supporting cache and security configurations are correct.
feature: Dispatcher
jira: KT-5918
topic: Development
role: Developer
level: Beginner, Intermediate
exl-id: f0adf7a6-c7c2-449a-9fa5-402c54b812e5
duration: 56
TQID: https://experienceleague.adobe.com/9rh-4gyrFQjq7picOBACMe3fZVHxNCALuvslHJ9w7lw
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
---
# Debugging Dispatcher Tools

The Dispatcher Tools provides a containerized Apache Web Server environment that can be used to simulate AEM as a Cloud Services' AEM Publish service's Dispatcher locally. 

Debugging Dispatcher Tools' logs and cache contents can be vital in ensuring the end-to-end AEM application and supporting cache and security configurations are correct.

>[!NOTE]
>
>Since Dispatcher Tools is container-based, every time it is restarted, prior logs and cache contents are destroyed.

## Dispatcher Tools logs

Dispatcher Tools logs are available via the `stdout` or the `bin/docker_run` command, or with more detail, available in the Docker container at `/etc/https/logs`.

See [Dispatcher logs](./logs.md#dispatcher-logs) for instructions on how to directly access the Dispatcher Tools' Docker container's logs.

## Dispatcher Tools cache

### Accessing logs in the Docker container

The Dispatcher cache can be directly accessing in the Docker container at ` /mnt/var/www/html`.

```shell
$ docker ps

# locate the CONTAINER ID associated with "adobe/aem-ethos/dispatcher-publisher" IMAGE
CONTAINER ID        IMAGE                                       COMMAND                  CREATED             STATUS              PORTS                  NAMES
46127c9d7081        adobe/aem-ethos/dispatcher-publish:2.0.23   "/docker_entrypoint.…"   6 seconds ago       Up 5 seconds        0.0.0.0:8080->80/tcp   wonderful_merkle

$ docker exec -it <CONTAINER ID> /bin/sh

/ # 
/ # cd /mnt/var/www/html

# When finished viewing the cache, exit the Docker container's shell
/# exit
```

### Copying the Docker logs to the local filesystem

Dispatcher logs can be copied out of the Docker container at `/mnt/var/www/html` to the local file system for inspection using your favorite tools. Note that this is a point-in-time copy, and does not provide real time updates to the cache.

```shell
$ docker ps

# locate the CONTAINER ID associated with "adobe/aem-ethos/dispatcher-publisher" IMAGE
CONTAINER ID        IMAGE                                       COMMAND                  CREATED             STATUS              PORTS                  NAMES
46127c9d7081        adobe/aem-ethos/dispatcher-publish:2.0.23   "/docker_entrypoint.…"   6 seconds ago       Up 5 seconds        0.0.0.0:8080->80/tcp   wonderful_ira

$ docker cp -L <CONTAINER ID>:/mnt/var/www/html cache 
$ cd cache
```
