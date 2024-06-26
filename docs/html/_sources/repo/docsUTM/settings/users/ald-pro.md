---
description: >- 
    Настройка односторонней синхронизации с системой управления каталогами ALD Pro
---

# ALD Pro

Название службы раздела **ALD Pro**: `ideco-ald-rest`; `ideco-ald-backend`. \
Список служб для других разделов доступен по [ссылке](/settings/server-management/terminal.md).

Ideco NGFW поддерживает версии ALD Pro от 1.4 и выше.

[ALD Pro](https://www.aldpro.ru/) предназначен для централизованного управления ресурсами под управлением ОС Astra Linux и может использоваться в организациях различного масштаба.

Руководства по эксплуатации ALD Pro доступны на [официальном сайте](https://www.aldpro.ru/docs/).

Синхронизация с ALD Pro приостанавливается, если локальные пользователи Ideco NGFW находятся в группах AD.
Для возобновления синхронизации вынесите локальных пользователей из групп ALD Pro. Автоматическая синхронизация произойдет через 15 минут.

## Ввод сервера в домен

1\. Перейдите в раздел **Сервисы -> DNS -> Внешние DNS-серверы** и добавьте IP-адрес DNS-сервера ALD:

![](/.gitbook/assets/ald-pro1.png)

2\. Перейдите на вкладку **Пользователи -> ALD Pro**.

2\. Нажмите на кнопку **Добавить**.

3\. Заполните следующие поля:

   * **Домен**: введите полное имя домена (не контроллера домена). Например: `mydomain.example`. Домен может содержать только латинские символы, цифры, подчеркивание, дефис и точку;
   * **IP-адрес DNS-сервера**: добавьте IP адрес DNS-сервера ALD;
   * **Имя сервера Ideco NGFW**: введите имя сервера. Оно может содержать только буквенные символы (A-z), цифры (0-9), а также не может начинаться или заканчиваться на дефис. Максимальное количество символов - 15;
   * **Логин и пароль администратора**: **эти данные не сохраняются** на сервере и используется один раз для присоединения к домену. Пользователь может не быть администратором домена, но должен обладать правами на присоединения компьютеров к домену.

![](/.gitbook/assets/ald-pro.png)

Инструкции по развертыванию и управлению ресурсами через ALD Pro доступны на [официальном сайте](https://www.aldpro.ru/docs/).

## Импорт пользователей

ALD Pro поддерживает импорт двух типов групп:

* Группа пользователей - содержит несколько пользователей ALD.
* Подразделение - содержит дерево пользователей ALD, обладающих определенным уровнем доступа.

Для импорта пользователей выполните действия:

1\. Перейдите в раздел **Пользователи -> Учетные записи** и создайте группу, в которую будут импортированы пользователи, нажав на ![](/.gitbook/assets/icon-folder.png).

2\. Перейдите на вкладку **ALD Pro**, выберите домен, тип группы и нажмите **Присоединить к домену**.

Импортированных пользователей можно использовать в качестве объектов для авторизации, настройки VPN-подключений, создания правил (например, в **Файрволе**).

В дальнейшем пользователи будут автоматически синхронизироваться с ALD Pro каждые 15 минут.

Пользователь может быть импортирован только в одну группу Ideco NGFW. Если он находится в нескольких группах ALD Pro, он попадет только в одну группу, которая была импортирована последней.

## Аутентификация пользователей

При аутентификации пользователей проверка осуществляется средствами Kerberos.

ALD Pro поддерживает два типа входа в систему:

* вход по логину/паролю;
* вход через SSO.

### Настройка Ideco NGFW

Для настройки аутентификации выполните действия: 

1\. Перейдите в раздел **Пользователи -> Авторизация -> Основное**.

2\. Активируйте опцию **Веб-аутентификация**.

3\. Выберите тип входа в систему:\
    3.1 Для входа по логину/паролю активируйте опцию **Аутентификация через веб-интерфейс**.\
    3.2 Для входа через SSO активируйте опцию **SSO-аутентификация через Active Directory и ALD Pro**.

![](/.gitbook/assets/active-directory5.png)

После заполнения поля *Доменное имя Ideco NGFW* и сохранения настроек будет выдан Let’s Encrypt сертификат, и пользователь будет перенаправляться на окно авторизации, минуя страницу исключения безопасности:

![](/.gitbook/assets/web-autorization2.png)

Если сертификат для такого домена уже загружен в разделе [Сертификаты](/settings/services/certificates/README.md), то будет использоваться загруженный сертификат, новый сертификат выдаваться не будет.

Если NGFW не подключен к интернету или доменное имя не соответствует внешнему IP-адресу NGFW, то страница авторизации будет подписана корневым сертификатом NGFW.

### Настройка клиентских машин для SSO-авторизации

На странице настроек браузера Mozilla Firefox (about:config в адресной строке) настройте следующие параметры:

* `network.automatic-ntlm-auth.trusted-uris` и `network.negotiate-auth.trusted-uris` добавьте адрес локального интерфейса Ideco NGFW (например, idecoNGFW.example.ru);
* `security.enterprise_roots.enabled` в значении `true` позволит Firefox доверять системным сертификатом и авторизовать пользователей при переходе на HTTPS-сайты.

Способы аутентификации импортированных пользователей:

* Авторизация по IP-адресу - подходит для пользователей с фиксированным IP-адресом. IP-адреса на NGFW необходимо прописать вручную каждому пользователю;
* Авторизация по VPN - подходит для аутентификации пользователей удаленных сетей.

Для настройки авторизации по VPN воспользуйтесь статьей [VPN-подключения](/settings/users/authorization/vpn-connection/README.md).
