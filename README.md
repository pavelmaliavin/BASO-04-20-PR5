# BASO-04-20-PR5
1. ОПРЕДЕЛЕНИЕ ТИПА HASH

Открываем консоль и устанавливаем утилиту с помощью команды sudo apt install hashid

<a target="_blank" href="https://radikal.ru"><img src="https://a.radikal.ru/a06/2011/f2/eceb3e22a962.png" /></a>

Далее, заходим в файл /etc/shadow, где хранятся пароли, с помощью команды sudo cat

<a target="_blank" href="https://radikal.ru"><img src="https://a.radikal.ru/a38/2011/ae/4bca84fe4159.png" /></a>

Пролистав вниз, мы увидем хэш

<a target="_blank" href="https://radikal.ru"><img src="https://d.radikal.ru/d34/2011/b9/941b5047e66c.png" /></a>

С помощью команды hashid -m мы сможем узнать тип хэша, просто копируем наш хэш и добавляем к команде

<a target="_blank" href="https://radikal.ru"><img src="https://b.radikal.ru/b21/2011/dd/8f8448ae7fc7.png" /></a>

Тип нашего хэша - MD5 (cisco-ASA)

2. СОЗДАНИЕ HASH В LINUX

Создал ноаого пользователя, добавил пароль

<a target="_blank" href="https://radikal.ru"><img src="https://c.radikal.ru/c14/2011/e0/502767705d3d.png" /></a>

<a target="_blank" href="https://radikal.ru"><img src="https://a.radikal.ru/a26/2011/b4/730460599035.png" /></a>

Теперь зайдем в шэдоу и посмотрим

<a target="_blank" href="https://radikal.ru"><img src="https://a.radikal.ru/a29/2011/77/6e88d4e8fa12.png" /></a>

Васян есть, хэш от его пароля тоже

Теперь мы должны заменить хэш и обновить пароль, но я не совсем понял, что значит "заменить хэш"

<a target="_blank" href="https://radikal.ru"><img src="https://d.radikal.ru/d22/2011/0a/af1b32025f73.png" /></a>

Обновляем пароль (через команду $update-passwd - safely update /etc/shadow обновить не получилось)

<a target="_blank" href="https://radikal.ru"><img src="https://d.radikal.ru/d25/2011/ee/e33b12e8543c.png" /></a>

При попытке входа выходит ошибка доступа этого юзера, но это решается выдачей рут прав

<a target="_blank" href="https://radikal.ru"><img src="https://b.radikal.ru/b34/2011/82/ca7b1b624ac1.png" /></a>

Ну и расчитываем потом хэшированный пароль, предварительно скопировав соль из етц шэдоу

<a target="_blank" href="https://radikal.ru"><img src="https://d.radikal.ru/d28/2011/55/b46743c2a1e9.png" /></a>

3. ПРОВЕРКА КОНТРОЛЬНЫХ СУММ

Копируем /etc/group в домашнюю папку

<a target="_blank" href="https://radikal.ru"><img src="https://a.radikal.ru/a20/2011/eb/7c06c0683b5e.png" /></a>

Далее, считаем контрольную сумму с помощью команды sha1sum group

<a target="_blank" href="https://radikal.ru"><img src="https://a.radikal.ru/a42/2011/7d/80d467aa049f.png" /></a>

<a target="_blank" href="https://radikal.ru"><img src="https://b.radikal.ru/b00/2011/33/f664b88a17e0.png" /></a>

Теперь, изменим содержимое файла, а именно удалим первую строчку

<a target="_blank" href="https://radikal.ru"><img src="https://c.radikal.ru/c00/2011/3b/c847eff8fd2a.png" /></a>

Сохраняем (я в первый раз забыл, и не понял, почему все равно group ЦЕЛ )))) )

<a target="_blank" href="https://radikal.ru"><img src="https://c.radikal.ru/c40/2011/40/686da4ef2184.png" /></a>

Ну и проверяем

<a target="_blank" href="https://radikal.ru"><img src="https://c.radikal.ru/c39/2011/0e/3f003b32df7e.png" /></a>

Очевидно, что файл поврежден

Копируем и переименовываем тот же файл group.sha1 на grouptest.sha1

<a target="_blank" href="https://radikal.ru"><img src="https://a.radikal.ru/a22/2011/c1/4ef91352fbfb.png" /></a>

Значение не поменялось, значит от названия не зависит

4. ШИФРОВАНИЕ ФАЙЛОВ С ПОМОЩЬЮ ПАРОЛЯ

Создадим пустой файл с помощью команды touch и поставим на него пароль

<a target="_blank" href="https://radikal.ru"><img src="https://c.radikal.ru/c12/2011/6e/23dd6ab9c0a3.png" /></a>

Как видим, зашифровалось успешно

<a target="_blank" href="https://radikal.ru"><img src="https://c.radikal.ru/c24/2011/fb/136c6513d29c.png" /></a>

5. ШИФРОВАНИЕ С ПОМОЩЬЮ КЛЮЧА

Создадим файл + ключик к нему

