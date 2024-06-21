
Время хранения логов в разделе **Журналы** - три месяца. После этого логи доступны в разделе **Управление сервером -> Терминал**.

Для просмотра логов определенной службы воспользуйтесь строкой поиска или фильтром. 
Для фильтрации логов по нескольким параметрам нажмите **Добавить фильтр** и выберите соответствующий критерий, значение и оператор в форме.

Фильтрация по нескольким критериям:

![](/.gitbook/assets/cc-logs.png)

По кнопке **Скачать CSV** сохраняются те строки логов, которые заданы фильтрацией.

<details>

<summary>Список служб, доступных в разделе</summary>

* **Файрвол** - ideco-firewall-backend, ideco-nflog;
* **Контроль приложений** - ideco-app-backend, ideco-app-control@Leth<номер локального интерфейса>;
* **Контент-фильтр** - ideco-content-filter-backend;
* **Ограничение скорости** - ideco-shaper-backend;
* **Объекты** - ideco-alias-backend;
* **Сетевые интерфейсы** - ideco-network-backend, ideco-network-nic;
* **Маршрутизация** - ideco-routing-backend;
* **DNS** - ideco-dns-backend, unbound;
* **DDNS** - ideco-dns-backend;
* **Автоматическое обновление** - ideco-sysupdate-backend;
* **Резервное копирование** - ideco-backup-backend, ideco-backup-create, ideco-backup-rotate;
* **Лицензия** - ideco-license-backend;
* **Syslog** - ideco-monitor-backend.

</details>


Ideco Center логирует действия администраторов, которые вносят изменения в конфигурацию Ideco Center из веб-интерфейса, локального меню и терминала.

![](/.gitbook/assets/cc-admins.png)