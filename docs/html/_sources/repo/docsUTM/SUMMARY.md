# Table of contents

* [Об Ideco NGFW](README.md)

## Общая информация <a href="#general" id="general"></a>

* [Лицензирование](general/license.md)
* [Cистемные требования и источники обновления данных Ideco NGFW](general/data-update-source-ideco-utm.md)
* [Техническая поддержка](general/technical-support.md)

## Быстрый старт Ideco NGFW <a href="#installation" id="installation"></a>

* [Рекомендации при первоначальной настройке](installation/tips-for-initial-setup.md)
* [MY.IDECO.RU](installation/initial-action-my-ideco.md)
* [Подготовка к установке на устройство](installation/preparation-install.md)
  * [Настройка гипервизора](installation/specifics-of-hypervisor-settings.md)
  * [Подготовка загрузочного диска](installation/usb.md)
* [Установка](installation/installation-process.md)
* [Первоначальная настройка](installation/initial-setup.md)
* [Регистрация сервера](installation/server-registration.md)

## Настройка Ideco NGFW <a href="#settings" id="settings"></a>

* [Панель мониторинга](settings/monitor-panel.md)
* [Пользователи](settings/users/README.md)
  * [Учетные записи](settings/users/user-tree/README.md)
    * [Управление пользователями](settings/users/user-tree/user-management.md)
    * [Настройка пользователей](settings/users/user-tree/customization-of-users.md)
  * [Авторизация пользователей](settings/users/authorization/README.md)
    * [Веб-аутентификация](settings/users/authorization/web-authorization.md)
    * [IP и MAC авторизация](settings/users/authorization/ip-and-mac-authorization/README.md)
      * [Авторизация по IP-адресу](settings/users/authorization/ip-and-mac-authorization/ip-authorization.md)
      * [Авторизация по MAC-адресу](settings/users/authorization/ip-and-mac-authorization/mac-authorization.md)
    * [Авторизация по подсетям](settings/users/authorization/authorization-by-subnet.md)
    * [Авторизация пользователей терминальных серверов](settings/users/authorization/terminal-server.md)
  * [Личный кабинет пользователя](settings/users/user-personal-account.md)
  * [VPN-подключение](settings/users/authorization/vpn-connection/README.md)
    * [Двухфакторная аутентификация](settings/users/two-factor-authentication.md)
    * [Подключение по PPTP](settings/users/authorization/vpn-connection/pptp.md)
    * [Подключение по PPPoE](settings/users/authorization/vpn-connection/pppoe.md)
    * [Подключение по IKEv2/IPsec](settings/users/authorization/vpn-connection/ipsec-ikev2.md)
    * [Подключение по SSTP](settings/users/authorization/vpn-connection/sstp.md)
    * [Подключение по L2TP/IPsec](settings/users/authorization/vpn-connection/l2tp-ipsec.md)
    * [Особенности маршрутизации и организации доступа](settings/users/authorization/vpn-connection/features.md)
    * [Инструкция по запуску PowerShell скриптов](settings/users/authorization/vpn-connection/running-powershell-scripts.md)
  * [Ideco Client](settings/users/ideco-client/README.md)
    * [Установка и настройка Ideco Client на Windows](settings/users/ideco-client/ideco-client-windows.md)
    * [Установка и настройка Ideco Client на MacOS](settings/users/ideco-client/ideco-client-macos.md)
  * [Профили устройств](settings/users/hip-profiles.md)
  * [Интеграция с Active Directory/Samba DC](settings/users/active-directory/README.md)
    * [Ввод сервера в домен](settings/users/active-directory/entering-the-server-into-the-domain.md)
    * [Аутентификация пользователей AD/Samba DC](settings/users/active-directory/active-directory-user-authorization.md)
    * [Скрипты автоматической разавторизации](settings/users/active-directory/auto-de-authorization-script.md)
    * [Импорт пользователей](settings/users/active-directory/user-import.md)
  * [Интеграция с RADIUS-сервером](settings/users/radius.md)
  * [ALD Pro](settings/users/ald-pro.md)
  * [Обнаружение устройств](settings/users/device-discovery.md)
  * [Wi-Fi-сети](settings/users/wifi-network.md)
* [Мониторинг](settings/monitor/README.md)
  * [Авторизованные пользователи](settings/monitor/authorized-users.md)
  * [График загруженности](settings/monitor/workload-schedule.md)
  * [Монитор трафика](settings/monitor/traffic.md)
  * [Telegram-бот](settings/monitor/telegram-bot.md)
  * [SNMP](settings/monitor/snmp.md)
  * [Zabbix-агент](settings/monitor/zabbix.md)
