1. Сначала качаем его это итак понятно
2. ОТКЛЮЧАЕМ UNBOUND DNS, он занимает порт и мешает нам
3. Заходим в bind указываем в Listen IPs 
```
0.0.0.0
```
4. В Listen Port указываем 53
5. В DNS Forwarders указываем
```
100.100.100.100
```
6. На первой странице пока что ничего не трогаем
7. Идем в ACLs и создаем так acl так ее и называем и в networks указываем
```
192.168.20.0/24 192.168.21.0/24
```
8. Возвращаемся на первую страницу и там везде проставляем нашу acl
9. Идем в prinary zone и создаем там зону с такими параметрами
```
Zone Name: tul.jun.profi
Allow Transfer: acl
Allow Query: acl
Mail Admin admin@tul.jun.profi
DNS Server tul.jun.profi
Все остальное оставляем как есть
```
10.  Спускаемся в низ и создаем Records записи как по примеру, **ПЕРВАЯ САМАЯ ВАЖНАЯ**
```
Zone: tul.jun.profi
Name: @
Type: NS
Value: fw-tul.tul.jun.profi
```

```
Zone: tul.jun.profi
Name: Имя любой машины
Type: A
Value: ip этой машины
```
