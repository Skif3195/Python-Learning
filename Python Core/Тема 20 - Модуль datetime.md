# Модуль datetime

- `[ datetime ]` - Модуль стандартной библиотеки Python, предоставляет предоставляет классы для работы с датами и временем:
    
   - `[ date ]` - предоставляет функционал для работы с датой (год, месяц и ден), без учета времени.
   - `[ time ]` - предоставляет функционал для работы с временем (часы, минуты, секунды и микросекунды), без учета даты.
   - `[ datetime ]` - Комбинирует информацию о дате и времени в один объект. Содержит атрибуты для года, месяца, дня, часов, минут, секунд и микросекунд.
   - `[ timedelta ]` - предоставляет функционал для работы с временными интервалами. Используется для арифметических операций с датами и временем.
   - `[ tzinfo ]` - Абстрактный базовый класс, предоставляющий интерфейс для временных зон.
   - `[ timezone ]` - Конкретная реализация tzinfo, представляющая постоянное смещение относительно UTC.
#
### Для использовния модуля, его нужно импортировать
 1) `[import datetime]` - импортирует модуль целиком. В таком случае, перед использованием конкретной функции требуется явное указание модуля `[datetime]`.
 2) `[from datetime import n]` - импорт одной конкретной функции `[n]` из модуля `[random]`. В этом случае, перед использованием функции не требуется явное указание модуля `[datetime]`.
 3) `[from datetime import *]` - импорт всех функций модуля. Эквиволентен первому способу, но в этом случае перед использованием функции не требуется явное указание модуля `[datetime]`.
 4) `[as]` - ключевое слово, используется для установки псевдонима модуля или функции. `[import datetime as dt]` или `[from datetime import time as t]`
#
<details>
  <summary>Класс date</summary> 

 #
- `[date]` - используется для представления данных о дате и включает информацию о годе, месяце и дне.  
Синтаксис:
```
[my_date = date(YYYY,MM,DD)]
```
#
- Для использования необходимо предварительно его импортировать из модуля datetime:
```
from datetime import date
```
#
- По умолчанию объекты типов date выводятся в ISO 8601 формате:
```
Дата в формате ISO 8601 имеет вид: YYYY-MM-DD
```
#
- При создании объекта типа `[date]` нужно указать год, месяц и день.
```
from datetime import date

my_date = date(1992, 10, 6)    # тип date: год + месяц + день

print(my_date)        # 1992-10-06
print(type(my_date))  # <class 'datetime.date'>
```
#
- `[date]` - неизменяемый тип данных
#
- `[Атрибуты класса]` - для работы с отдельно взятой информацией о дате (день, месяц, год) допускается работа с атрибутами:
    - my_date.year -> выведет только год
    - my_date.month -> выведет только месяц
    - my_date.day -> выведет только день
#
- Ограничения атрибутов:
```
0 < year < 9999
0 < month < 12
0 < day < 31 (30/28)
```
#
- Объекты типа `[date]` можно сравнивать между собой (`[>]`, `[<]`, `[>=]`, `[<=]`, `[==]`, `[!=]`)
- К объектам типа `[date]` допускается применение встроенных функций `[min()]`, `[max()]` и `[sorted()]`
#
<details>
  <summary>Методы класса date</summary> 

