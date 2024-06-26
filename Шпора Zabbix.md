1. Скачиваем докер и докер компоуз
```bash
apt update
apt install docker-ce docker-compose -y
systemctl enable docker
systemctl start docker
```

2. Настраиваем директории для хранения файлов:
```bash
mkdir -p /opt/app/{nginx,db} /opt/app/nginx/{conf.d,certs}
cd /opt/appbash
mkdir -p /opt/app/{nginx,db} /opt/app/nginx/{conf.d,certs}
cd /opt/app
touch docker-compose.yml .env /opt/app/nginx/default.conf
touch docker-compose.yml .env /opt/app/nginx/default.conf
```
3. Создаём .env файл:
``` env
POSTGRES_DB=zabbix
POSTGRES_USER=zabbix
POSTGRES_PASSWORD=P@ssw0rd
DB_SERVER_HOST=db
ZBX_SERVER_HOST=zabbix-server
```
4. Создаём docker-compose:
```yaml
version: '3'
services:
  db:
    image: postgres:15
    container_name: db
    hostname: db
    restart: always
    env-file:
      - /opt/app/.env
    volumes:
	  - /opt/app/db:/var/lib/postgresql/data

  zabbix-server:
    image: zabbix/zabbix-server-pgsql
    container_name: zabbix-server
    hostname: zabbix-server
    restart: always
    ports:
      - 10051:10051
    env-file:
      - /opt/app/.env

  zabbix-web:
    image: zabbix/zabbix-web-nginx-pgsql
    container_name: zabbix-web
    hostname: zabbix-web
    restart: always
    env-file:
      - /opt/app/.env

  nginx:
    image: nginx
    container_name: nginx
    hostname: nginx
    restart: always
    ports:
      - 80:80
      - 443:443
    volumes:
     - /opt/app/nginx/conf.d:/etc/nginx/conf.d
     - /opt/app/nginx/certs:/etc/nginx/certs

  pg-admin:
    image: dpage/pgadmin4
    container_name: pg-admin
    hostname: pg-admin
    restart: always
    environment:
      PGADMIN_DEFAULT_EMAIL: admin@nvr.jun.profi
      PGADMIN_DEFAULT_PASSWORD: P@ssw0rd
```
5. Создаём конфигурационный файл nginx
``` nginx.conf
server {
	listen 80;
	server_name _;

	location / {
		proxy_pass http://zabbix-web:8080;
	}
}

## Использовать когда сертификаты будут в /opt/app/nginx/certs
## ${CERT_NAME} и ${KEY_NAME} заменить на название файлов ключа и сертификата
## когда они будут лежать в директории /opt/app/nginx/certs

#server {
#	listen 443 ssl;
#	server_name _;
#
#	ssl_certificate /etc/nginx/certs/${CERT_NAME}
#	ssl_certificate_key /etc/nginx/certs/${KEY_NAME}
#
#	location / {
#		proxy_pass http://zabbix-web:8080;
#	}
#}
```

6. Запускаем докер
```bash
docker compose --file /opt/app/docker-compose.yml up -d
```