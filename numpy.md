Основные функции NumPy
======================

``` python
import numpy as np
```

Создание массивов
-----------------

1. `np.array(l)`
   Преобразование вложенного питоновского списка в ndarray:

   - `np.array([[1, 2, 3], [4, 5, 6]])`:

     |     |     |     |
     | --- | --- | --- |
     | 1   | 2   | 3   |
     | 4   | 5   | 6   |

2. `np.identity(n)`
   Единичная матрица размера `n×n`:

   - `np.identity(2)`:

     |    |    |
     |----|----|
     | 1. | 0. |
     | 0. | 1. |

3.
   - `np.zeros(n)`
     Нулевой одномерный массив длины `n`.

     - `np.zeros(4)`:

       |    |    |    |    |
       |----|----|----|----|
       | 0. | 0. | 0. | 0. |

   - `np.zeros((n, m))`
     Нулевой двумерный массив `n×m`.

     - `np.zeros((2, 2))`:

       |    |    |
       |----|----|
       | 0. | 0. |
       | 0. | 0. |

   - `np.zeroes((n, m, k))`
     Нулевой трехмерный массив `n×m×k`.

     - `np.zeros((2, 2, 2))`:

       | 0  | 1  | 0  | 1  |
       |----|----|----|----|
       |    | 0. |    | 0. |
       | 0. |    | 0. |    |
       |    | 0. |    | 0. |
       | 0. |    | 0. |    |

2. `np.arange(start, end, delta)`
   Одномерный массив `[start, start + delta, …, last]`, где `last + delta >= end`:
   - `np.arange(1, 5, 1)`:

     |   |   |   |   |
     |---|---|---|---|
     | 1 | 2 | 3 | 4 |

   - `np.arange(1, 5, 1.9)`:

     |     |     |     |
     |-----|-----|-----|
     | 1.0 | 2.9 | 4.8 |

3. `np.linspace(start, end, n)`
   Одномерный массив из `n` точек, равномерно распределенных между `start` и `end`.
   - `np.linspace(1, 10, 2)`:

     |     |      |
     |-----|------|
     | 1.0 | 10.0 |

   - `np.linspace(1, 10, 3)`:

     |     |     |      |
     |-----|-----|------|
     | 1.0 | 5.5 | 10.0 |

   - `np.linspace(1, 10, 10)`:

     |     |     |     |     |     |     |     |     |     |      |
     |-----|-----|-----|-----|-----|-----|-----|-----|-----|------|
     | 1.0 | 2.0 | 3.0 | 4.0 | 5.0 | 6.0 | 7.0 | 8.0 | 9.0 | 10.0 |

4. `np.copy(a)` или `a.copy()` --- копия массива `a`.
   Изменения в копии гарантировано не затрагивают исходного массива (см. ниже).


Доступ к элементам массива
--------------------------

Индексация элементов начинается с 0. Как и в случае с обычными последовательностями
в Python, отрицательные индексы означают счет с конца: `-1` --- последний элемент,
`-2` --- предпоследний и т.д.

1. `a[n]`
   - `n`-ый элемент одномерного массива
   - `n`-ая строка двумерного массива

2. `a[n, m]`
   - `m`-ый элемент `n`-ой строчки двумерного массива

     `a[n, m] == a[n][m]`

3. `a[n:m]` --- подмассив из элементов с `n` по `m-1` массива `a`.
   Если `m <= n`, то подмассив пустой.

   - `np.array([1, 2, 3, 4])[1:3]`

     |   |   |
     |---|---|
     | 2 | 3 |

   Если `a` --- двумерный массив, то `a[n:m]` содержит строки с
   `n` по `m-1` исходного массива:

   - `np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])[1:3]`

     |   |   |   |
     |---|---|---|
     | 4 | 5 | 6 |
     | 7 | 8 | 9 |

4. `a[n:m, k:l]` --- кусок прямоугольного массива, содержащий строки
   с `n` по `m-1` и столбцы с `k` по `l-1`.

   - `np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])[1:3, 0:2]`:

     |   |   |
     |---|---|
     | 4 | 5 |
     | 7 | 8 |

   Обратите внимание: `a[n:m, k:l]` --- **не то же**, что `a[n:m][k:l]`:

   - `np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])[1:3][0:2]`:

     |   |   |   |
     |---|---|---|
     | 4 | 5 | 6 |
     | 7 | 8 | 9 |

