# Docker for Laravel

This repo is contain docker files and how to config environment for dev with ```Laravel``` - The PHP Framework For Web Artisans. It include: ```NGINX```, ```PHP```, ```MySQL```, ```phpMyAdmin```, ```Node.js```, ```Traefik```. Recommend you should use ```Visual Studio Code``` with ```Xdebug``` to coding and debugging.

## How to setup

### First your copy both ```docker_config``` folder and ```docker-compose.yml``` file to root path of your app

### Before run docker you should stop services run on port ```80```, ```3306```, ```9090```, ```8080```. Or you can change port number using by docker container like Treafik, Apache, MySQL

### Edit hosts file

```bash
sudo nano /etc/hosts
```

* Add your virtual hosts to this file

```bash
127.0.0.1 dev.yourdomain.com
```

### Put your sql script into ```docker_config/script.sql```

### Create docker's network name

```bash
docker network create [name]
```

### Start docker-compose

* In docker current directory run following command

```bash
docker-compose up -d
```

### Access docker apache/php container

```bash
docker exec -ti -u 1000:1000 [your container name] /bin/bash
cd app
composer install
composer dumpautoload
php artisan key:generate
php artisan cache:clear
php artisan view:clear
php artisan config:clear
exit
```

### Access docker database container

```bash
docker exec -ti -u 1000:1000 [your container name] bash ./tmp/import.sh
```

### Get docker container ip address

```bash
docker inspect [your container name]
```

### Access docker nodejs container

```bash
docker exec -ti -u 1000:1000 nodejs.dev bash
npm install
npm run dev
```

### Setup debuging with XDebug on Visual Studio Code

* Open file you want to debug and set break-point

* Click on icon Debug on left side-bar or press ```Ctrl + Shift + D```

* Click on setting icon and a menu appear with some options Docker, Node.js, PHP. You select PHP

* A new file ```launch.json``` open

* You change ```port``` option with your owns in ```docker_config\php.ini```

* Add new option

```json
    "pathMappings": {
        "/app": "${workspaceFolder}"
    }
```