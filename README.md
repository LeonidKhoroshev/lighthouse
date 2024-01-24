Lighthouse
=========

Роль позволяет установить и настроить на удаленных или локальных хостах графический интерфейс для СУБД ClickHouse. 

Требования
------------
На настраиваемых хостах должна быть уствновлена ОС Linux (RPM линейка), так как установка производится пакетным менеджером yum. Таже должен быть установлен web-сервер Nginx (роль для его установки доступна по [ссылке](https://github.com/LeonidKhoroshev/nginx)). 


Переменные
--------------
Данная роль доступна к использованию без переменных, так как все значения прописаны в коде. При необходимости можно изменить отдельные настройки в шаблоне конфигурационного файла `templates/lighthouse.j2, такие как: порт, сервер, хранение логов.


Зависимости
------------

Поскольку Lighthouse представляет собой графический интерфейс  ClickHouse, нам потребуется роль для установки и настройки данной СУБД (доступна по [ссылке](https://github.com/LeonidKhoroshev/clickhouse-role)). Для сбора 
преобразования и отправки данных может быть использован Vector (роль доступна по [ссылке](https://github.com/LeonidKhoroshev/vector)).


Пример плейбука
----------------

Установить роль можно через ansible-galaxy:
```
ansible-galaxy install -r requirements.yml
```

указав в файле requirements.yml cледующее содержание:
```
  - src: https://github.com/LeonidKhoroshev/lighthouse
    scm: git
    name: lighthouse
```

Далее вписываем роль в плейбук:
```
- name: Install Lighthouse
  hosts: lighthouse
  remote_user: leo
  become: true
  roles:
    - lighthouse-role
```
