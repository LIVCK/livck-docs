---
title: Installation via Docker-Compose
---

### These instructions are based on an Ubuntu 20.04 server.
##### If you have not yet found a suitable hosting provider to host this status page, we can recommend [Hetzner Online GmbH](https://hetzner.cloud/?ref=1sCLayBw4vyG)

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

Now we install the necessary dependencies for the software, including Docker & Docker-Compose

```shell
apt -y install unzip wget
```

```shell
curl https://get.docker.com | sh
```

```shell
apt -y install docker-compose
```

## Step 3 - `Download files from LIVCK`

You can find your license on the [LIVCK](https://livck.com/manage/licenses) page under your profile, copy it and paste it in the URL (Replace it with REPLACE)

Before you can start the download, you have to enter the IP of the server into the [IP Whitelist](https://livck.com/manage/whitelist) of LIVCK.

```shell
cd /opt && wget -4 https://livck.com/dl/self-hosted/REPLACE -O livck.zip
```

### Step 3.1 - `Unpacking LIVCK files`

```shell
unzip livck.zip
```

### Step 3.2 - `Move LIVCK files to correct folder`

```shell
mkdir livck && mv LIVCK-self-hosted-*/* /opt/livck
```

### Step 3.3 - `Delete useless files`

```shell
rm LIVCK-self-hosted-* -R && rm livck.zip
```

## Step 4 - `Configure Application`

Go into the livck folder

```shell
cd livck
```

Execute the following commands to start the installation script.

```shell
chmod 700 install.sh
```

```shell
./install.sh
```














