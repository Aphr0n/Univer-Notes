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

На кожному підінтервалі $\langle x_i, x_{i+1} \rangle$ функцію замінюємо константою:

$$
f_i(x) = f(c_i)
$$

де середина:
$$
c_i = \frac{x_i + x_{i+1}}{2}
$$

---

## Площа одного прямокутника

$$
s_i = (x_{i+1} - x_i)\cdot f(c_i)
$$

---

## Сума площ

$$
s(n) = \sum_{i=0}^{n-1} s_i = \sum_{i=0}^{n-1} (x_{i+1} - x_i)\cdot f(c_i)
$$

З урахуванням $h$:

$$
s(n) = h \cdot \sum_{i=0}^{n-1} f\left(x_i + \frac{h}{2}\right)
$$

---

## Формула методу

$$
\int_a^b f(x)\,dx \approx s(n) =
h \cdot \sum_{i=0}^{n-1} f\left(x_i + \frac{h}{2}\right)
$$

---

## Оцінка похибки

$$
\left| s(n) - \int_a^b f(x)\,dx \right|
\le \frac{(b - a)^2}{2n} \cdot M_1
$$

де:
$$
M_1 = \max_{x \in \langle a,b \rangle} |f'(x)|
$$

Або через $h$:

$$
\left| s(n) - \int_a^b f(x)\,dx \right|
\le \frac{(b - a)}{2} \cdot h \cdot M_1
$$