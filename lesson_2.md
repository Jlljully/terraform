# Домашнее задание к занятию «Основы Terraform. Yandex Cloud»


### Задание 0

1. Ознакомьтесь с [документацией к security-groups в Yandex Cloud](https://cloud.yandex.ru/docs/vpc/concepts/security-groups?from=int-console-help-center-or-nav).
2. Запросите preview-доступ к этому функционалу в личном кабинете Yandex Cloud. Обычно его выдают в течение 24-х часов.
https://console.cloud.yandex.ru/folders/<ваш cloud_id>/vpc/security-groups.   
Этот функционал понадобится к следующей лекции. 

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_2/Untitled.png "")  


### Задание 1
В качестве ответа всегда полностью прикладывайте ваш terraform-код в git.

1. Изучите проект. В файле variables.tf объявлены переменные для Yandex provider.
2. Переименуйте файл personal.auto.tfvars_example в personal.auto.tfvars. Заполните переменные: идентификаторы облака, токен доступа. Благодаря .gitignore этот файл не попадёт в публичный репозиторий. **Вы можете выбрать иной способ безопасно передать секретные данные в terraform.**
3. Сгенерируйте или используйте свой текущий ssh-ключ. Запишите его открытую часть в переменную **vms_ssh_root_key**.
4. Инициализируйте проект, выполните код. Исправьте намеренно допущенные синтаксические ошибки. Ищите внимательно, посимвольно. Ответьте, в чём заключается их суть.
5. Ответьте, как в процессе обучения могут пригодиться параметры ```preemptible = true``` и ```core_fraction=5``` в параметрах ВМ. Ответ в документации Yandex Cloud.

В качестве решения приложите:

- скриншот ЛК Yandex Cloud с созданной ВМ;
- скриншот успешного подключения к консоли ВМ через ssh. К OS ubuntu необходимо подключаться под пользователем ubuntu: "ssh ubuntu@vm_ip_address";
- ответы на вопросы.


### Ответ

4. При запуске validate и plan ошибок не выдавал. На этапе apply начались ошибки: Была ошибка синтаксическая сначала - standatD, потом обнаружилось, что стардартов у яндекса не 4, а 3, я выбрала второй. Выяснила, что он не поддерживает 1-ядерную конфигурацию, поменяла на 2 и ВМ развернулась.
5. Прерываемая ВМ (preemptible) подходит для тестовых платформ, которые можно останавливать для высвобождения ресурсов для запуска более важных для работы ВМ в рамках той же зоны доступности (а так же они останавливаются при простое 24ч+). Их использование значительно дешевле, но не подходит для прода.
А использование core_fraction=Х обеспечит предоставление не менее Х% частотности процессора при высокой нагрузке и до 100% при высвобожении ресурсов.

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_2/Untitled7.png "")  

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_2/Untitled6.png "")  

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_2/Untitled5.png "")  

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_2/Untitled4.png "")  



### Задание 2

1. Изучите файлы проекта.
2. Замените все хардкод-**значения** для ресурсов **yandex_compute_image** и **yandex_compute_instance** на **отдельные** переменные. К названиям переменных ВМ добавьте в начало префикс **vm_web_** .  Пример: **vm_web_name**.
2. Объявите нужные переменные в файле variables.tf, обязательно указывайте тип переменной. Заполните их **default** прежними значениями из main.tf. 
3. Проверьте terraform plan. Изменений быть не должно. 


### Ответ

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_2/Untitled8.png "")    

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_2/Untitled9.png "")  

//Следующие задания выполнялись в другой день, поэтому ресурсы подняты с нуля.//


### Задание 3

1. Создайте в корне проекта файл 'vms_platform.tf' . Перенесите в него все переменные первой ВМ.
2. Скопируйте блок ресурса и создайте с его помощью вторую ВМ в файле main.tf: **"netology-develop-platform-db"** ,  cores  = 2, memory = 2, core_fraction = 20. Объявите её переменные с префиксом **vm_db_** в том же файле ('vms_platform.tf').
3. Примените изменения.


### Ответ

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_2/Untitled10.png "")  

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_2/Untitled11.png "")  

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_2/Untitled12.png "")  


### Задание 4

1. Объявите в файле outputs.tf output типа map, содержащий { instance_name = external_ip } для каждой из ВМ.
2. Примените изменения.

В качестве решения приложите вывод значений ip-адресов команды ```terraform output```.

### Ответ

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_2/Untitled13.png "")  

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_2/Untitled14.png "")  


### Задание 5

1. В файле locals.tf опишите в **одном** local-блоке имя каждой ВМ, используйте интерполяцию ${..} с несколькими переменными по примеру из лекции.
2. Замените переменные с именами ВМ из файла variables.tf на созданные вами local-переменные.
3. Примените изменения.


### Ответ

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_2/Untitled15.png "")  


### Задание 6

1. Вместо использования трёх переменных  ".._cores",".._memory",".._core_fraction" в блоке  resources {...}, объедините их в переменные типа **map** с именами "vm_web_resources" и "vm_db_resources". В качестве продвинутой практики попробуйте создать одну map-переменную **vms_resources** и уже внутри неё конфиги обеих ВМ — вложенный map.
2. Также поступите с блоком **metadata {serial-port-enable, ssh-keys}**, эта переменная должна быть общая для всех ваших ВМ.
3. Найдите и удалите все более не используемые переменные проекта.
4. Проверьте terraform plan. Изменений быть не должно.


### Ответ

1. 
   
![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_2/Untitled16.png "")  

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_2/Untitled17.png "")  

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_2/Untitled18.png "")  

2-4. 

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_2/Untitled19.png "")  

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_2/Untitled20.png "")  

   
------

## Дополнительное задание (со звёздочкой*)

**Настоятельно рекомендуем выполнять все задания со звёздочкой.**   
Они помогут глубже разобраться в материале. Задания со звёздочкой дополнительные, не обязательные к выполнению и никак не повлияют на получение вами зачёта по этому домашнему заданию. 

### Задание 7*

Изучите содержимое файла console.tf. Откройте terraform console, выполните следующие задания: 

1. Напишите, какой командой можно отобразить **второй** элемент списка test_list.
2. Найдите длину списка test_list с помощью функции length(<имя переменной>).
3. Напишите, какой командой можно отобразить значение ключа admin из map test_map.
4. Напишите interpolation-выражение, результатом которого будет: "John is admin for production server based on OS ubuntu-20-04 with X vcpu, Y ram and Z virtual disks", используйте данные из переменных test_list, test_map, servers и функцию length() для подстановки значений.

В качестве решения предоставьте необходимые команды и их вывод.


### Ответ

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_2/Untitled21.png "")  

4ое оставлю на потом :)


[push code](https://github.com/Jlljully/terr02_push)
