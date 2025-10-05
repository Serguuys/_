1. Скачиваем пакет `mdadm`
#смотреть сайт https://www.dmosk.ru/miniinstruktions.php?mini=mdadm
```bash
apt install mdadm
```
2. Создаём raid
```bash
mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sdb /dev/sdc
mkfs.ext4 /dev/md0
```
3. Сохраняем его блт!!!
```bash
mdadm --detail --scan --verbose | sudo tee -a /etc/mdadm/mdadm.conf
update-initramfs -u # Если работает)
```
4. Записываем его в fstab
```fstab
/dev/md0 /mnt/ ext4 defaults 0 0
```
5. Чтобы посмотреть статусы используем эту команду
```bash
sudo mdadm --detail /dev/md0
cat /proc/mdstat
```