<a target="_blank" href="https://radikal.ru"><img src="https://a.radikal.ru/a11/2011/82/6f5538711ac1.png" /></a>

Теперь настроим его

<a target="_blank" href="https://radikal.ru"><img src="https://d.radikal.ru/d12/2011/b8/f664e9b56b04.png" /></a>

<a target="_blank" href="https://radikal.ru"><img src="https://c.radikal.ru/c00/2011/8e/b7b28ffff360.png" /></a>

Открытый и секретный ключи успешно созданы

Теперь посмотрим доуступные нам ключи

<a target="_blank" href="https://radikal.ru"><img src="https://d.radikal.ru/d31/2011/24/30e9b3219c06.png" /></a>

Экспортируем, потом импортируем

<a target="_blank" href="https://radikal.ru"><img src="https://d.radikal.ru/d37/2011/ae/b73df9596fee.png" /></a>

Далее воспользуемся редактором ключей, чтобы повысить уровень достоверности

<a target="_blank" href="https://radikal.ru"><img src="https://d.radikal.ru/d30/2011/1b/c0f8066838d3.png" /></a>

Выбираем максимальный уровень достоверности

<a target="_blank" href="https://radikal.ru"><img src="https://c.radikal.ru/c02/2011/48/7fa540188788.png" /></a>

6. ПОДПИСИ И ШИФРОВАНИЕ

Создаем файл, вешаем на него подпись

<a target="_blank" href="https://radikal.ru"><img src="https://c.radikal.ru/c01/2011/e5/6512e9dfc3ed.png" /></a>

<a target="_blank" href="https://radikal.ru"><img src="https://a.radikal.ru/a15/2011/82/624e38f87a5b.png" /></a>

Проверим, как было изначально

<a target="_blank" href="https://radikal.ru"><img src="https://c.radikal.ru/c00/2011/de/139661c12d5c.png" /></a>

Теперь изменим содержимое файла

<a target="_blank" href="https://radikal.ru"><img src="https://d.radikal.ru/d32/2011/a7/a9cd58f940f6.png" /></a>

И снова проверим

<a target="_blank" href="https://radikal.ru"><img src="https://b.radikal.ru/b04/2011/44/071d0781d627.png" /></a>

7. ОТПРАВКА ПИСЬМА

Поставил thunderbird, добавил в расширения Enigmail

Теперь добавим ключ

<a target="_blank" href="https://radikal.ru"><img src="https://d.radikal.ru/d22/2011/d9/0788daccd5c7.png" /></a>

<a target="_blank" href="https://radikal.ru"><img src="https://c.radikal.ru/c01/2011/55/276d45f99ed0.png" /></a>

Ключ создан

<a target="_blank" href="https://radikal.ru"><img src="https://b.radikal.ru/b19/2011/df/ce7e0cdddee3.png" /></a>

Далее мы экспортируем ключ, чтобы потом его опубликовать

<a target="_blank" href="https://radikal.ru"><img src="https://a.radikal.ru/a33/2011/61/33fd21ce6d9a.png" /></a>

Открываем keys.openpgp.org и заливаем туда ключ

<a target="_blank" href="https://radikal.ru"><img src="https://a.radikal.ru/a39/2011/60/576c6456f6cb.png" /></a>

<a target="_blank" href="https://radikal.ru"><img src="https://b.radikal.ru/b02/2011/91/386c9844fcf8.png" /></a>

Отправляем на почту

<a target="_blank" href="https://radikal.ru"><img src="https://b.radikal.ru/b09/2011/c8/8d97c737e37d.png" /></a>

Ну и находим на этом же сайте привязанный ключ к почте 

<a target="_blank" href="https://radikal.ru"><img src="https://d.radikal.ru/d25/2011/4f/d171c2c05ebe.png" /></a>

<a target="_blank" href="https://radikal.ru"><img src="https://d.radikal.ru/d04/2011/a7/0ae63216a765.png" /></a>

Теперь поищем открытый ключ, привязанный к почте мирэа

<a target="_blank" href="https://radikal.ru"><img src="https://c.radikal.ru/c23/2011/fd/33701740a307.png" /></a>

<a target="_blank" href="https://radikal.ru"><img src="https://a.radikal.ru/a04/2011/d2/4f18b793e443.png" /></a>

<a target="_blank" href="https://radikal.ru"><img src="https://b.radikal.ru/b16/2011/f1/f8038d89e062.png" /></a>

Теперь пишем письмо

<a target="_blank" href="https://radikal.ru"><img src="https://d.radikal.ru/d19/2011/5e/91f0e8006242.png" /></a>

<a target="_blank" href="https://radikal.ru"><img src="https://a.radikal.ru/a21/2011/fd/667b19078fd7.png" /></a>

Вот так выглядит отпрпавленное мной письмо (на телефоне)

<a target="_blank" href="https://radikal.ru"><img src="https://c.radikal.ru/c15/2011/be/694e6792025e.png" /></a>

Письмо отправил на почту mobil.mirea@gmail.com с включенным шифрованием 