* [Правила трафика](settings/access-rules/README.md)
  * [Файрвол](settings/access-rules/firewall.md)
    * [Таблицы файрвола (FORWARD, DNAT, INPUT и SNAT)](settings/access-rules/firewall-tables.md)
    * [Логирование](settings/access-rules/logging.md)
  * [Контроль приложений](settings/access-rules/application-control.md)
  * [Контент-фильтр](settings/access-rules/content-filter/README.md)
    * [Описание категорий контент-фильтра](settings/access-rules/content-filter/custom-categories.md)
    * [Настройка фильтрации HTTPS](settings/access-rules/content-filter/filtering-https-traffic.md)
    * [Изменение страницы блокировки](settings/access-rules/content-filter/block-page.md)
  * [Ограничение скорости](settings/access-rules/shaper.md)
  * [Антивирусы веб-трафика](settings/access-rules/antivirus.md)
  * [Предотвращение вторжений](settings/access-rules/ips/README.md)
    * [Журнал](settings/access-rules/ips/log.md)
    * [Правила](settings/access-rules/ips/rules.md)
    * [Исключения из правил](settings/access-rules/ips/exceptions-rules.md)
    * [Настройки](settings/access-rules/ips/settings.md)
  * [Исключения](settings/access-rules/ips/user-ip-exceptions.md)
  * [Объекты](settings/access-rules/aliases.md)
  * [Квоты](settings/access-rules/quotas.md)
* [Сервисы](settings/services/README.md)
  * [Сетевые интерфейсы](settings/services/connection-to-provider/README.md)
    * [Настройка Локального Ethernet](settings/services/connection-to-provider/local-ethernet.md)
    * [Настройка Внешнего Ethernet](settings/services/connection-to-provider/ethernet-connection.md)
    * [Настройка подключения по PPTP](settings/services/connection-to-provider/pptp-connection.md)
    * [Настройка подключения по L2TP](settings/services/connection-to-provider/l2tp-connection.md)
    * [Настройка подключения по PPPoE](settings/services/connection-to-provider/pppoe-connection.md)
    * [Подключение по 3G и 4G](settings/services/connection-to-provider/3g-4g-connection.md)
  * [Балансировка и резервирование](settings/services/multiple-simultaneous-connections.md)
  * [Маршрутизация](settings/services/routing.md)
  * [BGP](settings/services/bgp.md)
  * [OSPF](settings/services/ospf.md)
  * [IGMP Proxy](settings/services/igmp.md)
  * [Прокси](settings/services/proxy/README.md)
    * [Исключения](settings/services/proxy/exclusions.md)
    * [Настройка прямого подключения к прокси](settings/services/proxy/direct-connection-proxy.md)
    * [Настройка прокси с одним интерфейсом](settings/services/proxy/proxy-single-interface.md)
  * [Обратный прокси](settings/services/reverse-proxy.md)
  * [DNS](settings/services/dns/README.md)
    * [Внешние DNS-серверы](settings/services/dns/dns-external.md)
    * [Master-зоны](settings/services/dns/master-zon.md)
    * [Forward-зоны](settings/services/dns/forward-zon.md)
    * [DDNS](settings/services/dns/ddns.md)
  * [DHCP-сервер](settings/services/dhcp.md)
  * [NTP-сервер](settings/services/ntp.md)
  * [IPsec](settings/services/ipsec/README.md)
    * [Подключение между двумя Ideco NGFW в туннельном режиме работы](settings/services/ipsec/site-to-site/ipsec-utm-to-utm-tunnel.md)
    * [Подключение между двумя Ideco NGFW в транспортном режиме работы](settings/services/ipsec/site-to-site/ipsec-utm-to-utm-transport.md)
    * [Подключение Ideco NGFW и Mikrotik](settings/services/ipsec/site-to-site/site-to-site-ideco-mikrotik.md)
    * [Подключение MikroTik и Ideco NGFW по L2TP/IPsec и IKev2/IPsec](settings/services/ipsec/site-to-site/utm-to-mikrotik-vpn.md)
    * [Подключение Cisco IOS и Ideco NGFW](settings/services/ipsec/site-to-site/connect-utm-to-cisco-via-ipsec.md)
    * [Подключение pfSense к Ideco NGFW по IPsec](settings/services/ipsec/site-to-site/ipsec-connection-pfsense-to-utm.md)
    * [Подключение Kerio Control и Ideco NGFW по IPsec](settings/services/ipsec/site-to-site/ipsec-connection-kerio-control-to-utm.md)
    * [Подключение Keenetic по SSTP или IPsec](settings/services/ipsec/site-to-site/keenetic-connection.md)
  * [Сертификаты](settings/services/certificates/README.md)
    * [Загрузка SSL-сертификата на сервер](settings/services/certificates/upload-ssl-certificate-to-server.md)
    * [Создание самоподписанного сертификата c помощью Powershell](settings/services/certificates/creating-ssl-sert-powershell.md)
    * [Создание сертификата c помощью openssl](settings/services/certificates/creating-openssl-cert.md)
