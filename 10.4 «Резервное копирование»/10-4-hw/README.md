# Домашнее задание к занятию "`10.4. Резервное копирование`" - `Соколов Александр`



---

## Задание 1

В чём разница между:
- полным резервным копированием,
- дифференциальным резервным копированием,
- инкрементным резервным копированием.

Ответ:

```
Полное резервное копирование (Full BackUp) - каждый раз выполняется полное копирование всех данных.
- самый надёжный, т.к. каждый раз копируются все данные;
- самый быстрый, с точки зрения скорости восстановления;
- самый медленный и ресурсоемкий, с точки зрения создание и хранения копии.

Дифференциальное резервное копирование (Differential BackUp) - полное резервное копирование делается только первый раз, затем резервируются измененные данные с момента последней полной копии.
- восстановление выполняется медленнее, чем в полном и быстрее, чем в инкрементальном;
- копирование выполняется быстрее, чем в полном и медленне, чем в инкрементальном.

Инкрементное резервное копирование (Incremental BackUp) - похоже на дифифференциальное копирование, за исключением того, что каждая новая копия содержит только данные, изменённые после последней инкрементальной копии.
- самый медленный, с точки зрения скорости восстановления;
- самый быстрый на наименее ресурсоёмкий, с точки зрения создание и хранения копии.

---

## Задание 2

Установите программное обеспечении Bacula, настройте bacula-dir, bacula-sd, bacula-fd. Протестируйте работу сервисов.

*Пришлите конфигурационные файлы для bacula-dir, bacula-sd, bacula-fd.*
```
sudo apt install bacula postgresql
sudo nano /etc/bacula/bacula-sd.conf
sudo /usr/sbin/bacula-sd -t -c /etc/bacula/bacula-sd.conf
sudo systemctl restart bacula-sd.service
sudo systemctl status bacula-sd.service
sudo nano /etc/bacula/bacula-fd.conf # Конфиг локал клиента
sudo /usr/sbin/bacula-fd -t -c /etc/bacula/bacula-fd.conf
sudo systemctl restart bacula-fd.service
sudo systemctl status bacula-fd.service
sudo nano /etc/bacula/bacula-dir.conf # Конфиг консоль
sudo /usr/sbin/bacula-dir -t -c /etc/bacula/bacula-dir.conf
sudo systemctl restart bacula-dir.service
sudo systemctl status bacula-dir.service
# Переходим в консоль
sudo bconsole
* run
* message
* exit
```
Файл bacula-sd.conf

https://github.com/sakol86/netology/blob/ready/10.4%20«Резервное%20копирование»/10-4-hw/data_file/bacula-sd.conf

Файл bacula-fd.conf

https://github.com/sakol86/netology/blob/ready/10.4%20«Резервное%20копирование»/10-4-hw/data_file/bacula-fd.conf

Файл bacula-dir.conf
https://github.com/sakol86/netology/blob/ready/10.4%20«Резервное%20копирование»/10-4-hw/data_file/bacula-dir.conf

---

## Задание 3

Установите программное обеспечении Rsync. Настройте синхронизацию на двух нодах. Протестируйте работу сервиса.

*Пришлите рабочую конфигурацию сервера и клиента Rsync.*
```
sudo apt install rsync
sudo nano /etc/default/rsync # RSYNC_ENABLE=true
sudo nano /etc/rsyncd.conf 
sudo systemctl start rsync.service
sudo systemctl status rsync.service
sudo netstat -tulnp |grep rsync # 
sudo nano /etc/rsyncd.scrt # backup:12345
sudo chmod 0600 /etc/rsyncd.scrt

sudo mkdir /root/scripts
sudo nano /root/scripts/backup-node1.sh 
chmod 0744 /root/scripts/backup-node1.sh
sudo nano /etc/rsyncd.scrt 
sudo chmod 0600 /etc/rsyncd.scrt
/root/scripts/backup-node1.sh 
```
Файл rsyncd.conf 

https://github.com/sakol86/netology/blob/ready/10.4%20«Резервное%20копирование»/10-4-hw/data_file/rsyncd.conf
```
pid file = /var/run/rsyncd.pid
log file = /var/log/rsyncd.log
transfer logging = true
munge symlinks = yes
# папка источник для бэкапа
[data]
path = /data
uid = root
read only = yes
list = yes
comment = Data backup Dir
auth users = backup
secrets file = /etc/rsyncd.scrt
```
Файл backup-node1.sh

https://github.com/sakol86/netology/blob/ready/10.4%20«Резервное%20копирование»/10-4-hw/data_file/backup-node1.sh)

---


```

---
