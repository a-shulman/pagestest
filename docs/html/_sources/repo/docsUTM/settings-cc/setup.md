# Установка Ideco Center

**Технические требования для серверов и виртуальных машин:**

|Комплектующие|Минимальные системные требования|
|-------------|--------------------------------|
|Процессор|Intel i3/i5/i7/i9/Xeon с поддержкой SSE 4.2|
|Объем оперативной памяти|16 ГБ (16-64 ГБ в зависимости от количества пользователей)|
|Дисковая подсистема|SSD объемом 150 Гб или больше, с интерфейсом SATA, mSATA, SAS, NVMe.|
|Сеть|Одна сетевая карта. Рекомендуется использовать карты на чипах Intel. Поддерживаются Realtek, D-Link и другие.|
|Гипервизоры|VMware, Microsoft Hyper-V (2-го поколения), VirtualBox, KVM, Citrix XenServer.|
|Дополнительно|Монитор и клавиатура|
|Замечания|Обязательна поддержка UEFI. Не поддерживаются программные RAID-контроллеры (интегрированные в чипсет). Для виртуальных машин необходимо использовать фиксированный, а не динамический размер хранилища и оперативной памяти.|

Файл для установки центральной консоли доступен для скачивания в [личном кабинете](https://my.ideco.ru/#/utm/download). Процесс установки Ideco Center аналогичен [процессу установки Ideco NGFW](/installation/installation-process.md).

## Процесс установки

При установке Ideco Center с загрузочного USB диска выберите загрузку с USB диска в настройках UEFI компьютера.

Для установки Ideco Center выполните действия:

1\. Перейдите к установке, нажав **Install Ideco CC**.

![](/.gitbook/assets/setup1-cc.png)

2\. Выберите диск для установки и ознакомьтесь с **предупреждением об уничтожении данных на диске**:

![](/.gitbook/assets/setup2-cc.png)

3\. Выберите временную зону, в которой вы находитесь:

![](/.gitbook/assets/installation-process2.png)

4\. Настройте дату и время в соответствии с вашей временной зоной. **Обязательно проверьте правильность даты и времени**:

![](/.gitbook/assets/installation-process3.png)

Не забудьте извлечь USB диск после установки Ideco Center, чтобы загрузка с USB диска не началась заново.

## Создание учетной записи администратора

Для входа в веб-интерфейс Ideco CC нужно создать учетную запись администратора с соблюдением требований к паролю:

![](/.gitbook/assets/installation-process4.png)

<details>
<summary>Требования к паролю</summary>

* **Минимальная длина пароля** - 12 символов;
* **Содержит только строчные и заглавные латинские буквы**;
* **Содержит цифры**;
* **Содержит специальные символы** (! # $ % & ' * + и другие).
</details>

Если пароль не соответствует требованиям политики безопасности, то появится надпись с информацией, что пароль ненадежен. Потребуется ввести новый пароль с учетом требований к паролю.

## Настройка локального интерфейса

При использовании сетевых карт одного производителя могут возникнуть трудности при идентификации сетевой карты для настройки сетевого интерфейса.
Для корректной идентификации сетевой карты используйте ее MAC-адрес.

Для настройки Ideco Center через веб-интерфейс нужно настроить локальный интерфейс в локальном меню:

1\. Введите номер сетевого адаптера под локальный интерфейс:

![](/.gitbook/assets/installation-process7.png)

2\. Настройте локальную сеть автоматически через DHCP введя **y** или настройте вручную, введя **n**:

![](/.gitbook/assets/installation-process8.png)

3\. Введите локальный IP-адрес и маску подсети в формате `ip/маска` и нажмите **Enter**:

![](/.gitbook/assets/installation-process5.png)

4\. Введите адрес шлюза или оставьте поле пустым:

![](/.gitbook/assets/installation-process9.png)

5\. Задайте тег VLAN (стандарт VLAN 802.3q) или оставьте поле пустым:

![](/.gitbook/assets/installation-process11.png)

После создания локального интерфейса откроется локальное меню управления: 

![](/.gitbook/assets/installation-process12.png)