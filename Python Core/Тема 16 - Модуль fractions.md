# Модуль fractions

- `[ fractions ]` - Модуль стандартной библиотеки Python, предоставляет класс Fraction для работы с рациональными числами (дробями).
#
### Для использовния модуля, его нужно импортировать
 - `[from fractions import Fraction]` - импортирует класс `[Fraction]` из модуля `[fractions]`, вместе со всеми его методами.
```
from fractions import Fraction

n = Fraction(3, 4)   # 3/4
```
#
- Числа `[fractions]` стоит создавать из целых чисел (int) или из строк (str)
- Для чисел `[fractions]` доступны:
    - Операторы сравнения (==, !=, >, <, >=, <=,)
    - Математические операторы (+, -, *, /, %, //)
    - Модуль math (но результатом всегда будет число float)
- Не стои проводить арифметические операции чисел `[fractions]` с числами float из-за не точного округления.

## Основные методы класса `[Fraction]`
<details>
  <summary>Основные методы класса Fraction</summary>
 
#
 ### 1) `[numerator()]` - возвращает числитель дроби (числа fractions).  
```
from fractions import Fraction

frac = Fraction(3, 4)

# Получаем числитель
numerator_value = frac.numerator

print(numerator_value)  # Вывод: 3
```
#
 ### 2) `[denominator()]` - возвращает знаменатель дроби (числа fractions).
```
from fractions import Fraction

frac = Fraction(3, 4)

# Получаем знаменатель
denominator_value = frac.denominator

print(denominator_value)  # Вывод: 4
```
#
 ### 3) `[as_integer_ratio()]` - возвращает кортеж из двух целых чисел - числителя и знаменателя дроби.  
```
from fractions import Fraction

frac = Fraction(3, 4)

# Получаем кортеж из числителя и знаменателя
ratio = frac.as_integer_ratio()

print(ratio)  # Вывод: (3, 4)
```
</details>
