# Install Elasticsearch and kibana to host

## Variables

- java_jdk_version - set java jdk version
- elastic_version - set elasticsearch version
- elastic_home - set Elasticsearch installation directory
- kibana_version - set Kibana version
- kibana_home - set Kibana installation directory

## Tags
- java
- elastic
- kibana

## Usage

```sh 
ansible-playbook -i inventory/prod.yml site.yml -K
```


# Домашнее задание к занятию "08.02 Работа с Playbook" "Alexandr-Sokolov"

## Подготовка к выполнению
1. Создайте свой собственный (или используйте старый) публичный репозиторий на github с произвольным именем.
2. Скачайте [playbook](./playbook/) из репозитория с домашним заданием и перенесите его в свой репозиторий.
3. Подготовьте хосты в соотвтествии с группами из предподготовленного playbook. 
4. Скачайте дистрибутив [java](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html) и положите его в директорию `playbook/files/`. 

## Основная часть
1. Приготовьте свой собственный inventory файл `prod.yml`.
2. Допишите playbook: нужно сделать ещё один play, который устанавливает и настраивает kibana.
3. При создании tasks рекомендую использовать модули: `get_url`, `template`, `unarchive`, `file`.
4. Tasks должны: скачать нужной версии дистрибутив, выполнить распаковку в выбранную директорию, сгенерировать конфигурацию с параметрами.
5. Запустите `ansible-lint site.yml` и исправьте ошибки, если они есть.
```sh
$ sudo ansible-lint site.yml && echo $?
0
```
6. Попробуйте запустить playbook на этом окружении с флагом `--check`.
```
$ ansible-playbook -i inventory/prod.yml site.yml --check

PLAY [Install Java] *********************************************************************************

TASK [Gathering Facts] ******************************************************************************
ok: [testubuntu2]

TASK [Set facts for Java 11 vars] *******************************************************************
ok: [testubuntu2]

TASK [Upload .tar.gz file containing binaries from local storage] ***********************************
changed: [testubuntu2]

TASK [Ensure installation dir exists] ***************************************************************
fatal: [testubuntu2]: FAILED! => {"msg": "Missing sudo password"}

PLAY RECAP ******************************************************************************************
testubuntu2                : ok=3    changed=1    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0   
```
7. Запустите playbook на `prod.yml` окружении с флагом `--diff`. Убедитесь, что изменения на системе произведены.
```
$ ansible-playbook -i inventory/prod.yml site.yml --diff -K
BECOME password: 

PLAY [Install Java] *********************************************************************************

TASK [Gathering Facts] ******************************************************************************
ok: [testubuntu2]

TASK [Set facts for Java 11 vars] *******************************************************************
ok: [testubuntu2]

TASK [Upload .tar.gz file containing binaries from local storage] ***********************************
ok: [testubuntu2]

TASK [Ensure installation dir exists] ***************************************************************
--- before
+++ after
@@ -1,4 +1,4 @@
 {
     "path": "/opt/jdk/11.0.12",
-    "state": "absent"
+    "state": "directory"
 }

changed: [testubuntu2]

TASK [Extract java in the installation directory] ***************************************************
changed: [testubuntu2]

TASK [Export environment variables] *****************************************************************
ok: [testubuntu2]

PLAY [Install Elasticsearch] ************************************************************************

TASK [Gathering Facts] ******************************************************************************
ok: [testubuntu2]

TASK [Upload tar.gz Elasticsearch from remote URL] **************************************************
ok: [testubuntu2]

TASK [Create directrory for Elasticsearch] **********************************************************
--- before
+++ after
@@ -1,4 +1,4 @@
 {
     "path": "/opt/elastic/7.10.1",
-    "state": "absent"
+    "state": "directory"
 }

changed: [testubuntu2]

TASK [Extract Elasticsearch in the installation directory] ******************************************
changed: [testubuntu2]

TASK [Set environment Elastic] **********************************************************************
ok: [testubuntu2]

PLAY [Install Kibana] *******************************************************************************

TASK [Gathering Facts] ******************************************************************************
ok: [testubuntu2]

TASK [Upload tar.gz Kibana from remote URL] *********************************************************
ok: [testubuntu2]

TASK [Create directrory for Kibana] *****************************************************************
--- before
+++ after
@@ -1,4 +1,4 @@
 {
     "path": "/opt/kibana/7.14.1",
-    "state": "absent"
+    "state": "directory"
 }

changed: [testubuntu2]

TASK [Extract kibana in the installation directory] *************************************************
changed: [testubuntu2]

PLAY RECAP ******************************************************************************************
testubuntu2                : ok=15   changed=6    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```
```sh
$ ssh user@testubuntu2 "ls /opt; echo "----"; ls /tmp/*.tar.gz"
elastic
jdk
kibana
----
/tmp/elasticsearch-7.10.1-linux-x86_64.tar.gz
/tmp/jdk-11.0.12.tar.gz
/tmp/kibana-7.14.1-linux-x86_64.tar.gz
```
8. Повторно запустите playbook с флагом `--diff` и убедитесь, что playbook идемпотентен.
```
$ ansible-playbook -i inventory/prod.yml site.yml --diff -K
BECOME password: 

PLAY [Install Java] *********************************************************************************

TASK [Gathering Facts] ******************************************************************************
ok: [testubuntu2]

TASK [Set facts for Java 11 vars] *******************************************************************
ok: [testubuntu2]

TASK [Upload .tar.gz file containing binaries from local storage] ***********************************
ok: [testubuntu2]

TASK [Ensure installation dir exists] ***************************************************************
ok: [testubuntu2]

TASK [Extract java in the installation directory] ***************************************************
skipping: [testubuntu2]

TASK [Export environment variables] *****************************************************************
ok: [testubuntu2]

PLAY [Install Elasticsearch] ************************************************************************

TASK [Gathering Facts] ******************************************************************************
ok: [testubuntu2]

TASK [Upload tar.gz Elasticsearch from remote URL] **************************************************
ok: [testubuntu2]

TASK [Create directrory for Elasticsearch] **********************************************************
ok: [testubuntu2]

TASK [Extract Elasticsearch in the installation directory] ******************************************
skipping: [testubuntu2]

TASK [Set environment Elastic] **********************************************************************
ok: [testubuntu2]

PLAY [Install Kibana] *******************************************************************************

TASK [Gathering Facts] ******************************************************************************
ok: [testubuntu2]

TASK [Upload tar.gz Kibana from remote URL] *********************************************************
ok: [testubuntu2]

TASK [Create directrory for Kibana] *****************************************************************
ok: [testubuntu2]

TASK [Extract kibana in the installation directory] *************************************************
skipping: [testubuntu2]

PLAY RECAP ******************************************************************************************
testubuntu2                : ok=12   changed=0    unreachable=0    failed=0    skipped=3    rescued=0    ignored=0  
```


---
