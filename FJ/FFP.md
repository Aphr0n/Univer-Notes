# Правила
## First
$$\begin{equation}
\begin{aligned}
\text{1. } & X \rightarrow a,\; a \in T \;\Rightarrow\; First(X) = \{a\} \\
\text{2. } & X \rightarrow \epsilon \;\Rightarrow\; First(X) = \{\epsilon\} \\
\text{3. } & X \rightarrow Y_1, Y_2, \dots, Y_n: \\
           & \quad \text{якщо } \epsilon \notin First(Y_1), \text{ то } First(X) = First(Y_1) \\
           & \quad \text{якщо } \epsilon \in First(Y_1), \text{ то } First(X) = First(Y_1) \setminus \{\epsilon\}
\end{aligned}
\end{equation}$$
## Follow
$$
\begin{equation}\begin{aligned}
\text{1.} & X \in S \rightarrow \text{стартовий символ} \rightarrow Follow(X) = \{$\} \\
\text{2.} & A \rightarrow pB \rightarrow Follow(B) = Follow(A) \\
\text{3\\p} & \ - \ послідовність T \ i \ N \\
\text{3.} & A \rightarrow aBg \rightarrow \\
 & \quad \text{якщо} \ \epsilon \notin First(g); Follow(B) = First(g) \\
& \quad \text{якщо} \ \epsilon \in First(g); Follow(B) = First(g)- \{\epsilon\} \ \cup \ Follow(A)
\end{aligned}
\end{equation}
$$
## Predict
$$
\mathit{PREDICT}(A\to\alpha)=\left\{\begin{array}{ll}
\mathit{FIRST}(\alpha), & \text{якщо } \varepsilon \notin \mathit{FIRST}(\alpha),\\
(\mathit{FIRST}(\alpha)-\{\varepsilon\})\cup \mathit{FOLLOW}(A), & \text{якщо } \varepsilon \in \mathit{FIRST}(\alpha).
\end{array}\color{transparent}\right\}
$$



S → AB
A → aA 
A -> ε
B → bB 
B -> c

First(S) = {a,b,c}
First(A) = {a, eps}
First(B) = {b,c}

Follow(S) = {$}
Follow(A) = {b,c}
Follow(B) = {$}

Predict 
1. a,b,c
2. a
3. b,c
4. b
5. c












