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

# Плюсы и отличия от dict()

- Позволяет избежать проверок на несуществующие словари
- Позволяет инициализировать элементы словаря некоторым значением по умолчанию
- Удобная группировка элементов
- Удобная группировка уникальных элементов
- Удобный подсчёт элементов
- Удобное наполнение элементов значениями
- `default dict` быстрее чем `dict`

#

# Частные случаи использования defaultdict

<details>
   <summary>Группировка элементов</summary>

Типичным использованием `defaultdict` является группировка элементов. В качестве значения по умолчанию у казывается тип `list`. Далее, происходит обращение к, несуществующему в словаре, ключу `[key]` при помощи функции `append()`. Так как значения по умолчанию для ключей это списки, то ключу `[key]` присваивается значение, возвращаемое методом `append()`. 

```
from collections import defaultdict
dd = defaultdict(list)
dd['key'].append(1)
print(dd)   # defaultdict(<class 'list'>, {'key': [1]})

dd['key'].append(2)
print(dd)   # defaultdict(<class 'list'>, {'key': [1, 2]})

dd['key'].append(3)
print(dd)   # defaultdict(<class 'list'>, {'key': [1, 2, 3]})
```
Таким образом мы можем сортировать данные по какому-то конкретному признаку. Например у нас есть список кортежей, которые хранят пары значений `(отдел, имя сотрудника)`. Привед>нный ниже код отсортирует список сотрудников и сгруппирует их по отделам:

```
from collections import defaultdict

dep = [('Sales', 'John Doe'),
       ('Sales', 'Martin Smith'),
       ('Accounting', 'Jane Doe'),
       ('Marketing', 'Elizabeth Smith'),
       ('Marketing', 'Adam Doe')]

dep_dd = defaultdict(list)
for department, employee in dep:
    dep_dd[department].append(employee)

print(dep_dd)   # defaultdict(<class 'list'>, {'Sales': ['John Doe', 'Martin Smith'], 'Accounting': ['Jane Doe'], 'Marketing': ['Elizabeth Smith', 'Adam Doe']})

```

</details>
<details>
   <summary>Группировка уникальных элементов</summary>

Продолжаем работать с данными отделов и сотрудников из предыдущего примера.  
После некоторой обработки мы понимаем, что несколько сотрудников были продублированы в базе данных по ошибке.  
Вам необходимо очистить данные и удалить дублирующихся сотрудников из вашего dep_dd словаря.  
Для этого мы можем использовать a множества `(set)` в качестве значения по умолчанию `.default_factory`:

```
from collections import defaultdict

dep = [('Sales', 'John Doe'),
       ('Sales', 'Martin Smith'),
       ('Accounting', 'Jane Doe'),
       ('Marketing', 'Elizabeth Smith'),
       ('Marketing', 'Elizabeth Smith'),
       ('Marketing', 'Adam Doe'),
       ('Marketing', 'Adam Doe'),
       ('Marketing', 'Adam Doe')]

dep_dd = defaultdict(set)
for department, employee in dep:
    dep_dd[department].add(employee)

print(dep_dd) #defaultdict(<class 'set'>, {'Sales': {'John Doe', 'Martin Smith'}, 'Accounting': {'Jane Doe'}, 'Marketing': {'Elizabeth Smith', 'Adam Doe'}})
```

В данном примере мы создаём словарь со значением по умолчанию в которое помещаем тип `set`.  
Далее при помощи цикла перебираем мары значений. В качестве ключа выступает первое значение, в качестве значения ключа - второе значение.
На выходе мы получаем словарь словарей, в ктором исключены повторения значений, так как тип значения по умолчанию исключает повторяющиеся элементы.

</details>












<details>
   <summary>Пример</summary>

</details>
