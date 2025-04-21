1. Заходим в captive portal Administration и создаем там zone
```
Interface: GUEST_KLG
ALLOW inbound: LAN_KLG,SRV_KLG,WG
Authenticate using: Local Database
Description: captive portal
```
2.  Заходим в Firewall > Rules > GUEST_KLG
3. Создаем правило для доступа к локальным сетям, в нем указываем
```
Destination: LAN net, SRV net, GUEST net, WG net
```
4. Заходим в консоль и пишем команду
```
nslookup docs.altlinux.org
```
5. Ip который мы получили вставляем в Destination в новом правиле
6. Создаем юзера в System > Access > Users