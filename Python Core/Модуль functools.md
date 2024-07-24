# Модуль functools

Модуль functools

1. functools - это встроенный модуль в Python, который предоставляет полезные функции высшего порядка для работы с другими функциями.

### Основные функции из functools включают:  

1. functools.reduce: Выполняет кумулятивное вычисление функции на последовательности элементов.  
2. functools.partial: Создаёт новую функцию с частично заданными аргументами.  
3. functools.lru_cache: Декоратор для кэширования результатов функций с целью повышения производительности.  
4. functools.wraps: Декоратор для сохранения метаданных обернутой функции при создании декораторов.  


<details>
  <summary>	Функция partial</summary>

`[partial()]` - позволяет частично использовать функцию, фиксируя некоторые её аргументы. Она создаёт новую функцию, которая уже содержит эти зафиксированные значения и принимает только оставшиеся аргументы.

Синтаксис:

```
functools.partial(func, /, *args, **keywords)
```
- func: Функция, которую нужно частично применить. Это обязательный параметр. 
- *args: Необязательные позиционные аргументы, которые фиксируются для функции func.
- **keywords: Необязательные ключевые аргументы, которые фиксируются для функции func.


<details>
  <summary>Пример</summary>

```
from functools import partial

def multiply(x, y):
    return x * y

# Создаём новую функцию, которая всегда умножает на 2
double = partial(multiply, 2)

# Теперь мы можем использовать double, передавая только второй аргумент
print(double(5))  # Выведет 10
```

1. В функцию `partial`, в качестве первого аргумента, передаётся функция `multiply`. 
2. Вторым аргументом в функцию `partial` передаётся число, которое будет первым аргументом функции `multiply`. 
3. Функция `partial(multiply, 2)` присваивается переменной `double`, которую далее можно вызывать, как возвратную функцию. 
4. Вывод на печать функцию `double`  с аргументом `5`, который встаёт на место второго аргумента функции `multiply`

#

</details>
<details>
  <summary>Атрибуты</summary>

Функция `partial` возвращает partial-объект.   
Созданный объект partial обладает следующими атрибутами:  

- partial.func: исходная функция, которую обёрнули.
- partial.args: аргументы, которые были переданы частично.
- partial.keywords: ключевые аргументы, которые были переданы частично.
```
from functools import partial

def multiply(x, y, z):
    return x * y * z

# Создаём частичную функцию, фиксируя первые два аргумента
partial_func = partial(multiply, 2, 3)

# Используем атрибуты частичной функции
print(partial_func.func)      # Выведет <function multiply at 0x...>
print(partial_func.args)      # Выведет (2, 3)
print(partial_func.keywords)  # Выведет {}
```


#

</details>
<details>
  <summary>Использование partial с именованными аргументами</summary>

```
from functools import partial

# объявляем основную функцию
def greet(greeting, name, punctuation='!', repeat=1):
    return f"{greeting}, {name}{punctuation * repeat}"

# Создаём частичную функцию с фиксированными значениями для аргументов 

shout_greet = partial(greet, punctuation='!!!', repeat=3) 

# Используем частичную функцию 
print(shout_greet('Hello', 'Alice')) # Выведет "Hello, Alice!!!"
```

В этом примере:
* Мы зафиксировали punctuation='!!!' и repeat=3.
* При вызове shout_greet, нам нужно передать только оставшиеся позиционные аргументы greeting и name.


#

</details>
<details>
  <summary>Использование только именованных аргументов</summary>

```
from functools import *

def log_message(level='INFO', message='', timestamp=None):
    return f"{timestamp} [{level}] {message}"

# Создаём частичную функцию с фиксированным уровнем и временем
error_logger = partial(log_message, level='ERROR', timestamp='2024-07-22')

# Используем частичную функцию
print(error_logger(message='Something went wrong'))  # Выведет "2024-07-22 [ERROR] Something went wrong"
```
В этом примере:
* Мы зафиксировали level='ERROR' и timestamp='2024-07-22'.
* При вызове error_logger, нам нужно передать только оставшиеся позиционные и именованные аргументы, такие как message.