#
### 1) `[date.today()]` - предоставляет текущую дату и время.
```
from datetime import date

today = date.today()
print(f"Текущая дата: {today}")
```
#
### 2) `[weekday()]` - возвращает номер дня недели для объекта date, где понедельник имеет индекс 0, а воскресенье 6.
```
from datetime import date

# Создаем объект date
some_date = date(2023, 5, 15)

# Получаем номер дня недели (0 - понедельник, 1 - вторник и так далее)
day_of_week = some_date.weekday()

print(f"Номер дня недели для {some_date}: {day_of_week}")   # Номер дня недели для 2023-05-15: 0
```
#
### 3) `[isoweekday()]` - возвращает номер дня недели для объекта date, где понедельник имеет индекс 1, а воскресенье 7.
```
from datetime import date

# Создаем объект date
some_date = date(2023, 5, 15)

# Получаем номер дня недели (1 - понедельник, 2 - вторник и так далее)
iso_day_of_week = some_date.isoweekday()

print(f"ISO номер дня недели для {some_date}: {iso_day_of_week}")   # ISO номер дня недели для 2023-05-15: 1
```
#
### 4) `[str()]` - переводит дату к строковому типу.
#
### 5) `[repr()]` - возвращает строковое значение даты, в виде, понятном интерпретатору.
```
from datetime import date

# Создаем объект date
some_date = date(2023, 5, 15)

# Получаем строковое представление объекта date с помощью repr()
date_repr = repr(some_date)

print(date_repr)           # datetime.date(2023, 5, 15)
print(type(date_repr))     # <class 'str'>
```
#
### 6) `[toordinal()]` - возвращает количество дней, прошедших с начала григорианского календаря, начиная с 1 января 1 года (1 AD) и заканчивая днем перед заданной датой объекта date.
```
from datetime import date

# Создаем объект date
some_date = date(2024, 1, 6)

# Получаем количество дней с начала григорианского календаря
ordinal_value = some_date.toordinal()

print(f"Количество дней с начала григорианского календаря для {some_date}: {ordinal_value}") # Количество дней с начала григорианского календаря для 2024-01-06: 738891
```
#
### 7) `[date.fromordinal()]` - возвращает объект date на основе значения, представляющего количество дней, прошедших с начала григорианского календаря.
```
from datetime import date

# Получаем количество дней с начала григорианского календаря
ordinal_value = 737961  # Замени это значением, полученным из toordinal()

# Создаем объект date из значения ordinal
some_date = date.fromordinal(ordinal_value)

print(f"Дата, восстановленная из значения {ordinal_value}: {some_date}")   # Дата, восстановленная из значения 737961: 2021-06-20
```
#
### 8) `[replace()]` - метод, возвращает новую дату с переданными измененными значениями свойств year, month, day.
```
from datetime import date

date1 = date(1992, 10, 6)
date2 = date1.replace(year=1995)            # заменяем год           
date3 = date1.replace(month=12, day=17)     # заменяем месяц и число

print(date1)   # 1992-10-06
print(date2)   # 1995-10-06
print(date3)   # 1992-12-17
```
</details>

#

</details>









#

<details>
  <summary>Класс time</summary> 

#
- `[time]` - используется для представления данных о времени и включает информацию о часах, минутах, секундах и микросекундах. Данный тип данных полностью игнорирует информацию о дате.  
Синтаксис:
```
[my_time = time(hh, mm, ss, ffffff)]
```
#
- Для использования необходимо предварительно его импортировать из модуля datetime:
```
from datetime import time
```
#
- При создании времени (тип данных time) нужно указать часы, минуты, секунды и микросекунды.
```
from datetime import time

my_time = time(11, 20, 54, 1234)    # тип time: часы + минуты + секунды + микросекунды

print(my_time)         # 11:20:54.001234
print(type(my_time))   # <class 'datetime.time'>
```
- Прии этом, не обязательно использование всех четырёх атрибутов сразу.
#
- `[date]` - неизменяемый тип данных
#
- По умолчанию объекты типов time выводятся в ISO 8601 формате:
```
Время в формате ISO 8601 имеет вид: HH:MM:SS или HH:MM:SS.ffffff
```
#
- `[Атрибуты класса]` - для работы с отдельно взятой информацией о времени (часы, минуты, секунды, микросекунды) допускается работа с атрибутами:
    - my_time.hour -> выведет только час
    - my_time.minute -> выведет только минуты
    - my_time.second -> выведет только секонды
    - my_time.microsecond -> выведет только микросекунды
#
- Ограничения атрибутов:
```
0 < hour < 24
0 < minute < 60
0 < second < 60
0 < microsecond < 1_000_000
```
#
- Объекты типа `[time]` можно сравнивать между собой (`[>]`, `[<]`, `[>=]`, `[<=]`, `[==]`, `[!=]`)
- К объектам типа `[time]` допускается применение встроенных функций `[min()]`, `[max()]` и `[sorted()]`
#
<details>
  <summary>Методы класса time</summary> 
    
 #
### 1) `[str()]` - функция, переводит объект типа `[time]` к строковому типу.
 #
### 2) `[repr]` - возвращает строковое значение времени, в виде, понятном интерпретатору.
```
from datetime import time

# Создаем объект date
some_time = time(12, 54, 25)

repr_time = repr(some_time)

print(repr_time)         # datetime.time(12, 54)
print(type(repr_time))   # <class 'str'>
```
#
### 3) `[replace()]` - метод, возвращает новое с переданными измененными значениями свойств hour, minute, second, microsecond.
```
from datetime import time

time1 = time(17, 10, 6)
time2 = time1.replace(hour=21)                  # заменяем час         
time3 = time1.replace(minute=48, second=59)     # заменяем минуты и секунды

print(time1)   # 17:10:06
print(time2)   # 21:10:06
print(time3)   # 17:48:59
```
</details>

