Сайт откуда инфа: https://sysadminium.ru/create-own-certificate-authority-on-linux/
apt-get install openssl
mkdir /opt/ssl
cd /opt/ssl
$ openssl genpkey -algorithm RSA -out rootCA.key -aes-128-cbc (#указываем пароль обязательно)
$ openssl req -x509 -new -key rootCA.key -sha256 -days 3650 -out rootCA.crt
 ```python
   Enter pass phrase for rootCA.key: P@ssw0rd
   Country Name (2 letter code) [AU]: RU
   State or Province Name (full name) [Some-State]: KLG
   Locality Name (eg, city) []: Kaluga
   Organization Name (eg, company) [Internet Widgits Pty Ltd]: KLG
   Organizational Unit Name (eg, section) []:. KLG
   Common Name (e.g. server FQDN or YOUR name) []: Jun Profi CA (Обязательно такой как по заданию)
```
 $ echo "00" > rootCA.srl
 $ nano klg.cnf
 ```python
[ req ]
default_bits = 2048
distinguished_name = req_distinguished_name
req_extensions = req_ext

[ req_distinguished_name ]
countryName = Country Name (2 letter code)
countryName_default = RU
stateOrProvinceName = State or Province Name (full name)
stateOrProvinceName_default = Kaluga
localityName = Locality Name (eg, city)
localityName_default = Kaluga
organizationName = Organization Name (eg, company)
organizationName_default = Kaluga
commonName = Common Name (eg, YOUR name or FQDN)
commonName_max = 64
commonName_default = corp.jun.profi

[ req_ext ]
basicConstraints = CA:FALSE
keyUsage = nonRepudiation, digitalSignature, keyEncipherment
subjectAltName = DNS:corp.jun.profi
```
$openssl genpkey -algorithm RSA -out site.key
$ openssl req -new -key site.key -config klg.cnf -reqexts req_ext -out site.csr
$ openssl x509 -req -days 365 -CA rootCA.crt -CAkey rootCA.key -extfile klg.cnf -extensions req_ext -in site.csr -out site.crt
$cp site.crt /etc/nginx/
$cp site.key /etc/nginx/
$cd /etc/nginx
инфу по nginx и ssl можно найти на сайте dmosk
$nano /etc/nginx/nginx.conf
```
Меняем все Listen 80 на Listen 443 ssl
Дописываем в наши server:
	ssl_certificate /etc/nginx/site.crt;
	ssl_certificate_key /etc/nginx/site.key;
```
 
$systemctl restart nginx
На клиенте заходим в терминал:
$scp root@192.168.10.101:/opt/ssl/rootCA.crt /etc/pki/ca-trust/source/anchors/
$update-ca-turst
$cp /etc/pki/ca-trust/source/anchors/rootCA.crt /home/student
$chown student:student /home/student/rootCA.crt
В настройках браузера firefox заходим в сертификацию и там добавляем сертификат который мы скопировалии
