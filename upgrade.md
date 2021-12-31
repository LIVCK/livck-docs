---
title: Update without Docker-Compose Stack
---

## Step 1 - `Update LIVCK`

If you installed the software without Docker, you've come to the right place.

The whole thing takes a few minutes and is very easy to understand.

```shell
cd /var/www/livck
```

This step can take a few minutes

```shell
php artisan update
```

## Step 2 - `Correcting file permissions`

After successfully updating the software, we should set the required rights again

```shell
chmod -R gu+w storage/ && chmod -R guo+w storage/ && chmod -R gu+w bootstrap/cache/ && chmod -R guo+w bootstrap/cache/
```





















