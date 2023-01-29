# SD-Two-factor-authorization
## Требуемый функционал

* Посетитель вводит email и пароль для авторизации;

* Если email и пароль верны, то посетитель перенаправляется на специальную страницу на которой предлагается ввести код, который ему был отправлен по email;

* Если код введен успешно, то посетитель авторизоваться на сайте. Если код неверен, авторизация не происходит;

* Код генерируется случайно и должен быть активен в течении 5 минут, обратный отсчет можно не реализовывать;

* Должна присутствовать ссылка на повторную отправку кода. Код можно отправлять не более трех раз. Если код был отправлен 3 раза, выводить сообщение о том, что необходимо повторно ввести email и пароль.

## Окружение
1. Используется Open Server со следующими настройками:
    [![imageup.ru](https://imageup.ru/img131/4137410/image_2022-12-25_23-54-12.png)](https://imageup.ru/img131/4137410/image_2022-12-25_23-54-12.png.html)

2. Версия CS-Cart **v4.15.2_ru**

## Установка 
1. Клонируем [этот репозиторий](https://github.com/Alexandr1807/SD-Two-factor-authorization) к себе на устройство.

2. В ветке main находится установка CS-Cart, а в ветке addon - файлы модуля (в отдельной папке). Пройдите все этапы установки CS-Cart.

3. Чтобы добавить файлы модуля можно использовать CS-Cart SDK.

## Настройка SMTP для отправки писем
1. Зайти в панель администратора и в верхнем меню направить указать на выпадающее меню "Настройки/Settings" и нажать на "Электронная почта/E-mails". Настройки на этой странице:
[![imageup.ru](https://imageup.ru/img252/4183214/nastroiki.png)](https://imageup.ru/img252/4183214/nastroiki.png.html)
2. В поле "SMTP сервер" требуется ввести smtp.gmail.com:465.
2. В поле "Имя пользователя для SMTP" требуется ввести действительный аккаунт gmail.
3. В поле "Пароль для SMTP сервера" требуется ввести сгенерированный в данном аакаунте gmail 16-значный пароль для приложений. [Инструкция для создания пароля для небезопасных приложений](https://support.google.com/accounts/answer/185833?hl=ru)
4.  В поле "Шифрованное соединение" требуется выбрать SSL.

## Установка модуля
1. Зайти в панель администратора

2. Зайти в учетную запись администратора

3. Пройти по следующему пути: 
Модули → Управление модулями → CS-Cart

4. При помощи поиска найти модуль, под названием "Simtech Development: Двухфакторная аутентификация". Если поиск результатов не выдает, нажмите на ссылку "Скачанные модули", в сайдбаре справа. Это обновит список и позволит увидеть новый модуль.

5. Установить модуль “Simtech Development: Двухфакторная аутентификация”.

## Проверка работы
1. Зарегистрируйте новый профиль (используется профиль не администратора, а простого покупателя) со своей почтой (понадобится чтобы проверить исправность работы отправки email писем с кодом)

2. Выйдите из аккаунта и снова откройте форму для входа в аккаунт. 

3. Введите свой email и пароль

4. Вы перейдете на страницу подтверждения входа. Функционал на этой странице:

	* При загрузке данной страницы автоматически сгенерируется код из случайных символов и сохранится в базу данных.

	* Реализован таймер, по умолчанию стоит на 5 минут (запускается при загрузке страницы). После того как истечет время, пользователь не сможет зайти в аккаунт, так как сгенерированный код будет удален из базы данных. Произойдет переход на предыдущую стадию входа в аккаунт.

	* Реализована функция повторной отправки кода на email. Для этого рядом с основной кнопкой отправки формы создана ссылка (копирует стили кнопки). При нажатии на данную ссылку пользователю на email придет еще одно письмо. Отправить повторно код можно всего три раза. На 3 попытке пользователю придет уведомление о том, что ему нужно ввести email и пароль заново. (Запись со сгенерированным кодом удалилась из базы данных). Произойдет переход на предыдущую стадию входа в аккаунт

	* При вводе корректного проверочного кода (из пришедшего письма на почту), пользователь успешно закончит вход в аккаунт.

## Дополнительные улучшения
* Добавлена мультиязычность. Существуют переменные на двух языках - русский и английский.
