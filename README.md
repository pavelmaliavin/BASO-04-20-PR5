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
