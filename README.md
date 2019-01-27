# Docker for Laravel

This repo is contain docker files for dev with ```laravel```. It include: LEMP stack, MySQL, Phpmyadmin, Traefik, NodeJS.

## How to setup

### Edit hosts file

```bash
sudo nano /etc/hosts
```

* Add your virtual hosts to this file

```bash
127.0.0.1 dev.yourdomain.com
```

### Put your sql script into docker_config/script.sql

### Create network docker

```bash
docker network create proxy
```

### Start docker-compose

* In docker current directory run following command

```bash
docker-compose up -d
```

### Access docker lemp.dev container

```bash
docker exec -ti -u 1000:1000 lemp.dev /bin/bash
cd app
Composer install
php artisan key:generate
php artisan cache:clear
exit
```

### Access docker database.dev container

```bash
docker exec -ti -u 1000:1000 database.dev bash ./tmp/import.sh
```

### Get docker container ip address

```bash
docker inspect database.dev
```

### Access docker nodejs.dev container

```bash
docker exec -ti -u 1000:1000 nodejs.dev bash
npm install
npm run dev
```
