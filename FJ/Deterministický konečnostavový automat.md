**Deterministický konečnostavový automat (DKA)** je usporiadaná pätica $M = (Q,T,\delta, q_0, F)$.
Konečnostavové automaty sa v teoerickej informatike bežne vytvárajú prostredníctvom zostavenia prechodových tabuliek. Takto vytvorené automaty sú **nedeterministické**, čo znamená, že pri niektorom vstupe je prechodová funkcia definovaná nie do jediného možného stavu , ale do množiny možných stavov. Na transformáciu NKA na DKA sa využíva metóda nazývaná **determinizácia**. My sa však teraz oboznámime s metódou priamej konštrukcie DKA za základe daného regulárneho výrazu tzv. **metódou tokenou**. Tá je uvedená v animovanej [prezentácii](https://kurzy.kpi.fei.tuke.sk/fj/labs/resources/ksa.ppsx) a taktiež detailne popísaná na nasledujúcich príkladoch.
- Q je konečna množina stavov automatu,
- T je konečna množina pripustnych vstupnych symbolov (alebo vstupna abeceda) automatu, 
- $\delta$ je prechodova funkcia automatu, $\delta: Q \times T \rightarrow Q$,
- $q_0$ je pociatocny alebo inicialny stav automatu, $g_0 \in Q$,
- F je množina akcepta¢nych stavov automatu, $F \subseteq Q$.
  >Upozornenie
	Prechodová funkcia je **parciálna** (čiastočne definovaná) funkcia, čo je v rámci jej špecifikácie vyjadrené využitím symbolu "$\rightharpoonup$" namiesto symbolu "$\rightarrow$" vyhradeného pre úplne definované funkcie. Znamená to, že funkcia $\delta$ nemusí byť definovaná pre všetky prvky z jej domény $Q \times T$.

**Konfigurácia** DKA je usporiadaná dvojica $(q,w) \in Q\times T$, kde je $q$ aktuálny stav automatu a $w$ je ešte nespracovaná časť vstupu. Vo výpočte automatu sa vyskytujú taktiež osobitné konfigurácie, ktoré zohrávajú špecifickú úlohu pri akceptácii vstupu:
- **Začiatočná konfigurácia automatu** – je konfigurácia $(q_0,w)$, kde je celý vstupný reťazec.
- **Koncová konfigurácia automatu** – je konfigurácia tvaru $(q, \epsilon)$, teda taká, pri ktorej bol celý vstup spracovaný.
- **Akceptujúca konfigurácia automatu** – je koncová konfigurácia, v ktorej $q \in F$.
  
  Na množine konfigurácií $Q \times T^*$ definujeme binárnu **reláciu prechodu** (alebo **krok výpočtu**) DKA, označovanú symbolom $\vdash$ nasledovne: Nech $q,p \in Q, w \in T^*$ . Potom
$$(q,xw) \vdash (p,w)\text{vtedy a len vtedy, ak} \delta(q,x)=0$$
**Výpočtom automatu** M nazývame konečnú lineárnu postupnosť konfigurácií $c_0,c_1, \dots, c_k$, kde $k \in N_0$ a pre každé $i \in \{0,1,\dots,k-1\}$ platí $c_i \vdash c_{i+1}$, kde $c_0$ je začiatočná konfigurácia a $c_k$ je koncová konfigurácia. Každá konfigurácia má tvar $c_i = (q_i, w_i)$ pričom $q_i \in Q$ a $w_i \in T^*$. Takýto výpočet budeme označovať symbolicky $c_0 \vdash^k c_k$, kde predstavuje počet krokov výpočtu. Na vyjadrenie výpočtového správania automatu v ľubovoľnom počte krokov využijeme uzávery relácie prechodu $\vdash$. Nech $M = (Q,T,\delta, q_0, F)$ je DKA a $\vdash$ je jeho relácia kroku výpočtu. Potom definujeme:
- **Tranzitívny uzáver relácie** ($\vdash$ alebo $\vdash^+$) – je množina všetkých dvojíc $(c,c') \in (Q \times T^*)^2$ , pre ktoré existuje $k \in N$ a konfigurácie $c_0,\dots,c_k$ také, že
$$c = c_0 \vdash c_1 \vdash \dots \vdash c_k = c', k\geq 1$$
- **Reflexívny a tranzitívny uzáver relácie** ($\vdash$ alebo $\vdash^*$) – je množina všetkých dvojíc $(c,c') \in (Q \times T^*)^2$ pre ktoré existuje $k \in N_0$ a konfigurácie $c_0,\dots,c_k$ také, že
$$c = c_0 \vdash c_1 \vdash \dots \vdash c_k = c', k\geq 0$$
Reťazec $w$ je akceptovaný DKA $M$, ak existuje výpočet, ktorého prvá konfigurácia je začiatočná konfigurácia so vstupným reťazcom $w$ a posledná konfigurácia je koncová akceptujúca konfigurácia, teda
$$(q_0,w)\vdash^* (q,\epsilon), \text{kde } q \in F$$
Jazyk $L(M)$ **rozpoznávaný** alebo taktiež **akceptovaný** konečným automatom $M$ je množina:
$$L(M) = \{w | (q_0,w) \vdash^* (q,\epsilon) \wedge w \in T^* \wedge q \in F$$
