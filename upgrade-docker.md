---
title: Update
---

## Step 1 - `Update LIVCK`

If you installed the software with the Docker-Compose Stack (install.sh), you've come to the right place.

The whole thing takes a few minutes and is very easy to understand.

```shell
cd /opt/livck
```

This step can take a few minutes

```shell
docker-compose exec app php artisan update --force
```

Restarting the application
```shell
docker-compose restart
```

## Step 2 - `Correcting file permissions`

After successfully updating the software, we should set the required rights again

```shell
chmod -R gu+w storage/ && chmod -R guo+w storage/ && chmod -R gu+w bootstrap/cache/ && chmod -R guo+w bootstrap/cache/
```

## Step 3 - `Restarting the container`

After the update, you should restart the container so that all changes are applied.

```shell
docker-compose restart
```



















