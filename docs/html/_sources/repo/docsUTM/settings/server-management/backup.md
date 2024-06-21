---
description: >-
  В этом разделе находится описание процесса создания бекапа
  интернет-шлюза Ideco NGFW.
---

Название службы раздела **Бекапы**: `ideco-backup-backend`; `ideco-backup-create`; `ideco-backup-restore`; `ideco-backup-rotate`.\
Список служб для других разделов доступен по [ссылке](/settings/server-management/terminal.md).

Интернет-шлюз поддерживает следующие типы автоматического бекапа:

* на сетевое файловое хранилище по протоколу FTP;
* на сетевое файловое хранилище по протоколу NetBIOS;
* на локальный жесткий диск.

Для настройки автоматического бекапа перейдите в раздел **Управление сервером -> Бекапы -> Настройки** и укажите в настройках час (рекомендуется выбирать ночное время для создания бекапа).

Бекапы включают в себя все настройки, которые администратор может создать в веб-интерфейсе.

Бекапы не включают в себя:

* Логи;
* Почту;
* Статистику web-трафика и другие отчеты;
* Любые кешируемые данные - базы антивирусов, правила IPS и т. п.;
* Настройки созданных [VCE](/settings/server-management/vce.md);
* Любые данные, генерируемые в процессе работы системы автоматически.

Хранить бекапы можно в течение недели или месяца.

![](/.gitbook/assets/backup.png)

Для создания быстрого бекапа нажмите ![](/.gitbook/assets/icon-backup.png) **Создать бекап** в правом верхнем углу веб-интерфейса.

## Бекапы на удаленное файловое хранилище по протоколу FTP

Ключевые параметры, необходимые для настройки бекапа на FTP-сервер, описаны в таблице ниже.

<table><thead><tr><th width="188">Параметр</th><th>Описание</th></tr></thead><tbody><tr><td>Адрес сервера</td><td>IP-адрес удаленного FTP-сервера, на котором будут размещаться копии базы данных</td></tr><tr><td>Логин</td><td>Имя пользователя для авторизации на FTP-сервере</td></tr><tr><td>Пароль</td><td>Пароль для авторизации на FTP-сервере</td></tr><tr><td>Путь к каталогу</td><td>Каталог, в который будут записываться копии базы данных</td></tr></tbody></table>

## Бекапы на сетевое файловое хранилище по протоколу NetBIOS (CIFS)

Ключевые параметры, необходимые для настройки бекапа на NetBIOS-сервер, описаны в таблице.

<table><thead><tr><th width="189">Параметр</th><th>Описание</th></tr></thead><tbody><tr><td>Адрес сервера</td><td>IP-адрес удаленного NetBIOS-сервера, на котором будут размещаться копии базы данных</td></tr><tr><td>Логин</td><td>Имя пользователя для авторизации на сетевом ресурсе Windows</td></tr><tr><td>Пароль</td><td>Пароль для авторизации на сетевом ресурсе Windows</td></tr><tr><td>Путь к каталогу</td><td>Каталог, в который будут записываться копии базы данных</td></tr></tbody></table>

Для доменной учетной записи формат поля **Логин** должен иметь вид: **Имя\_пользователя**.

Укажите путь к каталогу в UNIX-формате. К примеру, в ОС Windows каталог открывается по следующему пути `\\192.168.1.1\dir_1\dir_2\backup`, значит, в поле **Путь к каталогу** пропишите `dir_1/dir_2/backup`.

## Бекапы на локальный жесткий диск

Загрузите бекап с сервера или с компьютера на сервер с помощью веб-интерфейса либо локального меню.

* Кнопка **Добавить** позволяет создать бекап настроек сервера. Копии настроек создаются автоматически ежедневно;
* Кнопка **Мгновенное восстановление** позволяет восстановить все настройки, кроме использованного трафика по квотам, изменений в списке пользователей и отчетах. Бекап применится без перезагрузки;
* Кнопка **Полное восстановление** позволяет восстановить бекап настроек. Возможно восстановление настроек только для бекапа версии, одинаковой с установленной на сервере. Система будет перезагружена;
* Кнопка **Скачать** позволяет скачать бекап с сервера на ваш компьютер;
* Кнопка **Удалить** удаляет бекап с сервера.

Интерфейс управления бекапами:

![](/.gitbook/assets/backup4.png)

Чтобы создать новый бекап через локальное меню Ideco NGFW, выполните действия: 

1\. Выберите пункт **9** и нажмите **Enter**. 

2\. Введите комментарий для бекапа и нажмите **Enter**.

Пример создания бекапа через локальное меню приведен на скриншоте ниже:

![](/.gitbook/assets/backup5.png)

## Восстановление конфигурации из бекапа

Восстановите конфигурацию из бекапа, выбрав один из способов:

<details>

<summary>Через локальное меню</summary>

Перейдите в локальное меню и выполните действия:

1\. Выберите пункт:
* **10** - восстановятся все настройки и перезагрузится сервер;
* **11** - восстановятся все настройки без перезагрузки сервера, кроме использованного трафика по квотам, изменений в списке пользователей и отчетах.

  Нажмите **Enter**. 

2\. Выберите из списка бекап, введя пункт нужной копии, и нажмите **Enter**. 

3\. Перезагрузите сервер, введя **y**, а затем **Enter**.

Пример восстановления из бекапа через локальное меню:

![](/.gitbook/assets/backup6.png)

</details>

<details>

<summary>Через веб-интерфейс</summary>

Перейдите в раздел **Управление сервером -> Бекапы -> Бекапы** и нажмите кнопку **Применить** (![](/.gitbook/assets/icon-recovery.png) в столбце **Управление**). Система будет перезагружена для применения настроек сервера.

</details>

Чтобы перенести установленный Ideco NGFW с одного сервера на другой с сохранением всех настроек, воспользуйтесь статьей [Перенос данных и настроек на другой сервер](/recipes/popular-recipes/transferring-data-to-another-server.md).