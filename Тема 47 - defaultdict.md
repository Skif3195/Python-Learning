# Тема 47 - defaultdict

`[defaultdict]` - это подкласс dict в Python, который позволяет автоматически назначать значение по умолчанию для ключей, которые отсутствуют в словаре.

```
from collections import defaultdict

# Создаем defaultdict с значением по умолчанию типа int (0)
d = defaultdict(int)

# Мы можем обращаться к ключам, которых нет в словаре,
# и получим значение по умолчанию (0)
print(d['key1'])  # Выведет: 0

# Мы также можем установить значения для ключей, как обычно
d['key2'] = 2
print(d['key2'])  # Выведет: 2
```

- Позволяет работать с несуществующими, в конкретном словаре, ключами.
- Если ключ отсутствует, то он автоматически добавляется в словарь, с установленным значением по умолчанию
- В качестве значения по умолчанию могут применяться следующие типы данных (и эквивалентное им значение для ключа):

     - int - 0
     - float - 0.0
     - bool - False
     - str - '' (пустая строка)
     - list - [] (пустой список)
     - tuple - () (пустой кортеж)
     - set - set() (пустое множество)
     - dict - {} (пустой словарь)   
 
     - Любой итерируемый объект, содержащий пары значений (список кортежей, кортеж списков, и тд) (`defaultdict(int, [('name', 'Timur'), ('age', 29), ('job', 'Teacher')])
`)
     - `[Без значения по умолчанию!]` Передача имеованых аргументов, тогдa значение по умолчанию None (`defaultdict(name='Timur', age=29, job='Teacher')`)
 
     - Челез функцию `[lambda]` указывая любое значение по умолчанию
 
<details>
   <summary>Пример</summary>

```
info = defaultdict(lambda: '1000000$', {'name': 'Timur', 'age': 29, 'job': 'Teacher'})

print(info['name'])     # Timur
print(info['salary'])   # 1000000
```

</details>
 
   - Любую функцию, не принимающую аргументов и возвращающую некоторое дефолтное значение.

 <details>
   <summary>Пример</summary>
   
```
 def get_default():
    return 69

info = defaultdict(get_default, {'name': 'Timur', 'age': 29, 'job': 'Teacher'})

print(info['name'])     # Timur
print(info['salary'])   # 69
```
</details>

#

  - Без значения по умолчанию, `[defaultdict]` ведёт себя как обычный `[dict]`

<details>
   <summary>Пример</summary>
     
Привед>нный ниже код приведёт к ошибке `KeyError`:
```
from collections import defaultdict

data = defaultdict()

print(data['salary'])
```
В то время как следующий код работает как с обычным ловарём:

```
from collections import defaultdict

data = defaultdict()
data['sal'] = 'abc'

print(data)          # defaultdict(None, {'sal': 'abc'})
print(data['sal'])   # abc
```

</details>


  - Функцию, которая возвращает значение по умолчанию для отсутствующих ключей, можно явно менять через атрибут default_factory.

<details>
   <summary>Пример</summary>

```
from collections import defaultdict

data = defaultdict(int)
print(data['salary1'])   # 0

data.default_factory = list
print(data['salary2'])   # []

data.default_factory = float
print(data['salary3'])   # 0.0
```
</details>

  











<details>
   <summary>Пример</summary>

</details>
