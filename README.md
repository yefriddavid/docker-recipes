# docker-recipes




docker gat image-id image-name



docker run --rm --volume $PWD:/app/temp  -w /app/temp node npm install
docker run --rm -v $PWD:/app -w /app yefriddavid/nginx-php7.2 composer update
wget 127.0.0.1:81/api/ping

docker run --rm --interactive --tty \
    --volume $PWD:/app \
    composer install


las carpetas deben llamarsen
sistema
sistema-hoy softlik a sistema
etc/microvoz
phone

archivos que involucran la base de datos dentro de phone

phone/includes/xconfiguracion.php



archivos donde hay configuracion de la base de datos
/etc/microvoz
nvf_vars.inc
db_conf


phone/includes/xconfiguracion.php




en el puerto 1512 queda el phone
en el puerto 1513 queda el admin


3004 puerto de pruebas api


https://github.com/microvoz/deploy_basico.git

git clone https://github.com/microvoz/callcenter0_admin.git sistema
cd sistema/v4
composer install

git clone https://github.com/microvoz/phone.git



instalacion docker
sudo wget -qO- https://get.docker.com/ | sh
apt-get install docker.io




instalacion nodejs

curl https://raw.githubusercontent.com/creationix/nvm/v0.25.0/install.sh | bash
source ~/.bashrc
nvm install 9.2.0
nvm alias default 9.2.0








ips statics


networks:
  mynet:
    driver: bridge
    ipam:
      config:
      - subnet: 172.25.0.0/24




https://fordodone.com/2016/03/30/docker-compose-static-ip-address-in-docker-compose-yml/




Instalacion de AGI-ACD

1) Instalcion de Docker y docker-compose

    sudo wget -qO- https://get.docker.com/ | sh

    "sudo curl -L https://github.com/docker/compose/releases/download/1.19.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose"

    sudo curl -L https://github.com/docker/compose/releases/download/1.19.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

    sudo chmod +x /usr/local/bin/docker-compose


2) Descargar repositorio deply-basico

    mkdir /home/microvoz

    cd /home/microvoz

    git clone https://github.com/microvoz/deploy_basico.git deploy


3) Hacer deploy de docker

    cd deploy

    cp .env.example .env

    ./deploy.sh



A continuación se documenta paso a paso la instalación del api, los dockers y el manager:
git clone https://github.com/microvoz/deploy_basico.git deploy
cd deploy
sh deploy.sh
cp .env.example .env


```
Configurar las variables de entorno .env del api con los siguientes valores (.env)
cd callcenter0_api
cp .env.example .env

APP_ENV=local
APP_DEBUG=false
APP_LOG_LEVEL=error
```


#Comandos de intalacion API
```
cd deploy

docker-compose -f install-compose.yml up -d

si deseas subir las nuevas aplicaciones con el legacy
docker-compose -f apps-compose.yml -f legacy.yml up -d

Si deseas subur solo la nueva aplicacion
docker-compose -f apps-compose.yml up -d

Si deseas crear la base de datos
docker exec -it securitydb mysql -u root -pbCE2vnFLDBCznwZcNdKec6NdGX9dJSmwmQnsNSP4 -e "CREATE DATABASE security"

si deseas construir la base de datos de seguridad
docker exec -it api_microvoz php artisan migrate

si deseas instalar la aplicacion para crear las configuraciones
docker exec -it api_microvoz php artisan app:install

docker exec -it api_microvoz php artisan passport:install
docker exec -it api_microvoz php artisan passport:client --password
NOOOOdocker exec -it api_microvoz php artisan db:seed
docker exec -it api_microvoz composer dump-autoload
docker exec -it api_microvoz php artisan api:cache
docker exec -it api_microvoz php artisan dev:gen 1

Agregar el usuario para el sistema docker
grant privilege all on *.* to 'Microvoz2018'@'%'


CREATE USER 'ftxcn6eIj5Vuad8'@'173.17.0.18' IDENTIFIED BY 'VuHonIshkIcUjVewispoajFeghiv8swacGaw';
GRANT ALL PRIVILEGES ON OP.* TO 'ftxcn6eIj5Vuad8'@'173.17.0.18' WITH GRANT OPTION;
GRANT ALL PRIVILEGES ON asterisk.* TO 'ftxcn6eIj5Vuad8'@'173.17.0.18' WITH GRANT OPTION;
GRANT ALL PRIVILEGES ON CRM.* TO 'ftxcn6eIj5Vuad8'@'173.17.0.18' WITH GRANT OPTION;



//security db
CREATE USER 'kIc6jVe41s7oa2'@'173.17.0.18' IDENTIFIED BY 'bCE2vnFLDBCznwZcNdKec6NdGX9dJSmwmQnsNSP4'
GRANT ALL PRIVILEGES ON security.* TO 'kIc6jVe41s7oa2'@'173.17.0.18' WITH GRANT OPTION


```