#

</details>












#

<details>
  <summary>Класс datetime</summary> 

 #
- `[datetime]` - используется для представления данных о дате и времени и включает информацию о годе, месяце, дне, часах, минутах, секундах и микросекундах.   
Синтаксис:
```
[my_datetime = datetime(YYYY, MM, DD, hh, mm, ss, ffffff)]
```
#
- Для использования необходимо предварительно его импортировать из модуля datetime:
```
from datetime import datetime
```
#
- При создании объекта типа `[datetime]` указываются год, месяц, день, часы, минуты, секунды и микросекунды.
- Обязательно указание даты
- Не обязательно указание врени
```
from datetime import datetime

# Ручное создание объекта datetime
my_datetime = datetime(2023, 5, 15, 14, 30, 0)

print(my_datetime)         # 2023-05-15 14:30:00
print(type(my_datetime))   # <class 'datetime.datetime'>
```
#
- `[datetime]` - неизменяемый тип данных
#
- По умолчанию объекты типов `[datetime]` выводятся в ISO 8601 формате:
```
ДатаВремя в формате ISO 8601 имеет вид: YYYY-MM-DD HH:MM:SS.ffffff
```
#
- `[Атрибуты класса]` - для работы с отдельно взятой информацией о времени (часы, минуты, секунды, микросекунды) допускается работа с атрибутами:
    - my_datetime.year -> Вывыдет только год
    - my_datetime.moonth -> Выведет только месяц
    - my_datetime.day -> Выведет только день
    - my_datetime.hour -> выведет только час
    - my_datetime.minute -> выведет только минуты
    - my_datetime.second -> выведет только секонды
    - my_datetime.microsecond -> выведет только микросекунды
#
- Ограничения атрибутов:
```
0 < year < 9999
0 < month < 12
0 < day < 31 (30/28)
0 < hour < 24
0 < minute < 60
0 < second < 60
0 < microsecond < 1_000_000
```
#
- Объекты типа `[datetime]` можно сравнивать между собой (`[>]`, `[<]`, `[>=]`, `[<=]`, `[==]`, `[!=]`)
- К объектам типа `[datetime]` допускается применение встроенных функций `[min()]`, `[max()]` и `[sorted()]`
#
<details>
  <summary>Методы класса datetime</summary> 

#
### `[datetime]` - наследует атрибуты и методы класса `[date]`
#
### 1) `[datetime.now()]` - это метод, который возвращает объект datetime, представляющий текущую локальную дату и время.
```
from datetime import datetime

# Получаем текущую дату и время
current_datetime = datetime.now()

# Выводим результат
print("Текущая дата и время:", current_datetime)
```
#
### 2) `[datetime.combaine(date, time)]` - создаёт объект datetime из двух объектов - даты (date) и времени (time).
```
from datetime import datetime, date, time

# Создаем объекты date и time
my_date = date(2024, 1, 7)
my_time = time(14, 30, 0)

# Создаем новый объект datetime, объединив date и time
my_datetime = datetime.combine(my_date, my_time)

# Выводим результат
print("Объединенный datetime:", my_datetime)   # Объединенный datetime: 2024-01-07 14:30:00
```
#
### 3) `[my_datetime.date()]` - это метод объекта datetime, который возвращает объект date, представляющий только дату (год, месяц, день) без времени.
```
from datetime import datetime

# Создаем объект datetime
my_datetime = datetime(2024, 1, 7, 14, 30, 0)

# Получаем только дату
date_only = my_datetime.date()

# Выводим результат
print("Дата только:", date_only)   # Дата только: 2024-01-07
print(type(date_only))             # <class 'datetime.date'>
```
#
### 4) `[my_datetime.time()]` - это метод объекта datetime, который возвращает объект time, представляющий только время (часы, минуты, секунды, микросекунды) без даты.
```
from datetime import datetime

# Создаем объект datetime
my_datetime = datetime(2024, 1, 7, 14, 30, 0)

# Получаем только время
time_only = my_datetime.time()

# Выводим результат
print("Время только:", time_only)   # Время только: 14:30:00
print(type(time_only))              # <class 'datetime.time'>
```
#
### 5) `[my_datetime.timestamp()]` - это метод объекта datetime, который возвращает количество секунд с начала эпохи (1 января 1970 года) до указанного момента времени.
```
from datetime import datetime

# Создаем объект datetime
my_datetime = datetime(2024, 1, 7, 14, 30, 0)

# Получаем временную метку (timestamp)
timestamp_value = my_datetime.timestamp()

# Выводим результат
print("Кол-во секунд с начала эпохи:", timestamp_value)   # Кол-во секунд с начала эпохи: 1704601800.0
```
#
### 6) `[my_datetime.fromtimestamp()]` - создает объект datetime из переданной временной метки (timestamp), представляющей количество секунд с начала эпохи (1 января 1970 года).
```
from datetime import datetime

# Пример временной метки
timestamp_value = 1641534600

# Создаем объект datetime из временной метки
my_datetime = datetime.fromtimestamp(timestamp_value)

# Выводим результат
print("Datetime из временной метки:", my_datetime)   # Datetime из временной метки: 2022-01-07 15:50:00
```
#
### 6) `[datetime.strptime('str', 'format')]` - метод класса datetime, преобразует строку в объект datetime с использованием заданного формата.
```
from datetime import datetime

# Пример строки
date_string = '07/01/2024'

# Задаем формат строки
format_string = '%d/%m/%Y'

# Преобразуем строку в datetime
converted_datetime = datetime.strptime(date_string, format_string)

# Выводим результат
print("Преобразованный datetime:", converted_datetime)   # Преобразованный datetime: 2024-01-07 00:00:00
print(type(converted_datetime))                          # <class 'datetime.datetime'>
```
#
### 6) `[my_datetime.strftime('formate')]` - метод объекта datetime, форматирует объект datetime в строку в соответствии с заданным форматом.
```
from datetime import datetime

# Создаем объект datetime
my_datetime = datetime(2024, 1, 7, 14, 30, 0)

# Форматируем datetime в строку
formatted_string = my_datetime.strftime('%Y-%m-%d %H:%M:%S')

# Выводим результат
print("Форматированная строка:", formatted_string)   # Форматированная строка: 2024-01-07 14:30:00
print(type(formatted_string))                        # <class 'str'>
```

