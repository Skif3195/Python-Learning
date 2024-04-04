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

Типичным использованием `defaultdict` является группировка элементов.  
В качестве значения по умолчанию у казывается тип `list`. 
  
Далее, происходит обращение к, несуществующему в словаре, ключу `[key]` при помощи функции `append()`.   
Так как значения по умолчанию для ключей это списки, то ключу `[key]` присваивается значение, возвращаемое методом `append()`. 

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
Таким образом мы можем сортировать данные по какому-то конкретному признаку.  
Например у нас есть список кортежей, которые хранят пары значений `(отдел, имя сотрудника)`.   
Приведённый ниже код отсортирует список сотрудников и сгруппирует их по отделам:

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
  
Далее при помощи цикла перебираем пары значений. В качестве ключа выступает первое значение, в качестве значения ключа - второе значение.
  
На выходе мы получаем словарь словарей, в ктором исключены повторения значений, так как тип значения по умолчанию исключает повторяющиеся элементы.

</details>
<details>
   <summary>Подсчёт элементов последовательности</summary>

Если, в качестве значения по усмолчанию, указать тип `int`, то defaultdict можно использовать для подсчета элементов в последовательности или коллекции.   
При вызове int() без аргументов функция возвращает 0 типичное значение, которое мы использовали бы для инициализации счетчика.  

Прододолжим рассматривать базу данных сотрудников компаний.
При помощи `defaultdict` и значения по умолчанию `int` можно подсчитать количество сотрудников в каждом отделе:
```
from collections import defaultdict

dep = [('Sales', 'John Doe'),
       ('Sales', 'Martin Smith'),
       ('Accounting', 'Jane Doe'),
       ('Marketing', 'Elizabeth Smith'),
       ('Marketing', 'Adam Doe')]
dd = defaultdict(int)
for department, _ in dep:
    dd[department] += 1

print(dd)  # defaultdict(<class 'int'>, {'Sales': 2, 'Accounting': 1, 'Marketing': 2})
```
В данном примере мы создаём `defaultdict` со значением по умолчанию `int`.  
  
Далее при помощи цикла перебираем пары значений. В качестве ключа выступает первое значение, в качестве значения ключа - пропуск значения (нижний прочерк), так как нам не важно второе значение. Важен сам факт его наличия для того, что бы зафиксировать в отделе +1 сотрудника.  
При каждой итерации, ключ с именем отдела, к своему значению прибовляет +1, если отдел упоминается в паре значений.
  
На выходе, мы получаем словарь, в котором ключами являются названия отделов, а значениями - кол-во сотрудников этого отдела.

</details>
<details>
   <summary>Накопление значений</summary>

Для подсчета общей суммы значений последовательности, можно использовать тип `float` в качестве значения по умолчанию:

```
from collections import defaultdict

incomes = [('Books', 1250.00), # Март
           ('Books', 1300.00), # Апрель
           ('Books', 1420.00), # Май
           ('Tutorials', 560.00), # Март
           ('Tutorials', 630.00), # Апрель
           ('Tutorials', 750.00), # Май
           ('Courses', 2500.00), # Март
           ('Courses', 2430.00), # Апрель 
           ('Courses', 2750.00),] # Май

dd = defaultdict(float)
for product, income in incomes:
    dd[product] += income

for product, income in dd.items():
    print(f'Total income forъ {product}: ${income:,.2f}')

# Total income for Books: $3,970.00
  Total income for Tutorials: $1,940.00
  Total income for Courses: $7,680.00
```
У нас есть список кортежей, которые содержат пары значений - категория товара, суммы продаж за месяц.  
Необходимо подсчитать общую сумму продаж по каждой категории за все три месяца.  

В данном примере, создаём `  defaultdict` со значением по умолчанию `float`.  
Далее, перебор пар значений через цикл `for`. В качестве ключа - первоое значение, в качестве значения - второе значение.  
С каждой итерацией каждый ключ (категория товара) прибавляет к своему значению - второе значение в паре (сумму продаж за месяц).  

На выходе мы получаем слоарь содержащий информацию о сумме продаж каждой категории товара за три мецяца.



</details>
