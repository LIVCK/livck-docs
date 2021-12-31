---
title: Old Installation (Outdated)
---

::: warning
We recommend that you use the Docker-Compose stack.
This installation is no longer supported!

[Use the docker-compose Stack](/)
:::

### These instructions are based on an Ubuntu 20.04 server.
##### If you have not yet found a suitable hosting provider to host this status page, we can recommend [Hetzner Online GmbH](https://livck.com/go/hetzner)

## Introduction

**Prerequisites**

A server with Ubuntu-20.04 or newer is preinstalled for this.

The default credentials of the software
* Username: `admin@example.com`
* Password: `livvck`

## Step 1 - `Update & Upgrade`

The very first thing we do is update the package lists and packages on the server so that we are up to date.

```shell
apt update && apt upgrade -y
```

## Step 2 - `Install Dependencies`

Now we install the necessary dependencies for the software, including Php, Nginx & Supervisor

```shell
apt -y install php7.4 php7.4-{cli,gd,mysql,pdo,mbstring,tokenizer,bcmath,xml,fpm,curl,zip} wget unzip nginx supervisor curl redis-server
```

### Step 2.1 - `Install Composer`

Now we install the Package-Manager **Composer**, which allows the software to obtain more of its necessary packages

```shell
curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer
```

## Step 3 - `Create Source Folder`

We will now create a folder where the software will eventually reside

```shell
mkdir -p /var/www/livck
```

### Step 3.1 - `Download files from LIVCK`

You can find your license on the [LIVCK](https://livck.com/manage/licenses) page under your profile, copy it and paste it in the URL (Replace it with REPLACE)

Before you can start the download, you have to enter the IP of the server into the [IP Whitelist](https://livck.com/manage/whitelist) of LIVCK. You can find the IP in the HCloud panel, but it is enough to whitelist the IPv4.

```shell
cd /var/www/livck && wget -4 https://livck.com/dl/self-hosted/REPLACE -O livck.zip
```

### Step 3.2 - `Unpacking LIVCK files`

```shell
unzip livck.zip
```

### Step 3.3 - `Move LIVCK files to correct folder`

```shell
mv LIVCK-self-hosted-*/* . && cp LIVCK-self-hosted-*/.env.example .env
```

### Step 3.4 - `Delete unless files`

```shell
rm LIVCK-self-hosted-* -R && rm livck.zip
```

### Step 3.5 - `Configure Application`

For LIVCK a database like MySQL is needed, for this you can already find a tutorial [here](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04-de).

**Create a database and a user (or use the root), which we can specify in the application**

```shell
nano .env
```

You will now see this in the editor similar to the one shown below, there you can customize the name (APP_NAME) & under DB_DATABASE will be the database name you created as well as user and a password.
Finally you only have to set your license key under LICENSE_KEY and the configuration would be done.

```dotenv
APP_NAME=LIVCK
APP_URL=http://your-domain.com

LICENSE_KEY="XXXX-XXXX-XXXX-XXXX-XXXX"

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=livck
DB_USERNAME=root
DB_PASSWORD="password"
REDIS_HOST=127.0.0.1
CACHE_DRIVER=redis
```

## Step 4 - `Install LIVCK`

Now we install the required packages for the software.

```shell
composer install --no-dev --optimize-autoloader --ignore-platform-reqs && chmod -R gu+w storage/ && chmod -R guo+w storage/ && chmod -R gu+w bootstrap/cache/ && chmod -R guo+w bootstrap/cache/
```

### Step 4.1 - `Configure Supervisor`

Now we configure the queue with supervisor.

```shell
nano /etc/supervisor/conf.d/livck.conf
```

**Add the following content to the file and save it**

```
[program:livck-queue-worker]
process_name=%(program_name)s_%(process_num)02d
command=php /var/www/livck/artisan queue:work --queue=default,newsletter --timeout=60 --tries=255
autostart=true
autorestart=true
user=root
numprocs=1
redirect_stderr=true
```

Now restart the supervisor service

```shell
service supervisor restart
```

### Step 4.2 - `Configure Crontab`

Now we run the software backend on crontab.

```shell
{ crontab -l; echo "* * * * * php /var/www/livck/artisan schedule:run >/dev/null 2>&1"; } | crontab -
```

The return of the command is **no crontab for root** and is good!

### Step 4.3 - `Configure Nginx`

Now we configure nginx (webserver).

```shell
nano /etc/nginx/sites-enabled/livck
```

**Edit the content you see below, there replace DOMAIN-NAME to your domain and save it**

If your domain is not yet connected to the server, we would recommend you to set an A record in your DNS.

Name: status (or one of your choice)
Target: Your Server IP

```
server {
    root /var/www/livck/public;

    index index.php;
    server_name DOMAIN-NAME;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        fastcgi_pass unix:/run/php/php7.4-fpm.sock;
        include snippets/fastcgi-php.conf;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }

    location ~ /\.ht {
        deny all;
    }

    listen 80;
}
```

Now restart the nginx service

```shell
service nginx restart
```

### Step 4.4 - `Configure SSL`

Now we configure the ssl of the statuspage.

```shell
apt install certbot python3-certbot-nginx -y
```

**Replace the status.your-domain.de and acme@your-mail.de to yours**

```shell
certbot --nginx --agree-tos -m acme@your-mail.de --domain status.your-domain.de
```

**Please choose whether or not to redirect HTTP traffic to HTTPS, removing HTTP access - To Secure your traffic, choose number 2!**

### Step 4.5 - `Application Key`

Now we can generate the app key

```shell
php artisan key:generate --force
```

### Step 4.6 - `Migrate Database`

Now we can migrate all tables

```shell
php artisan migrate:fresh --seed --force
```

### Step 4.7 - `Storage Availability`

Now we can publish the storage

```shell
php artisan storage:link
```


