5. `a[..., k]` или `a[:, k]` --- `k`-ый столбец прямоугольного массива.
   - `np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])[..., 1]`

     |   |   |   |
     |---|---|---|
     | 2 | 5 | 8 |

   Обратите внимание: столбец превращается в одномерный массив, форма не сохраняется.
   Ср.:

   - `np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])[..., 1:2]`

     |   |
     |---|
     | 2 |
     | 5 |
     | 8 |

6. `a[n:m:l]` --- каждый `l`-ый элемент одномерного массива (каждая `l`-ая строка двумерного массива) 
   в диапазоне от `n` до `m-1`.

   - `np.arange(1, 10)[1:8:2]`:

     |   |   |   |   |
     |---|---|---|---|
     | 2 | 4 | 6 | 8 |

   - `np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]])[0:4:3]`:

     |    |    |    |
     |----|----|----|
     | 1  | 2  | 3  |
     | 10 | 11 | 12 |

7.  `a[n:m:p, k:l:q]` --- кусок прямоугольного массива, содержащий каждую `p`-ую строку
    с `n` по `m-1` и каждый `q`-ый столбец с `k` по `l-1`.

    - `np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12], [13, 14, 15, 16]])[0:4:3, 1:4:2]`:

      |    |    |
      |----|----|
      | 2  | 4  |
      | 14 | 16 |

8. `a[intlist]`, где `intlist` --- список целых чисел, выбирает из одномерного массива элементы
   с соответствующими индексами, а из двумерного массива --- строки с соответствующими индексами.
   Аналогично `a[intlist1, intlist2]` выбирает из двумерного массива строки с индексами, соотв.
   `intlist1`, а потом из каждой строки столбцы, соответствующие `intlist2`.

   - `np.array([1, 2, 3, 4, 5])[[0, 2, 3]]`:

     |   |   |   |
     |---|---|---|
     | 1 | 3 | 4 |

   - `np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]])[[0, 2, 3]]`:

     |    |    |    |
     |----|----|----|
     | 1  | 2  | 3  |
     | 7  | 8  | 9  |
     | 10 | 11 | 12 |

   - `np.array([[1, 2, 3, 4, 5], [6, 7, 8, 9, 10], [11, 12, 13, 14, 15], [16, 17, 18, 19, 20]])[[0, 2, 3], [1, 3, 4]]`:

     |   |    |    |
     |---|----|----|
     | 2 | 14 | 20 |

    Обратим внимание, что в отличие от случая `a[n:m:p, k:l:q]` получается одномерный массив: сначала из исходного массива
    выбираются строки 0, 2, 3, а потом из первой строки выбирается элемент 1, из второй -- элемент 3 и т.д.

9. `a[boolarray]`, где `boolarray` --- массив булевских величин, выбирает из массива `a` элементы, для которых соответствующее
   значение в `boolarray` истинно. Если `a` --- двумерный массив, а `boolarray` --- одномерный, то из `a` будут выбраны строки,
   соответствующие истинным элементам в `boolarray`. В противном случае полученный массив будет одномерным.

   - `np.array([1, 2, 3, 4, 5])[np.array([False, True, True, False, True])]`:

     |   |   |   |
     |---|---|---|
     | 2 | 3 | 5 |

   - `np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]])[np.array([False, True, True, False])]`:

     |   |   |   |
     |---|---|---|
     | 4 | 5 | 6 |
     | 7 | 8 | 9 |

   - `np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])[np.array([[False, True, True], [False, False, True], [True, False, False]])]`:

     |   |   |   |   |
     |---|---|---|---|
     | 2 | 3 | 6 | 7 |

Во всех случаях, кроме (8) и (9), создается не копия, а _представление_ (view) подмассива, так что изменения в подмассиве будут
затрагивать и исходных массив:

```
x = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
y = x[0:2, 1:3]
y[1, 1] = 0
→ x[1, 2] == 0
```

Но:

x = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
y = x[[0, 1]]
y[1, 2] = 0
→ x[1, 2] == 6



Форма массива
-------------

1. `np.shape(a)` или `a.shape` возвращает кортеж размерностей массива:

   - `np.shape(1) == ()` --- у скалярной величины нет размерностей
   - `np.shape(np.array([1, 2, 3, 4])) == (4,)` --- обращаем внимание, что результат --- кортеж длины один, а не просто число
   - `np.shape(np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]])) == (4, 3)` --- массив из 4 строк и трех столбцов

