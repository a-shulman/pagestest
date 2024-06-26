# Подключение Ideco NGFW и MikroTik

При объединении сетей с помощью VPN локальные сети в разных офисах не должны пересекаться.

Для корректной работы подключений по сертификатам синхронизируйте время на MikroTik по NTP (например, предоставьте доступ в интернет).

Исходящие IPsec-подключения по сертификатам к MikroTik ниже версии 6.45 не работают из-за невозможности использования современных криптоалгоритмов.

## Подключение в Туннельном режиме

**При использовании** [**нашего конфигуратора скриптов настроек MikroTik**](https://mikrotik.ideco.ru) **есть несколько особенностей:**

* При подключении нескольких устройств MikroTik к одному Ideco NGFW по PSK нужно указывать разные **Идентификаторы ключа (Key id)** для каждого устройства;
* При подключении нескольких устройств MikroTik к одному Ideco NGFW по сертификатам нужно указывать разные **Имена сервера** (Common Name) для каждого устройства:

![](/.gitbook/assets/site-to-site-ideco-mikrotik.png)

### Подключение от Ideco NGFW к MikroTik

#### Тип аутентификации PSK

<details>

<summary>Настройка Ideco NGFW</summary>

1\. Откройте вкладку **Сервисы -> IPsec -> Исходящие подключения**, нажмите **Добавить** и заполните поля:

  * **Название подключения** - укажите произвольное имя для подключения. Значение не должно быть длиннее 42 символов;
  * **Зона** - укажите зону для добавления IPSec-подключения;
  * **Адрес удаленного устройства** - укажите внешний IP-адрес устройства MikroTik;
  * **IP-адрес интерфейса туннеля** - укажите IP-адрес интерфейса туннеля. Поле необязательное, заполняется при настройке BGP-соседства для динамической маршрутизации и для получения статистики обмена пакетами;
  * **Удаленный IP-адрес туннеля** - укажите IP-адрес интерфейса туннеля удаленной стороны. Поле необязательное. Для получения статистики о потере пакетов, средней задержке и джиттере заполните поля **IP-адрес интрефейса туннеля** и **Удаленный IP-адрес туннеля**. Они должны находиться в одной подсети.
  * **PSK** - будет сгенерирован случайный PSK-ключ. Он потребуется для настройки подключения в MikroTik;
  * **NGFW идентификатор** - введенный ключ будет использоваться для идентификации исходящего подключения;
  * **Домашние локальные сети** - перечислите все **локальные сети NGFW**, которые будут видны противоположной стороне;
  * **Удаленные локальные сети** - перечислите все **локальные сети MikroTik**, которые будут видны противоположной стороне:

  ![](/.gitbook/assets/ipsec14.png)

2\. После заполнения всех полей нажмите **Добавить подключение**. В списке подключений появится созданное подключение:

  ![](/.gitbook/assets/ipsec15.png)

</details>

<details>

<summary>Настройка Mikrotik</summary>

Настройку устройства MikroTik можно осуществить несколькими способами:

* GUI;
* Консоль устройства;
* Конфигурационными скриптами ([https://mikrotik.ideco.ru/](https://mikrotik.ideco.ru)).

После генерации скрипта необходимо открыть раздел **System -> Scripts**, создать скрипт, вставить в него код, сгенерированный конфигуратором, и запустить.

</details>

#### Тип аутентификации Сертификат

Подключение по сертификатам является более безопасным по сравнению с PSK.

<details>

<summary>Настройка Ideco NGFW</summary>

Сгенерируйте запрос на подпись сертификата:

1\. В Ideco NGFW откройте вкладку **Сервисы -> IPsec -> Исходящие подключения**, нажмите **Добавить** и заполните поля:

  * **Название подключения** - укажите произвольное имя для подключения. Значение не должно быть длиннее 42 символов;
  * **Зона** - укажите зону для добавления IPsec-подключения;
  * **Адрес удаленного устройства** - укажите внешний IP-адрес MikroTik;
  * **IP-адрес интерфейса туннеля** - укажите IP-адрес интерфейса туннеля. Поле необязательное, заполняется при настройке BGP-соседства для динамической маршрутизации и для получения статистики обмена пакетами;
  * **Удаленный IP-адрес туннеля** - укажите IP-адрес интерфейса туннеля удаленной стороны. Поле необязательное. Для получения статистики о потере пакетов, средней задержке и джиттере заполните поля **IP-адрес интрефейса туннеля** и **Удаленный IP-адрес туннеля**. Они должны находиться в одной подсети.
  * **Домашние локальные сети** - перечислите все **локальные сети NGFW**, которые будут видны противоположной стороне;
  * **Удаленные локальные сети** - перечислите все **локальные сети MikroTik**, которые будут видны противоположной стороне;
  * **Запрос на подпись сертификата** - будет сгенерирован **запрос, который необходимо выслать для подписи на MikroTik**:

  ![](/.gitbook/assets/ipsec16.png)

2\. После подписания запроса необходимо продолжить настройку подключения в Ideco NGFW.

**Не закрывайте вкладку с настройками!** При закрытии вкладки с настройками _Запрос на подпись сертификата_ изменит значение и процесс подписания файла NGFW.csr потребуется повторить.

</details>

<details>

<summary>Настройка MikroTik</summary>

На этом этапе следует настроить MikroTik, чтобы продолжить настройку NGFW.

Файл **UTM.csr**, полученный из Ideco NGFW, необходимо загрузить в файловое хранилище MikroTik:

1\. Откройте раздел **File**.

2\. Нажмите кнопку **Browse**.

3\. Выберите файл и загрузите его.

Настроить MikroTik можно:

* Через GUI;
* Через консоль устройства;
* Через конфигурационные скрипты, сгенерированные по адресу [https://mikrotik.ideco.ru/](https://mikrotik.ideco.ru).

После генерации скрипта откройте раздел **System -> Scripts**, создайте скрипт и вставьте в него код, сгенерированный конфигуратором, затем запустите.

В файловой системе MikroTik появятся два файла, которые необходимо скачать, чтобы впоследствии загрузить на NGFW:

![](/.gitbook/assets/site-to-site-ideco-mikrotik3.png)

Файл вида `cert_export_device_<случайный набор символов>.ipsec.crt` - **это подписанный сертификат NGFW**.\
Файл вида `cert_export_mk_ca.crt` - **это корневой сертификат MikroTik.**

</details>

<details>

<summary>Завершение настройки Ideco NGFW</summary>

1\. Перейдите обратно на Ideco NGFW во вкладку с настройками подключения устройства и продолжите заполнять поля:

  * **Подписанный сертификат NGFW** - загрузите подписанный в MikroTik сертификат NGFW;
  * **Корневой сертификат удаленного устройства** - загрузите корневой сертификат MikroTik:

  ![](/.gitbook/assets/ipsec17.png)

2\. Нажмите кнопку **Добавить подключение**.

</details>

### Подключение от MikroTik к Ideco NGFW

#### Тип аутентификации PSK

<details>

<summary>Настройка MikroTik</summary>

Настроить устройство MikroTik можно:

* Через GUI;
* Через консоль устройства;
* Через конфигурационные скрипты, сгенерированные по адресу [https://mikrotik.ideco.ru/](https://mikrotik.ideco.ru).

После генерации скрипта необходимо открыть раздел **System -> Scripts**, создать скрипт, вставить в него код, сгенерированный конфигуратором, и запустить.

</details>

<details>

<summary>Настройка Ideco NGFW</summary>

1\. В Ideco NGFW откройте вкладку **Сервисы -> IPsec -> Входящие подключения**, нажмите **Добавить** и заполните поля:

  * **Название подключения** - укажите произвольное имя для подключения. Значение не должно быть длиннее 42 символов;
  * **Зона** - укажите зону для добавления IPsec-подключения;
  * **IP-адрес интерфейса туннеля** - укажите IP-адрес интерфейса туннеля. Поле необязательное, заполняется при настройке BGP-соседства для динамической маршрутизации и для получения статистики обмена пакетами;
  * **Удаленный IP-адрес туннеля** - укажите IP-адрес интерфейса туннеля удаленной стороны. Поле необязательное. Для получения статистики о потере пакетов, средней задержке и джиттере заполните поля **IP-адрес интрефейса туннеля** и **Удаленный IP-адрес туннеля**. Они должны находиться в одной подсети.
  * **PSK** - вставьте PSK-ключ, полученный от MikroTik;
  * **Идентификатор удаленной стороны** - вставьте идентификатор MikroTik (параметр Key ID в `/ip ipsec peers`);
  * **Домашние локальные сети** - перечислите все **локальные сети NGFW**, которые будут видны противоположной стороне;
  * **Удаленные локальные сети** - перечислите все локальные сети MikroTik, которые будут видны противоположной стороне:

  ![](/.gitbook/assets/ipsec18.png)

2\. Нажмите кнопку **Добавить подключение**.

</details>

#### Тип аутентификации Сертификат

Подключение по сертификатам является более безопасным, чем подключение по PSK.

<details>

<summary>Настройка MikroTik</summary>

Настроить MikroTik можно:

* Через GUI;
* Через консоль устройства;
* Через конфигурационные скрипты, сгенерированные по адресу [https://mikrotik.ideco.ru/](https://mikrotik.ideco.ru).

После генерации скрипта необходимо открыть раздел **System -> Scripts**, создать скрипт, вставить в него код, сгенерированный конфигуратором, и запустить его.

Конфигуратором генерируется два скрипта, потому в MikroTik также нужно создать два скрипта.

Перед настройкой необходимо запустить первый скрипт. В файловом хранилище MikroTik появятся два файла, которые необходимо скачать, они требуются для дальнейшей настройки:

![](/.gitbook/assets/site-to-site-ideco-mikrotik4.png)

* Файл `certificate-request.pem` - **запрос на подпись сертификата**;
* Файл `certificate-request_key.pem` - **приватный ключ**.

Далее переходим к настройке Ideco NGFW.

</details>

<details>

<summary>Настройка Ideco NGFW</summary>

1\. В Ideco NGFW откройте вкладку **Сервисы -> IPsec -> Входящие подключения**, нажмите **Добавить** и заполните поля:

  * **Название подключения** - укажите произвольное имя для подключения. Значение не должно быть длиннее 42 символов;
  * **Зона** - укажите зону, в которую требуется добавить IPsec-подключение;
  * **IP-адрес интерфейса туннеля** - укажите IP-адрес интерфейса туннеля. Поле необязательное, заполняется при настройке BGP-соседства для динамической маршрутизации и для получения статистики обмена пакетами;
  * **Удаленный IP-адрес туннеля** - укажите IP-адрес интерфейса туннеля удаленной стороны. Поле необязательное. Для получения статистики о потере пакетов, средней задержке и джиттере заполните поля **IP-адрес интрефейса туннеля** и **Удаленный IP-адрес туннеля**. Они должны находиться в одной подсети.
  * **Запрос на подпись сертификата** - загрузите запрос на подпись, **полученный от MikroTik**;
  * **Домашние локальные сети** - необходимо перечислить все локальные сети NGFW, которые будут доступны в IPsec-подключении, т. е. будут видны противоположной стороне:

  ![](/.gitbook/assets/ipsec19.png)

2\. Нажмите кнопку **Добавить подключение**. Нажмите на кнопку редактирования соединения, чтобы продолжить настройку:

  ![](/.gitbook/assets/ipsec20.png)

3\. Скачайте файлы, которые находятся в полях **Корневой сертификат NGFW** и **Подписанный сертификат устройства**, для их последующего использования в MikroTik:

  ![](/.gitbook/assets/ipsec21.png)

</details>

## Подключение в Транспортном режиме (GRE over IPsec)

GRE over IPsec поддерживает мультикаст-трафик, что позволяет использовать более сложные механизмы маршрутизации, включая динамическую маршрутизацию через OSPF.

Также в GRE over IPsec не требуется задавать **Домашние локальные сети** и **Удаленные локальные сети**. Транспортный режим IPsec шифрует только то, что выше уровня IP, а заголовок IP оставляет без изменений.

Рассмотрим настройку подключения по схеме:

![](/.gitbook/assets/site-to-site-ideco-mikrotik5.png)

* `172.16.50.3/24` - внешний IP-адрес NGFW;
* `192.168.100.2/24` - локальный IP-адрес NGFW;
* `10.100.0.1/16` - IP-адрес GRE-тунеля NGFW;
* `172.16.50.4/24` - внешний IP-адрес MikroTik;
* `192.168.50.2/24` - локальный IP-адрес MikroTik;
* `10.100.0.2/16` - IP-адрес GRE-тунеля MikroTik.

Для настройки подключения MikroTik и Ideco NGFW нужно следовать инструкции в каждом из пунктов.

### Подключение от Ideco NGFW к MikroTik

<details>

<summary>Предварительная настройка MikroTik</summary>

1\. Настройте на MikroTik IP-адреса:

```
/ip address add address=172.16.50.4/24 interface=ether1 network=172.16.50.0
/ip address add address=192.168.50.2/24 interface=ether2 network=192.168.50.0
```

2\. Создайте GRE-интерфейс и назначьте ему IP-адрес:

```
/interface gre add allow-fast-path=no local-address=172.16.50.4 name=gre-tunnel1 remote-address=172.16.50.3
/ip address add address=10.100.0.2/16 interface=gre-tunnel1 network=10.100.0.0
```

</details>

#### Тип аутентификации PSK

<details>

<summary>Настройка исходящего подключения на Ideco NGFW</summary>

Заполните поля:

![](/.gitbook/assets/ipsec.png)

* **Название подключения** - укажите произвольное имя для подключения. Значение не должно быть длиннее 42 символов;
* **Зона** - укажите зону для добавления IPSec-подключения;
* **Режим работы** - выберите **Транспортный** режим;
* **Адрес удаленного устройства** - укажите внешний IP-адрес устройства MikroTik;
* **IP-адрес интерфейса туннеля** - укажите IP-адрес интерфейса GRE-туннеля NGFW;
* **Удаленный IP-адрес туннеля** - укажите IP-адрес интерфейса GRE-туннеля MikroTik. Поле необязательное и заполняется для получения статистики о потере пакетов, средней задержке и джиттере. **IP-адрес интрефейса туннеля** и **Удаленный IP-адрес туннеля** должны находиться в одной подсети;
* **Интерфейс** - выберите внешний интерфейс NGFW;
* **Тип аутентификации** - выберите **PSK**;
* **PSK-ключ** - будет сгенерирован случайный PSK-ключ. Он потребуется для настройки подключения в MikroTik;
* **Тип идентификатора** - выберите **keyid**;
* **NGFW идентификатор** - введенный ключ будет использоваться для идентификации исходящего подключения.

</details>

<details>

<summary>Настройка входящего подключения на MikroTik</summary>

Настройте IPsec-подключение со стороны MikroTik:

```
/ip ipsec profile add dh-group=modp4096 enc-algorithm=aes-256 hash-algorithm=sha256 name=from_192.168.100.0/24

/ip ipsec proposal add auth-algorithms=sha256 comment=from_192.168.100.0/24 enc-algorithms=aes-256-cbc name=172.16.50.3 pfs-group=modp4096

/ip ipsec peer add address=172.16.50.3/32 comment=from_192.168.100.0/24 exchange-mode=ike2 name=from_192.168.100.0/24 passive=yes profile=from_192.168.100.0/24

/ip ipsec identity add comment=from_192.168.100.0/24 peer=from_192.168.100.0/24 secret="<Сгенерированный NGFW PSK-ключ>"

/ip ipsec policy add dst-address=172.16.50.3/32 peer=from_192.168.100.0/24 proposal=172.16.50.3 protocol=gre src-address=172.16.50.4/32
```

</details>

#### Тип аутентификации Сертификат

<details>

<summary>Настройка исходящего IPsec-подключения на Ideco NGFW</summary>

1\. Перейдите в раздел **IPsec -> Исходящие подключения** и нажмите **Добавить**.

2\. Заполните поля:

  ![](/.gitbook/assets/ipsec3.png)

  * **Название подключения** - укажите произвольное имя для подключения. Значение не должно быть длиннее 42 символов;
  * **Зона** - укажите зону для добавления IPSec-подключения;
  * **Режим работы** - выберите **Транспортный** режим;
  * **Адрес удаленного устройства** - укажите внешний IP-адрес устройства MikroTik;
  * **IP-адрес интерфейса туннеля** - укажите IP-адрес интерфейса GRE-туннеля NGFW;
  * **Удаленный IP-адрес туннеля** - укажите IP-адрес интерфейса GRE-туннеля MikroTik. Поле необязательное и заполняется для получения статистики о потере пакетов, средней задержке и джиттере. **IP-адрес интрефейса туннеля** и **Удаленный IP-адрес туннеля** должны находиться в одной подсети;
  * **Интерфейс** - выберите интерфейс NGFW;
  * **Режим работы** - выберите **Транспортный** режим;
  * **Тип аутентификации** - выберите **Сертификат**.

3\. Загрузите **Запрос на подпись сертификата**.

4\. Не закрывая форму создания исходящего подключения NGFW, перейдите к настройке Mikrotik.

</details>

<details>

<summary>Настройка входящего подключения на MikroTik</summary>

1\. Загрузите скачанный ранее файл с **Запросом на подпись сертификата** (`NGFW.crt`) на MikroTik через WinBox или по ssh.

2\. Создайте корневой сертификат MikroTik:

```
/certificate add common-name=mk_ca name=mk_ca_template key-usage=key-cert-sign,crl-sign,digital-signature,content-commitment
/certificate sign mk_ca_template ca-crl-host=172.16.50.4 name=mk_ca
```

3\. Подпишите сертификат Ideco NGFW и сделайте его доверенным:

```
/certificate sign-certificate-request file-name=UTM.csr ca=mk_ca
/certificate set [find name~"^device_.+\\.ipsec\$"] trusted=yes
```

4\. Экспортируйте корневой сертификат MikroTik и подписанный сертификат NGFW в формат `.pem`:

```
/certificate export-certificate mk_ca type=pem
/certificate export-certificate [find name~"^device_.+\\.ipsec\$"] type=pem
```

5\. Загрузите с MikroTik корневой сертификат MikroTik и подписанный сертификат NGFW через WinBox или по ssh. Названия файлов содержат `cert_export`.

6\. Настройте входящее IPsec-соединение на MikroTik:

```
/ip ipsec profile add name=from_192.168.100.0/24 hash-algorithm=sha256 enc-algorithm=aes-256 dh-group=modp4096 dpd-interval=120s dpd-maximum-failures=5

/ip ipsec peer add name=from_192.168.100.0/24 address=172.16.50.3/32 profile=from_192.168.100.0/24 exchange-mode=ike2 passive=yes comment=from_192.168.100.0/24

/ip ipsec identity add peer=from_192.168.100.0/24 auth-method=digital-signature certificate=mk_ca remote-certificate=[: put [/certificate get [/certificate find name~"^device_.+\\.ipsec\$"] name]] comment=from_192.168.100.0/24

/ip ipsec proposal add name=172.16.50.3 enc-algorithms=aes-256-cbc auth-algorithms=sha256 pfs-group=modp4096 comment=from_192.168.100.0/24

/ip ipsec policy add dst-address=172.16.50.3/32 peer=from_192.168.100.0/24 proposal=172.16.50.3 protocol=gre src-address=172.16.50.4/32
```

</details>

<details>

<summary>Донастройка исходящего IPsec-подключение на Ideco NGFW</summary>

Вернитесь к форме создания исходящего IPsec-соединения на Ideco NGFW.

1\. Загрузите скачанные ранее файлы **Корневого сертификата MikroTik** (`cert_export_mk_ca.crt`) и **Подписанный сертификат NGFW** (`cert_export_device_53c34ddc6d584d938f2098eae838e6ff.ipsec.crt`) в поля **Корневой сертификат удаленного устройства** и **Подписанный сертификат NGFW** соответственно.

2\. Нажмите **Сохранить**.

</details>

### Подключение от MikroTik к Ideco NGFW  

#### Тип аутентификации PSK

<details>

<summary>Настройка исходящего подключения на MikroTik</summary>

1\. Настройте на MikroTik IP-адреса:

```
/ip address add address=172.16.50.4/24 interface=ether1 network=172.16.50.0
/ip address add address=192.168.50.2/24 interface=ether2 network=192.168.50.0
```

2\. Создайте GRE-интерфейс и назначьте ему IP-адрес:

```
/interface gre add allow-fast-path=no local-address=172.16.50.4 name=gre-tunnel1 remote-address=172.16.50.3
/ip address add address=10.100.0.2/16 interface=gre-tunnel1 network=10.100.0.0
```

3\. Настройте IPsec-подключение со стороны MikroTik:

```
/ip ipsec profile add dh-group=modp4096 enc-algorithm=aes-256 hash-algorithm=sha256 name=to_192.168.100.0/24

/ip ipsec proposal add auth-algorithms=sha256 comment=to_192.168.100.0/24 enc-algorithms=aes-256-cbc name=172.16.50.3 pfs-group=modp4096

/ip ipsec peer add address=172.16.50.3/32 comment=to_192.168.100.0/24 exchange-mode=ike2 name=to_192.168.100.0/24 profile=to_192.168.100.0/24

/ip ipsec identity add comment=to_192.168.100.0/24 peer=to_192.168.100.0/24 my-id=key-id:"test_psk" secret="<PSK-ключ>"

/ip ipsec policy add dst-address=172.16.50.3/32 peer=to_192.168.100.0/24 proposal=172.16.50.3 protocol=gre src-address=172.16.50.4/32
```

</details>

<details>

<summary>Настройка входящего подключения на Ideco NGFW</summary>

Заполните поля:

![](/.gitbook/assets/ipsec1.png)

* **Название подключения** - укажите произвольное имя для подключения. Значение не должно быть длиннее 42 символов;
* **Зона** - укажите зону для добавления IPSec-подключения;
* **Режим работы** - выберите **Транспортный** режим;
* **IP-адрес интерфейса туннеля** - укажите IP-адрес интерфейса GRE-туннеля NGFW;
* **Удаленный IP-адрес туннеля** - укажите IP-адрес интерфейса GRE-туннеля MikroTik. Поле необязательное и заполняется для получения статистики о потере пакетов, средней задержке и джиттере. **IP-адрес интрефейса туннеля** и **Удаленный IP-адрес туннеля** должны находиться в одной подсети;
* **Тип аутентификации** - выберите **PSK**;
* **PSK-ключ** - введите PSK-ключ, указанный при настройке исходящего подключения в MikroTik;
* **Тип идентификатора** - выберите **keyid**;
* **NGFW идентификатор** - введите **key-id**, использованный при настройке исходящего подключения в MikroTik.

</details>

#### Тип аутентификации Сертификат

<details>

<summary>Предварительная настройка MikroTik</summary>

1\. Настройте на MikroTik IP-адреса:

```
/ip address add address=172.16.50.4/24 interface=ether1 network=172.16.50.0
/ip address add address=192.168.50.2/24 interface=ether2 network=192.168.50.0
```

2\. Создайте GRE-интерфейс и назначьте ему IP-адрес:

```
/interface gre add allow-fast-path=no local-address=172.16.50.4 name=gre-tunnel1 remote-address=172.16.50.3
/ip address add address=10.100.0.2/16 interface=gre-tunnel1 network=10.100.0.0
```

3\. Сгенерируйте запрос на подпись сертификата:

```
/certificate add name=mk_ca common-name=mk_ca key-usage=digital-signature,content-commitment
/certificate create-certificate-request key-passphrase="" template=mk_ca
```

4\. Загрузите файл `certificate-request.pem` c MikroTik через WinBox или по ssh.

</details>

<details>

<summary>Настройка входящего IPsec-подключения на Ideco NGFW</summary>

1\. Перейдите в раздел **IPsec -> Входящие подключения** и нажмите **Добавить**.

2\. Заполните поля:

  ![](/.gitbook/assets/ipsec2.png)

  * **Название подключения** - укажите произвольное имя для подключения. Значение не должно быть длиннее 42 символов;
  * **Зона** - укажите зону для добавления IPSec-подключения;
  * **Режим работы** - выберите **Транспортный** режим;
  * **IP-адрес интерфейса туннеля** - укажите IP-адрес интерфейса GRE-туннеля NGFW;
  * **Удаленный IP-адрес туннеля** - укажите IP-адрес интерфейса GRE-туннеля MikroTik. Поле необязательное и заполняется для получения статистики о потере пакетов, средней задержке и джиттере. **IP-адрес интрефейса туннеля** и **Удаленный IP-адрес туннеля** должны находиться в одной подсети;
  * **Тип аутентификации** - выберите **Сертификат**.

3\. Загрузите скачанный ранее с MikroTik файл `certificate-request.pem` в поле **Запрос на подпись сертификата**.

4\. Нажмите **Сохранить**.

5\. Откройте созданное IPsec-соединение, нажав на ![](/.gitbook/assets/icon-edit.png) и загрузите файлы **Корневого сертификата NGFW** (`NGFW.crt`) и **Подписанный сертификат устройства** (`device.crt`).

</details>

<details>

<summary>Настройка исходящего IPsec-подключение на MikroTik</summary>

1\. Загрузите на MikroTik скачанные ранее файлы **Корневого сертификата NGFW** (`NGFW.crt`) и **Подписанный сертификат устройства** (`device.crt`) через WinBox или по ssh.

2\. Импортируйте сертификаты:

```
/certificate import file-name=NGFW.crt passphrase=""
/certificate import file-name=device.crt passphrase=""
/certificate import file-name=certificate-request_key.pem passphrase=""
```

3\. Настройте IPsec-соединение:

```
/ip ipsec profile add dh-group=modp4096 enc-algorithm=aes-256 hash-algorithm=sha256 name=to_192.168.100.0/24 dpd-interval=120s dpd-maximum-failures=5

/ip ipsec peer add address=172.16.50.3/32 comment=to_192.168.100.0/24 exchange-mode=ike2 name=to_192.168.100.0/24 profile=to_192.168.100.0/24

/ip ipsec identity add comment=to_192.168.100.0/24 peer=to_192.168.100.0/24 auth-method=digital-signature certificate=device.crt_0 remote-certificate=NGFW.crt_0

/ip ipsec proposal add auth-algorithms=sha256 comment=to_192.168.100.0/24 enc-algorithms=aes-256-cbc name=172.16.50.3 pfs-group=modp4096

/ip ipsec policy add dst-address=172.16.50.3/32 peer=to_192.168.100.0/24 proposal=172.16.50.3 protocol=gre src-address=172.16.50.4/32
```

</details>

### Проблемы при повторной активации входящего подключения к Ideco NGFW

Если подключение было отключено и при попытке включения соединение не установилось, удаленное устройство попало в fail2ban. Для установки соединения сбросьте блокировки по IP на Ideco NGFW. О сбросе блокировки читайте в статье [Защита от brute-force атак](/settings/reports/logs.md#защита-от-brute-force-атак).

Fail2ban отслеживает в log-файлах попытки обратиться к сервисам, и, если находит повторяющиеся неудачные попытки авторизации с одного и того же IP-адреса или хоста, блокирует IP-адрес.