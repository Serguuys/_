apt-get update && apt-get dist-upgrade
apt-get install zfs-utils
apt-get install kernel-modules-zfs-std-def
reboot
modprobe zfs

Создаём пул дисков
sudo zpool create zfspool mirror /dev/sdb /dev/sdc
Смотрим статус
sudo zpool status
Создаём zfs файловую систему на пуле с именем data
sudo zfs create zfspool/data
Монтируем
sudo zfs set mountpoint=/opt/data zfspool/data