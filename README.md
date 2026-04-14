# Задание 1

## Установите Zabbix Server с веб-интерфейсом.
## Процесс выполнения

    1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
    2. Установите PostgreSQL. Для установки достаточна та версия, что есть в  системном репозитороии Debian 11.
    3. Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.
    Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server.

## Требования к результатам

    1. Прикрепите в файл README.md скриншот авторизации в админке.
    2. Приложите в файл README.md текст использованных команд в GitHub.

# Решение

    1. sudo -s
    2. sudo apt update
    3. sudo apt install postgresql
    4. wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_6.0+ubuntu24.04_all.deb
    5. dpkg -i zabbix-release_latest_6.0+ubuntu24.04_all.deb
    6. apt install zabbix-server-pgsql zabbix-frontend-php php8.3-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent
    7. sudo -u postgres createuser --pwprompt zabbix
    8. sudo -u postgres createdb -O zabbix zabbix
    9. zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
    10. nano /etc/zabbix/zabbix_server.conf
    11. ctrl+w > DBPassword = *****
    12. systemctl restart zabbix-server zabbix-agent apache2
    13. systemctl enable zabbix-server zabbix-agent apache2
    14. http://localhost/zabbix

## Админка

![screenshots](screenshots/zabbix_1.png)

# Задание 2

## Установите Zabbix Agent на два хоста.
## Процесс выполнения

    1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
    2. Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.
    3. Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.
    4. Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.
    5. Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.

## Требования к результатам

    1. Приложите в файл README.md скриншот раздела Configuration > Hosts, где  видно, что агенты подключены к серверу
    2. Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером
    3. Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.
    4. Приложите в файл README.md текст использованных команд в GitHub

# Решение

    1. ВМ созданы на YC
      A. zabbixvm_1
      B. zabbixvm_2
    2. ssh -l zabbixvm_1 111.88.147.229
    3. sudo -s
    4. wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_6.0+ubuntu24.04_all.deb
    5. dpkg -i zabbix-release_latest_6.0+ubuntu24.04_all.deb
    6. apt update
    7. в конфге добавляем Server и ServerActive адрес сервер хоста
    8. systemctl restart zabbix-agent
    9. systemctl enable zabbix-agent
    10. ssh -i ~/.ssh/ssh-key-1776189037803 zabbixvm_2@111.88.148.10
    11. Повторяем для второй машины

## Configuration>hosts

![screenshots](screenshots/zabbix_2_1.png)

## zabbixvm_1

![screenshots](screenshots/zabbix_2_2.png)

## zabbixvm_2

![screenshots](screenshots/zabbix_2_3.png)

## latest data

![screenshots](screenshots/zabbix_2_4.png)