2. `np.ravel(a)` --- одномерный массив, содержащий развертку массива `a`:

   - `np.ravel(np.array([1, 2, 3, 4])) == np.array([1, 2, 3, 4])`
   - `np.ravel(np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]]))`:

     |   |   |   |   |   |   |   |   |   |    |    |    |
     |---|---|---|---|---|---|---|---|---|----|----|----|
     | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |

3. `a.T` --- транспозиция двумерного массива:

   - `np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]]).T`:

     |   |   |   |    |
     |---|---|---|----|
     | 1 | 4 | 7 | 10 |
     | 2 | 5 | 8 | 11 |
     | 3 | 6 | 9 | 12 |

4. `np.reshape(a, shape)` или `a.reshape(shape)` --- изменение формы массива в соответствии с кортежем `shape`.
   Общее количество элементов остается неизменным. Один из элементов `shape` может быть отрицательным, тогда
   соответствующая размерность вычисляется автоматически. Исходный массив сначала развертывается в одномерный,
   аналогично функции `ravel`, после чего элементы группируются в новые измерения справа налево.

   - `np.reshape(np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]]), (12,)) == np.ravel(np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]])`
   - `np.reshape(np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]]), (-1,)) == np.ravel(np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]])`
   - `np.reshape(np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]]), (2, 6))` или
     `np.reshape(np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]]), (2, -1))` или
     `np.reshape(np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]]), (-1, 6))`:

     |   |   |   |    |    |    |
     |---|---|---|----|----|----|
     | 1 | 2 | 3 | 4  | 5  | 6  |
     | 7 | 8 | 9 | 10 | 11 | 12 |

   - `np.reshape(np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]), (2, 3, 2))`:

     | 0 | 1  | 0 | 1  |
     |---|----|---|----|
     |   | 7  |   | 8  |
     | 1 |    | 2 |    |
     |   | 9  |   | 10 |
     | 3 |    | 4 |    |
     |   | 11 |   | 12 |
     | 5 |    | 6 |    |

  **Внимание!** `reshape` может создавать как копию, так и представление исходного массива,
  в зависимости от того, каков этот исходный массив.


5. `np.hstack(arraylist)` --- склеивание списка массивов вдоль горизонтальной оси.
   Если все массивы одномерные, результатом будет одномерный массив; если они двумерные,
   их высота должна быть одинакова.

   - `np.hstack([np.array([1, 2, 3]), np.array([4, 5, 6])])`:

     |   |   |   |   |   |   |
     |---|---|---|---|---|---|
     | 1 | 2 | 3 | 4 | 5 | 6 |

   - `np.hstack([np.array([[1, 2, 3], [4, 5, 6]]), np.array([[7, 8, 9], [10, 11, 12]])])`:

     |   |   |   |    |    |    |
     |---|---|---|----|----|----|
     | 1 | 2 | 3 | 7  | 8  | 9  |
     | 4 | 5 | 6 | 10 | 11 | 12 |


6. `np.vstack(arraylist)` --- склеивание списка массивов вдоль вертикальной оси.
    Ширина/длина всех массивов должна быть одинакова, но в списке могут быть смешаны одномерные
    и двумерные массивы.

   - `np.vstack([np.array([1, 2, 3]), np.array([4, 5, 6])])`:

     |   |   |   |
     |---|---|---|
     | 1 | 2 | 3 |
     | 4 | 5 | 6 |

  - `np.vstack([np.array([[1, 2, 3], [4, 5, 6]]), np.array([[7, 8, 9], [10, 11, 12]])])`

     |    |    |    |
     |----|----|----|
     | 1  | 2  | 3  |
     | 4  | 5  | 6  |
     | 7  | 8  | 9  |
     | 10 | 11 | 12 |

7. `np.block(blocklist)` составляет массив из блоков (обобщение `hstack` и `vstack`).

  - `np.block([[np.array([1, 2, 3]), np.array([4, 5, 6])], [np.array([7, 8, 9]), np.array([10, 11, 12])]]`:

    |   |   |   |    |    |    |
    |---|---|---|----|----|----|
    | 1 | 2 | 3 | 7  | 8  | 9  |
    | 4 | 5 | 6 | 10 | 11 | 12 |

  - `np.block([[np.array([[1, 2, 3], [4, 5, 6]]), np.array([[7, 8, 9], [10, 11, 12]])], [np.array([13, 14, 15, 16, 17, 18])]])`:

    |    |    |    |    |    |    |
    |----|----|----|----|----|----|
    | 1  | 2  | 3  | 7  | 8  | 9  |
    | 4  | 5  | 6  | 10 | 11 | 12 |
    | 13 | 14 | 15 | 16 | 17 | 18 |

