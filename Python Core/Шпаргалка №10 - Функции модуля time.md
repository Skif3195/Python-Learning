# Шпаргалка №10 - Функции модуля time

<details>
  <summary>Атрибуты struct_time</summary> 
     
```
1) n.tm_year - год (0000 - 9999)
2) n.tm_mon - месяц (1 - 12)
3) n.tm_mday - день месяца (1 - 31)
4) n.tm_hour - час (00 - 24)
5) n.tm_min - минуты (00 - 59)
6) n.tm_sec - секунды (00 - 61)
7) n.tm_wday - день недели (Пн - 0, Вс - 6)
8) n.tm_yday - день года (1 - 366)
9) n.tm_zone - сокращённое название часового пояса

n - структура данных (struct_time)
```
#
#
</details>
<details>
  <summary>Функции struct_time</summary> 
     
#
   - 1 ) `[time.localtime()]` - эта функция принимает количество секунд с начала эпохи и возвращает структуру struct_time, представляющую локальное время учитывая локальные настройки часового пояса и летнего времени для предоставления локального времени.
```
import time

current_time = time.localtime()
print(current_time)   # time.struct_time(tm_year=2024, tm_mon=1, tm_mday=8, tm_hour=21, tm_min=59, tm_sec=8, tm_wday=0, tm_yday=8, tm_isdst=0)

print(current_time.tm_hour)   # Выведет час локального времени
print(current_time.tm_mday)   # Выведет день нынешнего месяца
```
#
   - 2 ) `[time.gmtime()]` - принимает количество секунд, возвращает структуру struct_time, представляющую время в UTC (Coordinated Universal Time), не учитывает локализацию, а просто возвращает время в мировом координированном времени (UTC).
```
import time

current_time = time.localtime()
print(current_time)   # time.struct_time(tm_year=2024, tm_mon=1, tm_mday=8, tm_hour=12, tm_min=30, tm_sec=45, tm_wday=0, tm_yday=8, tm_isdst=0)

print(current_time.tm_hour)   # Выведет час UTC времени
print(current_time.tm_mday)   # Выведет день нынешнего месяца
```
#
   - 3 ) `[time.asctime()]` - принимает объект struct_time (или кортеж, содержащий 9 значений, относящихся к struct_time), представляющий момент времени, и возвращает его в виде строки `[str]`, представляющей читаемое представление времени. Если вызвать time.asctime() без аргументов, то она автоматически использует текущее местное время.  

- Возвращает объект `[str]`

- По автомату выводит время в английской локализации.
```
import time

current_time = time.localtime()
formatted_time = time.asctime(current_time)

print(formatted_time)         # Mon Jan  8 22:12:56 2024
print(type(formatted_time))   # <class 'str'>
```
#
   - 4 ) `[time.mktime()]` - принимает объект struct_time (или кортеж, содержащий 9 значений, относящихся к struct_time), представляющий момент времени, и возвращает количество секунд, прошедших с начала эпохи, в местном времени.

- Возвращает объект `[float]`
```
import time

# Получаем текущее местное время в виде struct_time
current_time_struct = time.localtime()

# Преобразуем struct_time в количество секунд с начала эпохи
seconds_since_epoch = time.mktime(current_time_struct)

print(f"Текущее время в секундах с начала эпохи: {seconds_since_epoch}")
print(type(seconds_since_epoch))   # <class 'float'>
```
#
#
#
   - 5 ) `[time.strftime()]` - принимает строку с некоторым [набором правил для форматирования](https://github.com/Skif3195/Python-Learning/blob/Guides/Python%20Core/Шпаргалка%20№9%20-%20Таблица%20форматирования%20даты%20и%20времени.md) и объект struct_time (или соответствующий кортеж) в качестве аргументов и возвращает строку с датой в зависимости от использованного формата.
```
import time

time_obj = time.localtime()
result = time.strftime('%d.%m.%Y, %H:%M:%S', time_obj)

print(result)         # Текущее время в str: 09.01.2024, 20:37:20
print(type(result))   # <class 'str'>
```
#
   - 6 ) `[time.strptime()]` - делает разбор строки в зависимости от использованного [формата](https://github.com/Skif3195/Python-Learning/blob/Guides/Python%20Core/Шпаргалка%20№9%20-%20Таблица%20форматирования%20даты%20и%20времени.md) и возвращает объект struct_time.
```
import time

time_string = '1 September, 2021'
result = time.strptime(time_string, '%d %B, %Y')

print(result)         # time.struct_time(tm_year=2021, tm_mon=9, tm_mday=1, tm_hour=0, tm_min=0, tm_sec=0, tm_wday=2, tm_yday=244, tm_isdst=-1)
print(type(result))   # <class 'time.struct_time'>
```
#
#
</details>

<details>
  <summary>Функции time</summary> 

#
   - 1 ) `[time.time()]` - возвращает текущее время в секундах с начала эпохи (1 января 1970 года) в виде числа с плавающей точкой.
