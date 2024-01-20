# Тема 30 - Совместное использование функций map(), filter() и reduce()

<details>
  <summary>map() - применяет заданную функцию ко всем элементам входного итерируемого объекта и возвращает новый итератор.</summary> 
  
```
numbers = [1, 2, 3, 4, 5]
squared = map(lambda x: x**2, numbers)
print(list(squared))
```
</details> 
<details>
  <summary>filter() - фильтрует элементы входного итерируемого объекта, основываясь на результате переданной функции.</summary> 
  
```
numbers = [1, 2, 3, 4, 5]
even = filter(lambda x: x % 2 == 0, numbers)
print(list(even))
```
</details>
<details>
  <summary>reduce() - сводит итерируемый объект к единственному значению, используя указанную функцию.  </summary> 
  
```
from functools import reduce

numbers = [1, 2, 3, 4, 5]
product = reduce(lambda x, y: x * y, numbers)
print(product)
```
</details>
