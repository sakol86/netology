# Домашнее задание к занятию 4. «Оркестрация группой Docker-контейнеров на примере Docker Compose»

`Александр Соколов`

---

## Задача 1

Создайте собственный образ любой операционной системы (например, debian-11) с помощью Packer ([инструкция для установки плагина yandex-cloud](https://cloud.yandex.ru/docs/tutorials/infrastructure-management/packer-quickstart)).

Чтобы получить зачёт, вам нужно предоставить скриншот страницы с созданным образом из личного кабинета YandexCloud.

`Ответ:`
https://disk.yandex.ru/i/tLX3hFKO6WKS4w
![image](https://github.com/sakol86/netology/assets/86907205/ec7731c3-56d5-4034-9679-c009b12d1cd9)


## Задача 2

**2.1.** Создайте вашу первую виртуальную машину в YandexCloud с помощью web-интерфейса YandexCloud. 

`ответ:`

https://disk.yandex.ru/i/uQC1Br9nZVAXPA
![image](https://github.com/sakol86/netology/assets/86907205/e02e11cc-8a68-4780-9a9b-68a99cb7c914)


**2.2.*** **(Необязательное задание)**      
Создайте вашу первую виртуальную машину в YandexCloud с помощью Terraform (вместо использования веб-интерфейса YandexCloud).
Используйте Terraform-код в директории ([src/terraform](https://github.com/netology-group/virt-homeworks/tree/virt-11/05-virt-04-docker-compose/src/terraform)).

Чтобы получить зачёт, вам нужно предоставить вывод команды terraform apply и страницы свойств, созданной ВМ из личного кабинета YandexCloud.

## Задача 3

С помощью Ansible и Docker Compose разверните на виртуальной машине из предыдущего задания систему мониторинга на основе Prometheus/Grafana.
Используйте Ansible-код в директории ([src/ansible](https://github.com/netology-group/virt-homeworks/tree/virt-11/05-virt-04-docker-compose/src/ansible)).

Чтобы получить зачёт, вам нужно предоставить вывод команды "docker ps" , все контейнеры, описанные в [docker-compose](https://github.com/netology-group/virt-homeworks/blob/virt-11/05-virt-04-docker-compose/src/ansible/stack/docker-compose.yaml),  должны быть в статусе "Up".

```
test@fhmsn9cvm76pbcv5rjg2:~$ docker ps
CONTAINER ID        CREATED             STATUS              PORTS               NAMES
e65c4e1d3777        10 minutes ago      Up 10 minutes       9100/tcp            prom/node-exporter, ::::9100->9100/tcp
0b9dbca3f397        10 minutes ago      Up 10 minutes       3000/tcp            grafana/grafana:latest, ::::3000->3000/tcp
```

## Задача 4

1. Откройте веб-браузер, зайдите на страницу http://<внешний_ip_адрес_вашей_ВМ>:3000.
2. Используйте для авторизации логин и пароль из [.env-file](https://github.com/netology-group/virt-homeworks/blob/virt-11/05-virt-04-docker-compose/src/ansible/stack/.env).
3. Изучите доступный интерфейс, найдите в интерфейсе автоматически созданные docker-compose-панели с графиками([dashboards](https://grafana.com/docs/grafana/latest/dashboards/use-dashboards/)).
4. Подождите 5-10 минут, чтобы система мониторинга успела накопить данные.

Чтобы получить зачёт, предоставьте: 

- скриншот работающего веб-интерфейса Grafana с текущими метриками, как на примере ниже.
`ответ:`

https://disk.yandex.ru/i/2JedUfLp9y8C_A
![image](https://github.com/sakol86/netology/assets/86907205/075a713f-3bc9-4840-90b0-0b530b442d9b)


## Задача 5 (*)

Создайте вторую ВМ и подключите её к мониторингу, развёрнутому на первом сервере.

Чтобы получить зачёт, предоставьте:

- скриншот из Grafana, на котором будут отображаться метрики добавленного вами сервера.


