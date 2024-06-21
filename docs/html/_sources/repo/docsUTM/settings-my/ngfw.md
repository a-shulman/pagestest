---
description: Раздел позволяет управлять лицензиями, скачивать установочные файлы продуктов компании "Айдеко", переходить в режим online-демо и настройка оффлайн-лицензирования.
---

# NGFW

## Лицензирование

Подробнее о видах лицензий в статье [Лицензирование](/general/license.md).

Посмотреть информации о сервере и лицензии можно в разделе **NGFW -> Лицензирование**, нажав на иконку ![](/.gitbook/assets/icon-eye.png) напротив нужного сервера.

Информация о лицензии содержит сведения о сроке действия лицензии, количестве пользователей, сроке окончания обновлений, технической поддержки продукта и др.

### Добавление коммерческой (Enterprise) лицензии

1\. Скопируйте токен лицензии из письма, отправленного после покупки лицензии. Формат токена: `owhYLGvT6Xmt819JyinSxREkJfvjVO63`. 

2\. Перейдите в [личный кабинет MY.IDECO](https://my.ideco.ru/) в раздел **NGFW -> Лицензирование** и нажмите **Добавить коммерческую лицензию**.

3\. Введите токен в поле **Токен лицензии** и нажмите **Добавить**. 

Токен станет недействительным, а в таблице **Свободные лицензии** отобразится купленная лицензия.

### Добавление SMB (бесплатной) лицензии

Для добавления SMB-лицензии нажмите кнопку **Добавить бесплатную лицензию** в разделе **Лицензирование**. Добавленная лицензия отобразится в таблице **Свободные лицензии**.

### Привязка лицензии к серверу

Привязать лицензию к серверу можно двумя способами - онлайн и оффлайн. Онлайн проводится только в [MY.IDECO](https://my.ideco.ru/). Оффлайн потребует доступ к веб-интерфейсу сервера.

Назначьте имеющиеся коммерческие лицензии на любой зарегистрированный сервер Ideco NGFW с учетом следующих ограничений:

* Одна лицензия может быть привязана только к одному серверу;
* Демо-лицензию нельзя привязать к другому серверу;
* Демо-лицензию нельзя повторно получить на одну и ту же инсталляцию сервера;
* При удалении сервера с демо-лицензией также удаляется и лицензия.

#### Онлайн

Выберите удобный вариант привязки:
* Во вкладке **Лицензирование** нажмите ![](/.gitbook/assets/icon-lk1.png). Далее в открывшемся окне выберите нужную лицензию и сохраните изменения нажав **Привязать лицензию**.
* Во вкладке **Лицензирование** выберите **Свободные лицензии** и нажмите ![](/.gitbook/assets/icon-lk.png). Далее укажите нужный сервер и сохраните изменения нажав **Привязать**.

#### Оффлайн

1\. Для предоставления оффлайн лицензии обратитесь к менеджеру.

2\. Привяжите предоставленную лицензию к серверу:

* Во вкладке **Лицензирование** нажмите ![](/.gitbook/assets/icon-lk1.png). Далее в открывшемся окне выберите нужную лицензию и сохраните изменения нажав **Привязать лицензию**.
* Во вкладке **Лицензирование** выберите **Свободные лицензии** и нажмите ![](/.gitbook/assets/icon-lk.png). Далее укажите нужный сервер и сохраните изменения нажав **Привязать**.

Пример наименования сервера для **оффлайн**-регистрации: `UTM (UTM Unknown)`

Если была выбрана лицензия не подходящая для оффлайн-регистрации сервера, то появится ошибка:

![](/.gitbook/assets/initial-setup13.png)

3\. Перейдите в раздел **NGFW -> Оффлайн** и введите в соответствующие поля мажорный номер версии и номер лицензии:

![](/.gitbook/assets/initial-setup12.png)

4\. Нажмите **Получить ссылки** и сохраните файл конфигураций, нажав на license:

Помимо информации о лицензии личный кабинет предоставит файлы для обновления баз модулей безопасности. Подробнее о процессе обновления в статье [Регистрация сервера](/installation/server-registration.md#offlain-registraciya) (шаги 8 и 9).

5\. Добавьте конфигурационный файл c информацией о лицензии в Ideco NGFW:

* Перейдите в раздел **Управление сервером -> Терминал**;
* Загрузите полученный файл `license.json` на сервер Ideco NGFW в директорию `/var/cache/ideco/license-backend/`;
* Перезапустите сервис лицензий командой `systemctl restart ideco-license-backend.service`;
* Перейдите в раздел **Управление сервером - Лицензия** и убедитесь, что лицензия установлена.

## Скачать

Вкладка содержит установочные файлы последних версий разработанных компанией "Айдеко" программных продуктов и их краткое описание.

## Online-демо

Чтобы ознакомиться с демоверсией Ideco NGFW, зайдите в личный кабинет MY.IDECO, в раздел **NGFW -> Online-демо**. Перейдите по ссылке **Реквизиты для доступа на демо-сайт** и введите логин `administrator` и пароль `servicemode`.

Демоверсия Ideco NGFW всегда равна последней реализованной версии. Учетная запись, доступная по логину и паролю выше, имеет права только на просмотр интерфейса. Если необходима учетная запись с правами на редактирование, обратитесь в отдел продаж.