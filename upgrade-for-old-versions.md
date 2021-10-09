---
title: Update old versions of livck (~1.1.3 or older)
---

## Step 1 - `Update LIVCK Version **(1.1.3)**`

```shell
cd /var/www
```

### Step 1.1 - `Download files from LIVCK`

You can find your license on the [LIVCK](https://livck.com/manage/licenses) page under your profile, copy it and paste it in the URL (Replace it with REPLACE)

```shell
cd /var/www/livck && wget -4 https://livck.com/dl/self-hosted/REPLACE -O livck.zip
```

### Step 1.2 - `Backup current files of livck`

```shell
tar -cvf livck-backup.tar /var/www/livck
```

### Step 1.3 - `Unpacking & move files`

```shell
unzip livck.zip
```

```shell
cp -r LIVCK-self-hosted-*/* /var/www/livck
```

### Step 1.4 - `Delete Vendor & Caches`

```shell
rm vendor -r && rm composer.lock
```

### Step 1.5 - `Installing new version of LIVCK`

```shell
composer install --no-dev --optimize-autoloader --ignore-platform-reqs && chmod -R gu+w storage/ && chmod -R guo+w storage/ && chmod -R gu+w bootstrap/cache/ && chmod -R guo+w bootstrap/cache/
```

```shell
php artisan migrate --force
```

```shell
php artisan db:seed --class=LivckVersionUpgradeSeeder --force
```

### Step 1.6 - `Installing Cache`

```shell
apt -y install redis-server
```

Set following Parameters to the .env file

```env
REDIS_HOST=127.0.0.1
CACHE_DRIVER=redis
```














