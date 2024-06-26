---
description: >-
  Данный вид авторизации позволяет создать правило авторизации для конкретного
  пользователя NGFW из определенной подсети
---

# Авторизация по подсетям

Чтобы не регистрировать каждое устройство в виде отдельного NGFW-пользователя и не фиксировать для него факторы авторизации, можно воспользоваться **Авторизацией по подсети**.

Эта функция позволит пользователю NGFW из требуемой подсети авторизоваться автоматически без привязки к MAC и/или конкретному IP и будет полезна, если требуется автоматически авторизовать большое количество устройств.

Трафик по всей подсети будет фиксироваться на одного пользователя.

В сети, для которой создано правило _Авторизации по подсетям_, возможна работа DHCP.

Например, в подсети 192.168.10.0/24 есть Wi-Fi-подсеть, устройствам из которой нужно позволить авторизоваться. Создайте правило авторизации:

1\. Перейдите в раздел **Пользователи –> Учетные записи** и нажмите **Добавить пользователя**.

2\. Заполните поля _Имя подсети_, _Логин_ и нажмите **Сохранить**:

![](/.gitbook/assets/authorization-by-subnet.png)

3\. Перейдите в раздел **Пользователи –> Авторизация –> Авторизация по подсети** и нажмите **Добавить** в левом верхнем углу.

4\. Заполните поля и нажмите **Сохранить**:

* **Пользователь** - выберите созданного в п. 2 пользователя;
* **Подсеть** - введите IP и маску подсети;
* **Комментарий** - (необязательное).

![](/.gitbook/assets/authorization-by-subnet1.png)

При включении или отключении опции авторизации по подсетям может наблюдаться задержка в работе Ideco NGFW.

**Будьте внимательны при создании правил Авторизации по подсетям**\
Будут проблемы с авторизацией, если:

* Для разных пользователей создать пересекающиеся сети;
* Есть правила авторизаций пользователей по IP-адресам из подсети в правиле _Авторизации по подсетям_;
* Созданы правила в подразделе **Фиксированные IP-адреса VPN** с привязкой к IP-адресу из подсети правила _Авторизации по подсетям_.
