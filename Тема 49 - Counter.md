# Тема 49 - Counter

`[Counter]` - подтип класса `dict`, предназначеный для подсчёта хешируемых (неизменяемых) объектов.

   - `Counter` можно создать из любого итерируемого объекта, элемента которого - неизменяемые типы.
   - `Counter` создаёт словарь, ключи которого - элементы последовательности, значения - количество этих элементов в последовательности.
   - Ключи объекта `Counter` - должны быт хешируемыми типами
   - Значения могут быть любыми типами
#
### Создание Counter  

1. Передача итерируемого объекта напрямую конструктору Counter:
```
from collections import Counter

counter = Counter('mississippi')     # Создаем счетчик на основе строки
print(counter)                       # Counter({'i': 4, 's': 4, 'p': 2, 'm': 1})
```
2. Явное указание начального кол-ва элементов:
```
counter1 = Counter({'i': 4, 's': 4, 'p': 2, 'm': 1})
counter2 = Counter(i=4, s=4, p=2, m=1)

print(counter1)     # Counter({'i': 4, 's': 4, 'p': 2, 'm': 1})
print(counter2)     # Counter({'i': 4, 's': 4, 'p': 2, 'm': 1})
```
#
### Обновление данных в объектах Counter

- `Counter` наследует все [методы](https://github.com/Skif3195/Python-Learning/blob/Guides/Python%20Core/Шпаргалка%20№5%20-%20Методы%20Словарей.md) класса `dict` кроме метода `fromkeys()`

- `Counter` можно преобразовать в обычный словарь при помощи функции `dict()`
1. `[my_couner.update()]` - метод, для изменения объектов типа Counter.  

      - Метод не заменяет значения (как у типа `dict()`) а сумирует с существующими.
      - Для новых объектов создаёт пары `ключ : колличество` и добавляет к старому объекту `Counter`.
```
from collections import Counter

letters = Counter({'i': 4, 's': 4, 'p': 2, 'm': 1})
print(letters)   # Counter({'i': 4, 's': 4, 'p': 2, 'm': 1})

letters.update('missouri')
print(letters)   # Counter({'i': 6, 's': 6, 'p': 2, 'm': 2, 'o': 1, 'u': 1, 'r': 1})
```

- `update()` принимает любой итерируемый объект.
- Методу `update()` можно передать словарь (`dict()`) или другой объект `Counter`
#
### Доступ к элементам объекта Counter  

`letters = Counter('mississippi')`  

1. Обращение по о ключу:
```
print(letters['p'])
print(letters['i'])
```
2. Перебор ключей напрямую:
```
for letter in letters:
    print(letter, '->', letters[letter])
```
3. Перебор значений через методы `keys()`, `values()`, `items()`:
```
# перебор ключей через метод
for letter in letters.keys():
    print(letter, '->', letters[letter])

# перебор значений через метод
for count in letters.values():
    print(count)

# перебор пар (ключ, значение) через метод
for letter, count in letters.items():
    print(letter, '->', count)
```
- Нельзя обратиться к ключу, которого нет в объекте `Counter`
- Для удаления всех элементов объекта `Counter` используется метод `clear()`
- Объекты `Counter` можно сравнивать между собой (`==`  `!=`). Порядок элементов не важен.
- Элементы с нулевым значением воспринимаются как отсутствующие:
```
counter1 = Counter(i=4)
counter2 = Counter(i=4, s=0)

print(counter1 == counter2)   # True
```
- Значения по ключам могут иметь тип, отличный от числового, но при этом допускающий сложение (например, строки):
```
counter1 = Counter(i=4, s='4')
counter2 = Counter(i=5, s='5')

counter1.update(counter2)

print(counter1)   # Counter({'i': 9, 's': '54'})
```
#
## Метод most_common()

`[most_common(n)]` - метод используется для получения наиболее часто встречающихся элементов (ключей) и их количества в объекте Counter. Он возвращает список кортежей, где каждый кортеж содержит ключ и количество его повторений, `отсортированных по убыванию количества повторений`.
<details>
  <summary>Пример использования</summary> 
   
```
from collections import Counter

# Создаем объект Counter
counter = Counter({'a': 3, 'b': 1, 'c': 2, 'd': 3})

# Получаем наиболее часто встречающиеся элементы
most_common_elements = counter.most_common()

# Выводим результат
print(most_common_elements)   # [('a', 3), ('d', 3), ('c', 2), ('b', 1)]
```
</details>

- `[n]` - необязательный аргумент, при указании, метод возвращает `n` самых часто-повторяемых аргументов.
<details>
  <summary>Пример использования</summary> 

```
from collections import Counter

# Создаем объект Counter
counter = Counter({'a': 3, 'b': 1, 'c': 2, 'd': 3})

# Получаем два наиболее часто встречающихся элемента
most_common_elements = counter.most_common(2)

print(most_common_elements)   # [('a', 3), ('d', 3)]
```
</details>

- `reversed()` - функция, которая может вернуть список кортежей, `отсортированных по увеличению количества повторений`.
<details>
  <summary>Пример использования</summary>

```
from collections import Counter

# Создаем объект Counter
counter = Counter({'a': 3, 'b': 1, 'c': 2, 'd': 3})

# Получаем наиболее часто встречающиеся элементы
# По умолчанию - по возврастанию
most_common_elements = counter.most_common()

# Разворачиваем список значений
most_common_elements_asc = list(reversed(most_common_elements))

# Выводим результат
print(most_common_elements_asc)
```
</details>

#
## Метод elements()

- `[elements()]` - метод, возвращает `объект-итератор`, перечисляющий элементы в количестве, равном их счетчику в объекте Counter.

     - Возвращает `объект-итератор`. Что бы увидеть содержимое, приводим к типу коллекции (функция `list()`)

<details>
  <summary>Пример использования</summary>

```
from collections import Counter

# Создаем объект Counter
counter = Counter({'a': 3, 'b': 1, 'c': 2})

# Получаем итератор элементов
elements_iterator = counter.elements()

print(list(elements_iterator))   # ['a', 'a', 'a', 'b', 'c', 'c']
```

</details>

#

## Метод total()

- `[total()]` - метод, используется для вычисления суммы всех значений счетчика, включая как `положительные`, так и `отрицательные` значения.

<details>
  <summary>Пример использования</summary>

```
from collections import Counter

# Создаем объект Counter с положительными и отрицательными значениями
counter = Counter({'a': 3, 'b': -1, 'c': 2})

# Получаем сумму всех значений счетчика, включая отрицательные
total_count = counter.total()

# Выводим результат
print(total_count)   # 4
```

</details>

#

## метод subtract()

- `[subract()]` - метод, используется для вычитания значений одного счетчика из другого.

     - Значения результирующего счётчика могут быть `нулевыми` или `отрицательными`.
     - Метод может принимать как объект `Counter`, так и любой другой итерируемый объект.

<details>
  <summary>Пример использования</summary>

```
from collections import Counter

# Создаем два объекта Counter
counter1 = Counter({'a': 3, 'b': 2, 'c': 1})
counter2 = Counter({'a': 1, 'b': 1, 'd': 1})

# Вычитаем значения счетчика counter2 из счетчика counter1
counter1.subtract(counter2)

# Выводим результат
print(counter1)
```

</details>

#

## Операторы

- `[+]` - оператор сложения. Альтернатива методу `update()`
- `[-]` - оператор вычитания. Альтернатива методу `subtract()`
- `[&]` - минимальное пересечение. Находит минимальные значения из тех, что есть в обоих счётчиках.
- `[|]` - миксимальное пересечение. Находит максимальные значения из тех, что есть в обоих счётчиках.
- `[Унарный -]` - инвертирует знаки всех элементов счётчика.
- `[<=, <, >=, >]` - работают в стандартном режиме. Воспринимают отсутствующие элементы, как нулевые.

