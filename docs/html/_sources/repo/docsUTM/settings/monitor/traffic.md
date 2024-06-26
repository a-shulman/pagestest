---
description: >-
  В разделе Мониторинг -> Монитор трафика можно просматривать данные о
  трафике (вх./исх. скорость, количество сессий), проходящем через Ideco NGFW в
  режиме реального времени.
---

# Монитор трафика

Для включения мониторинга трафика необходимо запустить модуль [Контроля приложений](/settings/access-rules/application-control.md).

## По узлам локальной сети

Вкладка **По узлам локальной сети** позволяет отслеживать активность пользователей сети и выявлять тех, кто нагружает канал трафиком.

![](/.gitbook/assets/monitor-traffic.png)

Для просмотра информации об активности определенного узла локальной сети нажмите на количество сессий в таблице:

![](/.gitbook/assets/monitor-traffic1.png)

## По приложениям

Вкладка **По приложениям** позволяет отслеживать активность приложений.

Например, если пользователь не загружает канал трафиком, но в таблице **По узлам локальной сети** присутствует большое количество пакетов данных, то на вкладке **По приложениям** можно выявить приложение с подозрительной активностью.

![](/.gitbook/assets/monitor-traffic2.png)

Для просмотра подробной информации об активности определенного приложения нажмите на количество сессий в таблице:

![](/.gitbook/assets/monitor-traffic3.png)