8. `np.pad(array, padding)` --- дополнение массива нулями по заданной спецификации. Если `padding` --- целое число,
   то массив со всех сторон окружается данным количеством нулей. Если `padding` --- пара целых чисел,
   то первое число определяет количество нулей перед элементами массива, а второе --- после элементов массива. Наконец,
   если `padding` --- последовательность пар целых чисел, то каждая пара определяет величину дополнения по данной оси
   отдельно.

   - `np.pad(np.array([[1, 2, 3], [4, 5, 6]]), 1)`:

     |   |   |   |   |   |
     |---|---|---|---|---|
     | 0 | 0 | 0 | 0 | 0 |
     | 0 | 1 | 2 | 3 | 0 |
     | 0 | 4 | 5 | 6 | 0 |
     | 0 | 0 | 0 | 0 | 0 |

   - `np.pad(np.array([[1, 2, 3], [4, 5, 6]]), (0, 1))`:

     |   |   |   |   |
     |---|---|---|---|
     | 1 | 2 | 3 | 0 |
     | 4 | 5 | 6 | 0 |
     | 0 | 0 | 0 | 0 |

   - `np.pad(np.array([[1, 2, 3], [4, 5, 6]]), ((0, 1), (1, 2)))`:

     |   |   |   |   |   |   |
     |---|---|---|---|---|---|
     | 0 | 1 | 2 | 3 | 0 | 0 |
     | 0 | 4 | 5 | 6 | 0 | 0 |
     | 0 | 0 | 0 | 0 | 0 | 0 |


Распространение / Broadcasting
------------------------------

NumPy поддерживает арифметические операции с массивами. Если форма массивов-аргументов одинакова,
то вычисления производятся поэлементно. В противном случае, оси единичного размера "распространяются"
вдоль остальных. В частности, скалярные величины превращаются в массив нужной размерности, заполненный
данным скаляром:

- `np.array([1, 2, 3]) + np.array([4, 5, 6])`:

  |   |   |   |
  |---|---|---|
  | 5 | 7 | 9 |

- `np.array([1, 2, 3]) + 1` → `np.array([1, 2, 3]) + np.array([1, 1, 1])`:

  |   |   |   |
  |---|---|---|
  | 2 | 3 | 4 |

- `np.array([[1, 2, 3], [4, 5, 6]]) + np.array([[7, 8, 9], [10, 11, 12]])`:

  |    |    |    |
  |----|----|----|
  | 8  | 10 | 12 |
  | 14 | 16 | 18 |

- `np.array([[1, 2, 3], [4, 5, 6]]) + 1` → `np.array([[1, 2, 3], [4, 5, 6]]) + np.array([[1, 1, 1], [1, 1, 1]])`:

  |   |   |   |
  |---|---|---|
  | 2 | 3 | 4 |
  | 5 | 6 | 7 |

- `np.array([[1, 2, 3], [4, 5, 6]]) + np.array([7, 8, 9])` → `np.array([[1, 2, 3], [4, 5, 6]]) + np.array([[7, 8, 9], [7, 8, 9]])`:

  |    |    |    |
  |----|----|----|
  | 8  | 10 | 12 |
  | 11 | 13 | 15 |

- `np.array([[1, 2, 3], [4, 5, 6]]) + np.array([[7], [8]])` → `np.array([[1, 2, 3], [4, 5, 6]]) + np.array([[7, 7, 7], [8, 8, 8]])`:

  |    |    |    |
  |----|----|----|
  | 8  | 9  | 10 |
  | 12 | 13 | 14 |

- `np.array([1, 2, 3]) + np.array([[4], [5], [6]])` → `np.array([[1, 2, 3], [1, 2, 3], [1, 2, 3]]) + np.array([[4, 4, 4], [5, 5, 5], [6, 6, 6]])`:

  |   |   |   |
  |---|---|---|
  | 5 | 6 | 7 |
  | 6 | 7 | 8 |
  | 7 | 8 | 9 |

В таком режиме NumPy поддерживает все обычные арифметические операции: сложение, вычитание, умножение, деление, возведение в степень.
Отметим, что умножение в таком смысле --- это __не то же самое__, что векторное или матричное умножение.

Аналогичным образом работают и операторы сравнения, что может быть несколько неожиданно, но в сочетании с булевской индексацией позволяет
легко делать фильтрацию элементов массива:

