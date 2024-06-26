---
description: >-
  Используется для прозрачного проксирования веб-трафика потребителям в
  локальной сети.
---

# Прокси

Название службы раздела **Прокси**: `ideco-proxy-backend`; `squid`. \
Список служб для других разделов доступен по [ссылке](/settings/server-management/terminal.md).

Прокси-сервер, помимо проксирования веб-трафика, используется для передачи трафика следующим сервисам:

* Антивирус для веб-трафика (Антивирус Касперского или ClamAV);
* Сервис отчетности по веб-трафику пользователей;
* Контент-фильтр. 

Порядок обработки веб-трафика подробнее описан в [статье](/recipes/popular-recipes/processing-order.md).

Не указывайте на хостах локальной сети настройки прокси. Достаточно указания NGFW в качестве шлюза по умолчанию для устройств в сети.

Для настройки фильтрации HTTPS-трафика нужно добавить корневой сертификат NGFW на компьютеры пользователей. Подробнее в статье [Настройка фильтрации HTTPS](/settings/access-rules/content-filter/filtering-https-traffic.md).

![](/.gitbook/assets/proxy-server1.png)

## Основное

На вкладке **Основное** предоставлены возможности:
 
* **Разрешить прямые подключения к прокси** \
Этот режим применяется, когда Ideco NGFW не является шлюзом по умолчанию для клиентов сети. \
Порт, указанный на стороне NGFW, следует указать на сетевых устройствах локальной сети, веб-трафик которых нужно пропускать через прокси.
* **Включить журналирование** \
Включает запись логов Контент-фильтра и Антивирусов веб-трафика.\
  ![](/.gitbook/assets/proxy2.png)

О настройке прямого подключения к прокси и прокси с одним интерфейсом читайте в [статье](/settings/services/proxy/proxy-single-interface.md).

## ICAP

Протокол ICAP используется для отправки HTTP(S)-трафика в расшифрованном виде сторонним серверам. ICAP-сервисы будут обрабатывать трафик после антивирусов и контент-фильтра.

При добавлении ICAP-сервиса доступны следующие настройки:

* **Игнорировать ошибки** - если включена эта опция, то сервис будет считаться необязательным. При недоступности или неправильной работе сервиса он не будет задействован.
* **Задать количество подключений к сервису вручную** - если значение не задано, максимальное количество подключений берется из ответа сервиса на запрос OPTIONS. Если максимальное количество подключений не указано в ответе на запрос OPTIONS, тогда - без ограничений.

Если указать в опции **Задать количество подключений к сервису вручную** значение меньше четырех, то клиентские подключения могут быть нестабильными.

![](/.gitbook/assets/proxy3.png)

Для корректной работы ICAP-сервиса должна быть настроена расшифровка HTTPS-трафика в **Контент-фильтре**.


## WCCP

Протокол WCCP используется для перенаправления трафика на Ideco NGFW. 

По умолчанию перенаправляется только HTTP/HTTPS-трафик.

Для активации WCCP переведите опцию **Включить перенаправление трафика c WCCP-серверов на Ideco NGFW** в положение **Включен**. Ideco NGFW запустит процесс согласования параметров с WCCP-сервером.

В NGFW предусмотрено два режима работы WCCP - L2 и GRE. Для выбора режима раскройте блок **Настройки**. \
Если на WCCP-сервере задан пароль, сохраните его в соответствующем поле:

![](/.gitbook/assets/proxy4.png)

Если роутер использует несколько Ideco NGFW, настройте распределение трафика с помощью указания приоритета в поле **Вес**. Допустимые значения - от 1 до 10000.

Для добавления WCCP-сервера нажмите кнопку **Добавить** и укажите IP-адрес сервера:

![](/.gitbook/assets/proxy5.png)

<details>

<summary> L2 </summary>

Режим L2 используется, если роутер и Ideco NGFW находятся в одном сетевом сегменте.

![](/.gitbook/assets/proxy-server2.png)

Последовательность обработки веб-запросов на уровне L2:
* Пользователь отправляет веб-запрос;
* Запрос перенаправляется роутером на Ideco NGFW;
* Ideco NGFW обрабатывает запрос; 
* Если запрос заблокирован, информация о блокировке отправляется обратно пользователю;
* Если запрос не заблокирован, то Ideco NGFW подменяет IP-адрес источника и направляет запрос на внешний сервер. 

Ответ возвращается обратно по тому же пути, по которому уходил на внешний сервер.

</details>

<details>

<summary> GRE </summary>

Режим GRE используется, если роутер и Ideco NGFW находятся в разных сетевых сегментах.

![](/.gitbook/assets/proxy-server3.png)

Последовательность обработки веб-запросов на уровне GRE:

* Пользователь отправляет веб-запрос;
* Запрос перенаправляется по GRE-туннелю на Ideco NGFW;
* Ideco NGFW обрабатывает запрос.
* Если запрос заблокирован, то информация о блокировке отправляется обратно пользователю.
* Если запрос не заблокирован, то Ideco NGFW подменяет IP-адрес источника и направляет запрос на внешний сервер. 

Ответ возвращается напрямую от Ideco NGFW пользователю, минуя GRE-туннель.

</details>

## WCCP Service ID

Service ID - идентификаторы сервисной группы. Настройки на этой вкладке позволяют выбрать службы, трафик которых маршрутизатор WCCP будет перенаправлять на Ideco NGFW. 

По умолчанию настроены сервисы для HTTP/HTTPS-трафика:

![](/.gitbook/assets/proxy6.png)

Service ID с 0 по 50 зарезервированы под фиксированные сервисы. Для них выбирать порты и протоколы нельзя.

Service ID 70 - общепринятое значение для HTTPS-трафика на 443 TCP-порт.

Чтобы настроить Service ID, выполните действия:

1\. На вкладке **WCCP Service ID** нажмите кнопку **Добавить**.

2\. В открывшейся форме укажите следующие значения:

  ![](/.gitbook/assets/proxy7.png)

  * Service ID - идентификатор сервисной группы, трафик которой планируется перенаправлять на прокси-сервер. Выбирайте значения от 51 до 255, чтобы избежать проблем со старыми маршрутизаторами WCCP.
  * Порты - укажите порты назначения. Максимум 8 значений.
  * Протокол - укажите протокол для перенаправляемого трафика (TCP, UDP).
  * Приоритет - укажите приоритет Service ID от 0 до 255. Чем больше число, тем выше приоритет.

Service ID должен должен соответствовать идентификатору группы, определенному на маршрутизаторе WCCP.

3\. Нажмите **Сохранить**. Созданный Service ID появится в таблице:

  ![](/.gitbook/assets/proxy8.png)

## Исключения

Исключения ресурсов из обработки прокси-сервером работают только для прозрачного режима прокси. При прямых подключениях к прокси-серверу исключить что-либо из обработки прокси нельзя.

Подробнее о типах исключений в статье [Исключения](/settings/services/proxy/exclusions.md).
