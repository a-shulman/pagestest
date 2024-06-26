---
description: В разделе представлена информация о логах работы служб.
---

# Журнал событий

Время хранения логов в разделе **Журналы** - три месяца. После этого логи доступны в разделе **Управление сервером -> Терминал**.

Для просмотра логов определенной службы воспользуйтесь строкой поиска или фильтром. 
Для фильтрации логов по нескольким параметрам нажмите **Добавить фильтр** и выберите соответствующий критерий, значение и оператор в форме.

Фильтрация по нескольким критериям:

![](/.gitbook/assets/logs.png)

По кнопке **Скачать CSV** сохраняются те строки логов, которые заданны фильтрацией.

<details>

<summary>Список служб, доступных в разделе</summary>

* **Файрвол** - ideco-firewall-backend, ideco-nflog;
* **Контроль приложений** - ideco-app-backend, ideco-app-control@Leth<номер локального интерфейса>;
* **Контент-фильтр** - ideco-content-filter-backend;
* **Ограничение скорости** - ideco-shaper-backend;
* **Антивирусы веб-трафика** - ideco-av-backend, ideco-clamd;
* **Предотвращение вторжений** - ideco-suricata-backend, ideco-suricata, ideco-suricata-event-syncer, ideco-suricata-event-to-syslog;
* **Объекты** - ideco-alias-backend;
* **Квоты** - ideco-quotas-backend, systemd-quotacheck;
* **Сетевые интерфейсы** - ideco-network-backend, ideco-network-nic;
* **Балансировка и резервирование**, **Маршрутизация** - ideco-routing-backend;
* **BGP**, **OSPF** - ideco-routing-backend;
* **Прокси** - ideco-proxy-backend, squid;
* **Обратный прокси** - ideco-reverse-backend;
* **DNS** - ideco-dns-backend, unbound;
* **DDNS** - ideco-dns-backend;
* **DHCP** - ideco-dnsmasq;
* **IPsec** - ideco-ipsec-backend, strongswan;
* **Центральная консоль** - ideco-central-console-backend;
* **Кластеризация** - ideco-cluster-backend, ideco-cluster-backup-pusher;
* **Автоматическое обновление** - ideco-sysupdate-backend;
* **Бекапы** - ideco-backup-backend, ideco-backup-create, ideco-backup-restore, ideco-backup-rotate;
* **Лицензия** - ideco-license-backend;
* **VPN-подключения** - ideco-accel-l2tp, ideco-accel-pptp, ideco-accel-sstp, ideco-vpn-servers-backend, ideco-vpn-authd;
* **Авторизация** - ideco-auth-backend;
* **Двухфакторная аутентификация** - ideco-web-authd;
* **Active Directory** - ideco-ad-backend, ideco-ad-log-collector@<имя домена>;
* **ALD Pro** - ideco-ald-rest, ideco-ald-backend;
* **Ideco Client** - ideco-agent-backend, ideco-agent-websocket;
* **Syslog** - ideco-monitor-backend;
* **Обнаружение устройств** - ideco-netscan-backend;
* **Web Application Firewall** - ideco-waf-backend, ideco-waf-event-syncer;
* **IGMP Proxy** - igmpproxy.

</details>

## Защита от brute-force атак
Защита от brute-force атак работает только для NGFW. 

После 6 неудачных попыток ввода пароля в течение 15 минут IP-адрес подбирающего блокируется на 45 минут.

Логи службы `fail2ban` можно увидеть:

* В веб-интерфейсе в разделе **Отчеты и журналы -> Журнал Событий**, задав фильтр `fail2ban`.
* В разделе **Управление сервером -> Терминал**, введя команду `journalctl -u fail2ban`.

Сбросить блокировки можно из локального меню шлюза: **Сбросить блокировки по IP**.

![](/.gitbook/assets/local-menu2.png)