- `np.array([1, 2, 3]) == np.array([1, 4, 3])`:

  |      |       |      |
  |------|-------|------|
  | True | False | True |

- `x = np.array([1, 2, 3, 4, 5, 6]); x[x > 3]`:

  |   |   |   |
  |---|---|---|
  | 4 | 5 | 6 |


Также NumPy предоставляет эквиваленты стандартных математических функций, которые поэлементно применяются к массивам любой формы:
- `np.sqrt`
- `np.cbrt`
- `np.log`
- `np.exp`
- `np.sin`
- `np.cos`
- и так далее

- `np.sqrt(np.array([[1, 4, 9], [16, 25, 36]])):

  |    |    |    |
  |----|----|----|
  | 1. | 2. | 3. |
  | 4. | 5. | 6. |

Статистика и агрегация
----------------------

Все перечисленные в этом разделе функции по умолчанию оперируют над всеми элементами массива вместе, так что результат ---
скалярная величина. Если указан параметр `axis=N`, то агрегирование значений будет происходить вдоль соответствующей оси.
Если при этом указан еще `keepdims=True`, то полученный массив будет иметь такую же размерность, как и исходный.

- `np.sum([[1, 2, 3], [4, 5, 6]])` → `1 + 2 + 3 + 4 + 5 + 6 = 21`
- `np.sum([[1, 2, 3], [4, 5, 6]], axis=0)`:

   |           |           |           |
   |-----------|-----------|-----------|
   | 1 + 4 = 5 | 2 + 5 = 7 | 3 + 6 = 9 |

- `np.sum([[1, 2, 3], [4, 5, 6]]. axis=1)`:

  |               |                |
  |---------------|----------------|
  | 1 + 2 + 3 = 6 | 4 + 5 + 6 = 15 |

- `np.sum([[1, 2, 3], [4, 5, 6]], axis=1, keepdims=True)`:

  |                |
  |----------------|
  | 1 + 2 + 3 = 6  |
  | 4 + 5 + 6 = 15 |

NumPy поддерживает следующие агрегирующие функции:
- `np.sum` --- сумма
- `np.prod` --- произведение
- `np.amin` --- наименьшее значение
- `np.amax` --- наибольшее значение
- `np.mean` --- арифметическое среднее
- `np.median` --- медиана
- `np.std` --- среднеквадратичное отклонение
- `np.var` --- дисперсия
- `np.percentile(a, q)` --- `q`-ый перцентиль (`0 <= q <= 100`)
- `np.quantile(a, q)` --- `q`-ый квантиль (`0 <= q <= 1.0`)
- `np.average(a, weights=w)` --- взвешенное среднее. Массив весов должен
  быть либо одномерным, равным по длине оси агрегирования, или иметь такую
  же форму, как `a`. В отличие от предыдущих эта функция не поддерживает параметр `keepdims=True`.


Ввод/вывод
----------

### Чтение текстовых файлов

- `np.genfromtxt(fname, delimiter=d, skip_header=n1, skip_footer=n2)`.

  Считывает из файла `fname` двумерный массив данных. Каждая строка ввода соответствует строке
  массива. Элементы в строке разделяются символом `d` (по умолчанию --- пробел).
  Функция может пропустить `n1` строк заголовка и `n2` строк в конце.
  Остальные строки должны иметь одинаковое число столбцов.

  Функция автоматически распаковывает файлы, сжатые с помощью `gzip` или `bzip2`.

### Сохранение текстовых файлов

- `np.savetxt(fname, a, fmt=format, delimiter=d, header=hdr, footer=ftr, comments=c)`

  Записывает одно- или двумерный массив в файл `fname`.
  Каждой строке массива соответствует одна строка файла.
  Элементы в строке разделяются символом `d` (по умолчанию --- пробел).
  Каждый элемент будет отформатирован в соответствии со спецификатором `fmt`, например:
  - `%.2f` --- представление с плавающей точкой с двумя знаками после запятой
  - `%d` --- целочисленное представление

  Если указаны параметры `header` и/или `footer`, то соответствующие строки будут записаны
  в начало и конец файла. Если при этом указан и параметр `comment`, то они будут начинаться
  с этого символа.

  - `np.savetxt('sample.csv', np.array([[1, 2, 3], [4, 5, 6]]), fmt='%d', delimiter=',', header='Header', comments='# ')`

    ``` csv
    # Header
    1,2,3
    4,5,6
    ```
