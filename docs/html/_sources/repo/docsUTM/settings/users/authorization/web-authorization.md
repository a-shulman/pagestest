# Веб-аутентификация

Поддерживаемые браузеры:

* Google Chrome, версия >= 90;
* Firefox, версия >= 78;
* Safari, версия >= 14.

Этот тип авторизации предполагает, что запрос неавторизованного пользователя, отправленный через веб-браузер, будет переадресован на страницу авторизации Ideco NGFW. После успешной авторизации произойдет переход по указанному запросу.

Для этого типа авторизации у пользователя на сетевой карте в качестве шлюза (объединенных в цепочку нескольких шлюзов) или при прямых подключениях к прокси по умолчанию должен быть указан IP-адрес локального сетевого интерфейса Ideco NGFW. Также до подключения к интернету должен работать **DNS-резолвинг адресов**, иначе запрос браузера на адрес _example.com_ не будет перенаправлен на шлюз и в браузере не появится запрос логина и пароля.

Проверить разрешение имен в Windows можно командой: `nslookup ya.ru`. Вывод данной команды должен содержать IP-адреса.

Чтобы настроить авторизацию через веб-интерфейс, в разделе **Пользователи -> Авторизация** выберите пункты **Веб-аутентификация -> Аутентификация через веб-интерфейс**:

![](/.gitbook/assets/web-autorization.png)

После заполнения поля **Имя домена** и сохранения настроек будет выдан Let’s Encrypt сертификат, пользователь будет перенаправляться на окно авторизации, минуя страницу исключения безопасности:

![](/.gitbook/assets/web-autorization2.png)

Если NGFW не подключен к интернету или доменное имя не соответствует внешнему IP-адресу NGFW, то страница авторизации будет подписана корневым сертификатом NGFW.

Если сертификат для такого домена уже загружен в разделе [Сертификаты](/settings/services/certificates/), то будет использоваться он, новый сертификат выдаваться не будет.

Далее попробуйте выйти в интернет через веб-браузер. Должно появиться окно авторизации, где необходимо ввести логин и пароль от учетной записи пользователя, созданного на Ideco NGFW. Окно авторизации представлено на скриншоте ниже:

![](/.gitbook/assets/web-autorization1.png)

После прохождения пользователем веб-аутентификации доступ в сеть интернет будет предоставлен до тех пор, пока авторизация не будет принудительно отменена или прекращена по неактивности пользователя.

При входе на HTTPS-сайт пользователь должен подтвердить доверие к сертификату Ideco NGFW. Либо сертификат должен быть добавлен в доверенные корневые центры сертификации на устройстве (например, через политики домена).

Рекомендуется указывать в качестве DNS-сервера на компьютерах и устройствах локальной сети IP-адрес локального интерфейса Ideco NGFW.

Подробнее об авторизации пользователей **Active Directory** в статье [Аутентификация пользователей AD/Samba DC](/settings/users/active-directory/active-directory-user-authorization.md#veb-avtorizaciya-sso-ili-ntlm).

Подробнее об авторизации пользователей **ALD Pro** в статье [ALD Pro](/settings/users/ald-pro.md#autentifikaciya-polzovatelei).
