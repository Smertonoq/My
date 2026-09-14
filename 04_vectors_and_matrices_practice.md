# Векторы и матрицы: практикум

Этот практикум продолжает тему [«Векторы и матрицы: язык данных и нейросетей»](03_vectors_and_matrices_lecture.md). Его можно использовать и как отдельный материал: перед каждой группой задач есть короткое напоминание основных формул, а решения спрятаны в раскрывающихся блоках.

Задачи постепенно переходят от обычной арифметики к вычислениям, которые выполняет нейросеть: скалярным произведениям, матричным преобразованиям, embeddings и формуле слоя $\mathbf{a}=\varphi(W\mathbf{x}+\mathbf{b})$.

---

## 1. Векторы и их координаты

Вектор — упорядоченный набор чисел. Например,

$$
\mathbf{x}=
\begin{bmatrix}
2\\
-1\\
5
\end{bmatrix}.
$$

Сложение и вычитание векторов выполняются по координатам.

### Задача 1

Даны

$$
\mathbf{a}=
\begin{bmatrix}
2\\
-1\\
4
\end{bmatrix},
\qquad
\mathbf{b}=
\begin{bmatrix}
3\\
5\\
-2
\end{bmatrix}.
$$

Найдите:

1. $\mathbf{a}+\mathbf{b}$;
2. $\mathbf{a}-\mathbf{b}$;
3. $2\mathbf{a}$;
4. $-\mathbf{b}$.

<details>
<summary><strong>Решение</strong></summary>

$$
\mathbf{a}+\mathbf{b}=
\begin{bmatrix}
5\\
4\\
2
\end{bmatrix}.
$$

$$
\mathbf{a}-\mathbf{b}=
\begin{bmatrix}
-1\\
-6\\
6
\end{bmatrix}.
$$

$$
2\mathbf{a}=
\begin{bmatrix}
4\\
-2\\
8
\end{bmatrix}.
$$

$$
-\mathbf{b}=
\begin{bmatrix}
-3\\
-5\\
2
\end{bmatrix}.
$$

</details>

### Задача 2

Объект описан вектором признаков

$$
\mathbf{x}=
\begin{bmatrix}
8\\
2\\
5
\end{bmatrix}.
$$

После преобразования первый признак уменьшают в $2$ раза, второй оставляют без изменений, третий увеличивают в $3$ раза. Запишите новый вектор.

<details>
<summary><strong>Решение</strong></summary>

Новый вектор:

$$
\mathbf{x}_{\text{new}}=
\begin{bmatrix}
4\\
2\\
15
\end{bmatrix}.
$$

</details>

---

## 2. Длина и расстояние

Евклидова длина вектора:

$$
\|\mathbf{x}\|_2=\sqrt{x_1^2+x_2^2+\dots+x_n^2}.
$$

Расстояние между двумя векторами:

$$
d(\mathbf{a},\mathbf{b})=\|\mathbf{a}-\mathbf{b}\|_2.
$$

### Задача 3

Найдите длину вектора

$$
\mathbf{v}=
\begin{bmatrix}
5\\
12
\end{bmatrix}.
$$

<details>
<summary><strong>Решение</strong></summary>

$$
\|\mathbf{v}\|=\sqrt{5^2+12^2}=\sqrt{25+144}=13.
$$

</details>

### Задача 4

Даны два объекта:

$$
\mathbf{a}=
\begin{bmatrix}
1\\
2
\end{bmatrix},
\qquad
\mathbf{b}=
\begin{bmatrix}
4\\
6
\end{bmatrix}.
$$

Найдите евклидово расстояние между ними.

<details>
<summary><strong>Решение</strong></summary>

$$
\mathbf{b}-\mathbf{a}=
\begin{bmatrix}
3\\
4
\end{bmatrix}.
$$

$$
d(\mathbf{a},\mathbf{b})=\sqrt{3^2+4^2}=5.
$$

</details>

### Задача 5

Есть запрос

$$
\mathbf{q}=
\begin{bmatrix}
2\\
3
\end{bmatrix}
$$

и три объекта:

$$
\mathbf{a}=
\begin{bmatrix}
2\\
4
\end{bmatrix},
\quad
\mathbf{b}=
\begin{bmatrix}
5\\
3
\end{bmatrix},
\quad
\mathbf{c}=
\begin{bmatrix}
1\\
1
\end{bmatrix}.
$$

Какой объект ближе всего к запросу?

<details>
<summary><strong>Решение</strong></summary>

Для $\mathbf{a}$:

$$
d(\mathbf{q},\mathbf{a})=1.
$$

