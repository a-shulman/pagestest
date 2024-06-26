# VPN-подключения

Название службы раздела **VPN-подключения**: `ideco-accel-l2tp`; `ideco-accel-pptp`; `ideco-accel-sstp`; `ideco-vpn-servers-backend`; `ideco-vpn-authd`.\
Список служб для других разделов доступен по [ссылке](/settings/server-management/terminal.md).

Инструкция по настройке VPN-подключения через [Ideco Client](/settings/users/ideco-client/README.md).

Не рекомендуем использовать для VPN-подключений кириллические логины.

Для получения доступа извне (из дома, отеля, другого офиса) к локальной сети предприятия, которая находится за Ideco NGFW, можно подключиться по VPN с этой машины (компьютера или мобильного устройства) к серверу Ideco NGFW.

Для client-to-site VPN наш сервер поддерживает четыре протокола туннельных соединений: [IKEv2](ipsec-ikev2.md), [SSTP](sstp.md), [L2TP/IPsec](l2tp-ipsec.md), [PPTP](pptp.md).

В целях безопасности не рекомендуется использовать протокол PPTP (он оставлен для совместимости с устаревшими операционными системами и оборудованием, а также для авторизации в локальной сети, где нет требований к строгому шифрованию трафика).

**Рекомендуемым в плане скорости и безопасности является протокол IKEv2.**

Можно использовать [личный кабинет пользователя](/settings/users/user-personal-account.md) для раздачи инструкций по созданию пользовательских VPN-подключений.

## Основное

В поле **Сеть для VPN-подключений** указывается подсеть, в рамках которой будут динамически присваиваться IP-адреса. Маска подсети должна быть в диапазоне от 16 до 30.

### Основные настройки

В основных настройках выберите протоколы, по которым смогут подключаться пользователи. Подробнее о настройках в статьях: [PPTP](pptp.md), [PPPoE](pppoe.md), [IKEv2/IPsec](ipsec-ikev2.md), [SSTP](sstp.md) и [L2TP/IPsec](l2tp-ipsec.md).

Для настройки конфигурации VPN-подключения сразу на несколько сетевых интерфейсов:

1\. Создайте зону и добавьте сетевые интерфейсы для подключения по VPN в эту зону;

2\. Перейдите в раздел **Пользователи -> VPN-подключения -> Основное** и укажите зону, созданную на первом шаге.

![](/.gitbook/assets/vpn1.png)

Используйте зоны для настройки конфигурации VPN-подключения сразу нескольких сетевых интерфейсов.

Не рекомендуем использовать тип подключения PPTP. Этот способ подключения КРАЙНЕ небезопасен, оставлен исключительно для совместимости со старыми решениями. Используйте IPsec-IKEv2.

Инструкции по настройке VPN-подключений на разных ОС доступны по [ссылке](/recipes/popular-recipes/README.md).

### Статусы подключения

Начиная с 16.0 версии Ideco NGFW, у каждого протокола VPN-подключения появился статус использования. Статусы отображаются в виде подсказок под названиями протоколов, когда протокол используется в правилах таблицы **Доступ по VPN**.

Если включена опция рядом с названием протокола в разделе **Пользователи -> VPN-подключения -> Основное** и есть подключение, цвет статуса - зеленый, если протокол выключен - оранжевый.

![](/.gitbook/assets/vpn-connection.png)

### Передача маршрутов

Маршруты, переданные Ideco NGFW для VPN-клиента, имеют меньшую метрику (т. е. высокий приоритет). В меню передача маршрутов существует 5 опций для настройки передачи маршрутов клиентам:

1\. **Не отправлять**. При включении данной опции клиентам не будут передаваться никакие маршруты, то есть никакой трафик не будет проходить через NGFW.

2\. **Отправлять весь трафик на Ideco NGFW**. При включении этой опции клиентам будет передаваться маршрут 0.0.0.0/0, то есть весь трафик будет проходить через NGFW.

3\. **Отправлять маршруты до всех локальных сетей**. При включении опции клиентам будут передаваться маршруты до всех локальных сетей NGFW, в том числе подключенных через IPsec и маршрутизируемых.