Comentarios:
```
La red interna de los dockers es 173.17.0.0
ifconfig
```

#Comandos Adicionales
```
dokcer-compose up
docker inspect api_microvoz
ps -ef | grep docker | awk '{print"kill -9",$2}' | sh
```






Darle acceso a los dockers para que se conecten a la base de datos
Tener instalado docker-compose

docker exec -it securitydb mysql -u root -pbCE2vnFLDBCznwZcNdKec6NdGX9dJSmwmQnsNSP4 -e "CREATE DATABASE security"
php artisan passport:client --password
1
SpsKxZnRrEp1nky0tmrFJmJ8aXueX6G8kchqYzal
php artisan passport:install

grant privilege all on *.* to 'Microvoz2018'@'%'

git clonehttps://github.com/microvoz/callcenter0_gestion.git

git clonehttps://github.com/microvoz/callcenter0_admin.git(sistema)






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
interface microvoz-apps docker
        policy accept


Reiniciar  firehol

/etc/init.d/firehol restart





wget -d --header="Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImU5NmI4ZjJjNWRiNzZkODAxMzU2MWQzMWQ5YzQ3ODg5MzA0ZTU0OTQzYjViNjg1ZmEyNWM0ZDU4MDM2ZWZkOGYzNTQ1ZTg2NzFlYzQ5MjU3In0.eyJhdWQiOiIxIiwianRpIjoiZTk2YjhmMmM1ZGI3NmQ4MDEzNTYxZDMxZDljNDc4ODkzMDRlNTQ5NDNiNWI2ODVmYTI1YzRkNTgwMzZlZmQ4ZjM1NDVlODY3MWVjNDkyNTciLCJpYXQiOjE1MTg2NDc3MDQsIm5iZiI6MTUxODY0NzcwNCwiZXhwIjoxNTUwMTgzNzA0LCJzdWIiOiIxIiwic2NvcGVzIjpbXX0.oPhOPXk8_Zx6W75JLhJ7IEso78gW1tmp68csebYr-7_Xj_GpL23L3WGqGX4-VaMnsv8O-PLjlnTyRheh62U0m8b2RP2DVC6VFEyORGRClQjRy6wwgD98Jj_K1-441SOSknvpaGnzXpOL3YeyFna9DHnBWVzYvgD5o8RXiXAJUlgy0--gGy9UUnCdNedKTIeWbvAuCXwpTbUA-lUKkwtHpL6XUc9etEwHX3xBOX9EE92lKJtvfZ2JKwpGVwNLb-xiVszJzBghIQNCCSI-v0HysYt84aK4DWffo91frc8rCfK_7DgEdJ7UhBAd0hUap1GClPd538BhL7fYL3X_HDf5xXQZ8DsqdNCZQ_ZRA_TI8eQRyCxnb-LngqwnK6Xx4u2SPr5_hapORtc9pUvi19S8fZOF3iwj80Qw35UiIspu55qfsodCCn_Q-KcyRubZylJNLPCYPuH-rMHMznxH_cFp926LCcKAE4vRALQrGMGIGkyC_XlIPMDvYSJ4-bkYGbaS6SK4aSsV6keHm-oID77MrSyuH91MFKC_xe_OOVqO4xhT5AHL4hGAdYiVhbG0DX99xVvaUnEQDNr3RxzznJocj43njNaBBOE5qbDICFYnsbZiluzGvFpaEmtMwfCJPWhNmX0LUy9H2ViqeA34v7Jxo_jRX1M7bDlk5aX0TxZbbjk" --header='Accept: Application/json' http://10.10.0.89:81/api/campaigns



xinetd
telnet localhost 4573

wget -d --header="Authorization: Bearer PONERTOKENACA" --header='Accept: Application/json' http://173.17.0.20:81/api/campaigns

wget -d --header="Authorization: Bearer PONERTOKENACA" --header='Accept: Application/json' http://173.17.0.18/api/campaigns








ssh drios@10.10.0.29 -p 51122



crontab -u root microvoz-cron



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



apt-get install socat
sudo socat TCP-LISTEN:81,fork TCP:173.17.0.20:80
