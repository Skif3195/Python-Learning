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