* [Отчеты и журналы](settings/reports/README.md)
  * [Трафик](settings/reports/traffic.md)
  * [Журнал событий](settings/reports/logs.md)
  * [Журнал веб-доступа](settings/reports/web-logs.md)
  * [Журнал антивируса](settings/reports/antivirus-logs.md)
  * [События безопасности](settings/reports/security-events.md)
  * [Действия администраторов](settings/reports/administrator-actions.md)
  * [Журнал авторизации](settings/reports/authorization-log.md)
  * [Конструктор отчетов](settings/reports/report-designer.md)
  * [Syslog](settings/reports/syslog.md)
* [Управление сервером](settings/server-management/README.md)
  * [Администраторы](settings/server-management/admins.md)
  * [Центральная консоль](settings/server-management/central-console.md)
  * [VCE](settings/server-management/vce.md)
  * [Кластеризация](settings/server-management/cluster.md)
  * [Автоматическое обновление сервера](settings/server-management/server-update.md)
  * [Бекап](settings/server-management/backup.md)
  * [Терминал](settings/server-management/terminal.md)
  * [Лицензия](settings/server-management/license-management.md)
  * [Дополнительно](settings/server-management/additionally.md)
* [Почтовый релей](settings/mail/README.md)
  * [Основные настройки](settings/mail/mail-server-settings/README.md)
    * [Web-почта](settings/mail/mail-server-settings/web-mail.md)
    * [Настройка почтового релея](settings/mail/mail-server-settings/mail-relay-settings.md)
    * [Настройка почтового сервера](settings/mail/mail-server-settings/mail-server-settings.md)
  * [Расширенные настройки](settings/mail/advanced-settings/README.md)
    * [Настройка домена у регистратора/держателя зоны](settings/mail/advanced-settings/domain-settings-at-zone-holder.md)
  * [Антиспам](settings/mail/antispam.md)
  * [Правила](settings/mail/regulations/README.md)
    * [Переадресация почты](settings/mail/regulations/mail-forwarding.md)
  * [Почтовая очередь](settings/mail/mail-queue.md)
  * [Настройка почтовых клиентов](settings/mail/configuring-email-clients.md)
  * [Схема фильтрации почтового трафика](settings/mail/filtering-scheme-for-mail-traffic.md)
* [Публикация ресурсов](settings/publishing-resources/README.md)
  * [Доступ из внешней сети без NAT](settings/publishing-resources/access-from-external-network-without-nat.md)
  * [Публикация веб-приложений (обратный прокси-сервер)](settings/publishing-resources/publishing-web-applications.md)
  * [Настройка публичного IP-адреса на компьютере в локальной сети](settings/publishing-resources/configure-public-ip-on-computer-on-the-local-net.md)
  * [Портмаппинг (проброс портов, DNAT)](settings/publishing-resources/portmapping.md)
* [Интеграция NGFW и SkyDNS](settings/skydns.md)

## Настройка MY.IDECO <a href="#settings-my" id="settings-my"></a>

* [О личном кабинете MY.IDECO](settings-my/README.md)
* [NGFW](settings-my/ngfw.md)
* [Monitoring Bot и Security](settings-my/bot-security.md)
* [Личные данные и Компании](settings-my/personal-details-and-companies.md)

## Настройка Ideco Center <a href="#settings-cc" id="settings-cc"></a>

* [Об Ideco Center](settings-cc/README.md)
* [Установка Ideco Center](settings-cc/setup.md)
* [Серверы](settings-cc/servers.md)
* [Мониторинг](settings-cc/monitor.md)
* [Политики и объекты](settings-cc/policies-and-objects.md)
* [Сервисы](settings-cc/services.md)
* [Отчеты и журналы](settings-cc/reports.md)
* [Управление сервером](settings-cc/server-management.md)


## Популярные инструкции и диагностика проблем <a href="#recipes" id="recipes"></a>

