#VKOC — VK ONLINE CHECKER

##Описание
Для работы программы необходим Python не ниже 3 версии. И поставляемый модуль `requests-html`.
_`pip install requests-html`_

**Программа была придумана и разработана на полном энтузиазме 11 мая 2018 года, автор: 
[Олег Плаксин](https://github.io/plaxin).**

### <a name="begin"></a> Начать проверку
Для того чтобы начать цикл проверок пользователя на нахождение его в сети в социальной сети vk.com — необходимо
запустить Python файл `python .\main.py`. 

### <a name="params"></a> Передача параметров проверки
#### <a name="params-in"></a> В реальном времени выполнения программы
Следуйте инструкциям скрипта в командной строке.

#### <a name="params-argv"></a> Передача аргументов при запуске
Программа умеет отслеживать передачу аргументов при запуске, а то есть: `python .\main.py 140830142 0.5`. 
Где:
* `140830142` — id пользователей в социальной сети, перечисленных через запятую для многопользовательского режима,
* `0.5` — время ожидания между запросами (задержка программного 
цикла) в минутах. _(0.5 минут = 30 секунд)_.

### <a name="data"></a> Работа с данными
При правильной работе программы, она логирует всю информацию в командную строку, откуда был произведен запуск и
одновременно записывает те же данные в файлы, находящиеся по адресу `.\logs\%id%\%yearmonth%\%date%.log`.

При условии многопользовательского фиксирования онлайна, директория нахождения логов меняется на: 
`.\logs\few users\%yearmonth%\%date%.log`.

#### <a name="data-init"></a> Первый запуск или инициализация
При первом запуске — программа создает `.\config.ini` файл, или использует существующий, если есть.

##### <a name="data-init-config"></a> Содержание config.ini
Файл `.\config.ini` должен содержать следующие данные:
* `[Settings]` — обязательную считываемую программой секцию Settings,
* Параметр `vkapiuri` должен иметь значение ссылки до API ВКонтакте. По умолчанию, это — `"https://api.vk.com/method/"`
* Параметр `accesstoken` должен содержать сервисный ключ доступа вашего, 
[созданного вами приложения ВКонтакте](https://vk.com/apps?act=manage) или ключ доступа к вашему профилю ВКонтакте,
* Параметр `vkapiversion` должен содержать последнюю и самую актуальную версию API ВКонтакте на момент последнего 
обновления этой программы.

#### <a name="data-view-single"></a> Разбор информации проверки одиночного пользователя
Программа указывает информацию в консоли и в файле в следующем виде:
```
01 Sep 2018 00:00:05: main: ### ###
01 Sep 2018 00:00:05: main: Программный цикл: 273

01 Sep 2018 00:00:05: online: Олег Плаксин был в сети с Android, 31 Aug 2018 23:29:01

01 Sep 2018 00:00:05: user checker: Задержка 97 мс.
01 Sep 2018 00:00:05: main: Повтор команды через 0.5 минут.
01 Sep 2018 00:00:05: main: Uptime: 8552525 ms
```
Где:
* `01 Sep 2018 00:00:05` — время фиксации,
* `main` — название рабочего метода, который выслал информацию в лог,
* `Программный цикл: 273` — количество фиксаций после запуска программы, 
* `Олег Плаксин был в сети с Android, 31 Aug 2018 23:29:01` — сама информация об активности в социальной сети, с
указанием даты последего посещения, передаваемой социальной сетью,
* `Задержка 97 мс.` — задержка цикла или ping текущего обращения к серверам,
* `Повтор команды через 0.5 минут.` — уведомление о повторе команды и ее задержки,
* `Uptime: 8552525 ms` — время безотказной работы после запуска программы.

Заголовок командной строки, в которой выполняется программа, содержит краткую информацию о последней успешной фиксации:
`Олег Плаксин был в сети с Android, 23:29:01`. **К сожалению, здесь, пришлось экономить место, и указывать время
последнего посещения без указания даты. Подразумевается, что программа будет использоваться для отслеживания живых 
(активных) пользователей сети.**

#### <a name="data-view-multi"></a> Разбор информации многопользовательской проверки
Логирование и фиксация пользователей происходит практически также, за исключением выдаваемых строк.
```
01 Sep 2018 00:00:05: main: ### ###
01 Sep 2018 00:00:05: main: Программный цикл: 273

01 Sep 2018 00:00:05: online: Олег Плаксин был в сети с Android, 31 Aug 2018 23:29:01
01 Sep 2018 00:00:05: online: Соша Греч в сети с iPhone, 31 Aug 2018 23:59:42

01 Sep 2018 00:00:05: user checker: Задержка 97 мс.
01 Sep 2018 00:00:05: main: Повтор команды через 0.5 минут.
01 Sep 2018 00:00:05: main: Uptime: 8552525 ms
```
Информацию, о каждом пункте можно узнать из [разбора однопользовательского режима слежения](#data-view-single).

Заголовок командной строки, в которой выполняется программа, содержит краткую информацию о последней успешной фиксации:
`2 наблюдаемых / 1 в сети`. **К сожалению, здесь, пришлось экономить место, и указывать только количество пользователей
в сети из количества пользователей в проверке. Подразумевается, что программа будет использоваться для отслеживания живых 
(активных) пользователей сети.**
