
Нехай заданий визначений інтеграл:
$$
\int_a^b f(x)\,dx
$$

---

## Розбиття інтервалу

Інтервал $\langle a, b \rangle$ ділимо на $n$ рівних частин.

Крок:
$$
h = \frac{b - a}{n}
$$

Вузлові точки:
$$
x_0 = a,\quad x_n = b
$$

$$
x_{i+1} = x_i + h,\quad i = 0,1,2,\dots,n-1
$$

---

## Апроксимація функції

На кожному підінтервалі $\langle x_i, x_{i+1} \rangle$ функцію замінюємо **лінійною функцією**, яка проходить через точки:
$$
[x_i, f(x_i)] \quad \text{та} \quad [x_{i+1}, f(x_{i+1)}]
$$

---

## Площа однієї трапеції

$$
s_i = \frac{h}{2} \cdot \big(f(x_i) + f(x_{i+1})\big)
$$

---

## Сума площ

$$
s(n) = \sum_{i=0}^{n-1} s_i
= \frac{h}{2} \cdot \sum_{i=0}^{n-1} \big(f(x_i) + f(x_{i+1})\big)
$$

Після спрощення:

$$
s(n) = \frac{h}{2} \cdot \left[
f(a) + f(b) + 2 \cdot \sum_{i=1}^{n-1} f(x_i)
\right]
$$

---

## Формула методу

$$
\int_a^b f(x)\,dx \approx
\frac{h}{2} \cdot \left[
f(a) + f(b) + 2 \cdot \sum_{i=1}^{n-1} f(x_i)
\right]
$$

---

## Оцінка похибки

$$
\left| s(n) - \int_a^b f(x)\,dx \right|
\le \frac{(b - a)^3}{12 n^2} \cdot M_2
$$

де:
$$
M_2 = \max_{x \in \langle a,b \rangle} |f''(x)|
$$

Або через $h$:

$$
\left| s(n) - \int_a^b f(x)\,dx \right|
\le \frac{(b - a)}{12} \cdot h^2 \cdot M_2
$$