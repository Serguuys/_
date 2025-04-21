1. Скачиваем все обновления и обновляем репозитории 
```
apt-get update && apt-get dist-upgrade
```
2. Скачиваем саму zfs 
```
apt-get install zfs-utils && apt-get install kernel-modules-zfs-std-def
```
3. Перезагружаем сервер
4. Пишем modprobe zfs для запуска zfs и заходим в файлик и раскоменчиваем строчку для запуска zfs при загрузке сервера
```
nano /etc/modules-load.d/zfs.conf
...
zfs
...
```

5. Создаём пул дисков 
```
sudo zpool create zfspool mirror /dev/sdb /dev/sdc 
```
6. Смотрим статус 
```
sudo zpool status
```
7. Создаём zfs файловую систему на пуле с именем data 
```
sudo zfs create zfspool/data
```
8. Монтируем sudo 
```
zfs set mountpoint=/opt/data zfspool/data
```