# Тема 33 - Функции all() и any()

***`[all()]`*** -  это встроенная функция в Python, которая возвращает True, если все элементы в итерируемом объекте истинны, и False, если хотя бы один из них ложен. 

  - `[all()]` - ищет в последовательности False и возвращает False, если находит.

***`[any()]`*** -  это встроенная функция в Python, которая возвращает True, если хотя бы один элемент в итерируемом объекте истинен. Если все элементы ложны, то функция возвращает False. 

  - `[any()]` - ищет в последовательности True и возвращает True, если находит.
```
list1 = [0, 1, 2]

print(all(list1))   # False, потому что 0 - False
print(any(list1))   # True, потому что в последовательности есть True-элементы (1 и 2)
```
#

### Синтаксис:  `[all(iterable)]`  ,  `[any(iterable)]`

#
### Функции all() и any() могут принимать в качестве аргументов:

<details>
  <summary>1) Итерируемые объекты (str, list, tupple, dict, set)</summary> 
  
```
my_tuple = (0, 1, 2)

print(all(my_tuple))   # False, потому что 0 - False
print(any(my_tuple))   # True, потому что в последовательности есть True-элементы (1 и 2)
```
</details>
<details>
  <summary>2) Функции, возвращающие итераторы (map(), filter())</summary> 
  
```
my_list = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

print(all(map(lambda x: x ** 2, my_list)))   # False
print(any(map(lambda x: x ** 2, my_list)))   # True

```
</details>
<details>
  <summary>3) Генераторы выражений (expression for item in iterable if condition)</summary> 
  
```
print(all([i ** 2 for i in range(10) if i > -1]))   # False
print(any([i ** 2 for i in range(10) if i > -1]))   # True
```
</details>












