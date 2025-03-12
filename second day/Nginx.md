Первым делом надо скачать nginx

Dnf install nginx

Дальше заходим в директорию где будут лежать наши файлики

Cd /opt/data

Создаем файл index.html в котором напишем слова которые будут у нас на сайте

Touch index.html

Nano index.html

Внутри него пишем 

<meta charset=”utf-8”>

<html>

	<h1>добро пожаловать на корпоративный портал компании destination reachable</h1>
 <img src=”logo.svg” alt=”профессионалы”>
</html>


Сохраняем и выходим

Дальше нам надо сделать логотип професионалов чтобы отображалось на сайте

Переходим на сайт http://pro.firpo.ru

Нажимаем на верхнюю картинку открыть в новом окне и запоминаем его ссылку

Переходим в папку /opt/data и пишем

Wget https://pro.firpo.ru/tm/tm_4/assets/img/logo.svg

Теперь у нас будет картинка на сайте

Настроиваем lighttpd для реверс прокси

Dnf install lighttpd

Nano /etc/ligghtpd/lighttpd.conf

В файле меняем параметры под нас

(порт, стираем все до run, указываем /opt/data) порт 81

Дальше нам надо настроить конфиг nginx

Заходим в конфиг 

Nano /etc/nginx/nginx.conf

Удаляем все внизу после строчек с http

И пишем свое

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

Даем chmod и chown для папки

Chown -R lighttpd:lighttpd /opt/data

Chmod -R 0755 /opt/data

Дальше пишем команду после которой у меня все заработало

Restorecon -Rv 

Также надо отключить selinux

Nano /etc/selinux

Selinux=permissive

И навсякий случай setenforce 0


