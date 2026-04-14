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
