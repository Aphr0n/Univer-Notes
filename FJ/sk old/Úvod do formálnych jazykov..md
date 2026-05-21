# Abecedy a reťazcý

**Abeceda** *А* je konečná, neprázdna množina základných, ďalej nerozložiteľných (atomických) prvkov nazývaných **symboly** alebo **znaky**. Abecedou môže byť napríklad:
- $\{a,b,\dots, z\}$ - abeceda pozostávajúca z malých latinských písmen,
- $\{0,1\}$ - abeceda jazyka binárnych numerálov(číselnej sústavý),
- $\{0,1, \dots, 9, A,B, \dots, F\}$ - abeceda jazyka haxadecinálnych numerálov,
- $\{if, else, while, if, *, +, -, \dots\}$ - množina lexikálnych elementov ľubovoľného programovacieho jazyka.

**Reťazec** $w$  nad abecedou A je konečná postupnosť symbolov tejto abecedy.
- Počet symbolov v reťazci $w$ nazývame **dĺžkou reťazca** a označujeme $|w|$.
- Špeciálny prípad reťazca je tzv. **prázdny reťazec** označovaný , pre ktorého dĺžku platí $$|\epsilon| = 0$$
- **Zreťazenie reťazcov(konkatenácia)** $w_1$ a $w_2$ - binárna operácia spájania reťazcov, výsledkom ktorej bude reťazec $w_1*w_2$(alebo skrátene $w_1w_2$) pre ktorý bude platiť $w_1w_2 = \{a_1, \dots, b_i, \dots b_j\}$. _Táto operácia nie je komutatívna($w_1w_2 \neq w_2w_1$), ale je asociatívna($(w_1w_2)w_3 = w_1(w_2w_3)$)_	
- **Obrátený reťazec** k reťazcu $w$ je reťazec: $w^R = a_n,\dots, a_1$. Tiež je možne definovať túto operáciu induktívne:
$$
w^R =
\begin{cases}
\varepsilon, & \text{ak } w = \varepsilon, \\
w_r^R x, & \text{ak } w = x w_r \text{ pre nejaké } x \in A \text{ a reťazec } w_r.
\end{cases}
$$
- **Palindróm** je reťazec pre ktorý platí $w = w^R$
- _n-tou mocninou reťazca_ $w_1$ voláme reťazec pre ktorý plati: 
 $$
w^n = \underbrace{w w \dots w}_{n\text{-крат}}
$$
	Túto operáciu možno taktiež definovať induktívne, a to nasledovne:
	$$
	w^R =
\begin{cases}
\varepsilon, & \text{ak } n = 0, \\
w_r^R x, & \text{ak } n > 0.
\end{cases}
$$

Na základe tejto definície je taktiež zrejmé, že nulta mocnina ľubovoľného reťazca je prázdny reťazec, $w^0 = \varepsilon$

- **predpona (prefix)** reťazca $w$, ak existuje taký reťazec nad abecedou , pre ktorý platí $w = w'w_1$
-  **prípona (sufix)** reťazca $w$, ak existuje taký reťazec nad abecedou , pre ktorý platí $w = w_1w'$
- **podreťazec** reťazca $w$, ak existujú také reťazce a nad abecedou , pre ktoré platí $w = w_1w'w_2$
  
  - **Tranzitívny uzáver** je množina všetkých reťazcov $A^*$ (v rátane prázdneho reťazca $\epsilon$) nad abecedou A, teda $A^* = U_{n=0}^{\infty}A^n$
  - **Pozitívny uzáver** $A^+$ je množina všetkých neprázdnych reťazcov nad abecedou A, teda
  $$A^+ = U^\infty_{n = 1}A^n$$
		Potom platí že:
	$$A^+ = A^* - \{\epsilon\}$$
# Formálne jazyky

- **Formálny jazyk** L je ľubovoľná podmnožina množiny všetkých možných reťazcov nad abecedou tohto jazyka A, $L \subseteq A$. Reťazce, ktoré patria do jazyka označujeme ako **slová** alebo **vety** jazyka.
  - **Zreťazenie jazykov $L_1$ a $L_2$ ** nazývame jazyk:
  $$L_1 \cdot L_2 = \{w_1w_2 | w_1 \ in L1 | \wedge w_2 \in L_2$$
- **n-tou mocninou**  jazyka L nazývame jazyk definovaný nasledovne:
	$$
	w^R =
\begin{cases}
\{\varepsilon\}, & \text{pre } n = 0, \\
LL^{n-1}, & \text{pre } n > 0.
\end{cases}$$
To znamená, že jazyk $L^n$ sa skladá zo všetkých reťazcov, ktoré vzniknú zreťazením reťazcov jazyka L s reťazcami jazyka $L^{n-1}$.

- **Iterácia (Tranzitívny uzáver)** jazyka je jazyk , ktorý vznikne zjednotením všetkých celých nezáporných mocnín jazyka $L^* = U^\infty_{n = 0}L^n.$
- **Pozitívna iterácia** jazyka je jazyk , ktorý vznikne zjednotením všetkých prirodzených mocnín jazyka L $L^+ = U^\infty_{n=1}L^n$.
- **Zjednoteníe** jazykov $L_1$ a $L_2$, je jazyk, ktorý obsahuje všetky reťazce z $L_1$ a všetky reťazce z ​$L_2$, $L_1 \cup L_2 = \{w | w \in L_1 \vee w \in L_2\}$
- **Prienikom** jazykov $L_1$ a $L_2$, je jazyk, ktorý obsahuje len tie reťazce, ktoré sú súčasne v $L_1$ ​ aj $L_2$​, $L_1 \cap L_2 = \{w | w \in L_1 \wedge w \in L_2 \}$
- **Rozdielom** jazykov $L_1$ a $L_2$, je jazyk, ktorý obsahuje tie reťazce z $L_1$​, ktoré nie sú v $L_2$. 
$$L_1 - L_2 = {w | w \in L_1 \wedge w \notin L_2}$$
- **Komplementom** jazyka L nad abecedou A nazývame jazyk, ktorý obsahuje všetky reťazce nad abecedou A, ktoré nepatria do L, $L^C = A^* - L$.
- **Ľavý kvocient** jazyka podľa je jazyk, pre ktorý platí: $L_2 \backslash L_1 = \{w_1 | (\exists w_2 \in L_2)(w_2w_1 \in L_1)\}$. Іnými slovami to je operácia ktorá „odreže“ určitú časť slova zľava.