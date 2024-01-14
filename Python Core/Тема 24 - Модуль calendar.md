Тема 23 - Модуль calendar

- `[ calendar ]` - Модуль стандартной библиотеки Python, предоставляет функции для работы с календарями. Мы можем использовать его для получения информации о днях недели, месяцах, годах, а также для создания кастомных календарей.
  
     - По умолчанию следует следует григорианскому календарю, где понедельник является первым днем недели, (имеет номер 0), а воскресенье — последним днем недели (имеет номер 6).
     - Предоставляет возможности работы ТОЛЬКО с календарями.
#
### Для использовния модуля, его нужно импортировать
 1) `[import calendar]` - импортирует модуль целиком. В таком случае, перед использованием конкретной функции требуется явное указание модуля `[calendar]`.
 2) `[from calendar import n]` - импорт одной конкретной функции `[n]` из модуля `[calendar]`. В этом случае, перед использованием функции не требуется явное указание модуля `[calendar]`.
 3) `[from calendar import *]` - импорт всех функций модуля. Эквиволентен первому способу, но в этом случае перед использованием функции не требуется явное указание модуля `[calendar]`.
#
- Модуль может оперировать атрибутами и функциями.
- `[ Атрибуты ]` - это переменные или значения, предназначенные для доступа к различным характеристикам календаря.

<details>
  <summary>Атрибуты модуля calendar</summary>

- атрибуты `[month_name]`  и `[ month_abbr ]` соответствует обычному соглашению, что январь – это месяц номер 1, поэтому список имеет длину в 13 элементов, первый из которых – пустая строка.

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
#
</details>

#

<details>
  <summary>Функции модуля calendar</summary>

#
- `[ month_abbr ]` -
```

```
</details>













