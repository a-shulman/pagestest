# Антиспам

Раздел **Антиспам** состоит из двух подразделов: **Основное** и **Настройки фильтрации**.

## Основное

Позволяет управлять работой службы антиспама на основе технологий Лаборатории Касперского с функцией машинного обучения и искусственного интеллекта. Также на этой вкладке предоставлена возможность добавления лицензионного ключа антиспама. Ключ поставляется в файле, имеющем расширение `.key`. 

Если приобретена лицензия на антиспам, но нет в распоряжении лицензионного ключа, проверьте переписку с отделом продаж нашей компании (sales@ideco.ru) на наличие вложений. Если не удалось найти таких вложений, запросите ключ заново, выслав письмо на sales@ideco.ru с указанием наименования организации или номера лицензии.

Перед загрузкой ключа обязательно включите модуль антиспама.

![](/.gitbook/assets/antispam1.png)


## Настройки фильтрации

* **Сортировка спама.** Задание логики сортировки нежелательной корреспонденции (спама). На выбор предоставляются следующие опции: отключение сортировки, перемещение нежелательных отправлений в папку Spam, удаление таких писем с сервера;
* **Почтовый ящик для спама.** Весь входящий спам будет пересылаться на указанный ящик (не используйте ящик Spam);
* **Ящики, исключенные из сортировки спама.** Позволяет задать почтовые адреса, которые не будут проверяться на спам.

![](/.gitbook/assets/antispam.png)

### Веб-интерфейс для Антиспама

Для включения веб-интерфейса Антиспама требуется, чтобы сам модуль **Антиспам** был включен.

Веб-интерфейс имеет следующие преимущества:

* Отображает статистику по категориям Антиспама Касперского в удобном и понятном виде;
* Генерирует отчеты по работе за определенный период;
* Отображает очередь обрабатываемых сообщений;
* Позволяет задавать правила *Запрещенных и Разрешенных адресов*;
* Ведет аудит всех действий, производимых с Антиспамом.

Чтобы включить веб-интерфейс для Антиспама:

1\. Перейдите в раздел **Управление сервером -> Терминал** и выполните следующую команду `/opt/kaspersky/klms/bin/klms-control --set-web-admin-password`

2\. Задайте пароль для стандартного аккаунта **Administrator**, состоящий минимум из 8 символов:

* Строчных букв;
* Заглавных букв;
* Специальных символов;
* Чисел.

![](/.gitbook/assets/antispam2.png)

3\. Для доступа к веб-интерфейсу перейдите в адресной строке по пути `utm_ip_address:8443/klms/`:

![](/.gitbook/assets/antispam3.png)

4\. Войдите в веб-интерфейс с учетной записью **Administrator** и ранее заданным в терминале паролем:

![](/.gitbook/assets/antispam4.png)

После успешного входа будет отображен дашборд со статистикой работы Антиспама:

![](/.gitbook/assets/antispam5.png)

### Включение Антивируса почтового сервера

1\. Перейдите в веб-интерфейс Антиспама. Подробные шаги настройки и входа в веб-интерфейс описаны в статье [Веб-интерфейс для Антиспама](antispam.md#veb-interfeis-dlya-antispama);

2\. Включите антивирус почтового сервера, перейдите в раздел **Settings -> Protection** и активируйте опцию **Anti-Virus**:

![](/.gitbook/assets/antispam6.png)

Не рекомендуем вносить какие-либо изменения в разделе `Settings`, кроме указанных выше, потому как не можем гарантировать функциональность работы Антиспама в таких случаях.
