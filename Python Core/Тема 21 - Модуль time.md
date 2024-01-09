# Тема 21 - Модуль time

- `[ time ]` - Модуль стандартной библиотеки Python, редоставляет только функции, позволяющие работать со временем.

     - Использование модуля `[time]` дает возможность:
 
          - отображать информацию о времени, прошедшем с начала эпохи
          - преобразовывать значение системного времени к удобному виду
          - прерывать выполнение программы (установка паузы) на заданное количество секунд
          - измерять время выполнения программы целиком или ее отдельных модулей
#
- `[ Модуль time ]` - оперирует двумя типами данных:
  
     - Количество секунд, прошедших с начала эпохи
     - Структура данных `[struct_time]`
#
- `[ Начало эпохи ]` - это полночь 1 января 1970 года (00:00:00 UTC), когда счетчик секунд имел полностью нулевое значение.
#
- `[struct_time]` - является именованным кортежем, представляющий информацию о времени использую определённые атрибуты в связке со специальными функциями.
    - Используя функции, и кол-во секунд с начала эпохи, можно получить любую информацию о текущем времени
    - Использование атрибутов возвращают объект типа `[int]`
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
</details>
