# Режим удаленного помощника

Чтобы служба технической поддержки могла подключиться к серверу удаленно, необходимо включить режим удаленного помощника. Работа сервера в этом режиме не влияет на работу пользователей.

Для включения режима удаленного помощника нажмите на значок ![icon-help.png](/.gitbook/assets/icon-help.png) в правом верхнем углу экрана и переведите ползунок около пункта **Удаленный помощник** в статус **Включен**.

![](/.gitbook/assets/support1.gif)

## Включение режима удаленного помощника из веб-интерфейса

Для подключения специалиста технической поддержки сообщите ему **Информацию для технической поддержки**, нажав кнопку **Скопировать**. Также нужно отдельно передать публичный IP-адрес сервера. Если сервер подключен не напрямую к Ideco NGFW, выполните проброс с внешнего маршрутизатора 22-го порта на NGFW.

Режим удаленного помощника остается включенным даже при перезагрузке сервера. Отключайте этот режим, когда использовать его нет необходимости. **Крайне не рекомендуется постоянная эксплуатация сервера Ideco NGFW в этом режиме.**

## Включение режима удаленного помощника из локального меню сервера

Чтобы включить режим удаленного помощника, в локальном меню Ideco NGFW выберите пункт **Включить доступ Удаленного помощника**, введя пункт **11**, затем нажмите **Enter**.\
Сгенерируется пароль, который необходимо сообщить технической поддержке для подключения по SSH.

![](/.gitbook/assets/local-menu1.png)

## Работа с сервером по протоколу SSH в режиме удаленного помощника

Чтобы организовать работу с локальной консолью сервера удаленно по протоколу SSH от пользователя **root** в режиме удаленного помощника, необходимо выполнить следующие действия:

1\. Подключитесь к серверу с помощью SSH-клиента **PuTTY**. Программа бесплатна, и скачать ее можно на сайте разработчиков ([https://www.putty.org/](https://www.putty.org/)).

2\. При подключении из локальной сети используйте адрес, который настроен на локальной сетевой карте Ideco. Введите необходимые параметры для подключения:
   * **порт** - 22;
   * **логин** - remsup;
   * **пароль, указанный при включении удаленного помощника.**

Символ "#" свидетельствует, что работа ведется от имени суперпользователя.
