---
description: >-
  Используется для удаленной работы пользователей с предоставлением каждому отдельного рабочего стола. 
---

# Авторизация пользователей терминальных серверов

Особенности работы для пользователей терминальных серверов AD:

* Пользователи имеют один IP-адрес, поэтому правила **Файрвола** и **Контроля приложений**, примененные для одного пользователя, будут действовать на всех;
* **Контент-фильтр** распознает этих пользователей, поэтому его правила применяются для отдельных пользователей и групп;
* Сессии авторизации не создаются, так как пользователи терминальных серверов обращаются с одним IP-адресом;
* Работает только при прямых подключениях к прокси.

Для авторизации пользователей терминальных серверов установите флаг **Авторизовать пользователей терминальных серверов** и укажите IP-адрес терминального сервера в одноименной строке. Пользователи, отправляющие запросы с этих IP-адресов, считаются пользователями терминальных серверов и авторизуются через SSO.

Обратите внимание, что при большом количестве пользователей на сервере терминалов может потребоваться [увеличить количество одновременных сессий](https://docs.microsoft.com/ru-ru/windows-server/remote/remote-desktop-services/troubleshoot/remote-desktop-service-currently-busy#check-the-connection-limit-policy) с одного адреса в дополнительных параметрах безопасности.

Возможна **раздельная авторизация пользователей** терминального сервера (работающего под управлением ОС Windows Server 2008 R2 и Windows Server 2012) с помощью авторизации через [Ideco Client](/settings/users/ideco-client/README.md) или по [SSO (NTLM)](/settings/users/active-directory/active-directory-user-authorization.md). При этом сам сервер по IP авторизовать не нужно.

Для раздельной авторизации пользователей терминального сервера: 

* На сервере терминалов настройте [**Remote Desktop IP Virtualization**](https://docs.microsoft.com/en-us/troubleshoot/windows-server/remote/remote-desktop-ip-virtualization); 
* На сервере Ideco NGFW настройте авторизацию пользователей через [Ideco Client](/settings/users/ideco-client/README.md) или [веб-аутентификацию (SSO или NTLM)](/settings/users/active-directory/active-directory-user-authorization.md). 

Авторизация пользователей терминального сервера по логам контроллера домена AD пока не реализована.

## Настройка Remote Desktop IP Virtualization на Windows Server 2012

Для работы функции [Remote Desktop IP Virtualization](https://docs.microsoft.com/en-us/troubleshoot/windows-server/remote/remote-desktop-ip-virtualization) на одном из Windows-серверов должна быть добавлена роль DHCP-сервера (с другими DHCP-серверами эта функция может работать некорректно) и выделена область IP-адресов для пользователей терминального сервера.

В **Редакторе управления групповыми политиками** необходимо перейти по пути: **Computer Configation –> Policies –> Administrative Templates –> Windows Components -> Remote Desktop Service –> Remote Desktop Session Host –> Application Compatibility**

Путь для русскоязычной версии: **Конфигурация компьютера –> Административные шаблоны –> Компоненты Windows -> Служба удаленных рабочих столов –> Узел сеансов удаленных рабочих столов –> Совместимость приложений**. Включить опцию **Turn on Remote Desktop IP Virtualization (Включить IP-виртуализацию удаленных рабочих столов)** в групповой политике с параметром **Per Session (Для сеансов)**:

![](/.gitbook/assets/terminal-server.png)

Рекомендуется также включить опцию **Do not use Remote Desktop Session Host server IP address when virtual IP address is not available (Не использовать IP-адрес сервера узла сеансов удаленных рабочих столов, если виртуальный IP-адрес недоступен)**.

Командой `gpupdate /force` выполнить обновление всех политик.

Проверить, что настройки изменились, можно командой в PowerShell:

`Get-WmiObject -Namespace root\cimv2\TerminalServices -query "select * from Win32_TSVirtualIP"`

Где значения должны быть: 

* `VirtualIPActive = 1` - вкл. виртуализация;
* `VirtualIPMode=0` - для сессии.

Воспользуйтесь [альтернативным](https://social.technet.microsoft.com/wiki/ru-ru/contents/articles/22770.windows-server-2012-r2-ip.aspx) вариантом установки, если описанный выше вариант не подходит.
