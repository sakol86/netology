Домашнее задание к занятию «7.2. Terraform»

 7.2. Terraform — Александр Соколов.



Задание 1
Ответьте на вопрос в свободной форме.

Опишите виды подхода к IaC:

функциональный;
процедурный;
интеллектуальный.
Задание 2
Ответьте на вопрос в свободной форме.

Ответ:

три подхода декларативный (функциональный), императивный (процедурный) и интеллектуальный. Разница между ними выглядит как 'что' / 'как' / 'почему'. Декларативный подход нацелен на то, чтобы описать, как должна выглядеть целевая конфигурация; императивный сфокусирован на том, какие внести изменения; интеллектуальный описывает, почему инфраструктура должна быть так сконфигурирована.

Как вы считаете, в чём преимущество применения Terraform?

Ответ:

Основное преимущество Terraform состоит в том, что вы можете применять его со множеством поставщиков облачных решений, включая AWS, GCP и Azure. Шаблоны ARM более близки Azure, в то время как для Terraform вам всего лишь требуется изучить синтаксис языка программирования HCL и рабочий процесс Terraform и начать применять какого- то поставщика облачного решения, такого как GCP, Azure или AWS.

Задание 3
Ответьте на вопрос в свободной форме.

Какие минусы можно выделить при использовании IaC?

Ответ:

 IaC предоставляет отличный способ отслеживания изменений в инфраструктуре и мониторинга таких вещей, как дрифт инфраструктуры, обслуживание сетапа IaC само по себе становится проблемой при достижении определенного масштаба!

Задание 4
Выполните действия и приложите скриншоты запуска команд.

Установите Terraform на компьютерную систему (виртуальную или хостовую), используя лекцию или инструкцию.

Ответ:
for Mac OS X. Install:

    brew tap hashicorp/tap
    
    brew install hashicorp/tap/terraform
    
    brew update
    
   ![image](https://user-images.githubusercontent.com/86907205/216816009-a7cdd43a-0f2a-4b75-b992-09283b5b89a2.png)


    https://disk.yandex.ru/i/OBTepKXArgwfiA

В связи с недоступностью ресурсов для загрузки Terraform на территории РФ, вы можете воспользоваться VPN или использовать зеркало YandexCloud.

Документация по провайдерам Terraform в зеркале YandexCloud

Зеркало YandexCloud для загрузки Terraform

Инструкция по настройке провайдера

Дополнительные задания* (со звёздочкой)

Их выполнение необязательное и не влияет на получение зачёта по домашнему заданию. Можете их решить, если хотите лучше разобраться в материале.лнить, если хотите глубже и/или шире разобраться в материале.

Задание 5*
Ответьте на вопрос в свободной форме.

Перечислите основные функции, которые могут использоваться в Terraform.
