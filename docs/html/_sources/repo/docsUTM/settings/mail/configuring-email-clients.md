---
description: Настройка и примеры настроек популярных почтовых клиентов.
---

# Настройка почтовых клиентов

Начиная с версии UTM 7.0.0, подключиться из сети интернет программой Outlook (любой версии) по протоколу POP3 можно только с типом шифрования SSL. Подключение без шифрования извне запрещено на почтовом сервере. 

Остается возможность подключаться по протоколу IMAP с использованием STARTTLS или SSL. Для этого выберите соответствующий тип шифрования в Outlook.

В Ideco NGFW нет ограничений по количеству почтовых клиентов для одного почтового адреса по протоколу imap.

## Настройка почтового клиента при работе из локальной сети

1\. Сервер входящей почты работает на 995 TCP-порту (РОР3) и на 143 TCP-порту (IMAP) с шифрованием STARTTLS/SSL:
* В качестве логина прописывается логин от учетной записи пользователя.
* В качестве пароля всегда прописывается пароль от учетной записи пользователя (в том числе для пользователей, импортированных из Active Directory), задать отдельный пароль на почтовый ящик нельзя.

2\. Сервер исходящей почты работает на 587 порту TCP с шифрованием STARTTLS/SSL. Без авторизации возможна отправка почты только из доверенных сетей (их можно настроить в разделе **Почтовый релей -> Расширенные настройки -> Безопасность**).

## Настройка почтового клиента при работе из сети интернет

1\. Сервер входящей почты работает на 995 TCP-порту (POP3S) и на 143 TCP-порту (IMAP-STARTTLS/SSL), шифрование обязательно:

   * В качестве логина прописывается логин от учетной записи пользователя;
   * В качестве пароля всегда прописывается пароль от учетной записи пользователя, сделать отдельный пароль на почту нельзя.

2\. Сервер исходящей почты работает только с авторизацией и шифрованием. Необходимо обязательно использовать 587 порт для подключения (а не 25). Тип шифрования, логин и пароль указываются аналогично серверу входящей почты.

Для любого почтового клиента, кроме веб-интерфейса почты в составе NGFW, установите корневой сертификат сервера NGFW, его можно скачать в разделе **Сервисы -> Сертификаты**.

## Примеры настроек популярных почтовых клиентов

<details>

<summary>Настройка почтового клиента Outlook 2013 и 2016</summary>

Пример настроек клиента Microsoft Outlook 2013 по протоколу IMAP:

<img src="/.gitbook/assets/configuring-email-clients.png" alt="" data-size="original">

Пример настроек клиента Microsoft Outlook 2016 по протоколу IMAP:

<img src="/.gitbook/assets/configuring-email-clients1.png" alt="" data-size="original">

Для отображения IMAP-папок снимите галочку **При просмотре дерева в Outlook показывать только подписанные папки** в свойствах IMAP-папок:

<img src="/.gitbook/assets/mail-settings4.png" alt="" data-size="original">

</details>

<details>

<summary>Настройка почтового клиента iPhone</summary>

Процесс настройки делится на два этапа:
* Установка корневого SSL-сертификат NGFW;
* Настройка почтового ящика.

**Установка корневого SSL-сертификат NGFW:**

1\. Скачайте сертификат в разделе **Сервисы -> Сертификаты** и перенесите на настраиваемое устройство (например, отправив по почте). 

2\. Нажмите кнопку **Установить**.

3\. Зайдите в раздел **Настройки -> Основные**.

<img src="/.gitbook/assets/mail-settings5.png" alt="" data-size="original">

4\. Выберите **Об этом устройстве -> Доверие сертификатов**:

<img src="/.gitbook/assets/mail-settings6.png" alt="" data-size="original">

5\. Включите настройку **Доверять корневым сертификатам полностью**

<img src="/.gitbook/assets/mail-settings7.png" alt="" data-size="original">

**Настройка почтового ящика:**

1\. Перейдите в Учетную запись почты и нажмите **Дополнительно**:

<img src="/.gitbook/assets/mail-settings8.png" alt="" data-size="original">

2\. Скорректируйте настройки:

<img src="/.gitbook/assets/mail-settings9.png" alt="" data-size="original">

</details>

<details>

<summary>Настройка почтового клиента Thunderbird</summary>

1\. Перейдите в **Настройки -> Параметры ученой записи**.

2\. Заполните обязательные поля:

* Имя сервера;
* Порт;
* Имя пользователя;
* Защита соединения;
* Метод аутентификации (рекомендуем указать **Обычный пароль**).

При необходимости заполните _Параметры сервера_ и _Хранилище сообщений_.

<img src="/.gitbook/assets/mail-settings10.png" alt="" data-size="original">

</details>
