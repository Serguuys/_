1. Скачиваем докер и докер компоуз
```bash
apt update
apt install docker-ce docker-compose -y
systemctl enable docker
systemctl start docker
```

2. Настраиваем директории для хранения файлов:
```bash
mkdir -p /opt/app/{db,nextcloud}
cd /opt/app
touch docker-compose.yml .env
```
3. Создаём .env файл:
``` env
POSTGRES_DB=nextcloud
POSTGRES_USER=nextcloud
POSTGRES_PASSWORD=P@ssw0rd
PGADMIN_DEFAULT_EMAIL=pgadmin@jun.profi
PGADMIN_DEFSULT_PASSWORD=P@ssw0rd
```
4. Создаём docker-compose:
```yaml
version: '3'
services:
  db:
    image: postgres
    container_name: db
    hostname: db
    restart: always
    env_file:
      - /opt/app/.env
    volumes:
	  - /opt/app/db:/var/lib/postgresql/data

  nextcloud:
	 image: nextcloud
	 container_name: nextcloud
	 hostname: nextcloud
	 restart: always
	 ports:
	   - 80:80
	 env_file:
	   - /opt/app/.env
	 volumes:
	   - /opt/app/nextcloud:/var/www/html

  pgadmin:
    image: dpage/pgadmin4
    container_name: pgadmin
    hostname: pgadmin
    restart: always
    ports:
        - 8888:80
    env_file:
        - /opt/app/.env
```
5. Запускаем докер
```bash
docker compose --file /opt/app/docker-compose.yml up -d
```
