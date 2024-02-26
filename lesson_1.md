# Домашнее задание к занятию «Введение в Terraform»


### Задание 1

1. Перейдите в каталог [**src**](https://github.com/netology-code/ter-homeworks/tree/main/01/src). Скачайте все необходимые зависимости, использованные в проекте. 
2. Изучите файл **.gitignore**. В каком terraform файле согласно этому .gitignore допустимо сохранить личную, секретную информацию?
3. Выполните код проекта. Найдите  в State-файле секретное содержимое созданного ресурса **random_password**, пришлите в качестве ответа конкретный ключ и его значение.
4. Раскомментируйте блок кода, примерно расположенный на строчках 29-42 файла **main.tf**.
Выполните команду ```terraform validate```. Объясните в чем заключаются намеренно допущенные ошибки? Исправьте их.
5. Выполните код. В качестве ответа приложите вывод команды ```docker ps```
6. Замените имя docker-контейнера в блоке кода на ```hello_world```, выполните команду ```terraform apply -auto-approve```.
Объясните своими словами, в чем может быть опасность применения ключа  ```-auto-approve``` ? В качестве ответа дополнительно приложите вывод команды ```docker ps```
7. Уничтожьте созданные ресурсы с помощью **terraform**. Убедитесь, что все ресурсы удалены. Приложите содержимое файла **terraform.tfstate**. 
8. Объясните, почему при этом не был удален docker образ **nginx:latest** ? Ответ подкрепите выдержкой из документации провайдера.


### Ответ
1. 
![Скрин](https://github.com/Jlljully/terr01/blob/main/Untitled.png "клоне")

2. В
```
# own secret vars store.
personal.auto.tfvars
```
3.
![Скрин](https://github.com/Jlljully/terr01/blob/main/Untitled1.png "пасс")

4. Ошибки были допущены в описании ресурса (должно быть указано имя и тип), опечатка в "1nginx" - единицу убрала, большая Т в resulT и _FAKE
   
![Скрин](https://github.com/Jlljully/terr01/blob/main/Untitled2.png "ошибки")

![Скрин](https://github.com/Jlljully/terr01/blob/main/Untitled3.png "ошибки")  

5. Запущен
   
![Скрин](https://github.com/Jlljully/terr01/blob/main/Untitled4.png "контейнер")

6. При автоапруве можно случайно задестроить прод и уволиться. Поэтому всегда стоит делать сначала план, проверять что будет создано\удалено, а потом уже запускать аплай
   
![Скрин](https://github.com/Jlljully/terr01/blob/main/Untitled5.png "контейнер2")

7. удалено
   
![Скрин](https://github.com/Jlljully/terr01/blob/main/Untitled6.png "дестрой")

![Скрин](https://github.com/Jlljully/terr01/blob/main/Untitled7.png "дестрой")
   
8. Потому что у нас был задан keep_localy = true

![Скрин](https://github.com/Jlljully/terr01/blob/main/Untitled8.png "локал")
   
    
