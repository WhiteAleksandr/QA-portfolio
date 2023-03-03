# QA-portfolio#

# <a name="up" />Портфолио тестировщика

В портфолио собраны проекты, выполненные во время обучения по специальности [Инженер по тестированию](https://praktikum.yandex.ru/qa-engineer) в Яндекс.Практикуме.
[Проектирование тестов](#test-design)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Тест-анализ | Ассоциативные карты | Блок-схемы<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Тест-дизайн | Классы эквивалентности | Граничные значения<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Тестовая документация | Чек-листы | Тест-кейсы

[Тестирование веб-приложений](#web-testing)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Пользовательский интерфейс | Формы | DevTools | Charles<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Таблицы принятия решений | Парное тестирование | Баг-репорты

[Тестирование мобильных приложений](#mobile-testing)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Матрица устройств | Эмуляторы | Android Studio

[Тестирование API](#api-testing)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;REST API | JSON | Postman

[Тестирование баз данных](#data-bases)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Консоль | SQL | PostgreSQL

[Основы автоматизации тестирования](#test-automation)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JavaScript | NodeJS | Puppeteer

## <a name="test-design" />Проектирование тестов

### Задание 1

**1. Визуализируй требования**

Проанализируй требования к сервису Яндекс.Маршруты и нарисуй mindmap.

**2. Выдели классы эквивалентности и граничные значения**

Проверь: «Время начала поездки», «Откуда», «Куда».

- Выдели объекты тестирования.
- Определи классы эквивалентности. Укажи тип ограничений: диапазон или набор значений.
- Определи граничные значения каждого класса, если применимо.
- Выбери тестовые значения, которые проверят каждый класс; и границы, если они есть.

Не забудь проверить негативные сценарии.

<details>
<summary>Требования к сервису Яндекс.Маршруты</summary>

***

Яндекс.Маршруты — сервис, который строит маршруты для транспорта разных видов. Рассчитывает время и стоимость поездки.

**Интерфейс**

В интерфейсе есть поля «Время начала поездки», «Откуда», «Куда». Переключатели режимов маршрута: оптимальный, быстрый и свой, а также переключатели видов транспорта: свой автомобиль, каршеринг, такси, самокат, велосипед и пешком.

Пользователь вводит время отправления. Чтобы построить маршрут, нужно ввести улицу и номер дома в поля «Откуда» и «Куда». В начале и конце адреса могут быть пробелы: они допустимы, но при снятии фокуса система удалит их.

**Описание работы интерфейса**

В стартовом состоянии поля «Время начала поездки», «Откуда» и «Куда» пустые. Режимы маршрутов «Оптимальный», «Быстрый и «Свой» не выбраны; панель переключения видов транспорта неактивна.

**Логика работы полей «Откуда» и «Куда»**

Если поля адреса заполнены корректно, на карте отображаются точки А и В. Если поле «Откуда» заполнено некорректно, точка А не отображается. Если поле «Куда» заполнено некорректно, точка В не отображается. При некорректном значении поле подсвечивается красным; появляется сообщение об ошибке.

Примеры тестовых адресов есть в таблице.

**Режим «Оптимальный» и «Быстрый»**

Если выбрать режим «Оптимальный» или «Быстрый», система автоматически назначит вид транспорта; построится маршрут; отобразится время и стоимость поездки. Выбрать транспорт в этих режимах нельзя — панель видов транспорта неактивна.

**Режим «Свой»**

Если выбрать режим «Свой», панель видов транспорта активна — можно переключать. Под каждый вид транспорта строится маршрут; рассчитывается время и стоимость поездки.

Если сменить вид транспорта или поменять значение в любом поле, маршрут перестроится; время и стоимость поездки пересчитается.

**Ограничения**

Элементы системы | Требования
:----------------|:-----------
Поле ввода часов | Формат 24 часа. Нули перед однозначным числом обязательны. Корректны только целые числа от 0 до 23 включительно. При некорректном вводе подсвечивается красным, ошибка «Вы ввели некорректное время».
Поле ввода минут | Только целые числа. Нули перед однозначным числом обязательны. При некорректном вводе подсвечивается красным, ошибка «Вы ввели некорректное время».
Поле ввода адреса | Только русские буквы, цифры, пробел, тире, точка, запятая. Длина не более 50 символов. Пробелы до и после адреса удаляются при снятии фокуса. При некорректном вводе подсвечивается красным, ошибка «Вы ввели некорректный адрес».
Переключатели режима | Оптимальный, Быстрый и Свой. Состояние каждого переключателя — активен, выбран.
Переключатели видов транспорта | Пешком, самокат, велосипед, каршеринг, такси, собственный автомобиль. Состояние каждого переключателя — активен, неактивен, выбран.

**Макеты**

![Интерфейс](https://code.s3.yandex.net/qa/schemes/project-interface-fast.png)

![Сообщения об ошибках](https://code.s3.yandex.net/qa/schemes/project-interface-error.png)

**Логика расчёта**

Система получает данные о начале поездки, точке А и точке В. После этого рассчитывает продолжительность и стоимость поездки по определённому алгоритму.

![Логика расчёта](https://code.s3.yandex.net/qa/schemes/project-logics-2.png)

Расстояние, скорость и стоимость за минуту или километр можно получить из таблиц. Этих данных достаточно, чтобы рассчитать время и стоимость поездки для каждого вида транспорта.

Вид транспорта | Как расчитать время | Стоимость на км
:-------|:-----------|:----------
Пешком | Средняя скорость 4 км/ч | 0 р / км
Шеринг самокатов | Средняя скорость | 10 км/ч | 5,5 р / км
Шеринг велосипедов | Средняя скорость | 12 км/ч | 3 р / км
Каршеринг | см. Таблицу «Средняя скорость автомобиля» | 9 р / мин
Такси | см. Таблицу «Средняя скорость такси» | 11 р / мин
Собственное авто | см. Таблицу «Средняя скорость автомобиля» | 20 р / км

Средняя скорость автомобиля

Время суток | Средняя скорость автомобиля
:----------|:----------|
|00\:01-08:00 | 45 км/ч
|08\:01-12:00 | 30 км/ч
|12\:01-18:00 | 40 км/ч
|18\:01-22:00 | 25 км/ч
|22\:01-00:00 | 45 км/ч

Средняя скорость такси с учётом движения по выделенным полосам

Время суток | Средняя скорость такси
:----------|:----------|
|00\:01-08:00 | 50 км/ч
|08\:01-12:00 | 35 км/ч
|12\:01-18:00 | 42 км/ч
|18\:01-22:00 | 30 км/ч
|22\:01-00:00 | 50 км/ч

Матрица расстояний между адресами для автомобильных дорог, в километрах

Адрес | Усачева, 3 | Комсомольский проспект, 18 | Зубовский бульвар, 37 | М. Пироговская, 25 | Хамовнический Вал, 34 | Фрунзенская набережная, 46 | 3-я Фрунзенская улица, 12
:---|:---|:---|:---|:---|:---|:---|:---|
Усачева, 3 | 0 | 1,4 | 1,5 | 0,89 | 2,6 | 2,6 | 2,6
Комсомольский проспект, 18 | 1,4 | 0 | 2,9 | 2,3 | 2,3 | 2,3 | 2,3
Зубовский бульвар, 37 | 1,4 | 1,5 | 0 | 1,9 | 3,8 | 3 | 3,3
М. Пироговская, 25 | 1,5 | 3 | 2,4 | 0 | 1,2 | 3,4 | 2,3
Хамовнический Вал, 34 | 1,5 | 3,7 | 3,7 | 1,2 | 0 | 1,7 | 1,7
Фрунзенская набережная, 46 | 3,2 | 3,9 | 4,7 | 2,7 | 1,7 | 0 | 2,2
3-я Фрунзенская улица, 12 | 1,4 | 2,4 | 3,5 | 2,3 | 1,4 | 1,3 | 0

Матрица расстояний между адресами для пешеходов, в километрах

Адрес | Усачёва, 3 | Комсомольский проспект, 18 | Зубовский бульвар, 37 | М. Пироговская, 25 | Хамовнический Вал, 34 | Фрунзенская набережная, 46 | 3-я Фрунзенская улица, 12
:---|:---|:---|:---|:---|:---|:---|:---|
Усачёва, 3 | 0 | 0,96 | 1,4 | 0,91 | 1,4 | 1,7 | 1,1
Комсомольский проспект, 18 | 1 | 0 | 1,3 | 1,9 | 2 | 1,7 | 1,2
Зубовский бульвар, 37 | 1,4 | 1,3 | 0 | 1,9 | 2,7 | 2,7 | 2,3
М. Пироговская, 25 | 0,91 | 1,9 | 1,9 | 0 | 0,75 | 1,5 | 1,2
Хамовнический Вал, 34 | 1,4 | 2 | 2,7 | 0,75 | 0 | 1,4 | 1,2
Фрунзенская набережная, 46 | 1,7 | 1,7 | 2,7 | 1,5 | 1,4 | 0 | 0,57
3-я Фрунзенская улица, 12 | 1,1 | 1,2 | 2,3 | 1,2 | 1,2 | 0,57 | 0

Обрати внимание: для подсчёта времени и стоимости маршрута тебе доступны таблицы со скоростью движения разных видов транспорта. Они показывают скорость движения автомобиля в разное время суток. Если ты берёшь такие тестовые значения, что поездка захватывает несколько временных интервалов, алгоритм выбирает скорость автомобиля из того диапазона, в котором поездка началась.

![Временные интервалы](https://code.s3.yandex.net/qa/schemes/time-intervals.png)

***



</details>


**1. Ассоциативная карта**

![Mindmap]

[Ассоциативная карта в большом разрешении]![mindmap 1 1 спринт 1 правка](https://user-images.githubusercontent.com/126310621/222410215-1a63bdbd-d08d-49bf-9389-7b01f7e19c6c.jpg)


**2. Классы эквивалентности и граничные значения**

<details>
<summary>Поле ввода часов</summary>

***
<img width="453" alt="Сприн первый полле ввода часов" src="https://user-images.githubusercontent.com/126310621/222412163-f5515770-5c15-4deb-ad7c-6d6a6d19ceab.png">




*Курсивом* выделены повторяющиеся проверки, ~~зачёркнутые~~ значения - оптимизация проверок

***

</details>

<details>
<summary>Поле ввода минут</summary>
<img width="450" alt="спринт 1 поле ввода минут " src="https://user-images.githubusercontent.com/126310621/222413065-1ef3abdc-bde1-42eb-8f60-8dc9d90d6457.png">



*Курсивом* выделены повторяющиеся проверки, ~~зачёркнутые~~ значения - оптимизация проверок

***

</details>

<details>
<summary>Поля ввода адреса (Откуда, Куда)</summary>
<img width="451" alt="Спринт 1 поле ввода откуда " src="https://user-images.githubusercontent.com/126310621/222413121-34797be9-06d3-4977-a876-55f25a491a6d.png">
<img width="451" alt="Спринт 1 поле ввода куда " src="https://user-images.githubusercontent.com/126310621/222413143-40e2a648-4882-4164-bd76-da3390d9b1ff.png">

          

*Курсивом* выделены повторяющиеся проверки, ~~зачёркнутые~~ значения - оптимизация проверок

***

</details>

[Наверх](#up)

### Задание 2

**1. Спроектируй тесты расчёта времени и стоимости**

Выбери один вид транспорта для тестирования: собственный автомобиль, каршеринг или такси.

- Определи, какие требования описывают логику расчёта времени и стоимости выбранного транспорта.
- Напиши формулу, по которой рассчитывается время и стоимость поездки.
- Нарисуй блок-схему, которая визуализирует алгоритм выбора скорости транспорта в зависимости от времени начала поездки.
- Определи классы эквивалентности. И граничные значения каждого класса, к которому это применимо.
- Выбери тестовые значения, которые проверят каждый класс; и границы, если они есть.
- Напиши тест-кейсы на основе тестовых значений. Тест-кейсы должны проверять корректность логики расчёта.

**2. Напиши выводы**

Поразмышляй о результатах первого спринта:
- Как ты думаешь, какую часть функциональности удалось покрыть тестами?
- Как ты думаешь, какие новые навыки позволили тебе выполнить проект?

### Решение

> Выбери один вид транспорта для тестирования: собственный автомобиль, каршеринг или такси.

Такси 

> Определи, какие требования описывают логику расчёта времени и стоимости выбранного транспорта.

Поля "Начало поездки", "Откуда", "Куда"<br>
Переключатель режима ("Свой")<br>
Переключатель вида транспорта (Такси")<br>
Средняя скорость автомобиля в зависимости от времени суток<br>
Стоимость на км<br>
Расстояние между адресами для автомобильных дорог

> Напиши формулу, по которой рассчитывается время и стоимость поездки.

Время поездки = расстояние / скорость * 60<br>
Стоимость поездки = расстояние * стоимость 1 км

> Нарисуй блок-схему, которая визуализирует алгоритм выбора скорости транспорта в зависимости от времени начала поездки.

![Блок-схема]<img width="659" alt="блок схема спринт первый" src="https://user-images.githubusercontent.com/126310621/222664802-cbc1c682-9118-4370-a8aa-e6389ef4b566.png">




В соответствии с требованиями, если поездка захватывает несколько временных интервалов, алгоритм выбирает скорость автомобиля из того диапазона, в котором поездка началась. Так как для алгоритма выбора скорости транспорта время окончания поездки, которое зависит от расстояния между адресами, несущественно, в блок-схему не был добавлен ввод адресов Откуда и Куда, а также расчёт времени и стоимости поездки.

> Определи классы эквивалентности. И граничные значения каждого класса, к которому это применимо. Выбери тестовые значения, которые проверят каждый класс; и границы, если они есть.

Время начала поездки



> Напиши тест-кейсы на основе тестовых значений. Тест-кейсы должны проверять корректность логики расчёта.

Расчёт времени и стоимости поездки на своём автомобиле:

**Входные данные**:<br>
&nbsp;&nbsp;&nbsp;Время начала поездки <br>
&nbsp;&nbsp;&nbsp;Точка А (Откуда): ул. Усачёва, 3<br>
&nbsp;&nbsp;&nbsp;Точка Б (Куда): Зубовский бульвар, 37

**Расчёт**:<br>
&nbsp;&nbsp;&nbsp;Время поездки, формула: расстояние (1,5 км) / средняя скорость автомобиля * 60<br>
&nbsp;&nbsp;&nbsp;Стоимость поездки, формула: расстояние (1,5 км) * стоимость 1 км (20 руб.)

**Выходные данные**:<br>
&nbsp;&nbsp;&nbsp;Время в пути<br>
&nbsp;&nbsp;&nbsp;Стоимость поездки

**Тест-кейсы**



<details>
<summary>ID-003: Расчёт времени и стоимости поездки на Такси (начало поездки в 00:01)</summary>
<img width="717" alt="00 01 0800" src="https://user-images.githubusercontent.com/126310621/222668871-4de36a70-7e5d-4852-8fe5-b6b2dfbecebe.png">



</details>

<details>
<summary>ID-004: Расчёт времени и стоимости поездки на Такси (начало поездки в 08:01)</summary>
<img width="717" alt="08 01 12 00" src="https://user-images.githubusercontent.com/126310621/222668906-1f92d937-0d41-47fe-a955-f23058300e70.png">





</details>

<details>
<summary>ID-005: Расчёт времени и стоимости поездки на Такси (начало поездки в 12:01)</summary>
<img width="718" alt="12 01 18 00" src="https://user-images.githubusercontent.com/126310621/222668934-669b1fa0-0a8c-46d0-8550-f3b8ceb9e5e1.png">



</details>

<details>
<summary>ID-006: Расчёт времени и стоимости поездки на Такси (начало поездки в 18:01)</summary>

<img width="716" alt="1801 2200" src="https://user-images.githubusercontent.com/126310621/222668972-20c0370f-57eb-402c-861c-42854ea118c4.png">


</details>

<details>
<summary>ID-007: Расчёт времени и стоимости поездки на Такси (начало поездки в 22:01)</summary>
<img width="716" alt="22 01 00 00 " src="https://user-images.githubusercontent.com/126310621/222668993-8f6ff636-a662-4f0d-83d2-a6e49bc118c1.png">



</details>

<details>
<summary>ID-008: Расчёт времени и стоимости поездки на Такси (время поездки = 0)</summary>
<img width="720" alt="=0" src="https://user-images.githubusercontent.com/126310621/222669036-ec799700-50f7-41ce-8078-24b461a0b0ad.png">


</details>



> Как ты думаешь, какую часть функциональности удалось покрыть тестами?

Фактически тестами покрыта только часть основной функциональности – логика расчёта времени и стоимости поездки на собственном автомобиле. Также подготовлены данные для составления тест-кейсов, проверяющих ввод полей времени и адресов.

Осталось подготовить данные и написать тест-кейсы для тестирования логики расчёта времени/стоимости других видов транспорта и способов передвижения: каршеринг, такси, велосипед, самокат, пешком; переключателей режимов и видов транспорта; отображения данных на карте; масштабирования карты; остальных элементов интерфейса: шапки, подвала.

> Как ты думаешь, какие навыки позволили тебе выполнить проект?

Навыки тест-анализа: анализ и декомпозиция требований, составление ассоциативных карт и блок-схем.

Навыки тест-дизайна: выделение объектов и элементов тестирования, классов эквивалентности, подбор тестовых и граничных значений, оптимизация проверок.

Навыки написания тестовой документации: составление чек-листов и тест-кейсов.

## <a name="web-testing" />Тестирование веб-приложений

### Задание

**1. Анализ требований**

Изучи обновлённые требования к сервису Яндекс.Маршруты. Команда успела сделать первую версию продукта.

**2. Выбор конфигураций для кроссбраузерного тестирования**

Выбери операционные системы, браузеры и разрешения, в которых нужно провести тесты. В этой задаче примени парное тестирование, чтобы уменьшить количество комбинаций. Поддерживаемые ОС, браузеры и разрешения описаны в требованиях.

**3. Тестовая документация для вёрстки**

- Проанализируй требования к вёрстке и определи объекты тестирования: это все визуальные элементы на макете, у которых нужно проверить внешний вид и корректное расположение.
- Напиши чек-лист, чтобы протестировать вёрстку. Не забудь проверить: соответствие макетам (визуально — не «пиксель в пиксель»); как отображается результат расчёта стоимости и времени маршрута при длинных значениях; орфографию.

Напиши чек-лист в таблице «Чек-лист и результаты выполнения тестов: тестирование вёрстки и логики интерфейса».

**4. Тестовая документация для логики интерфейса**

Проанализируй требования к логике интерфейса и составь тестовую документацию.

- Напиши тест-кейсы на отображение результата расчёта стоимости и времени по всем видам транспорта. Чтобы составить тесты на отображение результатов, применяй технику «Таблица принятия решений». В тестировании используй только адреса из таблицы в уроке «Требования».

Важно: разработчики ещё не до конца реализовали расчёт стоимости поездки на бэкенде, поэтому логика расчёта суммы и времени может быть некорректной. Её тестировать не нужно.

- Составь чек-листы, которые помогут протестировать: отрисовку и скрытие точек на карте; отрисовку и скрытие маршрута на карте; масштабирование карты; перемещение карты. В требованиях есть ограниченный список адресов — тестировать можно только по ним.

Дополни чек-лист из задания 3. Оформи тест-кейсы в таблице «Тест-кейсы: логика интерфейса».

**5. Тестирование и заведение баг-репортов**

Протестируй сервис [Яндекс.Маршруты](https://qa-routes.praktikum-services.ru/).

У тебя уже есть набор конфигураций, в которых нужно проверить сервис. Но на тестирование осталось не так много времени, поэтому протестируй сервис на ограниченном наборе: в твоей текущей операционной системе в Яндекс.Браузере при разрешении экрана 800x600, а в Firefox — при 1280х720.

Чтобы проверить длинные строки в интерфейсе, примени DevTools — в нём можно заменить HTML; или Fiddler/Charles — в них можно изменить ответ от сервера.

В процессе тестирования отмечай результаты выполнения теста: PASSED или FAILED. Если тест со статусом FAILED, заведи баг-репорт в Яндекс.Трекере в очереди BUG и вписывай ID в соответствующую таблицу результатов.

Тестирование вёрстки нужно провести в обоих окружениях. Тесты на логику интерфейса можно сделать только в одном разрешении. В отчёте поставь статус N/A (Not Applicable, не применимо) около такого теста.

**6. Подведение итогов**

Представь, что тебе нужно рассказать команде о статусе протестированной части продукта:

- Какое впечатление оставил у тебя сервис как у пользователя?
- Расскажи, что именно тебе удалось протестировать в нескольких предложениях.
- Подведи итоги тестирования: например, тебе удалось провести все тесты и найти несколько багов. Приложи ссылки на них, чтобы коллеги могли их быстро открыть и посмотреть.
- Сделай вывод: как ты думаешь, можно ли отдать такой продукт пользователям, или его нужно доработать. Помни, тестировщик даёт рекомендации, а итоговое решение принимает команда менеджеров.

<details>
<summary>Требования 2.0</summary>


|Пользователю нужно открыть Яндекс.Маршруты и корректно заполнить поля «Откуда» и «Куда». Приложение построит маршрут, а под полями «Откуда» и «Куда» отобразятся режимы поездки: «Оптимальный», «Быстрый», «Свой».|
|:----|
|- Если выбрать режим «Оптимальный» или «Быстрый», система автоматически назначит способ передвижения: на авто, пешком, на такси, на самокате, на велосипеде, на каршеринге. Выбрать его самостоятельно нельзя — иконки неактивны.|
|- Если выбрать режим «Свой», способ передвижения можно поменять — иконки активны.|
|## Аренда машины|
|Арендовать машину можно в двух случаях:- Если приложение предлагает тип транспорта «Кар|
|шеринг» в режиме «Оптимальный» или «Быстрый».|
|- Если пользователь выбирает тип транспорта «Каршеринг» в режиме «Свой».|
|Под названиями режимов появится информация о стоимости и продолжительности поездки, а также кнопка «Забронировать».|


</details>
