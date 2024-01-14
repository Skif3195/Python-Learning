# Шпаргалка №11 - Функции модуля calendar

<details>
  <summary>Атрибуты модуля calendar</summary>

#
- Aтрибуты `[month_name]`  и `[ month_abbr ]` соответствует обычному соглашению, что январь – это месяц номер 1, поэтому список имеет длину в 13 элементов, первый из которых – пустая строка.

#
- `[ day_name ]` - представляет собой список строк, содержащих названия дней недели.
```
import calendar

# Получим названия дней недели
days_of_week = calendar.day_name

print(list(days_of_week))   # ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday']
```
#
- `[ day_abbr ]` - представляет собой список строк, содержащих сокращенные названия дней недели (три буквы).
```
import calendar

# Получим сокращенные названия дней недели
abbreviated_days = calendar.day_abbr

print(list(abbreviated_days))   # ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
```
# 
- `[ month_name ]` - представляет собой список строк, содержащих названия месяцев.
```
import calendar

# Получим названия месяцев
months = calendar.month_name

print(list(months))   # ['', 'January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']
```
#
- `[ month_abbr ]` - представляет собой список строк, содержащих сокращенные названия месяцев (три буквы).
```
import calendar

# Получим сокращенные названия месяцев
abbreviated_months = calendar.month_abbr

print(list(abbreviated_months))   # ['', 'Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']
```
#
- Для получения номеров дней недели можно использовать атрибуты: MONDAY, TUESDAY, ..., SUNDAY.
```
import calendar

print(calendar.MONDAY)      # 0
print(calendar.TUESDAY)     # 1
print(calendar.WEDNESDAY)   # 2
print(calendar.THURSDAY)    # 3
print(calendar.FRIDAY)      # 4
print(calendar.SATURDAY)    # 5
print(calendar.SUNDAY)      # 6
```
#
- Объекты, доступные по атрибутам day_name, day_abbr, month_name и month_abbr, поддерживают индексацию.
```
import calendar

print(calendar.day_name[1])     # Tuesday
print(calendar.day_abbr[1])     # Tue
print(calendar.month_name[1])   # January
print(calendar.month_abbr[1])   # Jan
```
#
#
</details>

#

<details>
  <summary>Функции модуля calendar</summary>

#
- `[ firstweekday() ]` - возвращает целое число, означающее первый день недели в календаре. По умолчанию это понедельник.
```
import calendar

# Получим текущий первый день недели
first_day = calendar.firstweekday()

print(first_day)   # 0
```
#
- `[ setfirstweekday(weekday) ]` -  устанавливает первый день недели в календаре в соответствии с указанным аргументом weekday.
```
import calendar

print(calendar.firstweekday())             # 0
calendar.setfirstweekday(calendar.SUNDAY)
print(calendar.firstweekday())             # 6
```
#
- `[ isleap(year) ]` - проверяет, является ли указанный год високосным. Возвращает True/False.
```
import calendar

print(calendar.isleap(2020))   # True
print(calendar.isleap(2021))   # False
```
#
- `[ leapdays(y1, y2) ]` - возвращает количество високосных годов между годами y1 и y2 (включительно).
```
import calendar

# Определим количество високосных годов между 2000 и 2020
start_year = 2000
end_year = 2020

leap_years = calendar.leapdays(start_year, end_year)

print(leap_years)   # 5
```
#
- `[ weekday(year, month, day) ]` - возвращает день недели в виде целого числа (где 0 – понедельник, 6 – воскресенье) для заданной даты.

     - `[year]` – год начиная с 1970
     - `[month]` – месяц в диапазоне 1−12
     - `[day]` – число в диапазоне 1−31