4\. **Отправлять маршруты до локальных сетей Ideco NGFW**. При включении опции клиентам будут переданы маршруты только до локальных сетей NGFW, без учета IPsec и маршрутизируемых.

5\. **Отправлять только указанные**. При включении опции предоставляется возможность выбрать, какие маршруты нужно отправлять клиентам.

![](/.gitbook/assets/vpn2.png)

Если маршруты VPN-клиентов пересекаются с маршрутами, передаваемыми Ideco NGFW, то выберите **Не отправлять** или **Отправлять только указанные**.

## Доступ по VPN

Вкладка содержит таблицу правил, которые действуют сверху вниз. Как только в правиле происходит совпадение полей **Источник подключения**, **Пользователи и группы**, **Протокол подключения** производится действие, выбранное при создании правила. В случае указания **Способа 2FA** будет происходить аутентификация по второму фактору. В правилах можно использовать как группы пользователей Ideco NGFW, так и группы безопасности AD.

Для добавления группы безопасности AD для VPN не требуется импорт в дерево пользователей. Введите Ideco NGFW в домен и выберите на вкладке **Доступ по VPN** требуемую группу безопасности.

Для включения доступа по VPN у группы пользователей выполните действия:

1\. Перейдите в раздел **Пользователи -> VPN-подключения -> Доступ по VPN**.

2\. Заполните необходимые поля формы:

![](/.gitbook/assets/vpn3.png)

3\. Нажмите **Сохранить**.

Для работы VPN-подключений по выбранному протоколу настройте Ideco NGFW соответствующим образом в разделе **VPN-подключения -> Основное**.

Для разных групп пользователей можно указать разные типы двухфакторной аутентификации. Для настройки двухфакторной аутентификации воспользуйтесь [статьей](/settings/users/two-factor-authentication.md)

## Правила выдачи IP-адресов

На вкладке доступно создание правил для выдачи IP-адресов пользователям, подключающимся по VPN. NGFW просматривает таблицу правил сверху вниз до первого совпадения пользователя.

Если пользователь не попал под условия правил, ему выдается свободный IP-адрес из сети для VPN-подключений. При этом из нее исключаются все подсети и одиночные адреса, указанные во всех правилах таблицы и использующиеся в текущих сессиях. Если ни одного адреса не осталось, соединение разрывается

Чтобы создать правило, нажмите **Добавить** и заполните следующие поля:

![](/.gitbook/assets/vpn-authorization.png)

* **Название** - введите название правила;
* **Пользователи и группы** - выберите пользователей или группы пользователей, на которых будет распространяться правило;
* **Выдаваемые адреса** - введите IP-адрес или подсеть;
* **Комментарий** - поле может быть пустым.

**Важно:**

* Подсеть, указанная в правиле, должна полностью входить в сеть для VPN-подключений. В противном случае правило считается невалидным, адрес выдать невозможно, соединение разрывается.
* В двух разных правилах нельзя указать одну и ту же сеть.
* Если в разных правилах указаны пересекающиеся сети (например, cеть `10.128.1.0/24` является подсетью cети `10.128.0.0/20`), то: 
    * адреса из cети `10.128.1.0/24` никогда не будут выдаваться; 
    * при выдаче адресов сети `10.128.0.0/20` из нее будут исключаться адреса подcети `10.128.1.0/24`.
* Если указать в правилах сеть, совпадающую с сетью для VPN-подключений, то все пользователи VPN, для которых не совпадет ни одно правило таблицы, не смогут получить адрес и подключиться.
* Количество одновременных VPN подключений от одного пользоавтеля в том числе будет ограничиваться размером сети, указанной для него в правилах.
* Если в правиле указан один IP-адрес и он уже используется в текущей сессии, то указанный в правиле пользователь не сможет установить второе VPN-подключение - оно не сможет получить адрес;
* Если в правиле указана сеть с префиксом /30 (или маской 255.255.255.252) и более широкие сети (например, `10.128.2.0/24`), то при выдаче адреса из таких сетей адрес самой сети и широковещательный адрес (`10.128.2.0` и `10.128.2.255`) использоваться не будут. 

Чтобы отключить правило, нажмите на ![](/.gitbook/assets/icon-on.png) в столбце управления. Чтобы удалить правило, нажмите ![](/.gitbook/assets/icon-delete1.png).