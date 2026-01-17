# Домашнее задание к занятию "`Zabbix`" - `Бойко Кирилл` 

---

### Задание 1 

Установите Zabbix Server с веб-интерфейсом. 

**Процесс выполнения** 

   1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции. 
   2. Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11. 
   3. Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache. 
   4. Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server. 

**Требования к результатам** 

   1. Прикрепите в файл README.md скриншот авторизации в админке. 
   2. Приложите в файл README.md текст использованных команд в GitHub. 
      


---

#### Решение 1 

*Скриншот авторизации в админке*
![Скриншот авторизации в админке](https://github.com/KupIOxaCaH/Zabbix/blob/main/img/Dashboard.png) 
*Использованные команды:*
*wget https://repo.zabbix.com/zabbix/7.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest+ubuntu24.04_all.deb* скачиваем конфигурационный пакет
*sudo dpkg -i zabbix-release_latest+ubuntu24.04_all.deb* устанавливаем его
*sudo apt update* обновляем списки пакетов
*sudo apt install zabbix-server-pgsql zabbix-frontend-php php8.3-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent postgresql -y* устанавливаем сервер, веб-интерфейс, агента, скрипты и пр.
*sudo -u postgres psql* заходим в psql
*create user zabbix with password 'zabbix';* создаём пользователя
*create database zabbix owner zabbix;* создаём БД
*\q* выходим
*zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix* импортируем начальную схему данных
*sudo nano /etc/zabbix/zabbix_server.conf* устанавливаем пароль от БД. Ещём строку # DBPaswworrd, раскоментируем её и пишем пароль
*sudo systemctl restart zabbix-server zabbix-agent apache2* запускаем сервер
*sudo systemctl enable zabbix-server zabbix-agent apache2* ставим в автозагрузку

---

### Задание 2 

Установите Zabbix Agent на два хоста. 

**Процесс выполнения** 

   1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции. 
   2. Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server. 
   3. Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов. 
   4. Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera. 
   5. Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов. 

**Требования к результатам** 

   1. Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу 
   2. Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером 
   3. Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные. 
   4. Приложите в файл README.md текст использованных команд в GitHub 



---

#### Решение 2  

*Скриншот раздела Configuration > Hosts* 
![Скриншот раздела Configuration > Hosts](https://github.com/KupIOxaCaH/Zabbix/blob/main/img/Hosts.png) 
*Скриншот лога zabbix agent* 
![Скриншот лога zabbix agent](https://github.com/KupIOxaCaH/Zabbix/blob/main/img/log.PNG) 
*Скриншот раздела Monitoring > Latest data* 
![Скриншот раздела Monitoring > Latest data](https://github.com/KupIOxaCaH/Zabbix/blob/main/img/Latest%20Data.png)  
Устанавливаем агента на машину и просто следуем указаниям установщика. На этапе указания адреса сервера (Zabbix Server IP) указываем адрес нашего сервера, также его указываем и в Zabbix Server Active IP. В Hostname пишем имя нашего ПК и запоминаем или копируем его. После установки агента заходим в веб-интерфейс zabbix и добавляем Host во вкладке "Сбор данных" - "Узла сети" - "Создать узел сети". И там мы пишеи имя хоста символ в символ как указали при установке агента. Выбираем
 шаблон, группу и указываем интерфейс "агент" куда пишем ip-адрес хоста
---

### Задание 3* 

Установите Zabbix Agent на Windows (компьютер) и подключите его к серверу Zabbix. 

**Требования к результатам** 

  *Скриншот свободного места на диске С:*
  ![Скриншот свободного места на диске С:](https://github.com/KupIOxaCaH/Zabbix/blob/main/img/Used%20space.png)


---

#### Решение 3 

*Скриншот раздела Latest Data*
![Скриншот раздела Latest Data]()
