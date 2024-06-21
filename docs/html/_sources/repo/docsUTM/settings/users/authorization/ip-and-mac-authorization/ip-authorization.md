# Авторизация по IP-адресу

При авторизации по IP пользователь получит доступ до интернет-ресурсов после инициации подключения. Без ввода логина и пароля.

Также можно авторизовать сетевые устройства (камеры видеонаблюдения, сетевые принтеры и прочее), которые находятся в разных с Ideco NGFW широковещательных доменах и требуют доступ в интернет.

Если устройством является маршрутизатор и в нем включен SNAT, то при авторизации его внешнего IP на NGFW все пользователи за этим маршрутизатором получат доступ в интернет.

Пользователи, которые находятся за маршрутизатором в локальной сети NGFW, не могут авторизоваться по связке IP-адрес - MAC-адрес, так как маршрутизатор не обрабатывает трафик уровня L2.

Если настроена авторизация по IP-адресу, то этот IP не будет выдаваться [DHCP](/settings/services/dhcp.md).

## Настройка авторизации по IP

Чтобы авторизовать пользователя по IP-адресу:

1\. [Создайте](/settings/users/user-tree/user-management.md) пользователя в Ideco NGFW или [импортируйте](/settings/users/active-directory/user-import.md) его из Active Directory, который будет авторизован по IP.

2\. Перейдите в раздел **Пользователи -> Учетные записи -> карточка пользователя -> IP и MAC авторизация** или **Пользователи -> Авторизация -> IP и MAC авторизация**. 

3\. Создайте правило-связку **IP-адрес <--> Пользователь**:

![](/.gitbook/assets/ip-authorization.png)

IP-адрес на компьютере/устройстве, с которого инициируется сессия, должен совпадать с указанным в правиле.

Кнопка *Получить MAC по IP* будет активна, если IP пользователя и IP Ideco NGFW в одной подсети.

Для пользователя, которым является сетевое оборудование, рекомендуем настроить **Постоянную авторизацию**. Это позволит NGFW создать сессию, а сетевому оборудованию не потребуется делать запрос в интернет. \
Так же рекомендуем настроить статический IP-адрес или DHCP с привязкой по IP-адресу. Это требуется, например, для ресурсов, [опубликованных через DNAT](/settings/publishing-resources/portmapping.md).

Воспользуйтесь поиском устройств для автоматического создания пользователей при попытке выхода в интернет. Подробнее о настройке читайте в статье [Обнаружение устройств](/settings/users/device-discovery.md).

Если используется авторизация по IP со статической привязкой в DHCP, то рекомендуем перенести такие правила на [авторизацию по MAC-адресу](mac-authorization.md).

## Просмотр сессии

После того как пользователь делает запрос в интернет, на NGFW будет автоматически создана сессия с типом авторизации `IP` в разделе **Мониторинг -> Авторизованные пользователи**:

![](/.gitbook/assets/ip-authorization1.png)

У сессий с типом `IP` не заполняется поле **MAC-адрес**, так как уже указан IP-адрес, необходимый для создания сессии.

Под одним пользователем можно авторизовать только одно устройство по IP-адресу. Но одновременно с данным типом авторизации под одним пользователем можно авторизовать еще четыре устройства любым другим методом авторизации.