#

</details>
<details>
  <summary>Комбинированное использование позиционных и именованных аргументов</summary>

```

from functools import *

# Функция с несколькими аргументами
def configure_device(name, ip, port=80, protocol='http'):
    return f"Configuring {name} at {ip}:{port} using {protocol}"

# Создаём частичную функцию, фиксируя имя устройства и IP
device_setup = partial(configure_device, 'Router', '192.168.1.1', port=443)

# Используем частичную функцию
print(device_setup())  # Выведет "Configuring Router at 192.168.1.1:443 using http"
```
В этом примере:
* Мы зафиксировали name='Router' и ip='192.168.1.1'.
* Мы также зафиксировали port=443.
* При вызове device_setup(), нам нужно передать только оставшийся именованный аргумент protocol, который принимает значение по умолчанию 'http'.

#

</details>
<details>
  <summary>Интересный пример</summary>

За кулисами нам доступна уже реализованная функция send_email(), которая  которая принимает три аргумента в следующем порядке:  

- `name` — имя  
- `email_address` — адрес электронной почты  
- `text` — содержание письма

Функция отправляет письмо пользователю с именем `name` на адрес `email_address` с содержанием `text`  

### Задача №1   

Реализовать функцию `to_Timur()` с помощью функции `partial()`, которая принимает один аргумент:  

`text` — содержание письма  

Функция должна отправлять письмо пользователю с именем Тимур на адрес `timyrik20@beegeek.ru` с содержанием `text`.   

### Задача №2

Реализовать функцию `send_an_invitation()` с помощью функции `partial()`, которая принимает два аргумента в следующем порядке:

- `name` — имя
- `email_address` — адрес электронной почты

Функция должна отправлять письмо на имя name и на адрес email_address со следующим содержанием:  

`Школа BEEGEEK приглашает Вас на новый курс по программированию на языке Python. тутут....`

---------------------------------------------------------------------------------------------

## Реализация:

```
from functools import partial

def to_Timur(text):
    partial_func = partial(send_email, "Тимур", "timyrik20@beegeek.ru")
    return partial_func(text)

def send_an_invitation(name, email_address):
    partial_func = partial(send_email, text='Школа BEEGEEK приглашает Вас на новый курс по программированию на языке Python. тутут....')
    return partial_func(name, email_address)
```

<details>
  <summary>to_Timur()</summary>

1. Что она делает:  

- Создаёт частичную функцию, фиксируя параметры `name` и `email_address` для функции `send_email`.  
- Возвращает результат вызова этой частичной функции с произвольным аргументом `text`.

2. Как она работает:

- `partial(send_email, "Тимур", "timyrik20@beegeek.ru")` создаёт новую функцию, которая будет вызывать `send_email` с зафиксированными аргументами `"Тимур"` и `"timyrik20@beegeek.ru"`, добавляя к ним аргумент text.

- `partial_func(text)` вызывает эту частичную функцию с произвольным аргументом `text`.

#

</details>
<details>
  <summary>send_an_invitation()</summary>

1. Что она делает:

- Создаёт частичную функцию, фиксируя параметр `text` для функции `send_email`.  
- Возвращает результат вызова этой частичной функции с аргументами `name` и `email_address`.  

2. Как она работает:  

- `partial(send_email, text='Школа BEEGEEK приглашает Вас на новый курс по программированию на языке Python. тутут....')` создаёт новую функцию, которая будет вызывать `send_email` с зафиксированным аргументом `text` и добавленными аргументами `name` и `email_address`.
- `partial_func(name, email_address)` вызывает эту частичную функцию с произвольными аргументами `name` и `email_address`.

#

</details>


#

</details>



#

</details>
















<details>
  <summary>Функция update_wrapper()</summary>



#

</details>















<details>
  <summary>Null</summary>



#

</details>
