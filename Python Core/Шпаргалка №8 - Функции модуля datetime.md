# Шпаргалка №8 - Функции модуля datetime

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

#

<details>
  <summary>Строку в datetime</summary>
  
### `[datetime.strptime('str', 'format')]` - метод класса datetime, преобразует строку в объект datetime с использованием заданного формата.
- Какой разделитель в строке, такой должен быть и в методе
- По автомату метод strptime переводит дату-время к формату ISO 8601
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
</details>

#

<details>
  <summary>datetime в строку</summary>
  
### `[my_datetime.strftime('formate')]` - метод объекта datetime, форматирует объект datetime в строку в соответствии с заданным форматом.
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

<details>
  <summary>Таблица Форматирования</summary>

#
```
1) `[%f]` - Число микросекунд (000_000 - 999_999)
2) `[%S]` - Число секунд (00-59)
3) `[%M]` - Число минут (00-59)
4) `[%I]` - Час 12-часовой формат (01-12) 
5) `[%H]` - Час 24-часовой формат (00-23) 
6) `[%p]` - до/послее полудня при 12-часовом формате (AM/PM)
7) `[%a]` - Сокращенное название дня недели (Sun, Пн) 
8) `[%A]` - Полное название дня недели (Sunday, Понедельник) 
9) `[%w]` - Номер дня недели (Вс - 0, Сб - 6)
10) `[%d]` - Номер дня месяца (01 - 31)
11) `[%b]` - Сокращенное название месяца (Jan, Feb / Янв, Февр)
12) `[%B]` - Полное название месяца (January / Январь) 
13) `[%m]` - Номер месяца (01 - 12)
14) `[%y]` - Год без века (00 - 99)
15) `[%Y]` - Год с веком (0001, 00033, 2023) (в Linux без нулей впереди 1, 33, 2023) 
16) `[%z]` - Разница с UTC формате +/-HHMM[ss[ffffff]] (+0000, -0400)
17) `[%Z]` - Временная зона (UTC, EST, CST)
18) `[%j]` - Номер дня года (001 -365)
19) `[%U]` - Номер недели в году. Нулевая неделя начинается с первого воскресенья года. (00 - 53)
20) `[%W]` - Номер недели в году. Нулевая неделя начинается с первого понедельника года. (00 - 53)
21) `[%c]` - Дата и время (Tue Aug 16 21:30:00 1988 (en_US))
                          (03.01.2019 23:18:32 (ru_RU))
22) `[%x]` - Дата (08/16/88 (none), 08/16/1988(en), 08.16.1988(ru))
23) `[%X]` - Время (21:30:00)
```
#
</details>

#

<details>
  <summary>Модуль locale</summary>

#
`[locale]` - устанавливает языковую локализацию
#
- Синтаксис:
```
import locale

# Для русской локализации
locale.setlocale(locale.LC_ALL, 'ru_RU.UTF-8')

# Для английской локализации
locale.setlocale(locale.LC_ALL, 'en_EN.UTF-8')
```
</details>
