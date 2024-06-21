---
description: >-
  Используется для маршрутизации сетевого трафика, проходящего через Ideco NGFW.
---

# Маршрутизация

Название службы раздела **Маршрутизация**: `ideco-routing-backend`. \
Список служб для других разделов доступен по [ссылке](/settings/server-management/terminal.md).

Преимущества маршрутизации Ideco NGFW:

* Возможность указывать сеть источника при маршрутизации внешних сетей;
* Функция адаптивности (в случае недоступности шлюза или интерфейса поиск маршрута продолжится по следующим правилам в таблице маршрутизации).

Доступность шлюза проверяется с помощью ICMP-запросов к набору IP-адресов, который определяется производителем сетевой карты.

В веб-интерфейсе Ideco NGFW есть возможность маршрутизировать локальные и внешние сети. Создавать и редактировать маршруты можно в разделе **Сервисы -> Маршрутизация**.

Для организации доступа в удаленные сети через роутер в локальной сети читайте статью по [ссылке](/settings/users/authorization/vpn-connection/features.md).

При маршрутизации локальных и внешних сетей доступны GRE-интерфейсы в качестве шлюза.


## Маршрутизация локальных сетей

Маршрутизация локальных сетей действует внутри локальных сетей. Поэтому при добавлении маршрута отсутствует поле **Адрес источника**. Для добавления нового маршрута перейдите на вкладку маршрутизации **Локальных сетей** и нажмите **Добавить**:

![](/.gitbook/assets/routing5.png)

* **Адрес назначения** - выберите объекты, при обращении к которым будет применяться это правило. Возможные типы объектов: IP-адрес, подсеть;
* **Шлюз** - выберите объект, через который направляется трафик. Возможный тип объекта: IP-адрес
* **Комментарий** - необязательное поле для описания маршрута. Значение - не длиннее 128 символов.

При создании IPSec-подключения в разделе **Сервисы -> IPsec** с включенной опцией **Автоматическое создание маршрутов** будут добавляться маршруты до локальных сетей NGFW в таблицу **Маршрутизации локальных сетей**.

## Маршрутизация внешних сетей



Для добавления нового маршрута перейдите на вкладку маршрутизации **Внешних сетей** и нажмите кнопку **Добавить**. На странице откроется форма создания маршрута:

![](/.gitbook/assets/routing6.png)

Опишем назначение каждой опции:

* **Адрес источника** - выберите объекты, для которых будет применяться правило. Возможные типы объектов: группы, пользователи, IP-адрес, домен, диапазон IP-адресов, подсеть, список адресов;
* **Адрес назначения** - выберите объекты, при обращении к которым будет применяться правило. Возможные типы объектов: группы, пользователи, IP-адрес, домен, диапазон IP-адресов, подсеть, список адресов;
* **Шлюз** - выберите объект, через который будет направлен трафик. Возможный тип объекта: сетевой интерфейс, IP-адрес;
* **Использовать только если шлюз доступен (адаптивность)** - если свойство включено, то при недоступности шлюза или интерфейса поиск маршрута продолжится по следующим правилам маршрутизации, а если свойство отключено (по умолчанию), то трафик отправляется в выбранный шлюз или интерфейс. Если шлюз недоступен или интерфейс не работает, то трафик будет отброшен (destination unreachable);
* **Комментарий** - необязательное поле для описания маршрута. Значение не должно быть длиннее 128 символов.

После сохранения маршрута страница выглядит так:

![](/.gitbook/assets/routing7.png)

Кнопки ![](/.gitbook/assets/icon-arrow-down.png) и ![](/.gitbook/assets/icon-arrow-up.png) повышают или понижают приоритет правила.

Статусы в столбце **Используется**:

* ![icon-marked-circle.png](/.gitbook/assets/icon-marked-circle.png) - маршрут активен и трафик, попадающий под условия маршрута, будет перенаправлен в указанный Шлюз;
* ![icon-minus.png](/.gitbook/assets/icon-minus.png) - маршрут не активен и трафик, попадающий под условия маршрута, не будет обработан правилом.

Трафик, не попавший под условия правил маршрутизации, или с объектом **Любой** в качестве шлюза, будет отправлен в [Балансировку и резервирование](multiple-simultaneous-connections.md).

#### Примеры популярных маршрутов

При маршрутизации трафика через подключения к провайдеру важно понимать, что чаще всего одного маршрута недостаточно, понадобится также переопределить адрес с помощью SNAT, иначе такой маршрут просто не будет работать. SNAT можно настроить с помощью [файрвола](/settings/access-rules/firewall.md).

<details>

<summary>Задача: любой трафик в подсеть `150.1.0.0/16` направлять на шлюз `67.12.8.9`</summary>

<img src="/.gitbook/assets/routing8.png" alt="" data-size="original">

</details>

<details>

<summary>Задача: весь трафик пользователей из группы Бухгалтерия направить через шлюз выбранного сетевого интерфейса</summary>

<img src="/.gitbook/assets/routing9.png" alt="" data-size="original">

Если настраивается маршрут в удаленную сеть через дополнительный роутер, расположенный в одной локальной сети с клиентами, то убедитесь, что нет "асимметричной маршрутизации" и роутер вынесен в DMZ. Подробнее в статье [Доступ в удаленные сети через роутер в локальной сети](/recipes/popular-recipes/access-to-remote-networks.md)

</details>

<details>

<summary>Задача: Предоставить доступ в интернет пользователям NGFW1, подключенного по IPsec к NGFW2, через внешний интерфейс NGFW2</summary>

Для доступа в интернет пользователям NGFW1 укажите в качестве шлюза IPsec-подключение к NGFW2:

![](/.gitbook/assets/routing1.png)


</details>