Для $\mathbf{b}$:

$$
d(\mathbf{q},\mathbf{b})=3.
$$

Для $\mathbf{c}$:

$$
d(\mathbf{q},\mathbf{c})=\sqrt{(2-1)^2+(3-1)^2}=\sqrt5\approx2.24.
$$

Ближе всего объект $\mathbf{a}$.

</details>

### Задача 6. Почему масштаб признаков важен

Два объекта описаны двумя признаками:

$$
\mathbf{a}=
\begin{bmatrix}
1\\
1000
\end{bmatrix},
\qquad
\mathbf{b}=
\begin{bmatrix}
5\\
1010
\end{bmatrix}.
$$

Объясните, какой признак сильнее влияет на евклидово расстояние и почему перед сравнением объектов признаки иногда нормируют.

<details>
<summary><strong>Ответ</strong></summary>

Разность признаков равна

$$
\mathbf{b}-\mathbf{a}=
\begin{bmatrix}
4\\
10
\end{bmatrix}.
$$

Вклад координаты в квадрат расстояния определяется квадратом разности. Первый признак даёт $16$, второй — $100$. Если масштабы признаков сильно различаются, крупномасштабный признак может доминировать независимо от его смысловой важности. Нормировка делает сравнение более сбалансированным.

</details>

---

## 3. Скалярное произведение

Для двух векторов одинаковой длины

$$
\mathbf{a}\cdot\mathbf{b}=a_1b_1+a_2b_2+\dots+a_nb_n.
$$

### Задача 7

Вычислите

$$
\begin{bmatrix}
2\\
3\\
-1
\end{bmatrix}
\cdot
\begin{bmatrix}
4\\
-2\\
5
\end{bmatrix}.
$$

<details>
<summary><strong>Решение</strong></summary>

$$
2\cdot4+3\cdot(-2)+(-1)\cdot5=8-6-5=-3.
$$

</details>

### Задача 8. Искусственный нейрон

Вход:

$$
\mathbf{x}=
\begin{bmatrix}
2\\
1\\
3
\end{bmatrix}.
$$

Веса:

$$
\mathbf{w}=
\begin{bmatrix}
0.5\\
-1\\
2
\end{bmatrix}.
$$

Смещение:

$$
b=-2.
$$

Вычислите

$$
z=\mathbf{w}\cdot\mathbf{x}+b
$$

и затем примените

$$
a=\operatorname{ReLU}(z)=\max(0,z).
$$

<details>
<summary><strong>Решение</strong></summary>

$$
\mathbf{w}\cdot\mathbf{x}=0.5\cdot2+(-1)\cdot1+2\cdot3=1-1+6=6.
$$

$$
z=6-2=4.
$$

$$
a=\operatorname{ReLU}(4)=4.
$$

</details>

### Задача 9

Даны два вектора единичной длины, и их скалярное произведение равно $0.92$. Что можно сказать об угле между ними?

<details>
<summary><strong>Ответ</strong></summary>

Для единичных векторов

$$
\mathbf{a}\cdot\mathbf{b}=\cos\theta.
$$

Значение $0.92$ близко к $1$, поэтому угол между векторами небольшой, а направления похожи.

</details>

---

## 4. Косинусное сходство

Косинусное сходство вычисляется по формуле

$$
\cos\theta=\frac{\mathbf{a}\cdot\mathbf{b}}{\|\mathbf{a}\|\|\mathbf{b}\|}.
$$

### Задача 10

Даны

$$
\mathbf{a}=
\begin{bmatrix}
1\\
0
\end{bmatrix},
\qquad
\mathbf{b}=
\begin{bmatrix}
1\\
1
\end{bmatrix}.
$$

Найдите косинусное сходство.

<details>
<summary><strong>Решение</strong></summary>

$$
\mathbf{a}\cdot\mathbf{b}=1.
$$

$$
\|\mathbf{a}\|=1,
$$

$$
\|\mathbf{b}\|=\sqrt2.
$$

Поэтому

$$
\cos\theta=\frac{1}{\sqrt2}\approx0.707.
$$

</details>

### Задача 11. Семантический поиск

Пусть embedding запроса равен

$$
\mathbf{q}=
\begin{bmatrix}
1\\
0
\end{bmatrix}.
$$

Документы представлены векторами

$$
\mathbf{d}_1=
\begin{bmatrix}
0.9\\
0.1
\end{bmatrix},
\qquad
\mathbf{d}_2=
\begin{bmatrix}
0.2\\
0.98
\end{bmatrix}.
$$

