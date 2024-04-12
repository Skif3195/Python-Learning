# Тема 48 - OrderDict

`[OrderDict]` - подкласс `[dict]`, который запоминает порядок добавления элементов. Он предоставляет функциональность обычного словаря, но также сохраняет порядок вставки элементов. Имеет несколько отличительных от `[dict]` особенностей:

   - Гарантирует, что элементы (ключи) будет распологаться в том порядке, в котором были добавлены в `[OrderDict-объект]`.
   - Гарантирует, что при итерации по `[OrderDict-объекту]` ключи останутся в том же порядке, в котором были добавлены в `[OrderDict-объект]`.
   - Позваляет вставлять элементы в `[OrderDict-объект]` только в начало или конец.  
  
   - `[dict]` - (стандартный словарь) не гарантирует порядок расположения элементов при добавлении и при итерации по словарю.
#
### Изменение OrderDict словаря

1. При стандартном добавлении элемента в `[OrderDict-объект]`, по умолчанию, оно будет вставлено в самый конец словаря.
2. При удалении случайного элемента из `[OrderDict-объекта]`, а за тем при повторном его добавлении, по умолчанию, элемент будет добавлен в самый конец словаря.
3. При обновлении значения по ключу, элемент остаётся на исходной позиции.

- Обновить элемент можно при помощи квадратных скобок (`[my_orderdict[key] = 'value']`) или при помощи словарного метода `[update]` (`[my_dict.update({'key': 'new_value'})]`)

#
### Способы создания OrderDict объекта

1. Из любого итерируемого объекта, содержащего пары значений:
```
my_orderdict = OrderedDict([('name', 'Timur'), ('age', 29), ('job', 'Teacher')])
```
2. Передавая создающей функции именованные аргументы:
```
my_orderdict = OrderedDict(name='Timur', age=29, job='Teacher')
```
3. Используя генератор:
```
my_ordered_dict = OrderedDict((key, value) for key, value in [('name', 'Timur'), ('surname', 'Guev'), ('hobby', 'math')])
```
4. С помощью метода `[fromkeys()]`:
```
keys = ['name', 'surname', 'hobby']
default_value = 'Unknown'
my_ordered_dict = OrderedDict.fromkeys(keys, default_value)
```
5. Создание пустого `OrderDict-объекта`, для добавления в него переменных:
```
my_ordered_dict = OrderedDict()
```
6. С использованием функции `update()`:
```
my_ordered_dict = OrderedDict()
my_ordered_dict.update({'name': 'Timur', 'surname': 'Guev', 'hobby': 'math'})
```
#
### Итерирование по объекту OrderDict

1. Доступ к элементам `OrderDict-словаря` производится напрямую, при помощи словарных методов `[keys()]`, `[values()]`, `[items()]`.
2. При итерировании по `OrderDict-объекту` допустимо использование встроенной функции `[reverced()]`:
```
from collections import OrderedDict

numbers = OrderedDict(one=1, two=2, three=3)

# перебор ключей напрямую
for key in reversed(numbers):
    print(key, '->', numbers[key])   # three -> 3
                                       two -> 2
                                       one -> 1


# перебор пар (ключ, значение) через метод
for key, value in reversed(numbers.items()):
    print(key, '->', value)          # three -> 3
                                       two -> 2
                                       one -> 1


# перебор ключей через метод
for key in reversed(numbers.keys()):
    print(key, '->', numbers[key])   # three -> 3
                                       two -> 2
                                       one -> 1

# перебор значений через метод
for value in reversed(numbers.values()):
    print(value)                     # 3
                                       2
                                       1
```
#
### Метод move_toend

`[move_to_end(key, last=True)]` - метод класса `OrderDict`, используется для перемещения элемента в конец или начало словаря.

   - `[key]` - ключ, который будет переноситься в начало или в конец словаря.
   - `[last=True]` - необязательный аргумент, указывает в каком направлении переносить ключ. `True` (по умолчанию) - перенос в конец словаря, `False` - перенос в начало словаря.
```
from collections import OrderedDict

numbers = OrderedDict(one=1, two=2, three=3)
print(numbers)                                 # OrderedDict([('one', 1), ('two', 2), ('three', 3)])

numbers.move_to_end('one')                     # last=True
print(numbers)                                 # OrderedDict([('two', 2), ('three', 3), ('one', 1)])

numbers.move_to_end('three', last=False)       # last=False
print(numbers)                                 #OrderedDict([('three', 3), ('two', 2), ('one', 1)])
```
#
### Метод popitem()

`[popitem(last=True)]` - метод, удаляет и возвращает последнюю (по умолчанию) или первую пару ключ-значение из словаря OrderedDict, в зависимости от значения параметра last.

   - В случае `last=True` (по умолчанию) удаляет ключ с конца словаря (принцип LIFO)
   - В случае `last=False` удаляет ключ с начала словаря (принцип FIFO)
```
from collections import OrderedDict

numbers = OrderedDict(one=1, two=2, three=3)
print(numbers)               # OrderedDict({'one': 1, 'two': 2, 'three': 3})


print(numbers.popitem())     # ('three', 3)
print(numbers)               # OrderedDict({'one': 1, 'two': 2})

print(numbers.popitem())     # ('two', 2)
print(numbers)               # OrderedDict({'one': 1})
```
#
### [OrderDict наследует все методы класса dict](https://github.com/Skif3195/Python-Learning/blob/Guides/Python%20Core/Шпаргалка%20№5%20-%20Методы%20Словарей.md)
#
### Сравнение словарей на равенство значений

- При сравнении `OrdedDict-словарей` - порядок расположения элементов важен.
- При сравнении обычных словарей (`dict`) - порядок расположения элементов не важен.
- при сравнении `OrderDict` и `dict` - порядок расположения элементов не важен.
#
### Конкатенация словарей
Операторы `|` и `|=` производят конкатенацию как обычных словарей (`dict`) так и `OrderDict-словарей`:
```
from collections import OrderedDict

physicists = OrderedDict(newton='1642-1726', einstein='1879-1955')
biologists = OrderedDict(darwin='1809-1882', mendel='1822-1884')

scientists = physicists | biologists
print(scientists)   # OrderedDict({'newton': '1642-1726', 'einstein': '1879-1955', 'darwin': '1809-1882', 'mendel': '1822-1884'})

physicists = OrderedDict(newton='1642-1726', einstein='1879-1955')
physicists1 = OrderedDict(newton='1642-1726/1727', hawking='1942-2018')

physicists |= physicists1
print(physicists)   # OrderedDict({'newton': '1642-1726/1727', 'einstein': '1879-1955', 'hawking': '1942-2018'})
```




