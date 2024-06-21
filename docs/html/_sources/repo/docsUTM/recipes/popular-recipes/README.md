# FAQ

## Как заблокировать чат-боты?

Заблокировать чат-боты можно, создав правило в Контент-фильтре. О том, как это сделать, написано в статье [Блокировка чат-ботов](/recipes/popular-recipes/block-chat-bot.md).

## Как настроить совместную работу ViPNet-Координатора c Ideco NGFW ?

Процесс настройки подробно описан в [статье](/recipes/popular-recipes/vipnet-coordinator.md).

## Как настроить автоматическую аутентификацию на Linux через веб-интерфейс ?

Процесс настройки подробно описан в статье [Настройка автоматической аутентификации на NGFW на Linux](/recipes/popular-recipes/auto-authorization-linux.md). Данный скрипт подходит для всех Linux-систем c Python 3.5 и выше.

## Есть ли возможность добавлять сигнатуры IPS?

Да, добавьте сигнатуру вручную в файл `/var/opt/ideco/suricata-backend/custom.rules`. Важно: sid правила не должен совпадать с существующими. \
Подробнее о добавлении в статье [Как исключить узел из обработки системой IDS/IPS через терминал](/settings/access-rules/ips/README.md#kak-isklyuchit-uzel-iz-obrabotki-sistemoi-ids-ips-cherez-terminal).

## Как настроить кластеризацию Active/Active?

Для настройки кластеризации Active/Active воспользуйтесь решением наших партнеров АО "НПП "Цифровые решения". Инструкция по интеграции Ideco NGFW и брокера сетевых пакетов DS Integrity NG - по [ссылке](/recipes/popular-recipes/integrity.md).

## Какими модулями и в каком порядке обрабатывается веб-трафик в Ideco NGFW?

Порядок обработки веб-трафика и примеры проверки работоспособности модулей описаны в [статье](processing-order.md).

## Хочу работать из дома, подключившись по RDP к своем компьютеру в офисе. Можно ли опубликовать RDP, чтобы он был доступен из интернета?

Не рекомендуем так делать. В такой ситуации существуют риски успешного взлома с помощью RDP. Даже сложный пароль и актуальные обновления не гарантируют того, что злоумышленники не смогут проникнуть внутрь сети через опубликованный RDP. Не рекомендуем публиковать RDP и подобные сервисы “наружу” (SSH, FTP и т.д.), так как это увеличивает количество потенциальных точек входа для злоумышленников. Рекомендуем использовать подключение по VPN к своей сети.

## Как создать VPN-подключение?

В зависимости от операционной системы выберите подходящую инструкцию из [Инструкций по созданию VPN-подключений](vpn/README.md).

## Что делать, если сети за роутером, находящимся после NGFW, не доступны по VPN?

Для решения вопроса воспользуйтесь статьей [Доступ в удаленные сети через роутер в локальной сети](access-to-remote-networks.md).

## Что делать, если ваш IP попал в черные списки DNSBL?

Если вы используете белый статический IP-адрес, то попадание IP-адреса в черные списки может означать, что в сети зафиксирована бот-активность, участие в DDoS-атаках, либо рассылка спама.

Наличие в черных списках динамического IP-адреса из "домашних" диапазонов IP-адресов провайдеров в целом нормальное явление, т. к. вредоносная активность в таком случае может исходить не из вашей сети. \
Порядок действий при попадании в черный список описан в [статье](dnsbl-list.md).

## Утрачен пароль администратора, как его восстановить?

При утере пароля администратора можно его восстановить, имея физический доступ к серверу. Подробнее о процессе восстановления в статье [Как восстановить доступ к Ideco NGFW](restore-access-to-ideco-utm.md).

## После обновления потребовалось вернуть предыдущую версию со всеми настройками. Как это сделать?

Возможность восстановиться на предыдущую версию после обновления Ideco NGFW доступна с 12.Х версий. Подробнее о процессе восстановления в статье [Как восстановиться на прошлую версию после обновления Ideco NGFW](go-back.md).

## Как понять, что контент-фильтр настроен эффективно?

Эффективность настроек контент-фильтра вы можете проверить с помощью сервиса security.ideco.ru. При правильной настройке общий уровень защиты должен показывать "зеленый" цвет. Если это не так, проверьте с помощью [статьи](security-ideco.md) настройки контент-фильтра и других служб фильтрации трафика.  

## Как подобрать аппаратную платформу для Ideco NGFW?

Ideco NGFW представляет собой операционную систему, устанавливаемую на сервер или виртуальную машину. Ideco NGFW основан на Fedora 39 и содержит ядро Linux с набором драйверов от этой ОС с небольшими изменениями с нашей стороны. Таким образом, Ideco NGFW можно установить на большую часть оборудования, поддерживающего Fedora 39. Подробнее в статье [Выбор аппаратной платформы для Ideco NGFW](choosing-hardware-platform.md).

## Есть необходимость использовать устаревшие алгоритмы шифрования. Как настроить Ideco NGFW?

Для настройки Ideco NGFW воспользуйтесь рекомендациями из статьи [Поддержка устаревших алгоритмов шифрования](legacy-encryption-support.md).

## Как настроить прямое подключение к прокси-серверу, если ПО его не поддерживает?

При использовании прямых подключений к прокси-серверу выход в интернет будет поддерживаться всеми программами, имеющими настройки прокси-сервера, либо программами, применяющими системные настройки прокси.

Некоторое ПО не имеет настроек прокси-сервера, поэтому необходимо использовать специализированное ПО на конечных рабочих станциях для вывода в интернет таких программ. Одно из таких ПО - Proxifier.

Инструкция по настройке программы Proxifier для прямых подключений к прокси-серверу доступна по [ссылке](configuring-proxifier.md).

## Как эффективно заблокировать Ammyy Admin, Анонимайзеры, BitTorrent и т. д.?

Примеры блокировки программ удаленного доступа, анонимайзеров, торрентов и др. описаны в статье [Блокировка популярных ресурсов](blocking-popular-resources.md). 

## Как настроить SSO-авторизацию для Astra Linux в домене AD?

Описание процесса настройки можно найти в статье [Настройка прозрачной авторизации на Astra linux](authorization-astra-linux.md). Это решение подходит для браузеров Chromium и Firefox.

## Как перенести данные и настройки с одного сервера на другой?

Чтобы перенести установленный Ideco NGFW с одного сервера на другой с сохранением всех настроек, следуйте [инструкции](transferring-data-to-another-server.md).