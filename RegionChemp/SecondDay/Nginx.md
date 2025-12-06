1. Первым делом надо скачать nginx

```bash
Dnf install nginx
```

2. Дальше заходим в директорию где будут лежать наши файлики

```bash
Cd /opt/data
```
3. Создаем файл index.html в котором напишем слова которые будут у нас на сайте
```bash
Touch index.html
Nano index.html
```
4. Внутри него пишем 
```html
<meta charset=”utf-8”>

<html>
	<h1>добро пожаловать на корпоративный портал компании destination reachable</h1>
 <img src=”logo.svg” alt=”профессионалы”>
</html>
```
5. Дальше нам надо сделать логотип професионалов чтобы отображалось на сайте

6. Переходим на сайт http://pro.firpo.ru Нажимаем на верхнюю картинку открыть в новом окне и запоминаем его ссылку

7. Переходим в папку /opt/data и пишем
```bash
Wget https://pro.firpo.ru/tm/tm_4/assets/img/logo.svg
```
8. Теперь у нас будет картинка на сайте

**Настраиваем lighttpd для реверс прокси**
```bash
Dnf install lighttpd
Nano /etc/ligghtpd/lighttpd.conf
```
1. В файле меняем параметры под нас
	(порт, стираем все до run, указываем /opt/data) порт 81
2. Дальше нам надо настроить конфиг nginx
	Заходим в конфиг 
```bash
Nano /etc/nginx/nginx.conf
```
3. Удаляем все внизу после строчек с http и пишем свое
```bash
Server {
 listen 80;
 Server_name _;
 Return 404;
}
Server {
 Listen 80;
 Server_name corp.jun.profi;

Location / {
 Proxy_pass http://127.0.0.1:81
 Proxy_set_header X-Real-IP $remote_addr;
 Proxy_set_header X-Forwarded-For $reemote_addr;
 Proxy_set_header Host $host;
 Proxy_set_header X-Forwarded-Port $server_port;
}
}
}
```
4. Даем chmod и chown для папки
```bash
Chown -R lighttpd:lighttpd /opt/data

Chmod -R 0755 /opt/data
```
5. Дальше пишем команду после которой у меня все заработало
```bash
Restorecon -Rv 
```
6. Также надо отключить selinux
```bash
Nano /etc/selinux
Selinux=permissive
```
7. И навсякий случай setenforce 0


