```python
user@alt apt-get install apache2
user@alt apt-get install apache2-mod_php8.1
user@alt apt-get install php7-pgsql
user@alt mkdir /var/www/html/joomla
user@alt chown -R  apache2:apache2 /var/www/html/joomla
user@alt service httpd2 start
user@alt chkconfig httpd2 on
user@alt apt-get install postgresql15-server
user@alt /etc/init.d/postgresql initdb
user@alt systemctl enable --now postgresql
user@alt psql -U postgres
...
create user cms with password 'P@ssw0rd';
create database cms;
...
user@alt apt install pgadmin3
user@alt apt-get install wget
user@alt wget ftp.postgresql.org/pub/pgadmin/pgadmin4/v8.8/source/pgadmin4-8.8.tar.gz
gzip -d pgadmin4-8.8.tar.gz
xvf
mv web /var/lib/
cp config.py config_local.py
chown apache2:apache2 /var/lib/web -R
chown apache2 /var/log -R
apt-get install python3
chmod 755 /opt/pgadmin4-8.8 -R
apt-get install pip
pip install -r /opt/pgadmin4-8.8/requirements.txt
apt-get install libkrb5-devel -y
apt-get install postgresql15-python




user@alt service mysqld start
user@alt chkconfig mysqld on
user@alt mysqladmin -uroot password пароль
user@alt cd /var/www/html/joomla/
user@alt unzip Joomla_x.x.x-Stable-Full_Package-jino-ru.zip
user@alt chmod -R 777 /var/www/html/joomla //или
user@alt chmod -R 755 /var/www/html/joomla
user@alt /etc/php/X.X/apache2-mod_php/php.ini
user@alt output_buffering = off
user@alt systemctl restart httpd2
```
user@alt who am i