Без точного вычисления объясните, какой документ, скорее всего, семантически ближе к запросу по косинусному сходству.

<details>
<summary><strong>Ответ</strong></summary>

Вектор $\mathbf{d}_1$ направлен почти так же, как $\mathbf{q}$: его первая координата велика, а вторая мала. Вектор $\mathbf{d}_2$ направлен почти вертикально. Поэтому $\mathbf{d}_1$ будет иметь большее косинусное сходство с запросом.

</details>

---

## 5. Матрицы и их формы

Матрица размера $m\times n$ имеет $m$ строк и $n$ столбцов.

### Задача 12

Определите форму каждой матрицы:

$$
A=
\begin{bmatrix}
1&2&3\\
4&5&6
\end{bmatrix},
$$

$$
B=
\begin{bmatrix}
1\\
2\\
3\\
4
\end{bmatrix},
$$

$$
C=
\begin{bmatrix}
1&2\\
3&4\\
5&6
\end{bmatrix}.
$$

<details>
<summary><strong>Решение</strong></summary>

- $A$: $2\times3$.
- $B$: $4\times1$.
- $C$: $3\times2$.

</details>

### Задача 13

Набор данных содержит $500$ объектов и $12$ признаков на объект. Если строки соответствуют объектам, а столбцы — признакам, какова форма матрицы данных?

<details>
<summary><strong>Ответ</strong></summary>

$$
500\times12.
$$

</details>

### Задача 14

Цветное изображение имеет высоту $128$ пикселей, ширину $256$ пикселей и три цветовых канала. Какую форму может иметь его тензор при порядке «высота × ширина × каналы»?

<details>
<summary><strong>Ответ</strong></summary>

$$
128\times256\times3.
$$

</details>

---

## 6. Умножение матрицы на вектор

Если

$$
A\in\mathbb{R}^{m\times n}
$$

и

$$
\mathbf{x}\in\mathbb{R}^{n},
$$

то

$$
A\mathbf{x}\in\mathbb{R}^{m}.
$$

### Задача 15

Вычислите

$$
A=
\begin{bmatrix}
1&2\\
3&4
\end{bmatrix},
\qquad
\mathbf{x}=
\begin{bmatrix}
5\\
6
\end{bmatrix}.
$$

<details>
<summary><strong>Решение</strong></summary>

$$
A\mathbf{x}=
\begin{bmatrix}
1\cdot5+2\cdot6\\
3\cdot5+4\cdot6
\end{bmatrix}
=
\begin{bmatrix}
17\\
39
\end{bmatrix}.
$$

</details>

### Задача 16

Можно ли умножить матрицу формы $4\times3$ на вектор длины $4$ справа, то есть вычислить $A\mathbf{x}$?

<details>
<summary><strong>Ответ</strong></summary>

Нет. Для произведения $A\mathbf{x}$ длина вектора должна совпадать с числом столбцов матрицы. Здесь требуется вектор длины $3$.

</details>

### Задача 17

Матрица $W$ имеет форму $6\times10$. Какой длины должен быть входной вектор $\mathbf{x}$? Какой длины будет $W\mathbf{x}$?

<details>
<summary><strong>Ответ</strong></summary>

Входной вектор должен иметь длину $10$. Результат будет иметь длину $6$.

</details>

---

## 7. Полносвязный слой нейросети

Полносвязный слой можно записать так:

$$
\mathbf{z}=W\mathbf{x}+\mathbf{b}.
$$

Затем к $\mathbf{z}$ часто применяют функцию активации.

### Задача 18

Пусть

$$
\mathbf{x}=
\begin{bmatrix}
2\\
1\\
3
\end{bmatrix},
$$

$$
W=
\begin{bmatrix}
1&0&-1\\
2&1&0
\end{bmatrix},
$$

$$
\mathbf{b}=
\begin{bmatrix}
1\\
-2
\end{bmatrix}.
$$

Найдите $\mathbf{z}=W\mathbf{x}+\mathbf{b}$, затем примените ReLU поэлементно.

<details>
<summary><strong>Решение</strong></summary>

Сначала

$$
W\mathbf{x}=
\begin{bmatrix}
1\cdot2+0\cdot1-1\cdot3\\
2\cdot2+1\cdot1+0\cdot3
\end{bmatrix}
=
\begin{bmatrix}
-1\\
5
\end{bmatrix}.
$$

Добавим смещение:

$$
\mathbf{z}=
\begin{bmatrix}
0\\
3
\end{bmatrix}.
$$

После ReLU:

$$
\mathbf{a}=
\begin{bmatrix}
0\\
3
\end{bmatrix}.
$$

