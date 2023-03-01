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

|Группа проверок|Название класса|Границы|Тестовые данные внутри класса (содержимое поля)|Тестовые данные на границах (содержимое поля)|Пояснение и оптимизации|
|:----|:----|:----|:----|:----|:----|
| |число символов 1-2|диапазон| 2 символа - 15|1 символ - 32 символа - 13
0 символов - пустой ввод
2 символа - 15
3 символа - 1661 символа - 5|Проверяем тут так же заполненость поля|Число симоволов 0|диапазон|0 символов  - пустой ввод |0 символов  - пустой ввод1 символа - 2| |
| |Число симоволов >=3|диапазон|7 символа - 1230567|3 символа - 123
2 символа - 11
4 символа -1412| |
| |Водимые  цифры от 0 до 23|диапазон|10|0. 