* [FAQ](recipes/popular-recipes/README.md)
  * [Режим удаленного помощника](recipes/popular-recipes/remote-assistant.md)
  * [Разрешить интернет всем: диагностика неполадок](recipes/popular-recipes/allow-internet-all.md)
  * [Удаленный доступ к серверу](recipes/popular-recipes/remote-access-for-server-management.md)
  * [Тестирование оперативной памяти сервера](recipes/popular-recipes/memory-testing.md)
  * [Инструкции по созданию VPN-подключений](recipes/popular-recipes/vpn/README.md)
    * [Создание VPN-подключения в Ubuntu](recipes/popular-recipes/vpn/connection-for-ubuntu.md)
    * [Cоздание VPN-подключения в Fedora](recipes/popular-recipes/vpn/connection-for-fedora.md)
    * [Создание подключения в Astra Linux](recipes/popular-recipes/vpn/connection-for-astra-linux.md)
    * [Автоматическое создание подключений](recipes/popular-recipes/vpn/auto-connect.md)
    * [Создание подключения в Windows 10](recipes/popular-recipes/vpn/connection-for-windows10.md)
    * [Создание подключения в Windows 7](recipes/popular-recipes/vpn/connection-for-windows7.md)
    * [Создание VPN-подключения на мобильных устройствах](recipes/popular-recipes/vpn/connection-for-mobile-devices.md)
    * [Создание подключения в Mac OS](recipes/popular-recipes/vpn/connection-for-high-sierra-macos.md)
    * [Подключение по SSTP Wi-Fi роутеров Keenetic](recipes/popular-recipes/vpn/sstp-connecting-keenetic-wi-fi-routers.md)
  * [Как избавиться от асимметричной маршрутизации трафика](recipes/popular-recipes/access-to-remote-networks.md)
  * [Что делать если ваш IP попал в черные списки DNSBL](recipes/popular-recipes/dnsbl-list.md)
  * [Как восстановить доступ к Ideco NGFW](recipes/popular-recipes/restore-access-to-ideco-utm.md)
  * [Как восстановиться на прошлую версию после обновления Ideco NGFW](recipes/popular-recipes/go-back.md)
  * [Проверка настроек фильтрации с помощью security ideco](recipes/popular-recipes/security-ideco.md)
  * [Выбор аппаратной платформы для Ideco NGFW](recipes/popular-recipes/choosing-hardware-platform.md)
  * [Поддержка устаревших алгоритмов шифрования](recipes/popular-recipes/legacy-encryption-support.md)
  * [Настройка программы Proxifier для прямых подключений к прокси серверу](recipes/popular-recipes/configuring-proxifier.md)
  * [Блокировка популярных ресурсов](recipes/popular-recipes/blocking-popular-resources.md)
  * [Настройка прозрачной авторизации на Astra linux](recipes/popular-recipes/authorization-astra-linux.md)
  * [Настройка автоматической веб-аутентификации на Ideco NGFW на Linux](recipes/popular-recipes/auto-authorization-linux.md)
  * [Перенос данных и настроек на другой сервер](recipes/popular-recipes/transferring-data-to-another-server.md)
  * [Порядок обработки веб-трафика в Ideco NGFW](recipes/popular-recipes/processing-order.md)
  * [Интеграция Ideco NGFW и брокера сетевых пакетов DS Integrity NG](recipes/popular-recipes/integrity.md)
  * [Настройка cовместной работы ViPNet Координатор с Ideco NGFW](recipes/popular-recipes/vipnet-coordinator.md)
  * [Блокировка чат-ботов](recipes/popular-recipes/block-chat-bot.md)
  * [Таблица портов Ideco NGFW, доступных из локальной и внешних сетей](recipes/popular-recipes/open-ports.md)
* [Диагностика проблем](recipes/problem-diagnosis/README.md)
  * [Ошибка при открытии сайта ERR\_CONNECTION\_TIMED\_OUT или Не открывается сайт](recipes/problem-diagnosis/site-does-not-open.md)
  * [Что делать если не работает интернет](recipes/problem-diagnosis/what-to-do-if-the-internet-does-not-work.md)
  * [Ошибка при авторизации "The browser is outdated"](recipes/problem-diagnosis/old-browser.md)
  * [Если соединение по IPsec не устанавливается](recipes/problem-diagnosis/ipsec.md)

## API

* [Описание основных хендлеров](api/description-of-handlers.md)
* [Управление интеграцией с Active Directory](api/active-directory-api.md)
* [Управление пользователями](api/user-management-api.md)
* [Управление правилами трафика](api/access-rules-api.md)
* [DHCP-сервер](api/dhcp-api.md)
* [DNS-сервер](api/dns-api.md)
* [Настройка удаленной передачи системных логов](api/logs-api.md)
* [Центральная консоль](api/cc-api.md)
* [Бекапы](api/backup-api.md)
* [Примеры использования](api/examples/README.md)
  * [Редактирование пользовательской категории контент-фильтра](api/examples/editing-a-custom-category.md)
  * [Создание правила Forward](api/examples/creating-a-forward-rule.md)

## changelog

* [Ideco NGFW 17.x](changelog/ideco-utm/README.md)
* [Ideco Center 17.Х](changelog/cc/README.md)