</details>

### Задача 19

Слой получает $20$ входных признаков и выдаёт $8$ чисел. Какую форму должна иметь матрица весов $W$? Какую длину должен иметь вектор смещений $\mathbf{b}$?

<details>
<summary><strong>Ответ</strong></summary>

$$
W:8\times20,
$$

$$
\mathbf{b}:8.
$$

</details>

### Задача 20

Сколько весовых коэффициентов содержит матрица слоя из предыдущей задачи? Сколько всего обучаемых параметров в слое вместе со смещениями?

<details>
<summary><strong>Решение</strong></summary>

Весов:

$$
8\cdot20=160.
$$

Смещений: $8$.

Всего:

$$
160+8=168.
$$

</details>

---

## 8. Умножение матриц

Для произведения

$$
A_{m\times n}B_{n\times p}
$$

внутренние размерности должны совпадать, а результат имеет форму

$$
m\times p.
$$

### Задача 21

Определите, какие произведения существуют, и укажите форму результата:

1. $(2\times3)(3\times4)$;
2. $(5\times2)(3\times5)$;
3. $(7\times1)(1\times6)$;
4. $(4\times4)(4\times2)$.

<details>
<summary><strong>Решение</strong></summary>

1. Существует, форма $2\times4$.
2. Не существует: внутренние размеры $2$ и $3$ не совпадают.
3. Существует, форма $7\times6$.
4. Существует, форма $4\times2$.

</details>

### Задача 22

Вычислите

$$
A=
\begin{bmatrix}
1&2\\
3&4
\end{bmatrix},
\qquad
B=
\begin{bmatrix}
2&0\\
1&5
\end{bmatrix}.
$$

Найдите $AB$ и $BA$. Совпадают ли результаты?

<details>
<summary><strong>Решение</strong></summary>

$$
AB=
\begin{bmatrix}
1\cdot2+2\cdot1 & 1\cdot0+2\cdot5\\
3\cdot2+4\cdot1 & 3\cdot0+4\cdot5
\end{bmatrix}
=
\begin{bmatrix}
4&10\\
10&20
\end{bmatrix}.
$$

$$
BA=
\begin{bmatrix}
2\cdot1+0\cdot3 & 2\cdot2+0\cdot4\\
1\cdot1+5\cdot3 & 1\cdot2+5\cdot4
\end{bmatrix}
=
\begin{bmatrix}
2&4\\
16&22
\end{bmatrix}.
$$

Результаты различаются. Это демонстрирует, что обычно

$$
AB\ne BA.
$$

</details>

---

## 9. Транспонирование

Транспонирование меняет строки и столбцы местами.

### Задача 23

Для

$$
A=
\begin{bmatrix}
1&2&3\\
4&5&6
\end{bmatrix}
$$

найдите $A^T$.

<details>
<summary><strong>Решение</strong></summary>

$$
A^T=
\begin{bmatrix}
1&4\\
2&5\\
3&6
\end{bmatrix}.
$$

</details>

---

## 10. Embeddings и поиск похожих объектов

Пусть три объекта представлены нормированными embeddings:

$$
\mathbf{e}_1=
\begin{bmatrix}
1\\
0
\end{bmatrix},
\qquad
\mathbf{e}_2=
\begin{bmatrix}
0.8\\
0.6
\end{bmatrix},
\qquad
\mathbf{e}_3=
\begin{bmatrix}
-1\\
0
\end{bmatrix}.
$$

### Задача 24

Сравните направления $\mathbf{e}_1$ с $\mathbf{e}_2$ и $\mathbf{e}_3$. Какой объект ближе по косинусному сходству к $\mathbf{e}_1$?

<details>
<summary><strong>Решение</strong></summary>

Поскольку векторы нормированы, косинусное сходство равно скалярному произведению.

$$
\mathbf{e}_1\cdot\mathbf{e}_2=0.8,
$$

$$
\mathbf{e}_1\cdot\mathbf{e}_3=-1.
$$

Значит, $\mathbf{e}_2$ похож по направлению, а $\mathbf{e}_3$ направлен противоположно. Ближе $\mathbf{e}_2$.

</details>

### Задача 25

Почему при поиске похожих текстов иногда используют косинусное сходство, а не только евклидово расстояние?

<details>
<summary><strong>Ответ</strong></summary>

Косинусное сходство сравнивает направление векторов и меньше зависит от их длины. Если длина embedding не должна влиять на смысловое сходство, такая мера бывает удобнее. Выбор конкретной метрики зависит от того, как были обучены и нормированы embeddings.

</details>

---

