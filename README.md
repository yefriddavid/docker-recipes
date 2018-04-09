# Docker-NodeJs-Laravel Recipes 

You will found some important commands for some of this beautyfull tools for developers **php 7.2, mongodb, cron-laravel, ngnex) among others**


### Documentation for humans or beginners

### I am buiding this for now, please sorry for this garabatos
Some topics that you will found here
1. Docker \
2. Laravel \
3. Laravel Installaction \
4. Laravel Passport \
5. NodeJs \
6. Utilities (Socat, Composer, wget) \
7. Dockerfile examples \
8. Laravel Schedules **(Cron)** \
9. Laravel Schedules \
10. Dockers Networks \
11. Firehole \



### Docker and Docker-compose install
```
$ sudo wget -qO- https://get.docker.com/ | sh

$ sudo curl -L https://github.com/docker/compose/releases/download/1.19.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose
```


### NodeJs and NVM Installaction
```
curl https://raw.githubusercontent.com/creationix/nvm/v0.25.0/install.sh | bash 
source ~/.bashrc 
nvm install 9.2.0 
nvm alias default 9.2.0
```





### Some utils docker commands

#### Generals commands
```
docker ps \
docker network ls \
docker network inspect **docker-network-name**
```

#### Change volumen name
```
docker tag image-id image-name
```

### Run docker image command over an specific folder
```
docker run --rm --volume $PWD:/app/temp  -w /app/temp node npm install \
docker run --rm -v $PWD:/app -w /app yefriddavid/nginx-php7.2 composer update 
```


### Docker composer container
```
docker run --rm --interactive --tty \
    --volume $PWD:/app \
    composer install
```











### Docker create networks

***Now we going to create or defined one networks for dockers***
```
networks:
  mynet:
    driver: bridge
    ipam:
      config:
      - subnet: 172.25.0.0/24
```


### Some friendly links
https://fordodone.com/2016/03/30/docker-compose-static-ip-address-in-docker-compose-yml/





```
Configurar las variables de entorno .env del api con los siguientes valores (.env)
cd callcenter0_api
cp .env.example .env

APP_ENV=local
APP_DEBUG=false
APP_LOG_LEVEL=error
```


### Comandos de intalacion API
```
cd deploy

docker-compose -f install-compose.yml up -d

si deseas subir las nuevas aplicaciones con el legacy
docker-compose -f apps-compose.yml -f legacy.yml up -d

Si deseas subur solo la nueva aplicacion
docker-compose -f apps-compose.yml up -d

Si deseas crear la base de datos
docker exec -it securitydb mysql -u root -pPASSWORDBD -e "CREATE DATABASE security"

si deseas construir la base de datos de seguridad
docker exec -it api_laravel php artisan migrate

si deseas instalar la aplicacion para crear las configuraciones
docker exec -it api_laravel php artisan app:install

docker exec -it api_laravel php artisan passport:install
docker exec -it api_laravel php artisan passport:client --password
docker exec -it api_laravel php artisan db:seed
docker exec -it api_laravel composer dump-autoload
docker exec -it api_laravel php artisan api:cache
docker exec -it api_laravel php artisan dev:gen 1

Agregar el usuario para el sistema docker
grant privilege all on *.* to 'Microvoz2018'@'%'


CREATE USER 'ftxcn6eIj5Vuad8'@'173.17.0.18' IDENTIFIED BY 'PASSWORDBD';
GRANT ALL PRIVILEGES ON OP.* TO 'username'@'173.17.0.18' WITH GRANT OPTION;
GRANT ALL PRIVILEGES ON asterisk.* TO 'username'@'173.17.0.18' WITH GRANT OPTION;
GRANT ALL PRIVILEGES ON CRM.* TO 'username'@'173.17.0.18' WITH GRANT OPTION;



//security db
CREATE USER 'username'@'173.17.0.18' IDENTIFIED BY 'PASSWORDBD'
GRANT ALL PRIVILEGES ON DBNAME.* TO 'username'@'173.17.0.18' WITH GRANT OPTION


```

### Notes and tips:
```
La red interna de los dockers es 173.17.0.0
ifconfig

**Sometimes we have problems with docker run with iptables, therefore it is important to run this command to kill docker services **
ps -ef | grep docker | awk '{print"kill -9",$2}' | sh
```

### Comandos Adicionales
```
dokcer-compose up -d 
docker-compose stop
docker-compose rm -f

docker inspect **dockername**
```





### Darle acceso a los dockers para que se conecten a la base de datos
Tener instalado docker-compose \
docker exec -it securitydb mysql -u root -pPASSWORD -e "CREATE DATABASE security" \
php artisan passport:client --password \
SpsKxZnRrEp1nky0tmrFJmJ8aXueX6G8kchqYzal \
php artisan passport:install \
grant privilege all on *.* to 'username'@'%'










docker run busybox ping 172.17.0.1

docker run busybox nslookup 172.17.0.1
docker run busybox nslookup google.com



--opt "com.docker.network.bridge.name"="docker1"






IPTABLES
iptables -I INPUT -s 173.17.0.0/16 -j ACCEPT
iptables -I OUTPUT -d 173.17.0.0/16 -j ACCEPT
iptables -I FORWARD -d 173.17.0.0/16 -j ACCEPT
iptables -I FORWARD -s 173.17.0.0/16 -j ACCEPT




firehol
interface docker-network-name docker
        policy accept


### Restart  firehol
/etc/init.d/firehol restart




### Here we going to test some routes
wget -d --header="Authorization: Bearer accessTocken" --header='Accept: Application/json' http://0.0.0.0:81/api/ping



xinetd
telnet localhost 4573

wget -d --header="Authorization: Bearer put-tocken-here" --header='Accept: Application/json' http://173.17.0.20:81/api/foo






crontab -u root laravel-cron



172.19.0.3      localhost
::1     localhost ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
172.19.0.2      8da2f8c0befd
~



para scripts

/etc/hosts
172.19.0.3      localhost
172.19.0.2      8da2f8c0befd
~
~


## Some utils apps

apt-get install socat \
sudo socat TCP-LISTEN:81,fork TCP:173.17.0.20:80


# docker-composer-php


