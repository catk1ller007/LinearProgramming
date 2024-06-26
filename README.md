# Библиотека алгоритмов решения задач линейного программирования
## Обзор ##
Эта библиотека содержит реализацию алгоритмов оптимизации, таких как `задача о рюкзаке`, `симплекс-метод` и `двухфазный симплекс-метод`. Эти алгоритмы используются для решения задач линейного программирования и комбинаторной оптимизации.

## Введение ##
В библиотеке реализованы следующие алгоритмы:

* `Задача о рюкзаке:` Комбинаторная задача, где нужно максимизировать стоимость предметов в рюкзаке с ограниченной вместимостью.
* `Симплекс-метод:` Алгоритм для решения задач линейного программирования.
* `Двухфазный симплекс-метод:` Расширение симплекс-метода для задач с искусственными переменными.

## Установка ##
Чтобы использовать библиотеку, клонируйте репозиторий:
```
git clone https://github.com/Kuznetsov-Artyom/LinearProgramming.git
cd LinearProgramming
```

## Использование ##
Все алгоритмы находятся в библиотеке `lp.hpp` и объединены в пространство имён `lp`.\
В `main.cpp` представлено использование всех алгоритмов на нескольких примерах.
1. `Симплекс-метод`\
Для использования сиплекс-метода используется метод `simplexMethodMax`.\
Для вывода результата используется метод `printResultMaxSimplexMethod`.
```
auto ansOne = lp::simplexMethodMax({3, 2}, {{1, 1, 4}, {1, 3, 6}});
lp::printResultMaxSimplexMethod(ansOne);

// И другие примеры
```
Метод `simplexMethodMax` принимает следующие параметры:  
  * `std::vector<double>` - вектор, содержащий коэффициенты при `x` в целевой функции.
  * `std::vector<std::vector<double>>` - вектор векторов, в котором содержатся коэффициенты перед `x` в ограничениях и сами ограничения.

2. `Двухфазный симплекс-метод`\
Для использования сиплекс-метода используется метод `simplexMethodMaxTwoPhaze`.\
Для вывода результата используется тот же метод `printResultMaxSimplexMethod`.
```
auto ansOneTwoPhazeNotFound = lp::simplexMethodMaxTwoPhaze(
    {3, -4}, {{-2, 1, 10}, {1, 3, 12}, {3, -1, 7}},
    {lp::OpCompare::LESS_EQ, lp::OpCompare::MORE_EQ, lp::OpCompare::MORE_EQ});
lp::printResultMaxSimplexMethod(ansOneTwoPhazeNotFound);

// И другие примеры
```
* `std::vector<double>` - вектор, содержащий коэффициенты при `x` в целевой функции.
* `std::vector<std::vector<double>>` - вектор векторов, в котором содержаться коэффициенты перед `x` в ограничениях и сами ограничения.
* `std::vector<OpCompare>` - вектор, содержащий информацию о знаках неравенства в ограничениях.


3. `Задача о рюкзаке`
Для решения задачи о рюкзаке используется метод `fillBackpack()`.\
Для вывода результата используется метод `printResultFillBackpack()`.
```
auto ansOneBackpack = lp::fillBackpack({4, 5, 3, 7, 6}, {5, 7, 4, 9, 8}, 16);
lp::printResultFillBackpack(ansOneBackpack);

// И другие примеры
```
* `std::vector<double>` - вектор, содержащий веса объектов.\
* `std::vector<std::vector<double>>` - вектор содержащий стоимости объектов.\
* `int` - вместимость рюкзака.

Также в программе реализован генератор тестов для симплес-метода, для его вызова необходимо использовать метод `testSimplexMethodMax`.
```
lp::testSimplexMethodMax({ 6, 2, 2.5, 4 },
    { {5, 1, 0, 2, 1000}, {1, 0, 2, 1, 150}, {4, 2, 2, 1, 600} });
```
* Параметры аналогичны параметрам стандартного **симплес-метода**.\
Генератор тестов прогоняет симплекс-метод для всех вариантов перестановок столбцов в симплекс таблице.
