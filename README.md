---
title: Installation & Usage
---

### These instructions are based on an Ubuntu 20.04 server.
##### If you have not yet found a suitable hosting provider to host this status page, we can recommend [Hetzner Online GmbH](https://hetzner.cloud/?ref=1sCLayBw4vyG)

## 1. Installing dependencies

```bash
# Update repositories list
apt update

# Install Dependencies
apt -y install php7.4 php7.4-{cli,gd,mysql,pdo,mbstring,tokenizer,bcmath,xml,fpm,curl,zip} nginx supervisor

# Installing Composer
curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer
```

## 2. Download files
The first step in this process is to create the folder where the panel will live and then move ourselves into that newly created folder. Below is an example of how to perform this operation.

##### You can [download](https://livck.com/manage/licenses) the files with your purchased license.
```bash
mkdir -p /var/www/livck
cd /var/www/livck
# Move downloaded files into the folder
# After moving the files, make sure that the storage and bootstrap have permission
chmod 777 * -R
```

## 3. MySQL installation
You will need a database setup and a user with the correct permissions created for that database before continuing any further. If you are unsure how to do this, please have a look at Setting up [MySQL](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04-de)

## 4. Configure the application
```bash
cp .env.example .env
composer install --no-dev --optimize-autoloader
php artisan key:generate --force
```

## 5. Configure Supervisor

```bash
nano /etc/supervisor/conf.d/livck.conf
```

```bash
# Append the following content to the livck.conf
[program:livck-queue-worker]
process_name=%(program_name)s_%(process_num)02d
command=php /var/www/livck/artisan queue:work --queue=default,newsletter --timeout=60 --tries=255
autostart=true
autorestart=true
user=root
numprocs=1
redirect_stderr=true
```

```text
service supervisor restart
``` 

## 6. Configure Crontab

```bash
{ crontab -l; echo "* * * * * php /var/www/livck/artisan schedule:run >/dev/null 2>&1"; } | crontab -
```

## 7. Configure Nginx 

```bash
nano /etc/nginx/sites-enabled/livck
```

```bash
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

## 8. Check Nginx Web-Server

At the end of the installation process, Ubuntu 20.04 starts Nginx. The web server should already be up and running.

```bash
systemctl status nginx
```

##### Output

```bash
● nginx.service - A high performance web server and a reverse proxy server
   Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
   Active: active (running) since Mon 2020-11-06 01:14:00 EDT; 1min 2s ago
 Main PID: 17357 (nginx)
   CGroup: /system.slice/nginx.service
           ├─17357 nginx: master process /usr/sbin/nginx -g daemon on; master_process on
           └─17358 nginx: worker process
```

## 9. Set Environment

Now we set your environment variables

```bash
# Configure your .env file in the project folder
nano .env
```
Make sure that the APP_KEY is not empty (It is empty so execute -> php artisan key:gen)
```bash
APP_NAME="NAME OF YOUR BUSINESS"
APP_ENV=production
APP_KEY="this value is generated"
APP_DEBUG=false
APP_URL=http://yourcompany.com

LICENSE_KEY="XXXX-XXXX-XXXX-XXXX-XXXX"

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=your-name-database
DB_USERNAME=your-database-username
DB_PASSWORD=database-password

MAIL_MAILER=smtp
MAIL_HOST=smtp.mailer.com
MAIL_PORT=25
MAIL_USERNAME=username
MAIL_PASSWORD=password
MAIL_ENCRYPTION=tls

TELEGRAM_BOT_TOKEN="your-generated-bot-token"
```

## 10. SSL / Certbot

If you want to secure your site with an SSL from Let's Encrypt, fly through the following [tutorial](https://certbot.eff.org/lets-encrypt/ubuntufocal-nginx)

## 11. Telegram-Bot Setup

If you have successfully created your Telegram bot and received your bot token, you can save it in your environment variables under **TELEGRAM_BOT_TOKEN**
- [Create Bot](https://t.me/BotFather)
- [Get own Client Id](https://t.me/userinfobot) ***(This value is an id and is stored in the user profile)***


## 12. Slack Setup

- [Create Slack Account & Channel](https://app.slack.com/workspace-signin)
- [Enable incomming webhooks](https://api.slack.com/messaging/webhooks) ***(This value is an url and is stored in the user profile)***

## 13. Login credentials

You can now call up the status page with your domain or IP
```bash
http://ip-address-or-domain/login
```

You should change the access data you receive as the administrator in your user profile.

Your login credentials:
- Admin
- livvck

To changing the profile password
```bash
http://ip-address-or-domain/manage/profile
```

## 14. Settings
#### The following setting values with their property.

**Title:** <br>This value is displayed in the page title.
<br><br>
**Description:** <br>This value is used for Search engine optimization.
<br><br>
**Monitor Refresh Interval:** <br>This value determines in what second intervals the page is updated.
<br><br>
**Header Logo:** <br>This value must be a URL, but if you don't want an image on your page, you can leave it blank
<br><br>
**Header Title:** <br>This value is the header title, this is only displayed if the header logo is empty.
<br><br>
**Header Color:**<br> This value defines the following backgrounds:
- Header
- Alerts

**Body Color:** <br>This value defines the body background.<br><br>
**Element Color:** <br>This value defines the following backgrounds:
- Tables
- Inputs
- Cards

**Text Color:** <br>This value defines all of the text colors on the page.
<br><br>
**[Open Graph](https://ogp.me/):**<br> All values that begin with og: belong to the Open Graph Protocol. <br><br>
**Whats is Open Graph?** <br>The Open Graph protocol enables any web page to become a rich object in a social graph. For instance, this is used on Facebook to allow any web page to have the same functionality as any other object on Facebook.
<br><br>
**Twitter:** <br>All values starting with twitter: belong to the Twitter-Cards, these let a post with a link from your site look more informative.
<br><br>
**Keywords:** <br>The keywords are to be given as a list, e.g. "livck, status"
<br><br>
**Robots:** <br>The robots are to be given as a list, e.g. "index, follow"
<br><br>
**Date-Format:** <br>The date format is made up of letters, each of which stands for a value in the date. [To build a valid format](https://www.w3.org/TR/NOTE-datetime).
<br><br>
**Monitor Timeout:** <br>This value is given in seconds and determines how long to wait on a monitor if it takes longer to respond.
