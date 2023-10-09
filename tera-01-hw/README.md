# Домашнее задание к занятию "`Введение в Terraform`" - `Соколов Александр`


### Задание 1

Задание 1
1. Перейдите в каталог src. Скачайте все необходимые зависимости, использованные в проекте.
2. Изучите файл .gitignore. В каком terraform файле согласно этому .gitignore допустимо сохранить личную, секретную информацию?
3. Выполните код проекта. Найдите в State-файле секретное содержимое созданного ресурса random_password, пришлите в качестве ответа конкретный ключ и его значение.
4. Раскомментируйте блок кода, примерно расположенный на строчках 29-42 файла main.tf. Выполните команду `terraform validate`. Объясните в чем заключаются намеренно допущенные ошибки? Исправьте их.
5. Выполните код. В качестве ответа приложите вывод команды `docker ps`
6. Замените имя docker-контейнера в блоке кода на `hello_world`, выполните команду `terraform apply -auto-approve`. Объясните своими словами, в чем может быть опасность применения ключа -auto-approve ? В качестве ответа дополнительно приложите вывод команды `docker ps`
7. Уничтожьте созданные ресурсы с помощью terraform. Убедитесь, что все ресурсы удалены. Приложите содержимое файла terraform.tfstate.
8. Объясните, почему при этом не был удален docker образ nginx:latest ? Ответ подкрепите выдержкой из документации провайдера.


`Ответ:`

2. Личную, секретную информацию можно сохранить в файле `personal.auto.tfvars`;
3. Секретное содержимое созданного ресурса random_password `"result": "cVC8UNdUxio9uucz",`


```
  {
  "version": 4,
  "terraform version": "1.4.5",
  "serial": 1,
  "lineage": "04a5199b-5f58-b6c0-27eb-6b7aa@fb9d1",
  "outputs": (},
  " resources": [

  "mode": "managed",
  "type": "random_password",
  "name": "random string"
  "provider":
  "provider\"registry. terraform.10/hashicorp/random\"]",
  "instances": [
  {
  "schema version": 3,
  "attributes": {
  "id": "none",
  "keepers": null,
  "length": 16,
  "lower": true,
  "min Lower": 1,
  "min numeric": 1,
  "min
  special": 0,
  "min upper": 1,
  "number": true,
  "numeric": true,
  "override_special": null,
  "result": "CVC8UNdUxio9uucz",
  "special": false,
  "upper": true
  "bcrypt_hash": "$2a$10$zgVNEiUsmYTEQ7ftiE7ouB30kfl85CRNC3wYPgNQvXiZ8DjwRIS",
  "sensitive attributes": [l

  "check results": null
```
 


4. Первая ошибка говорит о том, что у чоздаваемого ресурса не указано угикальное имя, во-второй ошибке говорится, что уникальное имя содержит не допустимое значение (символ), третья ошибка - заменить 31 строку `name  = "example_${random_password.random_string_FAKE.resulT}"` на `name  = "example_${random_password.random_string.result}"`
```
 
╰─$ terraform validate
╷
│ Error: Missing name for resource
│ 
│   on main.tf line 24, in resource "docker_image":
│   24: resource "docker_image" {
│ 
│ All resource blocks must have 2 labels (type, name).
╵
╷
│ Error: Invalid resource name
│ 
│   on main.tf line 29, in resource "docker_container" "1nginx":
│   29: resource "docker_container" "1nginx" {
│ 
│ A name must start with a letter or underscore and may contain only letters, digits, underscores, and dashes.

╷
│ Error: Unsupported attribute
│ 
│   on main.tf line 31, in resource "docker_container" "nginx":
│   31:   name  = "example_${random_password.random_string_FAKE.resulT}"
│ 
│ This object has no argument, nested block, or exported attribute named "resulT". Did you mean "result"?
```



5. Вывод команды `docker ps`
```

CONTAINER ID IMAGE        COMMAND                 CREATED        STATUS        PORTS                NAMES
49bla7bdccdf eb4a57159180 "/docker-entrypoint..." 18 seconds ago Up 10 seconds 0.0.0.0:8000->80/tcp example_CVC8UNdUxio9uucz
```




6. Опасность применения ключа `-auto-approve`, по моему мнению, заключается в отсутствии проверки за внесением измнений TERRAFORM в создоваемую, или, что ещё хуже, в изменяемую инфроструктуру. Если в файле конфигурации есть ошибки и/или неточности они без проверки и исправлений будут выполнены и применены, что повлечёт за собой последствия. Вывод команды `docker ps`

```

CONTAINER ID IMAGE         COMMAND                  CREATED        STATUS       PORTS                    NAMES
c129b00b1815 eb4a57159180  "/docker-entrypoint....  6 seconds ago  Up 4 seconds 0.0.0.0:8000->80/tcp     hello_world
```


7. Выполнение комманды `terraform destroy`
```
#
random_password, random string will be destroyed
- resource "random password" "random string" {
- bcrypt hash = (sensitive value) -> null
- id = "none" -> null
- length = 16 -> null
- lower = true - null
- min lower = 1 -> null
- min numeric = 1 -> null
- min special = 0 -> null
- min upper = 1 -> null
- number = true -> null
- numeric = true -> null
- result = (sensitive value) -> null
- special = false -> null
- upper = true -> null
  
Plan: 0 to add, 0 to change, 3 to destroy.

Do you really want to destroy all resources?
Terraform will destroy all your managed infrastructure, as shown above.
There is no undo. Only 'yes' will be accepted to confirm.

Enter a value: yes

docker_container.nginx: Destroying.. Tid=c129b00b18157ebd8ddff067a6818403ad4ablba62cfad0eadobb4a0abec7bca]
random_password. random_string: Destroying.. fid=none)
random_password. random_string: Destruction complete after Os 
docker_container.nginx: Destruction complete after 2s 
docker_image. nginx: Destroying. Tid=sha256: eb4a57159180767450c84266367611b999653d8f185b5e3b78a9ca30c2c31dnginx: Latest]
docker_image.nginx: Destruction complete after 0s
Destroy complete! Resources: 3 destroyed.
```



Содержание файла `terraform.tfstate`
```
{
  "version": 4,
  "terraform_version": "1.4.5",
  "serial": 11,
  "lineage": "04a5199b-5f58-b6c0-27eb-6b7a6a0fb9d1",
  "outputs": {},
  "resources": [],
  "check_results": null
}
```

8. Образ docker nginx:latest не был удален из-за того что TERRAFORM удаляет только то что создал сам, в обратном порядке по отношению к комманде `terraform apply`. В документации к провайдеру говорится, что terraform не может удалить ресурсы запущеные другими сервисами.

```
Destroy
The terraform destroy command terminates resources managed by your Terraform project. This command is the inverse of terraform apply in that it terminates all the resources specified in your Terraform state. It does not destroy resources running elsewhere that are not managed by the current Terraform project.

Destroy the resources you created.
```




