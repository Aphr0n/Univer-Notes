**Regulárne výrazy** predstavujú stručný formalizmus na opis tzv. regulárnych jazykov definovaný americkým matematikom a logikom **Stephenom Coleom Kleenem**. Samotný princíp určenia jazyka pomocou regulárneho výrazu spočíva v špecifikácii vzoru, ktorý splňajú všetky slová tohto jazyka, ktoré preto možno označiť za konkrétne inštancie tohto vzoru.
# Atomické (elementárne) tvary
- $\epsilon$– regulárny výraz označujúci jazyk pozostávajúci z jediného reťazca ,
- a, pre $a \in A$, kde $A$ je abeceda daného regulárneho jazyka – regulárny výraz označujúci jazyk pozostávajúci z jediného reťazca.
# Zložené tvarý
- $R_1R_2$ zreťazenie je regulárny výraz označujúci jazyk $L_1L_2$, napr. regulárny výraz $ab$ identifikuje jazyk pozostávajúci z jediného reťazca ab
- $R_1|R_2$ alternácia je regulárny výraz označujúci jazyk $L_1 \cup L_2$, napr. regulárny výraz $a|b$ identifikuje jazyk pozostávajúci z reťazcov $a,b$
- ${R}$ Kleeneho uzáver je regulárny výraz označujúci jazyk $L^*$ , napr. regulárny výraz ${a}$ identifikuje jazyk pozostávajúci z reťazcov $\epsilon, a, aa, aaa, \dots$
- $R\{R\}$ pozitívny uzáver je regulárny výraz označujúci jazyk $L^+$, napr. regulárny výraz $a{a}$ identifikuje jazyk pozostávajúci z reťazcov $a,aa,aaa,\dots$
- $|R|$ voliteľnosť je regulárny výraz označujúci jazyk $L \cup \{\epsilon\}$, napr. regulárny výraz $[a]$ identifikuje jazyk pozostávajúci z reťazcov $\epsilon, a$

>Upozornenie:
V regulárnych výrazoch sa termín **alternácia** používa na označenie operátora výberu, kým termín **alternatíva** označuje jednotlivé operandy tohto operátora.

>Poznámka
Zreťazenie má vyššiu prioritu ako alternácia. Z tohto dôvodu je regulárny výraz $ab|c\{d\}$ ekvivalentný regulárnemu výrazu $(ab)|c\{d\}$ a nie výrazu $a(b|c)\{d\}$.

# Notácie

| Tvar regulárneho výrazu               | Zjednodušený zápis (používaný na tomto predmete) | Zápis bežný v implementáciách | Grafická notácia                     |
| ------------------------------------- | ------------------------------------------------ | ----------------------------- | ------------------------------------ |
| Prázdny reťazec                       | $\epsilon$                                       |                               | ![[Pasted image 20260302125114.png]] |
| Symbol                                | $a$                                              | a                             | ![[Pasted image 20260302125909.png]] |
| Zreťazenie (sekvencia)                | $R_1R_2$                                         | $R_1R_2$                      | ![[Pasted image 20260302125920.png]] |
| Alternácia (výber)                    | $R_1\|R_2$                                       | $R_1\|R_2$                    | ![[Pasted image 20260302125928.png]] |
| Kleeneho uzáver (iterácia)            | $\{R\}$                                          | R*                            | ![[Pasted image 20260302125936.png]] |
| Pozitívny uzáver (pozitívna iterácia) | $R\{R\}$                                         | R+                            | ![[Pasted image 20260302125948.png]] |
| Voliteľnosť                           | $[R]$                                            | R?                            | ![[Pasted image 20260302125954.png]] |
