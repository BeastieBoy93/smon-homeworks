# Домашнее задание к занятию "`Система мониторинга Zabbix`" - `Эсадов Роман`
---
### Задание 1
1. Установил Postgresql 15:
```
sudo apt install -y postgresql-common
sudo /usr/share/postgresql-common/pgdg/apt.postgresql.org.sh
sudo apt install curl ca-certificates
sudo sh -c 'echo "deb [signed-by=/usr/share/postgresql-common/pgdg/apt.postgresql.org.asc] https://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
sudo apt update
sudo apt install postgresql-15
```
2. Установил компоненты Zabbix, добавил пользователя zabbix в PG и создал базу zabbix. Указал пароль PG пользователя zabbix в конфиге:
```
# wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.0-4+ubuntu20.04_all.deb
# dpkg -i zabbix-release_6.0-4+ubuntu20.04_all.deb
# apt update
# apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent
# sudo -u postgres createuser --pwprompt zabbix
# sudo -u postgres createdb -O zabbix zabbix
# zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
# sed -i 's/# DBPassword=/DBPassword=123456789/g' /etc/zabbix/zabbix_server.conf
# systemctl restart zabbix-server zabbix-agent apache2
# systemctl enable zabbix-server zabbix-agent apache2 
```
3. Авторизовался в админке:
![Zabbix](https://github.com/BeastieBoy93/smon-homeworks/blob/main/photo_2024-01-09_23-59-56.jpg)
---

### Задание 2
1. Установил агента из репы, указал актуальный ip zabbix хоста в конфиге агента:
```
# wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.0-4+ubuntu20.04_all.deb
# dpkg -i zabbix-release_6.0-4+ubuntu20.04_all.deb
# apt update
# apt install zabbix-agent
# sed -i 's/^Server=127.0.0.1/Server=192.168.3.100/g' /etc/zabbix/zabbix_agentd.conf
# systemctl restart zabbix-agent
# systemctl enable zabbix-agent
```
![Agent](https://github.com/BeastieBoy93/smon-homeworks/blob/main/photo_2024-01-09_23-57-23.jpg)

![Logs](https://github.com/BeastieBoy93/smon-homeworks/blob/main/photo_2024-01-09_23-57-16.jpg)

![Hosts](https://github.com/BeastieBoy93/smon-homeworks/blob/main/photo_2024-01-09_23-52-25.jpg)

![Latest data](https://github.com/BeastieBoy93/smon-homeworks/blob/main/photo_2024-01-10_10-06-32.jpg)

---

### Задание 3
1. Скачал и установил агнета (через командную строку с правами админа), отредактировал конфиг агента. Через PSh открыл порты в Windows:
```
C:\> c:\zabbix\zabbix_agentd.exe -c c:\zabbix\zabbix_agentd.conf -i
New-NetFirewallRule -DisplayName "Allow TCP 10050 and 10051 for Zabbix" -Direction Inbound -Action Allow -EdgeTraversalPolicy Allow -Protocol TCP -LocalPort 10050-10051 –Service "Zabbix Agent"
New-NetFirewallRule -DisplayName "Allow TCP 10050 and 10051 for Zabbix" -Direction Outbound -Action Allow  -Protocol TCP -LocalPort 10050-10051 –Service "Zabbix Agent"
```
![Диск C:](https://github.com/BeastieBoy93/smon-homeworks/blob/main/%D0%B8%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D0%B5.png)