</details>

#

</details>









#

<details>
  <summary>Класс timedelta</summary> 

# 
### `[timedelta]` - класс модуля `[datetime]` является вспомогательным инструментом для работы с арифметикой между объектами datetime. Он позволяет вычислять разницу между двумя датами и выполнять арифметические операции с временными интервалами.  

Основные задачи timedelta включают в себя:
   - Вычисление разницы между двумя датами или временными метками. `(datetime - datetime = timedelta)`
   - Арифметические операции с временными интервалами, такие как сложение и вычитание. `(datetime + timedelta = datetime)`
#
- Cинтаксис:
```
timedelta(weeks=0, days=0, hours=0, minutes=0, seconds=0, milliseconds=0, microseconds=0)
```
#
### Особенности:

- Под капотом `[timedelta]` оперирует информацией в формате дни/секунды/микросекунды. Такой формат представления времени более понятен для компьютера.
- На вывод `[timedelta]` выдаёт информацию в формате дни, часы, минуты, секунды, микросекунды. Такой формат легче читать и понимать, что упрощает работу с временными интервалами в коде.
- `[timedelta]` использует именные аргументы (`timedelta(weeks=0, days=0, hours=0, minutes=0, seconds=0, milliseconds=0, microseconds=0)`)
- Допустима работа с отдельными атрибутами (`days, seconds, microseconds`)

- `[timedelta]` поддерживает математические операции:
   - Сложение и вычитание объектов `[timedelta]` между собой
   - Умножение и деление объектов `[timedelta]` на число
   - Деление `[timedelta]` на `[timedelta]`
   - Сложение (+) и вычитание (-) из объектов datetime, date и time (используя соответствующие атрибуты)

- `[timedelta]` можно сравнивать между собой (`==, !=, <, >, <=, >=`)
#
### `[my_timedelta.total_seconds()]` - возвращает общее кол-во секунд в объекте `[timedelta]`
#
- У типа `[timedelta]` нет атрибутов `hours` и `minutes`, позволяющих получить количество часов и минут соответственно. Достать часы и минуты можно вручную:
```
from datetime import datetime, timedelta

# Создадим объект timedelta
delta = timedelta(days=7, seconds=125, minutes=10, hours=8, weeks=2)

# Что бы получить часы, Выведем секунды из объекта timedelta и разделим на цело на 3600
total_hours = delta.seconds // 3600
print(total_hours)   # 8

# Что бы получить минуты, Выведем секунды из объекта timedelta и разделим на цело на 60 и разделим по модулю на 60
total_minutes = (delta.seconds //60) % 60
print(total_minutes)   # 12
```


</details>

#










#

<details>
  <summary>Форматирование даты и времени</summary> 
 
</details>

#











