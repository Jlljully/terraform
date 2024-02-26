# Домашнее задание к занятию «Управляющие конструкции в коде Terraform»


### Задание 1

1. Изучите проект.
2. Заполните файл personal.auto.tfvars.
3. Инициализируйте проект, выполните код. Он выполнится, даже если доступа к preview нет.

Примечание. Если у вас не активирован preview-доступ к функционалу «Группы безопасности» в Yandex Cloud, запросите доступ у поддержки облачного провайдера. Обычно его выдают в течение 24-х часов.

Приложите скриншот входящих правил «Группы безопасности» в ЛК Yandex Cloud или скриншот отказа в предоставлении доступа к preview-версии.

------

### Ответ

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_3/Untitled.png "")   

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_3/Untitled2.png "")  

### Задание 2

1. Создайте файл count-vm.tf. Опишите в нём создание двух **одинаковых** ВМ  web-1 и web-2 (не web-0 и web-1) с минимальными параметрами, используя мета-аргумент **count loop**. Назначьте ВМ созданную в первом задании группу безопасности.(как это сделать узнайте в документации провайдера yandex/compute_instance )
2. Создайте файл for_each-vm.tf. Опишите в нём создание двух ВМ с именами "main" и "replica" **разных** по cpu/ram/disk , используя мета-аргумент **for_each loop**. Используйте для обеих ВМ одну общую переменную типа list(object({ vm_name=string, cpu=number, ram=number, disk=number  })). При желании внесите в переменную все возможные параметры.
3. ВМ из пункта 2.2 должны создаваться после создания ВМ из пункта 2.1.
4. Используйте функцию file в local-переменной для считывания ключа ~/.ssh/id_rsa.pub и его последующего использования в блоке metadata, взятому из ДЗ 2.
5. Инициализируйте проект, выполните код.

------

### Ответ

1.
![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_3/Untitled3.png "")   

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_3/Untitled4.png "")  

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_3/Untitled5.png "")  

2-3. 

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_3/Untitled6.png "")   

Не хочет без итератора обращаться к листу такого типа, просит map или set. Почти переделала на map, потому что так проще, но нашли с ребятами костыль с итератором (а, может, не костыль? так и должно быть?)  

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_3/Untitled7.png "")  

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_3/Untitled8.png "")  

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_3/Untitled9.png "")  

4-5. 

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_3/Untitled10.png "")  


### Задание 3

1. Создайте 3 одинаковых виртуальных диска размером 1 Гб с помощью ресурса yandex_compute_disk и мета-аргумента count в файле **disk_vm.tf** .
2. Создайте в том же файле одну ВМ c именем "storage" . Используйте блок **dynamic secondary_disk{..}** и мета-аргумент for_each для подключения созданных вами дополнительных дисков.

------

### Ответ

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_3/Untitled11.png "")  

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_3/Untitled12.png "")  


### Задание 4

1. В файле ansible.tf создайте inventory-файл для ansible.
Используйте функцию tepmplatefile и файл-шаблон для создания ansible inventory-файла из лекции.
Готовый код возьмите из демонстрации к лекции [**demonstration2**](https://github.com/netology-code/ter-homeworks/tree/main/03/demonstration2).
Передайте в него в качестве переменных группы виртуальных машин из задания 2.1, 2.2 и 3.2, т. е. 5 ВМ.
2. Инвентарь должен содержать 3 группы [webservers], [databases], [storage] и быть динамическим, т. е. обработать как группу из 2-х ВМ, так и 999 ВМ.
4. Выполните код. Приложите скриншот получившегося файла. 

Для общего зачёта создайте в вашем GitHub-репозитории новую ветку terraform-03. Закоммитьте в эту ветку свой финальный код проекта, пришлите ссылку на коммит.   
**Удалите все созданные ресурсы**.

------

### Ответ

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_3/Untitled13.png "")  

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_3/Untitled14.png "")  

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_3/Untitled15.png "")  

![скрин](https://github.com/Jlljully/terraform/blob/main/files/lesson_3/Untitled16.png "")  


[push code](https://github.com/Jlljully/terr03_push)https://github.com/Jlljully/terr03_push
