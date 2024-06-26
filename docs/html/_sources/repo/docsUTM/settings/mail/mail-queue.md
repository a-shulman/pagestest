---
description: Позволяет управлять очередью почтовых отправлений, которые по каким-либо причинам не могут быть прямо сейчас отправлены или получены.
---
# Почтовая очередь

Модуль позволяет управлять входящей и исходящей отложенной корреспонденцией. Для анализа возможных причин задержки корреспонденции в очереди можно использовать информацию из соответствующего столбца таблицы для каждого письма. 

Почтовая очередь позволяет выполнять следующие выборочные и групповые действия с отправлениями:

* Очистка очереди
* Повторная отправка отдельного письма
* Удаление отдельных писем из очереди
* Повторная отправка всей корреспонденции из очереди

Значение в столбце **Время доставки** соответствует времени поступления письма в очередь. Если письмо не будет отправлено в течение 7 дней, то оно будет удалено из почтовой очереди и не будет доставлено получателю.

При обновлении Ideco NGFW почтовая очередь очищается.

## Проверка настроек почтового сервера

Рекомендуется проверить корректность всех настроек DNS и почтового сервера с помощью сервиса [mail-tester.com](https://www.mail-tester.com).

При правильной настройке почтовый сервер на Ideco NGFW должен получить 10 баллов из 10.
