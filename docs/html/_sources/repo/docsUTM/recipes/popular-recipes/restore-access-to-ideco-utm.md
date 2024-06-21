---
description: >-
  При утере пароля администратора можно его восстановить, имея физический доступ
  к серверу.
---

# Как восстановить доступ к Ideco NGFW

Для этого нужно выполнить следующие действия:

1\. Перезагрузите сервер. При появлении меню загрузчика GRUB с выбором ядра Linux для загрузки системы нажмите англоязычную клавишу **E** на клавиатуре.

![](/.gitbook/assets/restore-access-to-ideco-utm1.png)

2\. Откроется окно параметров ядра с возможностью редактирования. Переместите указатель стрелками на клавиатуре вправо до слова `quiet` и допишите текст `p=1`:

![](/.gitbook/assets/restore-access-to-ideco-utm.gif)

3\. Нажмите комбинацию кнопок `Ctrl - X`. 

4\. После повторной загрузки системы появится окно создания аккаунта администратора. Задайте новый логин и пароль администратора.

![](/.gitbook/assets/restore-access-to-ideco-utm2.png)

Требования к созданию пароля администратора:

* Минимальная длина пароля - 12 символов;
* Строчные и заглавные латинские символы;
* Цифры;
* Специальные символы (! # $ % & ' \* + и т. д.).

Если пароль не будет соответствовать требованиям политики безопасности, то появится ошибка: 

![](/.gitbook/assets/restore-access-to-ideco-utm3.png)

Необходимо ввести новый пароль, учитывая требования к созданию паролей.

Если при создании нового логина администратора он будет совпадать с предыдущим логином, то откроется окно с выводом ошибки. Создайте имя администратора, отличное от предыдущего.

![](/.gitbook/assets/restore-access-to-ideco-utm4.png)