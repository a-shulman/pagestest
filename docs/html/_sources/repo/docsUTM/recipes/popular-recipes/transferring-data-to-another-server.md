# Перенос данных и настроек на другой сервер

Восстановить бекап настроек в Ideco UTM 9 из Ideco UTM 7 можно только с версии 7.9.9 Build 176.

Чтобы перенести установленный Ideco NGFW с одного сервера на другой с сохранением всех настроек, выполните следующие действия:

### Этап 1: Копирование бекапа с сервера

В разделе веб-интерфейса **Управление сервером -> Бекапы -> Бекапы** создайте бекап настроек сервера. Загрузите созданную копию на ваш компьютер, нажав на кнопку **Скачать** в столбце **Управление**.

### Этап 2. Установка Ideco NGFW на новый сервер

Инструкция по установке: [Процесс установки](/installation/installation-process.md).

### Этап 3: Перенос бекапа на новый сервер

В разделе **Сервисы -> Сетевые интерфейсы** посмотрите и запишите MAC-адрес локальной сетевой карты, он потребуется для перенастройки локального интерфейса в дальнейшем.

В разделе веб-интерфейса **Управление сервером -> Бекапы -> Бекапы** нажмите кнопку добавления бекапа -> **Загрузить из файла** и выберите выгруженный на первом этапе бекап.

### Этап 4: Восстановление БД из бекапа

Нажмите кнопку **Применить** (иконка ![](/.gitbook/assets/icon-recovery.png) в столбце **Управление**). Система будет перезагружена для применения настроек сервера.

### Этап 5: Настройка восстановленного сервера

После перезагрузки Ideco NGFW, восстановленного из бекапа, веб-интерфейс будет недоступен, поскольку ни один локальный интерфейс не будет настроен. Для настройки выполните действия:

1\. Перейдите в **Локальное меню**, введите логин и пароль.

2\. Выберите сетевую карту и настройте интерфейс.

![](/.gitbook/assets/transferring-data-to-another-server.png)

3\. Перейдите в веб-интерфейс в раздел **Сервисы -> Сетевые интерфейсы**. Настройте интерфейсы, восстановленные из бекапа, привязав к ним сетевые карты:

![](/.gitbook/assets/interfaces9.png)

4\. Проверьте:

* В разделе **Сервисы -> DNS** - выданные подключению внешние DNS-серверы;
* В разделе **Сервисы -> DHCP** - опции DHCP-сервера;
* В разделе **Сервисы -> Маршрутизация -> Внешних сетей** - правила маршрутизации;
* В разделе **Сервисы -> OSPF** - настройки интерфейсов;
* В разделе **Правила трафика -> Файрвол** - зоны источника и зоны назначения в правилах;

### Этап 6: Привязка лицензии к восстановленному из бекапа серверу

Если вы переносите бекап с одного сервера на другой в случае неисправности первого сервера, выполните "перепривязку" лицензии. Для этого перейдите в личный кабинет my.ideco.ru и выполните действия:

1\. Отвяжите лицензию от неисправного сервера, нажав на ![](/.gitbook/assets/delete_icon.png).

2\. Отвяжите демо-лицензию от нового сервера, нажав на ![](/.gitbook/assets/icon-cross.png).

3\. Привяжите энтерпрайз-лицензию к новому серверу, нажав на ![](/.gitbook/assets/icon-lk1.png).

При подключении к Ideco Center восстановленного из бэкапа клона сервера он не появится в таблице серверов Ideco Center. Возникает конфликт с донором бэкапа из-за одинакового claster_id. Сервер-клон подменяет собой уже подключенный Ideco NGFW:

![](/.gitbook/assets/transferring-data-to-another-server.gif)

В случае возникновения такой проблемы обратитесь в [Техническую поддержку](/general/technical-support.md).

## Перенос данных почтового сервера

Чтобы перенести данные с UTM 7.9.9 на UTM 9.x с переносом почты на отдельный диск, выполните следующие действия:

1\. Выкачайте всю почту из папки `/var/mail/` на внешнее хранилище. Это можно сделать с помощью различных программ для копирования файлов между локальным компьютером и удаленным сервером (например: rsync, WinSCP, scp от ssh и др.);

2\. Установите с загрузочного образа последнюю версию Ideco NGFW на физический диск;

3\. Подключите второй физический диск, который будет использоваться для хранения почты;

4\. В веб-интерфейсе Ideco NGFW перейдите в раздел **Почтовый релей -> Основные настройки**, выберите диск для хранения почты и отформатируйте его;

5\. Разрешите доступ по SSH из локальных сетей в разделе **Управление сервером -> Администраторы**;

6\. Подключитесь к NGFW, например, с помощью программы WinSCP и скопируйте всю почту по пути `/var/mail/`;

7\. По окончании копирования файлов почты, выполните команду `chown -R ideco-mail-backend:ideco-mail-backend /var/spool/mail/`. Она меняет владельца и группу для файлов почты, чтобы почтовый демон dovecot мог иметь доступ к этим файлам.