```
import calendar

print(calendar.weekday(2021, 9, 1))   # 2 (Среда)
print(calendar.weekday(2021, 9, 2))   # 3 (Четрверг)
```
#
- `[ monthrange(year, month) ]` - возвращает день недели, с которого начинается месяц, и количество дней в месяце.
```
import calendar

print(calendar.monthrange(2024, 1))   # (0, 31)
```
#
- `[ monthcalendar(year, month) ]` - возвращает матрицу, представляющую календарь на месяц. Каждая строка матрицы представляет неделю. Дни, не принадлежащие месяцу, будут представлены нулями.
```
import calendar

print(*calendar.monthcalendar(2021, 9), sep='\n')  # [0, 0, 1, 2, 3, 4, 5]
                                                     [6, 7, 8, 9, 10, 11, 12]
                                                     [13, 14, 15, 16, 17, 18, 19]
                                                     [20, 21, 22, 23, 24, 25, 26]
                                                     [27, 28, 29, 30, 0, 0, 0]
```
#
- `[ month(year, month, w=0, l=0) ]` -  возвращает календарь на месяц в многострочной строке. Возвращает объект типа `[str]`.

     - `[year]` - год
     - `[month]` - месяц
     - `[w]` - ширина столбца даты
     - `[l]` - количество строк, отводимые на неделю
```
import calendar

print(calendar.month(2024, 1))   #     January 2024
                                   Mo Tu We Th Fr Sa Su
                                    1  2  3  4  5  6  7
                                    8  9 10 11 12 13 14
                                   15 16 17 18 19 20 21
                                   22 23 24 25 26 27 28
                                   29 30 31
```
#
- `[ calendar(year, w=2, l=1, c=6, m=3) ]` - возвращает календарь на весь год в виде многострочной строки. Возвращает объект типа `[str]`.

     - `[year]` - год
     - `[w]` - ширина столбца даты
     - `[l]` - количество строк, отводимые на неделю
     - `[c]` - количество пробелов между столбцом месяца
     - `[m]` - количество столбцов
```
import calendar

print(calendar.calendar(2024))

#
                                  2024

      January                   February                   March
Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su
 1  2  3  4  5  6  7                1  2  3  4                   1  2  3
 8  9 10 11 12 13 14       5  6  7  8  9 10 11       4  5  6  7  8  9 10
15 16 17 18 19 20 21      12 13 14 15 16 17 18      11 12 13 14 15 16 17
22 23 24 25 26 27 28      19 20 21 22 23 24 25      18 19 20 21 22 23 24
29 30 31                  26 27 28 29               25 26 27 28 29 30 31

       April                      May                       June
Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su
 1  2  3  4  5  6  7             1  2  3  4  5                      1  2
 8  9 10 11 12 13 14       6  7  8  9 10 11 12       3  4  5  6  7  8  9
15 16 17 18 19 20 21      13 14 15 16 17 18 19      10 11 12 13 14 15 16
22 23 24 25 26 27 28      20 21 22 23 24 25 26      17 18 19 20 21 22 23
29 30                     27 28 29 30 31            24 25 26 27 28 29 30

        July                     August                  September
Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su
 1  2  3  4  5  6  7                1  2  3  4                         1
 8  9 10 11 12 13 14       5  6  7  8  9 10 11       2  3  4  5  6  7  8
15 16 17 18 19 20 21      12 13 14 15 16 17 18       9 10 11 12 13 14 15
22 23 24 25 26 27 28      19 20 21 22 23 24 25      16 17 18 19 20 21 22
29 30 31                  26 27 28 29 30 31         23 24 25 26 27 28 29
                                                    30

      October                   November                  December
Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su
    1  2  3  4  5  6                   1  2  3                         1
 7  8  9 10 11 12 13       4  5  6  7  8  9 10       2  3  4  5  6  7  8
14 15 16 17 18 19 20      11 12 13 14 15 16 17       9 10 11 12 13 14 15
21 22 23 24 25 26 27      18 19 20 21 22 23 24      16 17 18 19 20 21 22
28 29 30 31               25 26 27 28 29 30         23 24 25 26 27 28 29
                                                    30 31

```
#
- `[ prmonth(theyear, themonth, w=0, l=0) ]` - Эквивалентен функции month(theyear, themonth, w=0, l=0). Используется Преимущественно для отображения календаря в консоли или в текстовом интерфейсе. Не возвращает никакого значения. Выводит календарь на экран.
#
- `[ prcal(year, w=0, l=0, c=6, m=3) ]` - Эквивалентен функции calendar(theyear, themonth, w=0, l=0). Используется Преимущественно для отображения календаря в консоли или в текстовом интерфейсе. Не возвращает никакого значения. Выводит календарь на экран.
</details>