```
import time

seconds = time.time()    # получаем количество прошедших секунд в виде float числа
```
#
   - 2 ) `[time.time_ns()]` - возвращает текущее время в наносекундах с начала эпохи (1 января 1970 года) в виде целого числа. Эта функция доступна начиная с Python 3.7.
```
import time

current_time_ns = time.time_ns()
```
#
   - 3 ) `[time.ctime()]` - возвращает текущее местное время в виде строки `[str]` с удобочитаемым форматом. 
```
import time

current_time_str = time.ctime()

print(current_time_str)   # Mon Jan  8 12:30:45 2024
```
#
   - 4 ) `[time.sleep(n)]` - приостанавливает выполнение программы на n секунд. Эта функция полезна, когда необходимо добавить задержку в выполнение кода.
     
        - Аргумент n - количество секунд, на которое следует приостановить выполнение.
```
print("Начало выполнения")
time.sleep(3)  # Приостановка выполнения на 3 секунды
print("Прошло 3 секунды")
```
#
#
</details>

#

<details>
  <summary>Форматирование даты и времени</summary> 

`[ISO 8601]` - международный формат представления датты и аремени

  - Формат date в ISO 8601: `[YYYY-MM-DD]`
  - Формат time в ISO 8601: `[hh:mm:ss:ffffff]`
  - Формат datetime в ISO 8601: `[YYYY-MM-DD hh:mm:ss:ffffff]`
#
- Для удобства объекты datetime можно переводить в строковый тип и обратно по определенному формату.

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
#
#
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
#
#
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
#
#
</details>

#
#
</details>

#

<details>
  <summary>Время работы программы</summary> 

- Что бы измерить время работы программы (или её части), ннеобходимо вычислить разницу между моментом ее запуска и завершения.  

- Для этого нужно вызвать соответствующую функцию, которая вернёт время (системное или локальное) до начала работы программы и после ее окончания. И вычислить разницу этихдвух показателей.
#
Сделать это можно при помощи:

<details>
  <summary>Функций модуля time</summary> 

#
- 1 ) `[time.time()]` - возвращает текущее время в секундах с начала эпохи (1 января 1970 года) в виде числа с плавающей точкой. Может быть подвержено коррекциям системного времени, что может повлиять на его точность.  
```
import time

start_time = time.time()

# Ваш код, время выполнения которого вы хотите измерить

end_time = time.time()
elapsed_time = end_time - start_time

print(f"Прошло времени: {elapsed_time} секунд")
```
#
- 2 ) `[time.monotonic()]` - так же возвращает текущее время в секундах с начала эпохи, но обеспечивает стабильность в случае изменений системного времени.
```
import time

start_time = time.monotonic()

# Здесь находится код вашей программы

end_time = time.monotonic()
elapsed_time = end_time - start_time

print(f"Время выполнения программы: {elapsed_time} секунд")

```
#
- 3 ) `[time.pref_counter()]` - Возвращает высокоточное и монотонное время, не подверженное изменениям в системном времени.
```
import time

start_time = time.perf_counter()

# Здесь находится код вашей программы

end_time = time.perf_counter()
elapsed_time = end_time - start_time

print(f"Время выполнения программы: {elapsed_time} секунд")
```
#
- 4 ) `[time.process_time()]` - предназначенная для измерения процессорного времени исполнения текущего процесса. Измеряет только процессорное время, исключая время, когда программа не выполняется (например, время ввода/вывода или ожидания). Это полезно для измерения времени, фактически затраченного на вычисления в вашем коде.
```
import time

start_time = time.process_time()

# Здесь находится код вашей программы

end_time = time.process_time()
elapsed_time = end_time - start_time

print(f"Процессорное время выполнения программы: {elapsed_time} секунд")

```
#
#

</details>
<details>
  <summary>Функций модуля timeit</summary> 

#
- 1 ) `[timeit.default_timer()]` - это функция из модуля `[timeit]` в Python, которая предоставляет наилучший доступный таймер для измерения времени. Она автоматически выбирает между time.perf_counter(), time.process_time(), и в случае их отсутствия, time.time().
```
import timeit

start_time = timeit.default_timer()

# Здесь находится код вашей программы

end_time = timeit.default_timer()
elapsed_time = end_time - start_time

print(f"Время выполнения программы: {elapsed_time} секунд")
```
- Эта функция предназначена для использования в библиотеках или сценариях, где важно использовать наилучший доступный таймер в зависимости от платформы. В отличие от time.perf_counter(), она не привязана к измерению времени внутри интерпретатора Python и может быть более устойчивой к некоторым изменениям среды выполнения.

- Использование timeit.default_timer() делает код переносимым между различными платформами и обеспечивает использование наилучшего таймера в текущей среде выполнения.
#
#
</details>


  </details>
