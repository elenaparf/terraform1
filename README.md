# Домашнее задание к занятию «Введение в Terraform» - Парфенова Елена
### Цели задания

1. Установить и настроить Terrafrom.
2. Научиться использовать готовый код.

------

### Чек-лист готовности к домашнему заданию

1. Скачайте и установите **Terraform** версии >=1.8.4 . Приложите скриншот вывода команды ```terraform --version```.
2. Скачайте на свой ПК этот git-репозиторий. Исходный код для выполнения задания расположен в директории **01/src**.
3. Убедитесь, что в вашей ОС установлен docker.

------


### готовоность к выполнению домашнего задания
1. Terraform установлен  
![ter_1](https://github.com/user-attachments/assets/485cf802-27af-42b4-864d-9726d0c528c2)

2. Репозиторий скачан  
![ter_2](https://github.com/user-attachments/assets/02084453-5ca2-4818-b8d9-fcc32ed1850f)

3. Docker установлен  
![ter_3](https://github.com/user-attachments/assets/041e9b1a-3851-4f6d-a74a-3b0351964927)

### Инструменты и дополнительные материалы, которые пригодятся для выполнения задания

1. Репозиторий с ссылкой на зеркало для установки и настройки Terraform: [ссылка](https://github.com/netology-code/devops-materials).
2. Установка docker: [ссылка](https://docs.docker.com/engine/install/ubuntu/). 
------
### Внимание!! Обязательно предоставляем на проверку получившийся код в виде ссылки на ваш github-репозиторий!
------

### Задание 1

1. Перейдите в каталог [**src**](https://github.com/netology-code/ter-homeworks/tree/main/01/src). Скачайте все необходимые зависимости, использованные в проекте. 
2. Изучите файл **.gitignore**. В каком terraform-файле, согласно этому .gitignore, допустимо сохранить личную, секретную информацию?(логины,пароли,ключи,токены итд)
3. Выполните код проекта. Найдите  в state-файле секретное содержимое созданного ресурса **random_password**, пришлите в качестве ответа конкретный ключ и его значение.
4. Раскомментируйте блок кода, примерно расположенный на строчках 29–42 файла **main.tf**.
Выполните команду ```terraform validate```. Объясните, в чём заключаются намеренно допущенные ошибки. Исправьте их.
5. Выполните код. В качестве ответа приложите: исправленный фрагмент кода и вывод команды ```docker ps```.
6. Замените имя docker-контейнера в блоке кода на ```hello_world```. Не перепутайте имя контейнера и имя образа. Мы всё ещё продолжаем использовать name = "nginx:latest". Выполните команду ```terraform apply -auto-approve```.
Объясните своими словами, в чём может быть опасность применения ключа  ```-auto-approve```. Догадайтесь или нагуглите зачем может пригодиться данный ключ? В качестве ответа дополнительно приложите вывод команды ```docker ps```.
8. Уничтожьте созданные ресурсы с помощью **terraform**. Убедитесь, что все ресурсы удалены. Приложите содержимое файла **terraform.tfstate**. 
9. Объясните, почему при этом не был удалён docker-образ **nginx:latest**. Ответ **ОБЯЗАТЕЛЬНО НАЙДИТЕ В ПРЕДОСТАВЛЕННОМ КОДЕ**, а затем **ОБЯЗАТЕЛЬНО ПОДКРЕПИТЕ** строчкой из документации [**terraform провайдера docker**](https://docs.comcloud.xyz/providers/kreuzwerker/docker/latest/docs).  (ищите в классификаторе resource docker_image )


------

### Решение 1
1. Перейдем в каталог [**src**](https://github.com/netology-code/ter-homeworks/tree/main/01/src). Скачаем все необходимые зависимости, использованные в проекте. 
 ![ter_4](https://github.com/user-attachments/assets/1407066a-ade1-4c0c-8882-818b3d83da66)

2. Изучим содержимое .gitignore*
 ![ter_5](https://github.com/user-attachments/assets/468b8c0a-39e5-4a09-8f9d-37ce589eaf43)

**/.terraform/*
    Исключает все файлы и папки, находящиеся в любом каталоге .terraform.
    Каталог .terraform создаётся Terraform для хранения провайдеров, модуля и других временных данных, которые не должны попадать в репозиторий.

!.terraform*
    Исключает все файлы или каталоги, названия которых начинаются с .terraform.
    Например: .terraform.lock.hcl или .terraform_backup.

!.terraformrc
    Делает исключение для файла .terraformrc.
    Этот файл обычно используется для пользовательских настроек Terraform и может быть полезен для совместного использования, но его включение в репозиторий нужно учитывать осторожно, так как он может содержать конфиденциальные данные.

*.tfstate и *.tfstate.*
    Исключает файлы состояния Terraform:
        terraform.tfstate: основной файл состояния, который содержит текущую конфигурацию инфраструктуры.
        terraform.tfstate.backup или любые другие версии с суффиксом (например, .tfstate.12345).
    Эти файлы важны для работы Terraform, но их нельзя загружать в репозиторий, так как они могут содержать чувствительные данные (например, IP-адреса, токены доступа и т. д.).

Согласно этому .gitignore, для хранения личной и секретной информации допустимо использовать файл:
personal.auto.tfvars

3. Выполним код проекта. Найдем  в state-файле секретное содержимое созданного ресурса **random_password**, пришлите в качестве ответа конкретный ключ и его значение.  
 ![ter_6](https://github.com/user-attachments/assets/54c8d4d1-48f4-41dc-bb85-4379b4876464)
 ![ter_7](https://github.com/user-attachments/assets/037aaf1d-3581-4d26-b5b0-7db7d5cec842)
 ![ter_8](https://github.com/user-attachments/assets/12aab4a0-8d95-4132-ab06-a48a0b37776e)
```
"result": "8POGskoI6SaZr4yZ"
```  

4. Раскомментируем блок кода, примерно расположенный на строчках 29–42 файла **main.tf**.
Выполните команду ```terraform validate```. Объясните, в чём заключаются намеренно допущенные ошибки. Исправьте их.  
 ![ter_9](https://github.com/user-attachments/assets/3be899a6-ddb1-4548-a15d-ee0faeb0dd9a)

ошибка указывает что имя контейнера не может начинаться с цифры  

ошибка исправлена запускаем валидацию еще раз 
 ![ter_10](https://github.com/user-attachments/assets/3a82ca46-0090-4f18-9ad3-e3cb514640af)

 
 ![ter_11](https://github.com/user-attachments/assets/cbaaa069-0cc9-4e4f-a0f2-0b02924082cd)
  снова Ошибка, указывает что 
строка 24: resource "docker_image" должен иметь два параметра имя и тип  и имя 


исправляем запускаем снова 
опять ошибка,  31:   name  = "example_${random_password.random_string_FAKE.resulT}"
 ![ter_12](https://github.com/user-attachments/assets/f416168a-af68-4224-bb54-95065e324f95)

Имя контейнера формируется как example_${random_password.random_string_FAKE.resulT}, а правильно: example_${random_password.random_string.result}
Исправляем  
  
 ![ter_13](https://github.com/user-attachments/assets/79b0b004-1f03-4843-9198-50622ada04fb)

 Успешно!  
 ![ter_14](https://github.com/user-attachments/assets/85117b3f-1b27-4da2-9d48-99e52f279a59)
 ![ter_15](https://github.com/user-attachments/assets/080fecf1-9120-48bf-b39e-09a812ec670d)
 
5. Выполним код. В качестве ответа приложим: исправленный фрагмент кода и вывод команды ```docker ps```.  
 ![ter_16](https://github.com/user-attachments/assets/9cb23f5b-a103-4732-b68e-9ec3928caab2)
 ![ter_17](https://github.com/user-attachments/assets/0dc744a3-7859-46f8-8b6c-11ecd9ab1131)
 ![ter_18](https://github.com/user-attachments/assets/0dbec0ca-ecdd-49a8-b635-38e602c86b93)
 
6. Заменим имя docker-контейнера в блоке кода на hello_world. Не перепутайте имя контейнера и имя образа. Мы всё ещё продолжаем использовать name = "nginx:latest". Выполните команду terraform apply -auto-approve.
 ![ter_31](https://github.com/user-attachments/assets/e588e181-a746-4019-ad38-8c5ee59a6370)
 Опция -auto-approve позволяет автоматически применять изменения без запроса подтверждения у пользователя. Это может привести к тому, что нежелательные или ошибочные изменения будут внедрены в систему без должной проверки. Например, если в конфигурации есть ошибка или недоразумение, оно может быть немедленно применено, что может вызвать сбой или потерю данных.  

7. Удалим  объекты созданные terraform 
 ![ter_32](https://github.com/user-attachments/assets/ce98d1e9-0ba8-4af7-9690-065e7181fa6a)
 ![ter_33](https://github.com/user-attachments/assets/5b5c29c9-799a-4d70-804a-4ef96436e1fc)
 
8. Объясните, почему при этом не был удалён docker-образ nginx:latest. Ответ ОБЯЗАТЕЛЬНО НАЙДИТЕ В ПРЕДОСТАВЛЕННОМ КОДЕ, а затем ОБЯЗАТЕЛЬНО ПОДКРЕПИТЕ строчкой из документации terraform провайдера docker. (ищите в классификаторе resource docker_image )

потому что использовали параметр keep_locally = true при создании образа.Т.е. при удалении ресурса сам image останется в локальном хранилище docker. 
Из документации:
keep_locally - (Boolean) If true, then the Docker image won't be deleted on destroy operation. If this is false, it will delete the image from the docker local storage on destroy operation.