## 11. Градиент как вектор

Если функция ошибки зависит от нескольких параметров,

$$
L=L(w_1,w_2,w_3),
$$

то градиент имеет вид

$$
\nabla L=
\begin{bmatrix}
\frac{\partial L}{\partial w_1}\\
\frac{\partial L}{\partial w_2}\\
\frac{\partial L}{\partial w_3}
\end{bmatrix}.
$$

### Задача 26

Пусть текущий вектор параметров

$$
\mathbf{w}=
\begin{bmatrix}
2\\
-1
\end{bmatrix},
$$

а градиент

$$
\nabla L=
\begin{bmatrix}
4\\
-2
\end{bmatrix}.
$$

Скорость обучения равна

$$
\eta=0.1.
$$

Выполните шаг градиентного спуска:

$$
\mathbf{w}_{\text{new}}=\mathbf{w}-\eta\nabla L.
$$

<details>
<summary><strong>Решение</strong></summary>

$$
\eta\nabla L=
0.1
\begin{bmatrix}
4\\
-2
\end{bmatrix}
=
\begin{bmatrix}
0.4\\
-0.2
\end{bmatrix}.
$$

Тогда

$$
\mathbf{w}_{\text{new}}=
\begin{bmatrix}
2\\
-1
\end{bmatrix}
-
\begin{bmatrix}
0.4\\
-0.2
\end{bmatrix}
=
\begin{bmatrix}
1.6\\
-0.8
\end{bmatrix}.
$$

</details>

---

## 12. Итоговая задача: маленькая нейросеть вручную

Пусть входной вектор

$$
\mathbf{x}=
\begin{bmatrix}
1\\
2
\end{bmatrix}.
$$

Первый слой:

$$
W_1=
\begin{bmatrix}
1&-1\\
2&1
\end{bmatrix},
\qquad
\mathbf{b}_1=
\begin{bmatrix}
0\\
-1
\end{bmatrix}.
$$

После первого слоя применяется ReLU.

Второй слой имеет веса

$$
\mathbf{w}_2=
\begin{bmatrix}
3\\
-2
\end{bmatrix}
$$

и смещение

$$
b_2=1.
$$

### Задача 27

Вычислите выход модели:

1. $\mathbf{z}_1=W_1\mathbf{x}+\mathbf{b}_1$;
2. $\mathbf{a}_1=\operatorname{ReLU}(\mathbf{z}_1)$;
3. $z_2=\mathbf{w}_2\cdot\mathbf{a}_1+b_2$.

<details>
<summary><strong>Решение</strong></summary>

Первый слой:

$$
W_1\mathbf{x}=
\begin{bmatrix}
1\cdot1+(-1)\cdot2\\
2\cdot1+1\cdot2
\end{bmatrix}
=
\begin{bmatrix}
-1\\
4
\end{bmatrix}.
$$

Добавляем смещение:

$$
\mathbf{z}_1=
\begin{bmatrix}
-1\\
3
\end{bmatrix}.
$$

Применяем ReLU:

$$
\mathbf{a}_1=
\begin{bmatrix}
0\\
3
\end{bmatrix}.
$$

Второй слой:

$$
z_2=3\cdot0+(-2)\cdot3+1=-5.
$$

**Ответ:** выход модели равен $-5$.

</details>

---

## 13. Итоговый мини-тест

1. Найдите длину вектора $(6,8)$.
2. Вычислите скалярное произведение $(1,2,3)\cdot(4,0,-1)$.
3. Что означает форма матрицы $5\times12$?
4. Какой длины должен быть вектор, чтобы его можно было умножить слева на матрицу $7\times4$?
5. Какова форма результата $(3\times5)(5\times2)$?
6. Запишите формулу полносвязного слоя.
7. Что такое embedding?
8. Чем косинусное сходство отличается по смыслу от евклидова расстояния?
9. Почему $AB$ обычно не равно $BA$?
10. Как связан градиент с векторами?

<details>
<summary><strong>Ответы</strong></summary>

1. $10$.
2. $1\cdot4+2\cdot0+3\cdot(-1)=1$.
3. Пять строк и двенадцать столбцов.
4. Длина $4$.
5. $3\times2$.
6. $\mathbf{a}=\varphi(W\mathbf{x}+\mathbf{b})$.
7. Векторное представление объекта.
8. Косинусное сходство сравнивает направления, евклидово расстояние — расстояние между точками в пространстве.
9. Матричное умножение некоммутативно: перестановка множителей меняет порядок преобразований.
10. Градиент — это вектор частных производных функции ошибки по параметрам.

</details>
